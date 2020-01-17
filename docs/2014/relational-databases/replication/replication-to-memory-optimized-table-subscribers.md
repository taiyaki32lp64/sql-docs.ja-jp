---
title: メモリ最適化テーブル サブスクライバーへのレプリケーション | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9f58e472b0b6e6d164e45c2d1136c81bc4a46d6
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811229"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>メモリ最適化テーブル サブスクライバーへのレプリケーション
  トランザクション レプリケーションのサブスクライバーとして機能するテーブルは、ピア ツー ピア トランザクション レプリケーションを除き、メモリ最適化テーブルとして構成できます。 その他のレプリケーション構成はメモリ最適化テーブルとは互換性がありません。  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>サブスクライバーとしてのメモリ最適化テーブルの構成  
 サブスクライバーとしてメモリ最適化テーブルを構成するには、次の手順を実行します。  
  
 **パブリケーションの作成と有効化**  
  
1.  パブリケーションの作成。  
  
2.  パブリケーションにアーティクルを追加します。 `@upd_cmd` パラメーターには、SCALL または SQL 規約を使用します。  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **スナップショットを生成してスキーマを調整する**  
  
1.  スナップショット ジョブを作成し、スナップショットを生成します。  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  スナップショット フォルダーに移動します。 既定の場所は "C:\Program Server\MSSQL12. SQLインスタンス > \MSSQL\repldata\unc\XXX\YYYYMMDDHHMMSS\\"。 \<  
  
3.  を見つけ**ます。** テーブルの sch-m ファイルを開き、Management Studio で開きます。 次に説明するように、テーブル スキーマを変更し、ストアド プロシージャを更新します。  
  
     IDX ファイルで定義されているインデックスを評価します。 必要なインデックス、制約、主キー、メモリ最適化構文を指定するように `CREATE TABLE` を変更します。 メモリ最適化テーブルでは、インデックス列を null にしないでください。文字型のインデックス列は Unicode にし、BIN2 照合順序を使用する必要があります。 次の例を参照してください。  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  `@upd_cmd` パラメーターに SCALL 規約を使用するときは、スキーマ (.SCH) ファイルに移動し、`create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]` でテーブル更新ステートメントを変更して、主キー列を削除します。  
  
     主キーの更新をサポートするには、次のように、カスタムの更新ストアド プロシージャを使用して主キーの更新ステートメントを置き換えます。  
  
    1.  値のない列を選択します (SCALL では更新操作にかかわる列にのみ値を渡す)。  
  
    2.  既存のレコードを削除します。  
  
    3.  新しいレコードを挿入し、新しい主キーを含む新しい値を渡します。  
  
     元の更新プロシージャは次のようになります。  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     主キーがパブリッシャーで更新されない場合。 更新プロシージャのこのような列に対する更新を次のようにコメント アウトします。  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     主キーの更新のサポートを許可するには、読み取る更新プロシージャを次のように変更します。  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  **[スナップショット分離に昇格]** オプションを使用してサブスクライバーデータベースを作成し、Unicode 以外の文字データ型を使用している場合は、既定の照合順序を Latin1_General_CS_AS_KS_WS に設定します。  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  スキーマをサブスクライバーのデータベースに適用し、将来使用するためにスキーマを保存します。  
  
7.  パブリッシャー (ソース) のデータをサブスクライバーに読み込みます。 サブスクリプションを追加するまで、パブリッシャーでデータを変更しないでください。  次に示すように BCP を使用できます。  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  サブスクライバーでのスキーマの変更を無効にするようにアーティクルを再構成します。  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **同期サブスクリプションを追加しない**  
  
 非同期サブスクリプションを追加します。  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 これでメモリ最適化テーブルはパブリッシャーから更新を受け取り始めます。  
  
## <a name="restrictions"></a>制限  
 一方向トランザクション レプリケーションのみがサポートされています。 ピア ツー ピア トランザクション レプリケーションはサポートされていません。  
  
 メモリ最適化テーブルをパブリッシュすることはできません。  
  
 ディストリビューターのレプリケーション テーブルをメモリ最適化テーブルとして構成することはできません。  
  
 マージ レプリケーションにメモリ最適化テーブルを含めることはできません。  
  
 サブスクライバーで、トランザクション レプリケーションにかかわるテーブルをメモリ最適化テーブルとして構成できますが、サブスクライバーのテーブルはメモリ最適化テーブルの要件を満たす必要があります。 この場合の制限事項は次のとおりです。  
  
-   トランザクション レプリケーションのサブスクライバーでメモリ最適化テーブルを作成するには、メモリ最適化テーブルの作成に使用されるスナップショット スキーマ ファイルを手動で変更する必要があります。 詳細については、「[スキーマファイルの変更](#Schema)」を参照してください。  
  
-   サブスクライバーのメモリ最適化テーブルにレプリケートされるテーブルは、メモリ最適化テーブルの行の制限に従って 8,060 バイトに制限されます。  
  
-   サブスクライバーのメモリ最適化テーブルにレプリケートされるテーブルは、メモリ最適化テーブルに使用できるデータ型に制限されます。 詳細については、「[サポートされるデータ型](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md)」を参照してください。  
  
-   サブスクライバーのメモリ最適化テーブルにレプリケートされるテーブルの主キーを更新するには、制限があります。 詳細については、「[主キーへの変更のレプリケート](#PrimaryKey)」を参照してください。  
  
-   外部キー、UNIQUE 制約、トリガー、スキーマの変更、ROWGUIDCOL、計算列、データ圧縮、別名データ型、バージョン管理、ロックは、メモリ最適化テーブルではサポートされていません。 詳細については、「 [インメモリ OLTP でサポートされていない T-SQL の構造](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) 」を参照してください。  
  
##  <a name="Schema"></a> スキーマ ファイルの変更  
  
-   クラスター化インデックスはサポートされていません。 クラスター化インデックスを非クラスター化インデックスに変更します。  
  
-   インデックスのキーのすべての列を `NOT NULL` として指定する必要があります。  
  
-   メモリ最適化テーブルのオプション `DURABILITY = SCHEMA_AND_DATA` を使用する場合、テーブルには非クラスター化主キー インデックスが必要です。  
  
-   ANSI_PADDING は ON にする必要があります。  
  
##  <a name="PrimaryKey"></a>主キーへの変更のレプリケート  
 メモリ最適化テーブルの主キーを更新することはできません。 サブスクライバーの主キーの更新をレプリケートするには、DELETE/INSERT ペアとして更新を渡すように更新ストアド プロシージャを変更します。  
  
## <a name="see-also"></a>参照  
 [SQL Server のレプリケーション](sql-server-replication.md)  
  
  
