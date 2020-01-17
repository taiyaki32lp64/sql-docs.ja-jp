---
title: FileTable の管理 | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ef64d09c7f99f5081ebd1cbcdd7418614c3b41f1
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908746"
---
# <a name="manage-filetables"></a>FileTable の管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable を管理するための一般的な管理タスクについて説明します。  
  
##  <a name="HowToEnumerate"></a>方法:FileTable と関連オブジェクトの一覧を取得する  
 FileTable の一覧を取得するには、次のいずれかのカタログ ビューに対してクエリを実行します。  
  
-   [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
  
-   [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) (**is_filetable** 列の値を確認)  
  
```sql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 関連付けられている FileTable の作成時に作成されたシステム定義オブジェクトの一覧を取得するには、カタログ ビュー [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md) に対してクエリを実行します。  
  
```sql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
FROM sys.filetable_system_defined_objects;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> データベース レベルでの非トランザクション アクセスの無効化および再有効化  
 特定の管理タスクに必要な排他アクセスを取得するために、場合によっては一時的に非トランザクション アクセスを無効にする必要があります。  
  
 **非トランザクション アクセスのレベルを変更するときの ALTER DATABASE ステートメントの動作**  
  
-   非トランザクション アクセスが READ_ONLY または OFF に設定されている場合、ALTER DATABASE コマンドは、要求された操作と競合する開いたファイル ハンドルがある間はユーザーに制御を返しません。 この操作と競合するファイル ハンドルには、次のようなものがあります。  
  
    -   アクセスを **NONE**に設定している場合は、すべての開いているファイル ハンドル。  
  
    -   アクセスを **READ_ONLY**に設定している場合は、書き込みアクセスで開かれているすべてのファイル ハンドル。  
  
     開いているファイル ハンドルを終了する方法の詳細については、このトピックの「 [FileTable に関連付けられた開いているファイル ハンドルの終了](#BasicsKilling) 」を参照してください。  
  
     ALTER DATABASE コマンドが取り消されるかまたはタイムアウトによって終了した場合、トランザクション アクセスのレベルは変更されません。  
  
-   WITH \<termination> 句 (ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT) を指定して ALTER DATABASE ステートメントを呼び出した場合、開いているすべての非トランザクション ファイル ハンドルが終了します。  
  
> [!WARNING]  
>  開いているファイル ハンドルを終了すると、保存されていないデータをユーザーが失う可能性があります。 この動作は、ファイル システム自体の動作と一致しています。  
  
 **非トランザクション アクセスを無効化した場合の影響**  
  
 データベース レベルでの非トランザクション アクセスのレベルを変更した場合、データベース レベルのディレクトリの下の FileTable ディレクトリに次の影響が及びます。  
  
-   アクセスを **NONE**に設定した場合、すべての FileTable ディレクトリとそのコンテンツはアクセスも表示もできなくなります。  
  
-   アクセスを **READ_ONLY**に設定した場合、すべての FileTable ディレクトリとそのコンテンツも読み取り専用になります。  
  
 インスタンス レベルで FILESTREAM を無効化した場合、そのインスタンスのデータベース レベルのディレクトリと、その下の FileTable ディレクトリに、次の影響が及びます。  
  
-   FILESTREAM がインスタンス レベルで無効化された場合、そのインスタンスのデータベース レベルのディレクトリはすべて表示されません。  
  
###  <a name="HowToDisable"></a> 方法:データベース レベルで非トランザクション アクセスを無効化および再有効化する  
 詳細については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
 **完全な非トランザクション アクセスを無効化するには**  
 **ALTER DATABASE** ステートメントを呼び出し、 **NON_TRANSACTED_ACCESS** の値を **READ_ONLY** または **OFF**に設定します。  
  
```sql  
-- Disable write access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **完全な非トランザクション アクセスを再有効化するには**  
 **ALTER DATABASE** ステートメントを呼び出し、 **NON_TRANSACTED_ACCESS** の値を **FULL**に設定します。  
  
```sql  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> 方法:データベースの FileTable が必ず表示されるようにする  
 以下のすべての条件が満たされる場合、データベース レベルのディレクトリとその下の FileTable ディレクトリは表示状態になります。  
  
1.  インスタンス レベルで FILESTREAM が有効になっている。  
  
2.  データベース レベルで非トランザクション アクセスが有効になっている。  
  
3.  データベース レベルで有効なディレクトリが指定されている。  

##  <a name="BasicsEnabling"></a> テーブル レベルでの FileTable 名前空間の無効化および再有効化  
 FileTable 名前空間を無効にすると、FileTable に対して作成されたすべてのシステム定義制約およびトリガーが無効になります。 これは、FileTable セマンティクスの適用を行うことなく [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作を使用して FileTable を大幅に再編成する必要がある場合に便利です。 ただし、これらの操作によって FileTable の一貫性が損なわれ、FileTable 名前空間の再有効化が妨げられる可能性があります。  
  
 FileTable 名前空間を無効にすると、次のような結果になります。  
  
-   FileTable 列およびデータは、テーブルから物理的に削除されません。  
  
-   FileTable ディレクトリと、それに含まれているファイルおよびディレクトリは、ファイル システムから消失し、ファイル I/O アクセスに使用できなくなります。  
  
-   システム定義の FileTable 列を削除または再作成することはできませんが、これらの列は DML 操作で通常の列と同様に動作します。  
  
-   開いているファイル ハンドルがあると、FileTable 制約を無効化できません。この操作には、テーブルのスキーマ ロックが必要になるためです。  
  
-   FileTable 名前空間の無効化後、すべての FileTable セマンティクスの適用が、システム定義の制約およびトリガーも含めて、停止されます。  
  
 FileTable 名前空間を再有効化すると、次のような結果になります。  
  
-   FileTable の一貫性がチェックされます。 不整合が見つかった場合は、エラーが発生し、FileTable は無効のままになります。それ以外の場合、FileTable は再有効化されます。  
  
-   FileTable セマンティクスの適用が、システム定義の制約およびトリガーも含めて、復元されます。  
  
-   FileTable ディレクトリと、それに含まれているファイルおよびディレクトリは、ファイル システムに表示され、ファイル I/O アクセスに使用できるようになります。  
  
###  <a name="HowToEnableNS"></a> 方法:テーブル レベルで FileTable 名前空間を無効化および再有効化する  
 **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** オプションを指定して ALTER TABLE ステートメントを呼び出します。  
  
 **FileTable 名前空間を無効にするには**  
 ```sql  
ALTER TABLE filetable_name  
DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **FileTable 名前空間を再有効化するには**  
 ```sql  
ALTER TABLE filetable_name  
ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> FileTable に関連付けられた開いているファイル ハンドルの終了  
 FileTable に格納されているファイルへの開いているハンドルにより、特定の管理タスクで必要となる排他アクセスが妨げられる場合があります。 緊急のタスクを有効にするには、場合により 1 つまたは複数の FileTable に関連付けられている開いているファイル ハンドルを終了する必要があります。  
  
> [!WARNING]  
>  開いているファイル ハンドルを終了すると、保存されていないデータをユーザーが失う可能性があります。 この動作は、ファイル システム自体の動作と一致しています。  
  
###  <a name="HowToListOpen"></a> 方法:FileTable に関連付けられた開いているファイル ハンドルの一覧を取得する  
 カタログ ビュー [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) に対してクエリを実行します。  
  
```sql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> 方法:FileTable に関連付けられた開いているファイル ハンドルを終了する  
 データベースまたは FileTable のすべての開いているファイル ハンドルを終了するか、特定のハンドルを終了するための適切な引数を指定して、[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) ストアド プロシージャを呼び出します。  
  
```sql  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> 方法:FileTable によって保持されているロックを識別する  
 FileTable によって取得されるほとんどのロックは、アプリケーションによって開かれたファイルに対応します。  
  
 **開いているファイルおよび関連付けられているロックを識別するには**  
 動的管理ビュー [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) の **request_owner_id** フィールドを [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) の **fcb_id** フィールドと結合します。 場合によっては、ロックが単一の開いているファイル ハンドルと対応しないこともあります。  
  
```sql  
SELECT opened_file_name  
FROM sys.dm_filestream_non_transacted_handles  
WHERE fcb_id IN  
    ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> FileTable セキュリティ  
 FileTable に格納されているファイルとディレクトリは、SQL Server セキュリティのみによって保護されます。 テーブルおよび列ベースのセキュリティは、ファイル システム アクセスおよび [!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスに適用されます。 Windows ファイル システム セキュリティ API および ACL 設定はサポートされていません。  
  
 FILESTREAM ファイル グループおよびコンテナーに適用可能なセキュリティおよびアクセス許可は、FileTable にも適用されます。これは、ファイル データは FileTable の FILESTREAM 列として格納されるためです。  
  
 **FileTable セキュリティと Transact-SQL アクセス**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] FileTable のデータに対するアクセスは、他のすべてのテーブルと同様にセキュリティで保護されます。 データに対するアクセスや変更を行う各操作に関して、適切なテーブルおよび列レベルのセキュリティ チェックが行われます。  
  
 **FileTable セキュリティとファイル システム アクセス**  
 ファイル システム API には、FileTable に格納されているファイルまたはディレクトリへのハンドルを開くための、FileTable の行全体に対する適切な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 権限 (つまり、テーブル レベルの権限) が必要です。 FileTable の列に対する適切な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 権限がユーザーに与えられていない場合、ファイル システム アクセスは拒否されます。  
  
##  <a name="OtherBackup"></a> バックアップと FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して FileTable をバックアップすると、FILESTREAM データがデータベースの構造化データと共にバックアップされます。 FILESTREAM データをリレーショナル データと共にバックアップしない場合は、部分バックアップを使用して FILESTREAM ファイル グループを除外できます。  
  
 **FileTable バックアップのトランザクションの整合性**  
  
 多くの管理ツールおよび操作 (バックアップ、ログ バックアップ、トランザクション レプリケーションなど) では、トランザクション ログを読み取ることにより、トランザクション的に一貫したデータを読み取ります。 このとき、トランザクションの一部として更新された任意の FILESTREAM データが読み取られます。 非トランザクション アクセスがデータベース レベルで有効になっていない場合、これらのツールおよび操作は、完全なトランザクションの一貫性を保って動作します。  
  
 ただし、完全な非トランザクション アクセスが有効である場合、ツールまたはプロセスによってトランザクション ログから読み取られたトランザクション以降に (非トランザクション更新を介して) 更新されたデータが FileTable に含まれる可能性があります。 つまり、特定のトランザクションの "ある時点" への復元操作に、そのトランザクションよりも新しい FILESTREAM データが含められる可能性があります。 これは、非トランザクション更新が FileTable で許可される場合に想定される動作です。  
  
##  <a name="Monitor"></a> SQL Server Profiler と FileTables  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler は、FileTable に格納されているファイルに対するトレース出力内の Windows File Open および File Close 操作をキャプチャできます。  
  
##  <a name="OtherAuditing"></a> 監査と FileTable  
 FileTable は、他のテーブルと同じように監査できます。 ただし、Win32 アクセス パターンは、セット ベースの操作ではありません。 ファイル システムの単一のアクションが複数の Transact-SQL DML 操作に変換されます。 たとえば、Microsoft Word でファイルを開く操作は、複数の操作 (開く操作、閉じる操作、作成、名前の変更、削除) および対応する Transact-SQL DML アクティビティに変換されます。 その結果、詳細な監査レコードが生成され、ファイル システム アクションとそれに対応する Transact-SQL DML 監査レコードの間でレコードを関連付けることが困難になります。  
  
##  <a name="OtherDBCC"></a> DBCC と FileTable  
 DBCC CHECKCONSTRAINTS を使用すると、システム定義の制約を含む FileTable に対する制約を検証できます。  
  
## <a name="see-also"></a>参照  
 [FileTable と他の SQL Server 機能の互換性](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)   
 [FileTable DDL、関数、ストアド プロシージャ、およびビュー](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
