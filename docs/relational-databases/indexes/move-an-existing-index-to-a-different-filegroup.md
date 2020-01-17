---
title: 既存のインデックスの別のファイル グループへの移動 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- moving tables
- switching filegroups for index
- moving indexes
- indexes [SQL Server], moving
- filegroups [SQL Server], switching
ms.assetid: 167ebe77-487d-4ca8-9452-4b2c7d5cb96e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a2eaffb39868737c955224b3ccd3ba39366d6f92
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906383"
---
# <a name="move-an-existing-index-to-a-different-filegroup"></a>既存のインデックスの別のファイル グループへの移動
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、既存のインデックスを現在のファイル グループから別のファイル グループに移動する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **既存のインデックスを別のファイル グループに移動するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   テーブルにクラスター化インデックスがある場合、クラスター化インデックスを新しいファイル グループに移動すると、テーブルはそのファイル グループに移動します。  
  
-   UNIQUE 制約または PRIMARY KEY 制約を使用して作成されたインデックスは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を使用して移動することはできません。 これらのインデックスを移動するには、 [で](../../t-sql/statements/create-index-transact-sql.md) CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントを (DROP_EXISTING=ON) オプションと共に使用します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。 実行するには、 **sysadmin** 固定サーバー ロール、または **db_ddladmin** 固定データベース ロールおよび **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup-using-table-designer"></a>テーブル デザイナーを使用して既存のインデックスを別のファイル グループに移動するには  
  
1.  オブジェクト エクスプローラーで、移動するインデックスがあるテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  移動するインデックスがあるテーブルを右クリックし、 **[デザイン]** を選択します。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
5.  移動するインデックスを選択します。  
  
6.  メイン グリッドで、 **[データ領域の指定]** を展開します。  
  
7.  **[ファイル グループまたはパーティション構成名]** を選択し、インデックスの移動先のファイル グループまたはパーティション構成を一覧から選択します。  
  
8.  **[閉じる]** をクリックします。  
  
9. **ファイル** メニューの **table_name**_を保存_を選びます。  

#### <a name="to-move-an-existing-index-to-a-different-filegroup-in-object-explorer"></a>オブジェクト エクスプローラーで既存のインデックスを別のファイル グループに移動するには  
  
1.  オブジェクト エクスプローラーで、移動するインデックスがあるテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、移動するインデックスのあるテーブルを展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  移動するインデックスを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[ページの選択]** の **[ストレージ]** を選択します。  
  
7.  インデックスの移動先のファイル グループを選択します。  
  
     テーブルまたはインデックスがパーティション分割されている場合は、インデックスの移動先のパーティション構成を選択します。 パーティション インデックスの詳細については、「 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。  
  
     クラスター化インデックスを移動する場合は、オンライン処理を使用できます。 オンライン処理を使用すると、インデックス操作中、基になるデータや非クラスター化インデックスへの同時ユーザー アクセスが可能になります。 詳しくは、「 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)」をご覧ください。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]を使用するマルチプロセッサ コンピューターでは、並列処理の最大許容値を設定することで、インデックス ステートメントの実行に使用するプロセッサの数を構成できます。 並列インデックス操作機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「SQL Server 2016 の各エディションとサポートされる機能」を参照してください。 並列インデックス操作の詳細については、「 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)」を参照してください。  
  
8.  **[OK]** をクリックします。  
  
 **[インデックスのプロパティ – _index_name_]** ダイアログ ボックスの **[ストレージ]** ページでは、次の情報が利用できます。  
  
 **[ファイル グループ]**  
 指定したファイル グループのインデックスを格納します。 一覧には、標準 (ROW) ファイル グループのみが表示されます。 既定で選択されているのは、データベースのプライマリ ファイル グループです。  
  
 **[Filestream ファイル グループ]**  
 FILESTREAM データのファイル グループを指定します。 この一覧には FILESTREAM ファイル グループのみが表示されます。 既定で選択されているのは、PRIMARY FILESTREAM ファイル グループです。  
  
 **パーティション構成**  
 パーティション構成のインデックスを格納します。 **[パーティション構成]** をクリックすると、下のグリッドが有効になります。 既定で選択されているのは、テーブルのデータを格納するために使用されるパーティション構成です。 一覧にある他のパーティション構成を選択すると、グリッドに表示される情報が更新されます。  
  
 この [パーティション構成] オプションは、データベースにパーティション構成がなければ使用できません。  
  
 **[FileStream パーティション構成]**  
 FILESTREAM データのパーティション構成を指定します。 パーティション構成は、 **[パーティション構成]** オプションで指定した構成と対称である必要があります。  
  
 テーブルがパーティション分割されていない場合、このフィールドは空白です。  
  
 **[パーティション構成パラメーター]**  
 パーティション構成に使用される列の名前を表示します。  
  
 **[テーブル列]**  
 パーティション構成にマップされるテーブルまたはビューを選択します。  
  
 **[列データ型]**  
 列のデータ型情報を表示します。  
  
> [!NOTE]  
>  テーブルの列が計算列の場合、 **[列データ型]** には "計算列" と表示されます。  
  
 **[インデックスの移動中に DML ステートメントのオンライン処理を許可する]**  
 インデックス操作中に、基本となるテーブルやクラスター化インデックス データ、および関連する非クラスター化インデックスにユーザーがアクセスできるようにします。  
  
> [!NOTE]  
>  XML インデックスの場合、またはインデックスが無効なクラスター化インデックスの場合、このオプションは使用できません。  
  
 **[並列処理の最大限度の設定]**  
 並列実行プランの実行中に使用されるプロセッサ数を制限します。 既定値は 0 です。0 の場合、実際に使用可能な CPU 数が使用されます。 値を 1 に設定すると、並列実行プランが生成されなくなります。値を 1 よりも大きな数値に設定すると、1 つのクエリ実行で使用されるプロセッサの最大数が限定されます。 このオプションは、ダイアログ ボックスが **再構築** または **再作成** 状態のときにのみ使用できます。  
  
> [!NOTE]  
>  使用可能な CPU 数よりも多い値を指定すると、実際に使用可能な CPU 数が使用されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-move-an-existing-index-to-a-different-filegroup"></a>既存のインデックスを別のファイル グループに移動するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates the TransactionsFG1 filegroup on the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP TransactionsFG1;  
    GO  
    /* Adds the TransactionsFG1dat3 file to the TransactionsFG1 filegroup. Please note that you will have to change the filename parameter in this statement to execute it without errors.  
    */  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = TransactionsFG1dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\DATA\TransactionsFG1dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP TransactionsFG1;  
    GO  
    /*Creates the IX_Employee_OrganizationLevel_OrganizationNode index  
      on the TransactionsPS1 filegroup and drops the original IX_Employee_OrganizationLevel_OrganizationNode index.  
    */  
    CREATE NONCLUSTERED INDEX IX_Employee_OrganizationLevel_OrganizationNode  
        ON HumanResources.Employee (OrganizationLevel, OrganizationNode)  
        WITH (DROP_EXISTING = ON)  
        ON TransactionsFG1;  
    GO  
    ```  
  
 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  
  
  
