---
title: 完全復旧モデル (TRANSACT-SQL) で障害発生時点にデータベースを復元 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83319e8eb1fe692bc55b764445ac155d9e1ad38d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920995"
---
# <a name="restore-a-database-to-the-point-of-failure-under-the-full-recovery-model-transact-sql"></a>完全復旧モデルで障害発生時点までデータベースを復元する方法 (Transact-SQL)
  このトピックでは、障害が発生する直前の状態まで復元する方法について説明します。 このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用しているデータベースのみを対象としています。  
  
### <a name="to-restore-to-the-point-of-failure"></a>障害発生時点まで復元するには  
  
1.  次の基本的な [BACKUP](/sql/t-sql/statements/backup-transact-sql) ステートメントを実行して、ログの末尾をバックアップします。  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  次の基本的な [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントを実行して、データベースの完全バックアップを復元します。  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
3.  必要に応じて、次の基本的な RESTORE DATABASE ステートメントを実行して、データベースの差分バックアップを復元します。  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
4.  RESTORE LOG ステートメントで WITH NORECOVERY を指定して、手順 1. で作成したログ末尾のバックアップを含む各トランザクション ログ バックアップを適用します。  
  
    ```  
    RESTORE LOG <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
5.  次の RESTORE DATABASE ステートメントを実行して、データベースを復旧します。  
  
    ```  
    RESTORE DATABASE <database_name>   
       WITH RECOVERY;  
    ```  
  
## <a name="example"></a>例  
 この例を実行する前に、次の準備作業を完了する必要があります。  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの既定の復旧モデルは、単純復旧モデルです。 この復旧モデルでは障害発生時点までの復旧がサポートされていないため、次の [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ALTER DATABASE [ステートメントを実行して、完全復旧モデルが使用されるように](/sql/t-sql/statements/alter-database-transact-sql) を設定します。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
    ```  
  
2.  次の BACKUP ステートメントを使用して、このデータベースの完全バックアップを作成します。  
  
    ```  
    BACKUP DATABASE AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Data.bck';  
    ```  
  
3.  次のように、定期的なログ バックアップを作成します。  
  
    ```  
    BACKUP LOG AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Log.bck';  
    ```  
  
 次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのログ末尾のバックアップを作成した後に、以前作成したバックアップを復元します (この手順は、ログ ディスクにアクセスできることを前提としています)。  
  
 まず、データベースのログ末尾のバックアップを作成して、アクティブなログをキャプチャし、データベースを復元中の状態にしておきます。 次に、データベースのバックアップを復元し、以前作成した定期的なログ バックアップを適用し、ログ末尾のバックアップを適用します。 最後に、別の手順でデータベースを復旧します。  
  
> [!NOTE]  
>  既定の動作では、最終的なバックアップを復元するステートメントに、データベースの復旧が含まれています。  
  
```  
/* Example of restoring a to the point of failure */  
-- Step 1: Create a tail-log backup by using WITH NORECOVERY.  
BACKUP LOG AdventureWorks2012  
   TO DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 2: Restore the full database backup.  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Data.bck'  
   WITH NORECOVERY;  
GO  
-- Step 3: Restore the first transaction log backup.  
RESTORE LOG AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 4: Restore the tail-log backup.  
RESTORE LOG AdventureWorks2012  
   FROM  DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 5: Recover the database.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
