---
title: メモリ使用量の監視とトラブルシューティング | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 7a458b9c-3423-4e24-823d-99573544c877
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 63c877d9b9275ef482591f6345715569a25c5e2a
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285012"
---
# <a name="monitor-and-troubleshoot-memory-usage"></a>メモリ使用量の監視とトラブルシューティング
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] は、ディスク ベース テーブルとは異なるパターンでメモリを消費します。 メモリおよびガベージ コレクション サブシステムに提供される DMV またはパフォーマンス カウンターを使用して、データベース内のメモリ最適化テーブルとインデックス向けに割り当てられて使用されているメモリの量を監視できます。  これによって、システム レベルとデータベース レベルの両方で状況を表示でき、メモリの枯渇による問題を回避できます。  
  
 このトピックでは、 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] のメモリ使用量の監視について説明します。  
  
  
##  <a name="bkmk_CreateDB"></a> メモリ最適化テーブルが含まれるサンプル データベースの作成  
 既にメモリ最適化テーブルが含まれるデータベースがある場合は、このセクションを省略できます。  
  
 以下の手順では、このトピックの残りのセクションで使用する、3 つのメモリ最適化テーブルが含まれるデータベースを作成します。 例では、メモリ最適化テーブルで使用できるメモリの量を制御できるように、データベースをリソース プールにマップしました。  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を起動します。  
  
2.  **[新しいクエリ]** をクリックします。  
  
3.  次のコードを新しいクエリ ウィンドウに貼り付け、各セクションを実行します。  
  
    ```  
    -- create a database to be used  
    CREATE DATABASE IMOLTP_DB  
    GO  
  
    ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA  
    ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_xtp' , FILENAME = 'C:\Data\IMOLTP_DB_xtp') TO FILEGROUP IMOLTP_DB_xtp_fg;  
    GO  
  
    USE IMOLTP_DB  
    GO  
  
    -- create the resoure pool  
    CREATE RESOURCE POOL PoolIMOLTP WITH (MAX_MEMORY_PERCENT = 60);  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    GO  
  
    -- bind the database to a resource pool  
    EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'PoolIMOLTP'  
  
    -- you can query the binding using the catalog view as described here  
    SELECT d.database_id  
         , d.name  
         , d.resource_pool_id  
    FROM sys.databases d  
    GO  
  
    -- take database offline/online to finalize the binding to the resource pool  
    USE master  
    GO  
  
    ALTER DATABASE IMOLTP_DB SET OFFLINE  
    GO  
    ALTER DATABASE IMOLTP_DB SET ONLINE  
    GO  
  
    -- create some tables  
    USE IMOLTP_DB  
    GO  
  
    -- create table t1  
    CREATE TABLE dbo.t1 (  
           c1 int NOT NULL CONSTRAINT [pk_t1_c1] PRIMARY KEY NONCLUSTERED  
         , c2 char(40) NOT NULL  
         , c3 char(8000) NOT NULL  
         ) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    GO  
  
    -- load t1 150K rows  
    DECLARE @i int = 0  
    BEGIN TRAN  
    WHILE (@i <= 150000)  
       BEGIN  
          INSERT t1 VALUES (@i, 'a', replicate ('b', 8000))  
          SET @i += 1;  
       END  
    Commit  
    GO  
  
    -- Create another table, t2  
    CREATE TABLE dbo.t2 (  
           c1 int NOT NULL CONSTRAINT [pk_t2_c1] PRIMARY KEY NONCLUSTERED  
         , c2 char(40) NOT NULL  
         , c3 char(8000) NOT NULL  
         ) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    GO  
  
    -- Create another table, t3   
    CREATE TABLE dbo.t3 (  
           c1 int NOT NULL CONSTRAINT [pk_t3_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 1000000)  
         , c2 char(40) NOT NULL  
         , c3 char(8000) NOT NULL  
         ) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    GO  
    ```  
  
##  <a name="monitoring-memory-usage"></a>メモリ使用率の監視  
  
###  <a name="using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>使用してください。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] には、インメモリ テーブルによって消費されるメモリを監視するための標準レポートが組み込まれています。 これらのレポートには、 [ここ](https://blogs.msdn.com/b/managingsql/archive/2006/05/16/ssms-reports-1.aspx)で説明しているようにオブジェクト エクスプローラーを使用してアクセスできます。 オブジェクト エクスプローラーを使用すると、個々のメモリ最適化テーブルで消費されるメモリも監視できます。  
  
#### <a name="consumption-at-the-database-level"></a>データベース レベルでの消費量  
 次のように、データベース レベルでのメモリ使用を監視できます。  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を起動し、サーバーに接続します。  
  
2.  オブジェクト エクスプローラーで、レポートが必要なデータベースを右クリックします。  
  
3.  コンテキスト メニューで、 **[レポート]** -> **Standard [レポート]** -> **[メモリ最適化オブジェクトによるメモリ使用量]** の順にクリックします。  
  
 ![HK_MM_SSMS](../../database-engine/media/hk-mm-ssms-stdrpt-memuse.gif "HK_MM_SSMS")  
  
 このレポートは、上で作成したデータベースによるメモリ消費を示します。  
  
 ![HK_MM_SSMS](../../database-engine/media/hk-mm-ssms-stdrpt-memuserpt.gif "HK_MM_SSMS")  
  
###  <a name="using-dmvs"></a>DMV の使用  
 メモリ最適化テーブル、インデックス、システム オブジェクト、およびランタイム構造によって消費されるメモリを監視するために、いくつかの DMV を使用できます。  
  
#### <a name="memory-consumption-by-memory-optimized-tables-and-indexes"></a>メモリ最適化テーブルおよびインデックスによるメモリ消費  
 次に示すように、 `sys.dm_db_xtp_table_memory_stats` にクエリを実行することで、すべてのユーザー テーブル、インデックス、およびシステム オブジェクトのメモリ消費を確認できます。  
  
```sql  
SELECT object_name(object_id) AS Name  
     , *  
   FROM sys.dm_db_xtp_table_memory_stats  
```  
  
 **サンプル出力**  
  
```  
Name       object_id   memory_allocated_for_table_kb memory_used_by_table_kb memory_allocated_for_indexes_kb memory_used_by_indexes_kb  
---------- ----------- ----------------------------- ----------------------- ------------------------------- -------------------------  
t3         629577281   0                             0                       128                             0  
t1         565577053   1372928                       1200008                 7872                            1942  
t2         597577167   0                             0                       128                             0  
NULL       -6          0                             0                       2                               2  
NULL       -5          0                             0                       24                              24  
NULL       -4          0                             0                       2                               2  
NULL       -3          0                             0                       2                               2  
NULL       -2          192                           25                      16                              16  
```  
  
 詳細については、次を参照してください。 [sys.dm_db_xtp_table_memory_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql?view=sql-server-2016)します。  
  
#### <a name="memory-consumption-by-internal-system-structures"></a>内部システム構造によるメモリ消費  
 メモリは、トランザクション構造、データ ファイルとデルタ ファイルのバッファー、ガベージ コレクション構造などのシステム オブジェクトによっても消費されます。 次に示すように、 `sys.dm_xtp_system_memory_consumers` にクエリを実行することで、これらのシステム オブジェクトに使用されるメモリを確認できます。  
  
```sql  
SELECT memory_consumer_desc  
     , allocated_bytes/1024 AS allocated_bytes_kb  
     , used_bytes/1024 AS used_bytes_kb  
     , allocation_count  
   FROM sys.dm_xtp_system_memory_consumers  
```  
  
 **サンプル出力**  
  
```  
memory_consumer_ desc allocated_bytes_kb   used_bytes_kb        allocation_count  
------------------------- -------------------- -------------------- ----------------  
VARHEAP                   0                    0                    0  
VARHEAP                   384                  0                    0  
DBG_GC_OUTSTANDING_T      64                   64                   910  
ACTIVE_TX_MAP_LOOKAS      0                    0                    0  
RECOVERY_TABLE_CACHE      0                    0                    0  
RECENTLY_USED_ROWS_L      192                  192                  261  
RANGE_CURSOR_LOOKSID      0                    0                    0  
HASH_CURSOR_LOOKASID      128                  128                  455  
SAVEPOINT_LOOKASIDE       0                    0                    0  
PARTIAL_INSERT_SET_L      192                  192                  351  
CONSTRAINT_SET_LOOKA      192                  192                  646  
SAVEPOINT_SET_LOOKAS      0                    0                    0  
WRITE_SET_LOOKASIDE       192                  192                  183  
SCAN_SET_LOOKASIDE        64                   64                   31  
READ_SET_LOOKASIDE        0                    0                    0  
TRANSACTION_LOOKASID      448                  448                  156  
PGPOOL:256K               768                  768                  3  
PGPOOL: 64K               0                    0                    0  
PGPOOL:  4K               0                    0                    0  
```  

 詳細については、「[sys.dm_xtp_system_memory_consumers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql)」を参照してください。  

  
#### <a name="memory-consumption-at-run-time-when-accessing-memory-optimized-tables"></a>メモリ最適化テーブルにアクセスするときの実行時のメモリ消費  
 次のクエリを使用して、プロシージャ キャッシュなどのランタイム構造で消費されたメモリを確認できます。このクエリを実行して、プロシージャ キャッシュ用などのランタイム構造で使用されたメモリの情報を取得します。 すべてのランタイム構造は XTP でタグ付けされます。  
  
```sql  
SELECT memory_object_address  
     , pages_in_bytes  
     , bytes_used  
     , type  
   FROM sys.dm_os_memory_objects WHERE type LIKE '%xtp%'  
```  
  
 **サンプル出力**  
  
```  
memory_object_address pages_ in_bytes bytes_used type  
--------------------- ------------------- ---------- ----  
0x00000001F1EA8040    507904              NULL       MEMOBJ_XTPDB  
0x00000001F1EAA040    68337664            NULL       MEMOBJ_XTPDB  
0x00000001FD67A040    16384               NULL       MEMOBJ_XTPPROCCACHE  
0x00000001FD68C040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD284040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD302040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD382040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD402040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD482040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD502040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD67E040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001F813C040    8192                NULL       MEMOBJ_XTPBLOCKALLOC  
0x00000001F813E040    16842752            NULL       MEMOBJ_XTPBLOCKALLOC  
```  
  
 詳細については、次を参照してください。 [sys.dm_os_memory_objects (TRANSACT-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql)します。  
  
#### <a name="memory-consumed-by-includehek2includeshek-2-mdmd-engine-across-the-instance"></a>インスタンス全体で [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] エンジンによって消費されるメモリ  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] エンジンとメモリ最適化オブジェクトに割り当てられたメモリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の他のメモリ コンシューマーと同様に管理されます。 MEMORYCLERK_XTP 型のクラークによって、 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] エンジンに割り当てられたすべてのメモリについて確認できます。 次のクエリを使用して、 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] エンジンによって使用されるすべてのメモリを確認します。  
  
```sql  
-- this DMV accounts for all memory used by the hek_2 engine  
SELECT type  
     , name  
     , memory_node_id  
     , pages_kb/1024 AS pages_MB   
   FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 このサンプル出力は、割り当てられた合計メモリが、システム レベルのメモリ消費 18 MB と、データベース ID が 5 のデータベースに割り当てられた 1358 MB であることを示しています。 このデータベースは専用のリソース プールにマップされるため、このメモリはそのリソース プールに反映されます。  
  
 **サンプル出力**  
  
```  
type                 name       memory_node_id pages_MB  
-------------------- ---------- -------------- --------------------  
MEMORYCLERK_XTP      Default    0              18  
MEMORYCLERK_XTP      DB_ID_5    0              1358  
MEMORYCLERK_XTP      Default    64             0  
```  
  
 詳細については、次を参照してください。 [sys.dm_os_memory_clerks (TRANSACT-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql)します。  
  
##   <a name="managing-memory-consumed-by-memory-optimized-objects"></a>メモリ最適化オブジェクトに消費されるメモリの管理  
 トピック「 [メモリ最適化テーブルを持つデータベースのリソース プールへのバインド](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)」で説明しているように、名前付きリソース プールにバインドすることでメモリ最適化テーブルによって消費されるメモリの合計を制御できます。  
  
##  <a name="troubleshooting-memory-issues"></a>メモリに関する問題のトラブルシューティング  
 メモリに関する問題のトラブルシューティングは、次の 3 つの手順で行います。  
  
1.  データベースまたはインスタンスのオブジェクトによって消費されているメモリ量を特定します。 前に説明したように、メモリ最適化テーブルで使用可能な豊富な監視ツール セットを使用できます。  たとえば、DMV の `sys.dm_db_xtp_table_memory_stats` または `sys.dm_os_memory_clerks`を使用できます。  
  
2.  メモリ消費がどのように拡大し、どれぐらいの余裕が残されているかを確認します。 メモリ消費を定期的に監視することで、メモリの使用がどのように拡大しているかを確認できます。 たとえば、名前付きリソース プールにデータベースをマップしている場合は、パフォーマンス カウンターの Used Memory (KB) を監視して、メモリの使用量がどのように拡大しているかを確認することができます。  
  
3.  発生する可能性があるメモリの問題を軽減するアクションを実行します。 詳細については、次を参照してください。[メモリ不足の問題を解決する](resolve-out-of-memory-issues.md)します。  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルを持つデータベースのリソース プールへのバインド](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [既存のプール内での MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の変更](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool)
  
  
