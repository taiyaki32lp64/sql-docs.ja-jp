---
title: pdw_nodes_partitions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d0fc42e1ce8d15498caf89582b66549f4e083130
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305228"
---
# <a name="syspdw_nodes_partitions-transact-sql"></a>pdw_nodes_partitions (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  すべてのテーブルのパーティションごとに1行のデータを格納し、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] データベース内のほとんどの種類のインデックスを格納します。 すべてのテーブルとインデックスには、明示的にパーティション分割されているかどうかにかかわらず、少なくとも1つのパーティションが含まれます。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|パーティションの id。 データベース内で一意です。|  
|object_id|**int**|このパーティションが所属するオブジェクトの id。 すべてのテーブルまたはビューは、少なくとも1つのパーティションで構成されます。|  
|index_id|**int**|このパーティションが所属するオブジェクト内のインデックスの id。|  
|partition_number|**int**|所有しているインデックスまたはヒープ内の1から始まるパーティション番号。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]の場合、この列の値は1です。|  
|hobt_id|**bigint**|このパーティションの行を含むデータヒープまたは B ツリー (HoBT) の ID。|  
|rows|**bigint**|このパーティション内の行の概数です。 |  
|data_compression|**int**|各パーティションの圧縮の状態を示します。<br /><br /> 0 = NONE<br /><br /> 1 = 行<br /><br /> 2 = ページ<br /><br /> 3 = 列ストア|  
|data_compression_desc|**nvarchar(60)**|各パーティションの圧縮の状態を示します。 指定できる値は、[なし]、[行]、および [ページ] です。|  
|pdw_node_id|**int**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ノードの一意識別子。|  
  
## <a name="permissions"></a>アクセス許可  
 `CONTROL SERVER` 権限が必要です。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>例 A: 各ディストリビューション内の各パーティションに行を表示する 

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
各ディストリビューション内の各パーティションの行数を表示するには、 [DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md)を使用します。

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>例 B: システムビューを使用して、テーブルの各ディストリビューションの各パーティションの行を表示する

**適用対象:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
このクエリでは、`myTable`テーブルの各ディストリビューションの各パーティションの行数が返されます。  
 
```sql  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

