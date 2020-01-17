---
title: ユーザー データベースの移動 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- editions [SQL Server], moving databases between
- moving full-text catalogs
- scheduled disk maintenace [SQL Server]
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- moving user databases
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: ad9a4e92-13fb-457d-996a-66ffc2d55b79
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 602ac6de5a2b623e33b1b85b46a9f8cf31e0b225
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871721"
---
# <a name="move-user-databases"></a>ユーザー データベースの移動
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) ステートメントの FILENAME 句で新しいファイルの場所を指定することで、ユーザー データベースのデータ ファイル、ログ ファイル、およびフルテキスト カタログ ファイルを新しい場所に移動することができます。 この方法は、同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス内でデータベース ファイルを移動する場合に使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスや、別のサーバーにデータベースを移動する場合は、 [バックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md) 操作か [デタッチ操作とアタッチ操作](move-a-database-using-detach-and-attach-transact-sql.md)を使用します。  
  
## <a name="considerations"></a>考慮事項  
 データベースを別のサーバー インスタンスに移動するときは、ユーザーおよびアプリケーションに一貫した使用環境を提供するために、データベースのメタデータの一部またはすべてを作成し直す必要が生じる場合があります。 詳細については、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md)」を参照してください。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の一部の機能は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]がデータベース ファイルに情報を格納する方法を変更します。 これらの機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定のエディションでのみ使用できます。 これらの機能を備えたデータベースを、それらをサポートしない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションに移動することはできません。 現在のデータベースで有効なエディション固有の機能をすべて一覧表示するには、sys.dm_db_persisted_sku_features 動的管理ビューを使用します。  
  
 このトピックの手順では、データベース ファイルの論理名が必要です。 論理名を取得するには、 [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) カタログ ビューで name 列に対するクエリを実行します。  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]以降では、フルテキスト カタログは、ファイル システムに格納されるのではなく、データベースに統合されています。 フルテキスト カタログは、データベースの移動時に自動的に移動されるようになりました。  
  
## <a name="planned-relocation-procedure"></a>計画に従った再配置の手順  
 計画に従った再配置の一環としてデータ ファイルやログ ファイルを移動するには、次の手順を実行します。  
  
1.  次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name SET OFFLINE;  
    ```  
  
2.  ファイルを新しい場所に移動します。  
  
3.  移動したそれぞれのファイルに対して、次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name, FILENAME = 'new_path\os_file_name' );  
    ```  
  
4.  次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name SET ONLINE;  
    ```  
  
5.  次のクエリを実行して、ファイルが変更されたことを確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="relocation-for-scheduled-disk-maintenance"></a>スケジュールされたディスク メンテナンスでの再配置  
 スケジュールされたディスク メンテナンスの一環としてファイルを再配置するには、次の手順を実行します。  
  
1.  移動対象のそれぞれのファイルに対して、次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
2.  メンテナンスを行うため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを停止するか、システムをシャットダウンします。 詳しくは、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」をご覧ください。  
  
3.  ファイルを新しい場所に移動します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスまたはサーバーを再起動します。 詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」を参照してください。  
  
5.  次のクエリを実行して、ファイルが変更されたことを確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="failure-recovery-procedure"></a>障害復旧の手順  
 ハードウェア障害が原因でファイルを移動する必要がある場合、次の手順に従って別の場所にファイルを再配置します。  
  
> [!IMPORTANT]  
>  データベースを起動できないとき、つまり、データベースが問題のあるモードか復旧できない状態にある場合、ファイルを移動できるのは、sysadmin 固定ロールのメンバーだけです。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが起動していたら停止します。  
  
2.  コマンド プロンプトで次のいずれかのコマンドを入力し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを master のみを復旧するモードで開始します。  
  
    -   既定 (MSSQLSERVER) のインスタンスの場合は、次のコマンドを実行します。  
  
        ```  
        NET START MSSQLSERVER /f /T3608  
        ```  
  
    -   名前付きインスタンスの場合は、次のコマンドを実行します。  
  
        ```  
        NET START MSSQL$instancename /f /T3608  
        ```  
  
     詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md) 」を参照してください。  
  
3.  移動対象の各ファイルに対して、 **sqlcmd** コマンドか [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して、次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
     **sqlcmd** ユーティリティの使用方法については、「 [sqlcmd ユーティリティの使用](../scripting/sqlcmd-use-the-utility.md)」を参照してください。  
  
4.  **sqlcmd** ユーティリティまたは [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を終了します。  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを停止します。  
  
6.  ファイルを新しい場所に移動します。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを開始します。 たとえば、 `NET START MSSQLSERVER`を実行します。  
  
8.  次のクエリを実行して、ファイルが変更されたことを確認します。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="examples"></a>使用例  
 次の例では、計画に従った再配置の一環として、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] のログ ファイルを新しい場所に移動します。  
  
```  
USE master;  
GO  
-- Return the logical file name.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
GO  
ALTER DATABASE AdventureWorks2012 SET OFFLINE;  
GO  
-- Physically move the file to a new location.  
-- In the following statement, modify the path specified in FILENAME to  
-- the new location of the file on your server.  
ALTER DATABASE AdventureWorks2012   
    MODIFY FILE ( NAME = AdventureWorks2012_Log,   
                  FILENAME = 'C:\NewLoc\AdventureWorks2012_Log.ldf');  
GO  
ALTER DATABASE AdventureWorks2012 SET ONLINE;  
GO  
--Verify the new location.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [システム データベースの移動](system-databases.md)   
 [データベース ファイルの移動](move-database-files.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
