---
title: sys.dm_db_xtp_hash_index_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2bbaaaa6770c5644da227c7e64a9ff9e0fc2c13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026842"
---
# <a name="sysdmdbxtphashindexstats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  これらの統計は、バケット数を理解してチューニングするために役立ちます。 また、インデックス キーに多数の重複があるケースを検出するためにも使用できます。  
  
 チェーンの平均の長さが長いことは、多数の行が同じバケットにハッシュされていることを示します。 これは、次の理由で発生する可能性があります。  
  
-   空のバケットの数が少ない場合、またはチェーンの長さの平均値が最大値に近い場合は、合計バケット数が少なすぎる可能性があります。 これにより、多くの異なるインデックス キーが同じバケットにハッシュされます。  
  
-   空のバケットの数が多い場合、またはチェーンの長さの最大値が平均値よりも高い場合、インデックス キーの値が重複していて行が多数あるか、キーの値にスキューがある可能性があります。 インデックス キーの値が同じである行はすべて同じバケットにハッシュされるため、そのバケット内のチェーンの長さは長くなります。  
  
チェーンの長さが長いことは、SELECT と INSERT を含む個々の列に対して行われるすべての操作のパフォーマンスに著しい影響を与える可能性があります。 チェーンの長さが短く、空のバケット数が多いことは、bucket_count の値が高すぎることを意味します。 これにより、インデックス スキャンのパフォーマンスが低下します。  
  
> [!WARNING]
> **sys.dm_db_xtp_hash_index_stats**テーブル全体をスキャンします。 そのため、データベースの大規模なテーブルがある場合**sys.dm_db_xtp_hash_index_stats**実行時間がかかる場合があります。  
  
詳細については、次を参照してください。[メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|object_id|**int**|親テーブルのオブジェクト ID。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルの ID です。|  
|index_id|**int**|インデックス ID。|  
|total_bucket_count|**bigint**|インデックス内のハッシュ バケットの総数。|  
|empty_bucket_count|**bigint**|インデックス内の空のハッシュ バケットの数。|  
|avg_chain_length|**bigint**|インデックス内のすべてのハッシュ バケットを対象とした行チェーンの長さの平均値。|  
|max_chain_length|**bigint**|ハッシュ バケット内の行チェーンの長さの最大値。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルに対応する、インメモリ OLTP オブジェクトの ID。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  

## <a name="examples"></a>使用例  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. ハッシュ インデックスのバケット数のトラブルシューティング

既存のテーブルのハッシュ インデックスのバケット数のトラブルシューティングを行うには、次のクエリを使用できます。 クエリでは、ユーザー テーブルで空のバケットとハッシュ インデックスのすべてのチェーンの長さの割合に関する統計情報を返します。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

このクエリの結果を解釈する方法の詳細については、次を参照してください。[メモリ最適化テーブルのハッシュ インデックスのトラブルシューティング](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)します。  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. 内部テーブルのハッシュ インデックスの統計

特定の機能は、ハッシュ インデックスをメモリ最適化テーブルの列ストア インデックスなどを利用する内部テーブルを使用します。 次のクエリでは、ユーザー テーブルにリンクされている内部テーブルのハッシュ インデックスの統計を返します。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

内部テーブルのインデックスの BUCKET_COUNT を変更することはできません、したがってこのクエリの出力と見なす役に立つだけのことに注意してください。 必要な操作はありません。  

このクエリは、内部テーブルのハッシュ インデックスを利用する機能を使用している場合を除き、行を返す必要はありません。 次のメモリ最適化テーブルには、列ストア インデックスが含まれています。 このテーブルを作成すると、内部テーブルのハッシュ インデックスが表示されます。

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
