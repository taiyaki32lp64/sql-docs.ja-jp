---
title: データベースの全体復元 (単純復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- complete database restores
- database restores [SQL Server], complete database
- restoring databases [SQL Server], complete database
- simple recovery model [SQL Server]
- restoring [SQL Server], database
ms.assetid: 49828927-1727-4d1d-9ef5-3de43f68c026
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e64bf4d4642d8091cd0892283a996e7dccc56e26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877146"
---
# <a name="complete-database-restores-simple-recovery-model"></a>データベースの全体復元 (単純復旧モデル)
  データベースの全体復元の目的は、データベース全体を復元することです。 復元の実行中は、データベース全体がオフラインになります。 データベースの各部がオンラインになる前に、すべてのデータが一貫性のある状態に復旧されます。一貫性のある状態とは、データベースのすべての部分が同じ時点にあり、コミットされていないトランザクションが存在しない状態を示します。  
  
 単純復旧モデルでは、特定のバックアップ内にある特定の時点にデータベースを復元することはできません。  
  
> [!IMPORTANT]  
>  不明なソースや信頼されていないソースからデータベースをアタッチまたは復元しないことをお勧めします。 そのようなデータベースには、意図しない [!INCLUDE[tsql](../../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更することによりエラーを発生させる悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  

  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのバックアップに対するサポートの情報については、「 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」の「互換性サポート」のセクションを参照してください。  
  
##  <a name="Overview"></a> 単純復旧モデルでのデータベース復元の概要  
 単純復旧モデルでのデータベース全体の復元は、データベースの差分バックアップを復元する必要があるかどうかに応じて 1 つまたは 2 つの [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントで行われます。 次の図に示すように、データベースの完全バックアップのみを使用する場合は、最新のバックアップを復元するだけで完了します。  
  
 ![データベースの完全バックアップのみを復元](../../database-engine/media/bnrr-rmsimple1-fulldbbu.gif "データベースの完全バックアップのみを復元")  
  
 データベースの差分バックアップも使用する場合は、データベースを復旧しないで最新の完全バックアップを復元してから、最新の差分バックアップを復元してデータベースを復旧します。 次の図に、このプロセスを示します。  
  
 ![データベース全体と差分バックアップを復元](../../database-engine/media/bnrr-rmsimple2-diffdbbu.gif "データベース全体と差分バックアップを復元")  
  
> [!NOTE]  
>  データベースのバックアップを別のサーバー インスタンスに復元する予定の場合は、「 [バックアップと復元によるデータベースのコピー](../databases/copy-databases-with-backup-and-restore.md)」を参照してください。  
  
###  <a name="TsqlSyntax"></a> 基本的な Transact-SQL RESTORE 構文  
 データベースの完全バックアップを復元する際に使用する、 [!INCLUDE[tsql](../../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) の基本構文を次に示します。  
  
 RESTORE DATABASE *database_name* FROM *backup_device* [ WITH NORECOVERY ]  
  
> [!NOTE]  
>  データベースの差分バックアップも復元する場合は、WITH NORECOVERY を指定してください。  
  
 データベース バックアップを復元する際に使用する、 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) の基本構文を次に示します。  
  
 RESTORE DATABASE *database_name* FROM *backup_device* WITH RECOVERY  
  
###  <a name="Example"></a> 例 (Transact-SQL)  
 次の例では、まず [BACKUP](/sql/t-sql/statements/backup-transact-sql) ステートメントを使用して、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの完全バックアップと差分バックアップを作成します。 その後、これらのバックアップを順に復元します。 データベースは、差分データベース バックアップ完了時の状態に復元されます。  
  
 この例は、データベースの全体復元シナリオの復元シーケンスで重要なオプションを示しています。 *復元シーケンス* は、1 つ以上の復元フェーズによってデータを移動する、1 つ以上の復元操作で構成されます。 説明の目的に関係しない構文や詳細は、省略しています。 データベースを復旧する際は、RECOVERY オプションを明示的に指定することをお勧めします。このオプションは既定値ですが、指定しておくと判別がつきやすくなります。  
  
> [!NOTE]  
>  この例の先頭では、 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) ステートメントを使用して復旧モデルを `SIMPLE`に設定しています。  
  
```  
USE master;  
--Make sure the database is using the simple recovery model.  
ALTER DATABASE AdventureWorks2012 SET RECOVERY SIMPLE;  
GO  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
  WITH FORMAT;  
GO  
--Create a differential database backup.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH DIFFERENTIAL;  
GO  
--Restore the full database backup (from backup set 1).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=1, NORECOVERY;  
--Restore the differential backup (from backup set 2).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=2, RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベースの完全バックアップを復元するには**  
  
-   [単純復旧モデルでのデータベース バックアップの復元 &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [データベースのバックアップを復元&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [データベースを新しい場所に復元する &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
 **データベースの差分バックアップを復元するには**  
  
-   [データベースの差分バックアップの復元 &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
 **SQL Server 管理オブジェクト (SMO) を使用してバックアップを復元するには**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  

  
## <a name="see-also"></a>関連項目  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [データベースの完全バックアップ &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
