---
title: Azure でのデータベース ファイルのファイル スナップショット バックアップ | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 17a81fcd-8dbd-458d-a9c7-2b5209062f45
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: aed634232901aa116fddf361d3c3347d1e462eb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086282"
---
# <a name="file-snapshot-backups-for-database-files-in-azure"></a>Azure でのデータベース ファイルのスナップショット バックアップ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイル スナップショット バックアップは、Azure BLOB ストレージ サービスを使用して格納したデータベース ファイルを、Azure スナップショットを使用してほぼ瞬時にバックアップし、迅速に復元できます。 この機能により、バックアップと復元のポリシーを簡素化することができます。 ライブ デモについては、 [特定の時点での復元に関するデモ](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)を参照してください。 Azure Blob ストレージ サービスを使用してデータベース ファイルを格納する方法の詳細については、「[Microsoft Azure 内の SQL Server データ ファイル](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)」を参照してください。  
  
 ![スナップショット バックアップのアーキテクチャの図](../../relational-databases/backup-restore/media/snapshotbackups.PNG "スナップショット バックアップのアーキテクチャの図")  
  
 **ダウンロード**  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]をダウンロードするには、  **[評価センター](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** に移動してください。  
  
-   Azure アカウントをすでにお持ちですか?  既にお持ちの場合は、 **[こちら](https://azure.microsoft.com/services/virtual-machines/sql-server/)** にアクセスして、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] がインストール済みの仮想マシンをすぐにご利用いただけます。  
  
## <a name="using-azure-snapshots-to-back-up-database-files-stored-in-azure"></a>Azure のスナップショットを使用した Azure に格納されているデータベース ファイルのバックアップ  
  
### <a name="what-is-a-includessnoversionincludesssnoversion-mdmd-file-snapshot-backup"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイル スナップショット バックアップとは  
 ファイル スナップショット バックアップは、データベース ファイルが含まれる BLOB とそれらのファイル スナップショットに対するポインターが含まれるバックアップ ファイルの、一連の Azure スナップショットで構成されます。 各ファイル スナップショットは、コンテナーにベース BLOB とともに格納されています。 バックアップ ファイル自体を URL、ディスク、テープに書き込むように指定できます。 URL へのバックアップをお勧めします。 バックアップの詳細については「[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)」、URL へのバックアップについては「[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」を参照してください。  
  
 ![スナップショット機能のアーキテクチャ](../../relational-databases/backup-restore/media/snapshotbackups-flat.png "スナップショット機能のアーキテクチャ")  
  
 ベース BLOB を削除すると、バックアップ セットが無効になり、BLOB とそのファイル スナップショットすべてを明示的に削除するように選択しない限り、ファイル スナップショットが含まれる BLOB を削除できなくなります。 さらに、データベースまたはデータ ファイルを削除しても、ベース BLOB やそのファイル スナップショットは削除されません。 また、バックアップ ファイルを削除しても、そのバックアップ セット内のファイル スナップショットは削除されません。 ファイル スナップショットのバックアップ セットを削除するには、 **sys.sp_delete_backup** システム ストアド プロシージャを使用します。  
  
 **データベースの完全バックアップ:** ファイル スナップショット バックアップを使用してデータベースの完全バックアップを実行すると、データベースを構成する各データ ファイルとログ ファイルの Azure スナップショットが作成され、トランザクション ログのバックアップ チェーンが確立されて、バックアップ ファイルにファイル スナップショットの場所が書き込まれます。  
  
 **トランザクション ログのバックアップ**: ファイル スナップショット バックアップを使用してトランザクション ログのバックアップを実行すると、(トランザクション ログだけでなく) 各データベース ファイルのファイル スナップショットが作成され、バックアップ ファイルにファイル スナップショットの場所情報が記録されて、トランザクション ログ ファイルが切り捨てられす。  
  
> [!IMPORTANT]  
>  トランザクション ログのバックアップ チェーンの確立に必要な最初の完全バックアップ (ファイル スナップショット バックアップの場合もあり) の後、各トランザクション ログのファイル スナップショット ファイルはすべて、データベースの復元やログの復元の実行に使用できるため、トランザクション ログのバックアップのみを実行するのみで済みます。 データベースの最初の完全バックアップの後は、各ファイル スナップショットや各データベース ファイルのベース BLOB の現在の状態の違いは Azure BLOB ストレージ サービスが処理するため、追加の完全バックアップや差分バックアップは不要です。  
  
> [!NOTE]  
>  Microsoft Azure BLOB ストレージ サービスでの SQL Server 2016 の使用方法に関するチュートリアルについては、「[チュートリアル:Azure Blob Storage サービスと SQL Server 2016 データベースの使用](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)  
  
### <a name="restore-using-file-snapshot-backups"></a>ファイル スナップショット バックアップを使用した復元  
 各ファイル スナップショット バックアップ セットには各データベース ファイルのファイル スナップショットが含まれているため、復元プロセスには、最大で隣接する 2 つのファイル スナップショット バックアップ セットが必要です。 これは、バックアップ セットが完全バックアップまたはログ バックアップからのものであるかに関係なく当てはまります。 これは、従来のストリーミング バックアップ ファイルを使用して復元プロセスを実行するときとまったく異なります。 従来のストリーミング バックアップでは、復元プロセスにバックアップ セットのチェーン全体 (完全バックアップ、差分バックアップ、1 つ以上のトランザクション ログのバックアップ) を使用する必要があります。 復元プロセスの復旧の部分は、復元にファイル スナップショット バックアップまたはストリーミング バックアップ セットを使用しているかどうかに関係なく、同じです。  
  
 **任意のバックアップ セットの時点まで**: RESTORE DATABASE 操作を実行して特定のファイル スナップショット バックアップ セットの時点までデータベースを復元するには、ベース BLOB 自体と特定のバックアップ セットのみが必要です。 RESTORE DATABASE 操作を実行するにはトランザクション ログのファイル スナップショット バックアップ セットを使用できるため、この種類の RESTORE DATABASE オプションの実行には通常、トランザクション ログのバックアップ セットを使用し、データベースの完全バックアップ セットをほとんど使用されません。 このトピックの最後に、この手法について説明する例を紹介します。  
  
 **2 つのファイル スナップショット バックアップ セット間の時点まで**: RESTORE DATABASE 操作を実行して、2 つの隣接したトランザクション ログのバックアップ セットの間の特定の時点までデータベースをバックアップするには、2 つのトランザクション ログのバックアップ セット (それぞれデータベースを復元する時点の前後に 1 つ) のみが必要です。 これを実現するには、前の時点のトランザクション ログのファイル スナップショット バックアップ セットを使用して WITH NORECOVERY で RESTORE DATABASE 操作を実行し、後の時点のトランザクション ログのファイル スナップショット バックアップ セットを使用して WITH RECOVERY で RESTORE LOG 操作を実行して、STOPAT 引数を使用してトランザクション ログのバックアップからの復旧を停止する時点を指定します。 このトピックの最後に、この手法について説明する例を紹介します。 ライブ デモについては、 [特定の時点での復元に関するデモ](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)を参照してください。  
  
### <a name="file-backup-set-maintenance"></a>ファイル バックアップ セットのメンテナンス  
 **ファイル スナップショット バックアップ セットの削除**: FORMAT 引数を使用してファイル スナップショット バックアップ セットを上書きすることはできません。 元のファイル スナップショット バックアップで作成されたファイル スナップショットが孤立したまま残されるのを避けるために、FORMAT 引数は使用できません。 ファイル スナップショットのバックアップ セットを削除するには、 **sys.sp_delete_backup** システム ストアド プロシージャを使用します。 このストアド プロシージャは、バックアップ セットを構成するバックアップ ファイルとファイル スナップショットを削除します。 別のメソッドを使用してファイル スナップショットのバックアップ セットを削除すると、バックアップ セット内のファイル スナップショットを削除することなくバックアップ ファイルが削除されることがあります。  
  
 **孤立したバックアップ ファイル スナップショットの削除**: バックアップ ファイルが **sys.sp_delete_backup** システム ストアド プロシージャを使用せずに削除された場合、またはデータベースやデータベース ファイルが含まれる BLOB に関連付けられたバックアップ ファイル スナップショットが存在する間にデータベースやデータベース ファイルが削除された場合は、ファイル スナップショットが孤立している可能性があります。 ファイル スナップショットが孤立していることを特定するには、 **sys.fn_db_backup_file_snapshots** のシステム関数を使用してデータベース ファイルのすべてのファイル スナップショットを一覧表示します。 ファイル スナップショットが特定のファイル スナップショットのバックアップ セットの一部であることを特定するには、RESTORE FILELISTONLY システム ストアド プロシージャを使用します。 その後、 **sys.sp_delete_backup_file_snapshot** システム ストアド プロシージャを使用して各バックアップ ファイルの孤立したスナップショットを削除できます。 このトピックの最後に、このシステム関数とこれらのシステム ストアド プロシージャを使用する例を紹介します。 詳細については、「[sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)」、「[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)」、「[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)」、「[RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)」を参照してください。  
  
### <a name="considerations-and-limitations"></a>注意点と制限事項  
 **Premium Storage:** Premium Storage を使用するときは、次の制限が適用されます。  
  
-   バックアップ ファイル自体は、Premium Storage を使用して格納できません。  
  
-   バックアップの間隔は、10 分よりも短くすることはできません。  
  
-   レポートに格納できるスナップショットの最大数は 100 個です。  
  
-   RESTORE WITH MOVE が必須です。  
  
-   Premium Storage の詳細については、[Premium Storage: Azure 仮想マシン ワークロード向けの高パフォーマンス ストレージ](https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/)に関するページを参照してください  
  
 **単一のストレージ アカウント**: ファイル スナップショットと目的の BLOB では同じストレージ アカウントが使用されている必要があります。  
  
 **一括復旧モデル**: 一括ログ復旧モードを使用して最小ログ記録トランザクションを含むトランザクション ログのバックアップを実行するときは、トランザクション ログのバックアップを使用してログの復元 (特定の時点への復旧を含む) を実行することはできません。 代わりに、ファイル スナップショット バックアップ セットの特定の時点までのデータベースの復元を実行します。 この制限は、ストリーミング バックアップの制限と同じです。  
  
 **オンライン復元**: ファイル スナップショット バックアップを使用するときは、オンライン復元を実行することはできません。 オンライン復元の詳細については、「[オンライン復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)」を参照してください。  
  
 **課金**: SQL Server のファイル スナップショット バックアップを使用すると、データの変化に応じて追加料金が発生します。 詳細については、「 [スナップショットの課金方法について](https://msdn.microsoft.com/library/azure/hh768807.aspx)」を参照してください。  
  
 **アーカイブ**: ファイル スナップショット バックアップをアーカイブする場合は、BLOB ストレージまたはストリーミング バックアップにアーカイブできます。 Blob ストレージにアーカイブするには、ファイル スナップショット バックアップ セット内のスナップショットを別個の BLOB にコピーします。 ストリーミング バックアップにアーカイブするには、ファイル スナップショット バックアップを新しいデータベースとして復元し、圧縮や暗号化を使用した通常のストリーミング バックアップを実行して、必要に応じて、ベース BLOB とは別個にアーカイブします。  
  
> [!IMPORTANT]  
>  複数のファイル スナップショット バックアップの管理には、パフォーマンス上わずかなオーバーヘッドしか発生しません。 ただし、管理するファイル スナップショット バックアップの数が多すぎる場合は、データベースに対してI/O パフォーマンス上の影響を及ぼす可能性があります。 復旧ポイントをサポートする目的において必要なファイル スナップショット バックアップのみを管理することをお勧めします。  
  
## <a name="backing-up-the-database-and-log-using-a-file-snapshot-backup"></a>ファイル スナップショット バックアップを使用してデータベースとログをバックアップする  
 次の例では、ファイル スナップショット バックアップを使用して、AdventureWorks2016 のサンプル データベースを URL にバックアップします。  
  
```  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2016  
   SET RECOVERY FULL;  
GO  
-- Back up the full AdventureWorks2016 database.  
BACKUP DATABASE AdventureWorks2016   
TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016.bak'   
WITH FILE_SNAPSHOT;  
GO  
-- Back up the AdventureWorks2016 log using a time stamp in the backup file name.  
DECLARE @Log_Filename AS VARCHAR (300);  
SET @Log_Filename = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_Log_'+   
REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
BACKUP LOG AdventureWorks2016  
 TO URL = @Log_Filename WITH FILE_SNAPSHOT;  
GO  
```  
  
## <a name="restoring-from-a-includessnoversionincludesssnoversion-mdmd-file-snapshot-backup"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイル スナップショット バックアップからの復元  
 次の例では、トランザクション ログのファイル スナップショット バックアップ セットを使用して AdventureWorks2016 データベースを復元し、復旧操作を示します。 データベースは、単一のトランザクション ログ ファイル スナップショットのバックアップ セットから復元できます。  
  
```  
RESTORE DATABASE AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_16_00_00.trn'   
WITH RECOVERY, REPLACE;  
GO  
```  
  
## <a name="restoring-from-a-includessnoversionincludesssnoversion-mdmd-file-snapshot-backup-to-a-point-in-time"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイル スナップショット バックアップからの特定の時点への復元  
 次の例では、2 つのトランザクション ログのファイル スナップショット バックアップ セットを使用して AdventureWorks2016 データベースをその特定の時点の状態に復元し、復旧操作を示します。  
  
```  
RESTORE DATABASE AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_16_00_00.trn'   
WITH NORECOVERY,REPLACE;  
GO   
  
RESTORE LOG AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_18_00_00.trn'   
WITH RECOVERY,STOPAT = 'May 18, 2015 5:35 PM';  
GO  
```  
  
## <a name="deleting-a-database-file-snapshot-backup-set"></a>データベース ファイル スナップショット バックアップ セットを削除する  
 ファイル スナップショットのバックアップ セットを削除するには、 **sys.sp_delete_backup** システム ストアド プロシージャを使用します。 データベース名を指定すると、指定されたファイル スナップショット バックアップ セットが実際に指定したデータベースのバックアップであることをシステムが検証します。 データベース名を指定しないと、このような検証が行われることなく、指定したバックアップ セットとそのファイル スナップショットが削除されます。 詳細については、「[sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)」を参照してください。  
  
> [!WARNING]  
>  Microsoft Azure 管理ポータルや SQL Server Management Studio の Azure Storage ビューアーなどの別の方法を使用してファイル スナップショット バックアップ セットの削除を試行しても、そのバックアップ セット内のファイル スナップショットは削除されません。 これらのツールは、ファイル スナップショット バックアップ セット内のファイル スナップショットへのポインターが含まれる、バックアップ ファイル自体のみを削除します。 **sys.fn_db_backup_file_snapshots** システム関数を使用して、バックアップ ファイルが不適切に削除された後にバックアップ ファイル スナップショットが残っていないかを確認し、その後 **sys.sp_delete_backup_file_snapshot** システム ストアド プロシージャを使用して個々のバックアップ ファイル スナップショットを削除します。  
  
 次の例では、指定したバックアップ セットを構成するバックアップ ファイルとファイル スナップショットを含む、指定のファイル スナップショット バックアップ セットを削除します。  
  
```  
sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016.bak', 'adventureworks2016' ;  
GO  
  
```  
  
## <a name="viewing-database-backup-file-snapshots"></a>データベース バックアップ ファイル スナップショットを表示する  
 各データベース ファイルのベース BLOB のファイル スナップショットを表示するには、 **sys.fn_db_backup_file_snapshots** システム関数を使用します。 このシステム関数を使用すると、Azure Blob ストレージ サービスを使用して格納されたデータベースの、各ベース BLOB のバックアップ ファイル スナップショットをすべて表示できます。 この関数の主な用途は、 **sys.sp_delete_backup** システム ストアド プロシージャ以外のメカニズムを使用してファイル スナップショット バックアップ セットのバックアップ ファイルを削除した際に、削除されずに残ったデータベースのバックアップ ファイル スナップショットを識別することです。 バックアップ ファイル スナップショットがそのまま残っているバックアップ セットの一部であるかそうではないかを判別するには、**RESTORE FILELISTONLY** システム ストアド プロシージャを使用して各バックアップ ファイルに属するファイル スナップショットを一覧表示します。 詳細については、「[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)」および「[RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)」を参照してください。  
  
 次の例は、指定したデータベースのすべてのバックアップ ファイル スナップショットの一覧を返します。  
  
```  
--Either specify the database name or set the database context  
USE AdventureWorks2016  
select * from sys.fn_db_backup_file_snapshots (null) ;  
GO  
select * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016') ;  
GO  
  
```  
  
## <a name="deleting-an-individual-database-backup-file-snapshot"></a>個々のデータベース バックアップ ファイル スナップショットを削除する  
 データベースのベース BLOB の個々のバックアップ ファイル スナップショットを削除するには、 **sys.sp_delete_backup_file_snapshot** システム ストアド プロシージャを使用します。 このシステム ストアド プロシージャの主な用途は、**sys.sp_delete_backup** システム ストアド プロシージャ以外のメソッドを使用してバックアップ ファイルを削除した後に残った、孤立したファイル スナップショット ファイルを削除することです。 詳細については、「[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)」を参照してください。  
  
> [!WARNING]  
>  ファイル スナップショット バックアップ セットの一部である個々のファイル スナップショットを削除すると、バックアップ セットが無効になります。  
  
 次の例では、指定したバックアップ ファイル スナップショットを削除します。 指定したバックアップの URL は、 **sys.fn_db_backup_file_snapshots** システム関数を使用して取得されました。  
  
```  
sys.sp_delete_backup_file_snapshot N'adventureworks2016', N'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016Data.mdf?snapshot=2015-05-29T21:31:31.6502195Z';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [チュートリアル: Azure Blob Storage サービスと SQL Server 2016 データベースの使用](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)  
  
  
