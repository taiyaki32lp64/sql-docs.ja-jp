---
title: sys.memory_optimized_tables_internal_attributes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.memory_optimized_tables_internal_attributes
- sys.memory_optimized_tables_internal_attributes_TSQL
- memory_optimized_tables_internal_attributes
- memory_optimized_tables_internal_attributes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.memory_optimized_tables_internal_attributes catalog view
ms.assetid: 78ef5807-0504-4de8-9a01-ede6c03c7ff1
author: jodebrui
ms.author: jodebrui
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea116b0d4a70b647c6c3a719443f8e35f177169b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102381"
---
# <a name="sysmemoryoptimizedtablesinternalattributes-transact-sql"></a>sys.memory_optimized_tables_internal_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

ユーザー メモリ最適化テーブルを格納するために使用される各内部メモリ最適化テーブルの行が含まれます。 各ユーザー テーブルは、1 つ以上の内部テーブルに対応します。 1 つのテーブルは、コア データ ストレージで使用されます。 その他の内部テーブルは、メモリ最適化テーブルの一時的な列ストア インデックスおよび行外 (LOB) ストレージなどの機能をサポートするために使用されます。
 
| 列名  | データ型  | 説明 |
| :------ |:----------| :-----|
|object_id  |**int**|       ユーザー テーブルの ID。 ユーザー テーブル (hk/列ストアの組み合わせの場合は行外ストレージまたは削除行など) をサポートするために存在する内部メモリ最適化テーブルは、その親と同じ object_id を持ちます。 |
|xtp_object_id  |**bigint**|    ユーザー テーブルをサポートするために使用される内部メモリ最適化テーブルに対応するインメモリ OLTP オブジェクト ID。 データベース内では一意であり、オブジェクトの有効期間中に変わる可能性があります。 
|type|  **int** |   内部テーブルの種類。<br/><br/> 0 => DELETED_ROWS_TABLE <br/> 1 => USER_TABLE <br/> 2 => DICTIONARIES_TABLE<br/>3 => SEGMENTS_TABLE<br/>4 => ROW_GROUPS_INFO_TABLE<br/>5 => INTERNAL OFF-ROW DATA TABLE<br/>252 => INTERNAL_TEMPORAL_HISTORY_TABLE | 
|type_desc| **nvarchar(60)**|   種類の説明<br/><br/>DELETED_ROWS_TABLE -> 列ストア インデックスの削除行を追跡する内部テーブル<br/>USER_TABLE -> 行内ユーザー データを含むテーブル<br/>DICTIONARIES_TABLE -> 列ストア インデックスの辞書<br/>SEGMENTS_TABLE -> 列ストア インデックスの圧縮セグメント<br/>ROW_GROUPS_INFO_TABLE -> 列ストア インデックスの圧縮行グループに関するメタデータ<br/>INTERNAL OFF-ROW DATA TABLE -> 行外列のストレージに使用される内部テーブル。 この場合、minor_id には column_id が反映されます。<br/>INTERNAL_TEMPORAL_HISTORY_TABLE -> ディスク ベース履歴テーブルの末尾。 履歴に挿入された行は、最初にこの内部メモリ最適化テーブルに挿入されます。 この内部テーブルからディスク ベースの履歴テーブルに行を非同期的に移動するバックグラウンド タスクがあります。 |
|minor_id|  **int**|    0 は、ユーザー テーブルまたは内部テーブルを示します。<br/><br/>0 以外は、行外に格納されている列の ID を示します。 sys.columns で column_id と結合されます。<br/><br/>このシステム ビューには行外に格納されている各列に対応する行があります。|

## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-all-columns-that-are-stored-off-row"></a>A. 行外に格納されているすべての列を返す

次の T-SQL スクリプトは、複数の大きな LOB 以外の列と 1 つの LOB 列を含むテーブルを示しています。

```Transact-SQL
CREATE TABLE dbo.LargeTableSample
(
      Id   int IDENTITY PRIMARY KEY NONCLUSTERED,
      C1   nvarchar(4000),
      C2   nvarchar(4000),
      C3   nvarchar(4000),
      C4   nvarchar(4000),
      Misc nvarchar(max)
) WITH (MEMORY_OPTIMIZED = ON);
GO
```

次のクエリでは、行外に格納されるすべての列とそのサイズを示します。 サイズ - 1 は LOB 列を示します。 すべての LOB 列は行外に格納されます。

```Transact-SQL
SELECT 
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table', 
  c.name AS 'column', 
  c.max_length
FROM sys.memory_optimized_tables_internal_attributes moa
     JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
     JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="b-returning-memory-consumption-of-all-columns-that-are-stored-off-row"></a>B. 行外に格納されているすべての列のメモリ使用量を返す

行外列のメモリ使用量の詳細を取得する場合は、以下のクエリを使用できます。このクエリでは、行外列を格納するために使用されるすべての内部テーブルとそのインデックスのメモリ使用量が示されます。

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  c.name AS 'column',
  c.max_length,
  mc.memory_consumer_desc,
  mc.index_id,
  mc.allocated_bytes,
  mc.used_bytes
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="c-returning-memory-consumption-of-columnstore-indexes-on-memory-optimized-tables"></a>C. メモリ最適化テーブルでの列ストア インデックスのメモリ使用量を返す

メモリ最適化テーブルに列ストア インデックスのメモリ使用量を表示するのにには、次のクエリを使用します。

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  SUM(mc.allocated_bytes) / 1024 as [allocated_kb],
  SUM(mc.used_bytes) / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
GROUP BY o.schema_id, moa.object_id, i.name;
```

列ストア インデックスのメモリ最適化テーブルで使用される内部構造全体でメモリ消費量を次のクエリ break を使用します。

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  moa.type_desc AS 'internal table',
  mc.index_id AS 'index',
  mc.memory_consumer_desc,
  mc.allocated_bytes / 1024 as [allocated_kb],
  mc.used_bytes / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
```


