---
title: sys.dm_db_xtp_table_memory_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_table_memory_stats_TSQL
- dm_db_xtp_table_memory_stats
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats
ms.assetid: ad0efc06-3d9c-4861-9dfa-a7a87822d0c8
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d04238e0f476f39b0158fad4aa3350875d471ecc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097941"
---
# <a name="sysdmdbxtptablememorystats-transact-sql"></a>sys.dm_db_xtp_table_memory_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  現在のデータベースの各 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] テーブル (ユーザーおよびシステム) におけるメモリ使用量に関する統計を返します。 システム テーブルの id が負の値のオブジェクトとの実行時の情報を格納するため、[!INCLUDE[hek_2](../../includes/hek-2-md.md)]エンジン。 ユーザー オブジェクトとは異なり、システム テーブルは内部で使用され、メモリ内にしか存在しないため、カタログ ビューには表示されません。 システム テーブルは、記憶域で、すべてのデータ/デルタ ファイルのメタデータはマージ要求、デルタ ファイルの行のフィルター処理、削除されたテーブル、および関連情報を回復し、バックアップのウォーターマークの情報を保存するために使用されます。 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]エンジンは、最大 8,192 のデータを持つことができ、大規模なメモリ内データベース、システム テーブルによって使用されたメモリのデルタ ファイルのペアは、数メガ バイトを指定できます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|テーブルのオブジェクト ID です。 インメモリ OLTP システム テーブルの場合は NULL です。|  
|memory_allocated_for_table_kb|**bigint**|このテーブルに割り当てられているメモリです。|  
|memory_used_by_table_kb|**bigint**|行バージョンも含めて、テーブルによって使用されているメモリです。|  
|memory_allocated_for_indexes_kb|**bigint**|このテーブルのインデックスに割り当てられているメモリです。|  
|memory_used_by_indexes_kb|**bigint**|このテーブルのインデックスに消費されるメモリ。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限がある場合は、すべての行が返されます。 それ以外の場合、空の行セットが返されます。  
  
 VIEW DATABASE 権限がない場合は、SELECT 権限を持っているテーブル内の行に対するすべての列が返されます。  
  
 システム テーブルは、VIEW DATABASE STATE 権限を持つユーザーにのみ返されます。  
  
## <a name="examples"></a>使用例  
 次の DMV に対してクエリを実行して、データベース内のテーブルとインデックスに割り当てられたメモリを取得できます。  
  
```  
-- finding memory for objects  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
 データベース内のすべてのオブジェクトのメモリが見つかりません。  
  
```  
SELECT SUM( memory_allocated_for_indexes_kb + memory_allocated_for_table_kb) AS  
 memoryallocated_objects_in_kb   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
## <a name="user-scenario"></a>ユーザー シナリオ  
 まず HkDb1 という名前のデータベースで次の表を作成します。  
  
```  
-- set max server memory to 4 GB  
EXEC sp_configure 'max server memory (MB)', 4048  
go  
  
RECONFIGURE  
go  
  
-- create a resource pool for database with memory-optimized objects  
CREATE RESOURCE POOL PoolHkDb1 WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
go  
  
--bind the pool to the database  
EXEC sp_xtp_bind_db_resource_pool 'HkDb1', 'PoolHkdb1'  
go  
  
-- take database offline/online to associate the pool  
use master  
go  
  
alter database HkDb1 set offline  
go  
alter database HkDb1 set online  
go  
  
USE HkDb1  
go  
  
CREATE TABLE dbo.t1 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t1_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t2 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t2_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t3 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t3_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 1000000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
-- load 150K rows  
declare @i int = 0  
while (@i <= 150000)  
begin  
       insert t1 values (@i, 'a', replicate ('b', 8000))  
       set @i += 1;  
end  
go  
```  
  
 テーブルにデータが読み込まれると、ユーザー定義テーブルを表示できますと使用中の記憶域の量。 たとえば、テーブル内の各行が約 8,070 バイト (割り当てサイズは 8 K (8,192 バイト)) を使用していることなどを確認できます。 テーブルごとのインデックスを確認でき、記憶域の量、インデックスを使用します。 1 MB (2 * * 17) の 2 のべき乗に丸められた、100 K エントリは、たとえば、8 バイトごとの 131072 を = です。 テーブルにはインデックスがない場合があります。このような場合は、インデックスに対するメモリ割り当てが表示されます。 他の行は、システム テーブルを表すことがあります。  
  
```  
select convert(char(10), object_name(object_id)) as Name,*   
from sys.dm_db_xtp_table_memory_stats  
```  
  
 2 つの部分で、出力を示します。  
  
```  
Name       object_id   memory_allocated_for_table_kb memory_used_by_table_kb  
---------- ----------- ----------------------------- -----------------------  
t3         629577281   0                             0  
t1         565577053   1372928                       1202351  
t2         597577167   0                             0  
NULL       -6          0                             0  
NULL       -5          0                             0  
NULL       -4          0                             0  
NULL       -3          0                             0  
NULL       -2          192                           25  
  
memory_allocated_for_indexes_kb memory_used_by_indexes_kb  
------------------------------- -------------------------  
8192                            8192  
1024                            1024  
8192                            8192  
2                               2  
24                              24  
2                               2  
2                               2  
16                              16  
```  
  
 出力  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
       sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
```  
  
 します。  
  
```  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1357                 1191  
```  
  
 次に、リソース プールからの出力を確認してみましょう。 プールから使用されているメモリは 1356 MB です。  
  
```  
select pool_id,convert(char(10), name) as Name, min_memory_percent, max_memory_percent,   
   max_memory_kb/1024 as max_memory_mb  
from sys.dm_resource_governor_resource_pools  
  
select used_memory_kb/1024 as used_memory_mb ,target_memory_kb/1024 as target_memory_mb  
from sys.dm_resource_governor_resource_pools  
```  
  
 出力は次のようになります。  
  
```  
pool_id     Name       min_memory_percent max_memory_percent max_memory_mb  
----------- ---------- ------------------ ------------------ --------------------  
1           internal   0                  100                3845  
2           default    0                  100                3845  
259         PoolHkDb1  0                  100                3845  
  
used_memory_mb       target_memory_mb  
-------------------- --------------------  
125                  3845  
32                   3845  
1356                 3845  
```  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
