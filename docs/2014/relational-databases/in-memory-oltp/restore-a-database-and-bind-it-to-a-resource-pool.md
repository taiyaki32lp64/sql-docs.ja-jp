---
title: データベースの復元とリソース プールへのバインド | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cac1e775d5cccaccca90b03104de4132e651284e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467846"
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>データベースの復元とリソース プールへのバインド
  メモリ最適化テーブルが含まれるデータベースを復元するためのメモリが十分にある場合も、ベスト プラクティスに従って名前付きリソース プールにデータベースをバインドする必要があります。 データベースをプールにバインドする前に、そのデータベースが存在する必要があるため、データベースを復元するプロセスには複数のステップが含まれます。 このトピックでは、そのプロセスについて説明します。  
  
##  <a name="restore-with-norecovery"></a>NORECOVERY を指定して復元を行う  
 データベースを復元するときに、NORECOVERY ではメモリを使用せずにデータベースが作成され、ディスク イメージが復元されます。  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
##  <a name="create-the-resource-pool"></a>リソース プールを作成する  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] では、使用可能なメモリを 50% に指定して、Pool_IMOLTP という名前のリソース プールが作成されます。  プールが作成された後、Pool_IMOLTP が含まれるようにリソース ガバナーが再構成されます。  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bind-the-database-and-resource-pool"></a>データベースとリソース プールをバインドする  
 システム関数 `sp_xtp_bind_db_resource_pool` を使用して、データベースをリソース プールにバインドします。 この関数は、パラメーターとしてデータベース名とリソース プール名をこの順序で受け取ります。  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] では、リソース プール Pool_IMOLTP へのデータベース IMOLTP_DB のバインドを定義しています。 このバインドは、次の手順を完了するまで有効になりません。  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
##  <a name="restore-with-recovery"></a>RECOVERY を指定して復元を行う  
 RECOVERY を指定してデータベースを復元すると、データベースがオンラインになり、すべてのデータが復元されます。  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
##  <a name="monitor-the-resource-pool-performance"></a>リソース プール パフォーマンスの監視  
 データベースが名前付きリソース プールにバインドされ、RECOVERY を指定して復元されたら、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Resource Pool Stats オブジェクトを監視します。 詳細については、「 [SQL Server、Resource Pool Stats オブジェクト](../performance-monitor/sql-server-resource-pool-stats-object.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルを持つデータベースのリソース プールへのバインド](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [SQL Server、Resource Pool Stats オブジェクト](../performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)  
  
  
