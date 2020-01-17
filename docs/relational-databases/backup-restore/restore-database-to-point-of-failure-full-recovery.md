---
title: 'データベースの復旧: 障害発生時点 - 完全復旧'
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
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
ms.openlocfilehash: 5cf3638c1f79c560abd96c262f4ff2c23e312d09
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241858"
---
# <a name="restore-database-to-point-of-failure---full-recovery"></a>データベースを障害発生時点まで復元する - 完全復旧
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、障害が発生する直前の状態まで復元する方法について説明します。 このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用しているデータベースのみを対象としています。  
  
### <a name="to-restore-to-the-point-of-failure"></a>障害発生時点まで復元するには  
  
1.  次の基本的な [BACKUP](../../t-sql/statements/backup-transact-sql.md) ステートメントを実行して、ログの末尾をバックアップします。  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  次の基本的な [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) ステートメントを実行して、データベースの完全バックアップを復元します。  
  
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
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの既定の復旧モデルは、単純復旧モデルです。 この復旧モデルでは障害発生時点までの復旧がサポートされていないため、次の [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ALTER DATABASE [ステートメントを実行して、完全復旧モデルが使用されるように](../../t-sql/statements/alter-database-transact-sql.md) を設定します。  
  
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
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
