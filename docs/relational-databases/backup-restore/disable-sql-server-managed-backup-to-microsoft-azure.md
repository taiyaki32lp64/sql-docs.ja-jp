---
title: Azure Blob Storage へのマネージド バックアップを無効にする
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 3e02187f-363f-4e69-a82f-583953592544
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d85df8c4d07a61c75dcb42eadbc9c7cdae4faad6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257973"
---
# <a name="disable-sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure への SQL Server マネージド バックアップを無効にする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、データベース レベルとインスタンス レベルの両方で、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を無効または一時停止する方法について説明します。  
  
##  <a name="DatabaseDisable"></a> データベースに対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を無効にする  
 システム ストアド プロシージャの [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) を使用し、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 設定を無効にできます。 特定のデータベースの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の構成を有効または無効にするには、 *\@enable_backup* を使用します。構成設定を有効にする場合は 1、無効にする場合は 0 を指定します。  
  
#### <a name="to-disable-includess_smartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>特定のデータベースに対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を無効にするには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
```sql
EXEC msdb.managed_backup.sp_backup_config_basic  
                @database_name = 'TestDB'   
                ,@enable_backup = 0;  
GO
```

> [!NOTE]
> ご利用の構成によって、`@container_url` パラメーターの設定が必要になる場合があります。
  
##  <a name="DatabaseAllDisable"></a> インスタンス上のすべてのデータベースについて [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を無効にする  
 インスタンスで現在 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] が有効になっているすべてのデータベースから [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の構成設定を無効にするための手順を次に示します。  ストレージ URL、保有期間、SQL 資格情報などの構成設定はメタデータに残るため、後で [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] をデータベースに対して有効にした場合に使用できます。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] サービスを一時的に停止するだけの場合は、このトピックの以降のセクションで説明するマスターの切り替えを使用できます。  
  
#### <a name="to-disable-includess_smartbackupincludesss-smartbackup-mdmd-for-all-the-databases"></a>すべてのデータベースについて [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を無効にするには:  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 次の例では、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] がインスタンス レベルで構成され、インスタンスのすべてのデータベースで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] が有効になっているかどうかを識別し、システム ストアド プロシージャ **sp_backup_config_basic** を実行して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を無効にします。  
  
```sql
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       msdb.managed_backup.fn_backup_db_config (NULL)  
       WHERE is_managed_backup_enabled = 1 
       AND is_dropped = 0
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC msdb.managed_backup.sp_backup_config_basic    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
```  
  
 インスタンスのすべてのデータベースの構成設定を確認するには、次のクエリを使用します。  
  
```sql
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL);  
GO  
```  
  
##  <a name="InstanceDisable"></a> インスタンスについて [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の既定設定を無効にする  
 インスタンス レベルの既定の設定は、そのインスタンスに作成されたすべての新しいデータベースに適用されます。  既定の設定が必要なくなった場合は、**managed_backup.sp_backup_config_basic** システム ストアド プロシージャを使用し、 *\@database_name* パラメーターを NULL に設定して、この構成を無効にすることができます。 無効にしても、ストレージ URL、保有期間の設定、SQL 資格情報名など、その他の構成設定は削除されません。 これらの設定は、後でインスタンスに対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にする場合に使用されます。  
  
#### <a name="to-disable-includess_smartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の既定の構成設定を無効にするには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql
    EXEC msdb.managed_backup.sp_backup_config_basic  
                    @enable_backup = 0;  
    GO
    ```  
  
##  <a name="InstancePause"></a> インスタンス レベルで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を一時停止する  
 一時的に少しの間 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] サービスを停止する必要が生じる場合があります。  マスターを切り替えるための **managed_backup.sp_backup_master_switch** システム ストアド プロシージャを使用すると、インスタンス レベルで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] サービスを無効にできます。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を再開するには、同じストアド プロシージャを使用します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を無効にするか有効にするかを定義するには、\@state パラメーターが使用されます。  
  
#### <a name="to-pause-includess_smartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>Transact-SQL を使用して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] サービスを一時停止するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
```sql
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go
```  
  
#### <a name="to-resume-includess_smartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>Transact-SQL を使用して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を再開するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
```sql
Use msdb;  
Go  
EXEC managed_backup.sp_backup_master_switch @new_state=1;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Microsoft Azure への SQL Server マネージド バックアップを有効にする](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)  
  
  
