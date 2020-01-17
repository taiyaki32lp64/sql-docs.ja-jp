---
title: pdw_nodes_column_store_segments (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/28/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: julieMSFT
ms.author: jrasnick
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bea8e0d51b2918d7280f4afdb8b9d02f6b757827
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401672"
---
# <a name="syspdw_nodes_column_store_segments-transact-sql"></a>pdw_nodes_column_store_segments (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

列ストアインデックスの列ごとに1行の値を格納します。

| 列名                 | データ型  | 説明                                                  |
| :-------------------------- | :--------- | :----------------------------------------------------------- |
| **partition_id**            | **bigint** | パーティション ID を示します。 データベース内で一意です。     |
| **hobt_id**                 | **bigint** | この列ストアインデックスを持つテーブルのヒープまたは B ツリーインデックス (hobt) の ID。 |
| **column_id**               | **通り**    | 列ストア列の ID。                                |
| **segment_id**              | **通り**    | 列セグメントの ID。 旧バージョンとの互換性を維持するために、列名は行グループ ID でも segment_id 呼び出されます。 セグメントを一意に識別するには、<hobt_id、partition_id、column_id>、<segment_id> を使用します。 |
| **バージョン**                 | **通り**    | 列セグメント形式のバージョン。                        |
| **encoding_type**           | **通り**    | そのセグメントに使用されるエンコードの種類:<br /><br /> 1 = VALUE_BASED-辞書のない文字列/バイナリ (内部のバリエーションがある場合は4に似ています)<br /><br /> 2 = VALUE_HASH_BASED-ディクショナリに共通の値を持つ非文字列/バイナリ列<br /><br /> 3 = ディクショナリに共通の値を持つ STRING_HASH_BASED 文字列/バイナリ列<br /><br /> 4 = STORE_BY_VALUE_BASED-辞書のない文字列/バイナリ<br /><br /> 5 = ディクショナリのない STRING_STORE_BY_VALUE_BASED 文字列/バイナリ<br /><br /> すべてのエンコーディングは、可能であれば、ビットパックと実行時間のエンコーディングを利用します。 |
| **row_count**               | **通り**    | 行グループ内の行の数。                             |
| **has_nulls**               | **通り**    | 列セグメントに null 値が含まれている場合は1。                     |
| **base_id**                 | **bigint** | エンコードの種類1が使用されている場合は、ベース値 ID。  エンコードの種類1が使用されていない場合、base_id は1に設定されます。 |
| **桁違い**               | **点**  | エンコードの種類1が使用されている場合の大きさ。  エンコードの種類1が使用されていない場合、マグニチュードは1に設定されます。 |
| **primary__dictionary_id**  | **通り**    | プライマリ辞書の ID。 0以外の値は、現在のセグメント (つまり、行グループ) のこの列のローカル辞書を指します。 値-1 は、このセグメントにローカルディクショナリがないことを示します。 |
| **secondary_dictionary_id** | **通り**    | セカンダリ辞書の ID。 0以外の値は、現在のセグメント (つまり、行グループ) のこの列のローカル辞書を指します。 値-1 は、このセグメントにローカルディクショナリがないことを示します。 |
| **min_data_id**             | **bigint** | 列セグメントの最小データ ID。                       |
| **max_data_id**             | **bigint** | 列セグメントの最大データ ID。                       |
| **null_value**              | **bigint** | NULL を表すために使用される値。                               |
| **on_disk_size**            | **bigint** | セグメントのサイズ (バイト単位)。                                    |
| **pdw_node_id**             | **通り**    | [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]ノードの一意識別子。 |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

論理テーブルあたりの列ストアセグメントの数を決定するには、他のシステムテーブルと共に sys. pdw_nodes_column_store_segments を結合します。

```sql
SELECT  sm.name           as schema_nm
,       tb.name           as table_nm
,       nc.name           as col_nm
,       nc.column_id
,       COUNT(*)          as segment_count
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb                   ON  sm.[schema_id]          = tb.[schema_id]
JOIN    sys.[pdw_table_mappings] mp       ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt         ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[pdw_nodes_partitions] np     ON  np.[object_id]          = nt.[object_id]
                                          AND np.[pdw_node_id]        = nt.[pdw_node_id]
                                          AND np.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_nodes_columns] nc        ON  np.[object_id]          = nc.[object_id]
                                          AND np.[pdw_node_id]        = nc.[pdw_node_id]
                                          AND np.[distribution_id]    = nc.[distribution_id]
JOIN    sys.[pdw_nodes_column_store_segments] rg  ON  rg.[partition_id]         = np.[partition_id]
                                                      AND rg.[pdw_node_id]      = np.[pdw_node_id]
                                                      AND rg.[distribution_id]  = np.[distribution_id]
                                                      AND rg.[column_id]        = nc.[column_id]
GROUP BY    sm.name
,           tb.name
,           nc.name
,           nc.column_id  
ORDER BY    table_nm
,           nc.column_id
,           sm.name ;
```

## <a name="permissions"></a>アクセス許可


  **VIEW SERVER STATE** アクセス許可が必要です。

## <a name="see-also"></a>参照

[SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
[Transact-sql&#41;&#40;列ストアインデックスの作成](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
[pdw_nodes_column_store_row_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
[pdw_nodes_column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)
