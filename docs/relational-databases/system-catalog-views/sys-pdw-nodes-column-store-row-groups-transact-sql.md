---
title: pdw_nodes_column_store_row_groups (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b1cbdc63907933f173c7d32a2dde3151dd4db7af
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399872"
---
# <a name="syspdw_nodes_column_store_row_groups-transact-sql"></a>pdw_nodes_column_store_row_groups (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  では、管理者がで[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]システム管理を決定できるように、セグメント単位でクラスター化列ストアインデックス情報が提供されます。 **pdw_nodes_column_store_row_groups**には、物理的に格納された行の合計数 (削除済みとしてマークされている行を含む) の列と、削除済みとしてマークされた行の数の列があります。 削除された行の割合が高く、再構築する必要がある行グループを確認するには、 **pdw_nodes_column_store_row_groups**を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**通り**|基になるテーブルの ID。 これは、[制御] ノードの論理テーブルの object_id ではなく、計算ノードの物理テーブルです。 たとえば、object_id が、sys. テーブルの object_id と一致しません。<br /><br /> テーブルと結合するには、pdw_index_mappings を使用します。|  
|**index_id**|**通り**|*Object_id*テーブルのクラスター化列ストアインデックスの ID。|  
|**partition_number**|**通り**|行グループ*row_group_id*を保持するテーブルパーティションの ID。 *Partition_number*を使用して、この DMV を sys パーティションに参加させることができます。|  
|**row_group_id**|**通り**|この行グループの ID。 これは、パーティション内で一意です。|  
|**dellta_store_hobt_id**|**bigint**|デルタ行グループの hobt_id で、行グループの種類がデルタではない場合は NULL。 デルタ行グループとは、新しいレコードを受け入れる読み取り/書き込み行グループのことです。 デルタ行グループの状態は**OPEN**です。 デルタ行グループは、行ストア形式のままであり、列ストア形式に圧縮されていません。|  
|**状態**|**tinyint**|State_description に関連付けられている ID 番号。<br /><br /> 1 = OPEN <br /><br /> 2 = CLOSED <br /><br /> 3 = 圧縮|  
|**state_desccription**|**nvarchar (60)**|行グループの永続的な状態の説明。<br /><br /> OPEN-新しいレコードを受け入れる読み取り/書き込み行グループ。 開いている行グループは、行ストア形式のままであり、列ストア形式に圧縮されていません。<br /><br /> CLOSED-組ムーバープロセスによってまだ圧縮されていない、いっぱいになっている行グループ。<br /><br /> 圧縮-格納され、圧縮された行グループ。|  
|**total_rows**|**bigint**|行グループに物理的に格納されている行の合計。 削除されたものの、まだ保存されているものもあります。 行グループ内の行の最大数は 1048576 (16 進数 FFFFF) です。|  
|**deleted_rows**|**bigint**|削除対象としてマークされている行グループに物理的に格納されている行の数。<br /><br /> デルタ行グループの場合は常に0です。|  
|**size_in_bytes**|**通り**|この行グループ内のすべてのページの合計サイズ (バイト単位)。 このサイズには、メタデータまたは共有辞書を格納するために必要なサイズは含まれていません。|  
|**pdw_node_id**|**通り**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]ノードの一意の id。|  
|**distribution_id**|**通り**|ディストリビューションの一意の id。|
  
## <a name="remarks"></a>コメント  
 クラスター化または非クラスター化列ストアインデックスを持つ各テーブルの列ストア行グループごとに1行の値を返します。  
  
 行グループに含まれる行の数と行グループのサイズを決定するには、 **pdw_nodes_column_store_row_groups**を使用します。  
  
 行グループ内の削除済みの行の数が合計行数に対して占める割合が高くなると、テーブルの効率が低下します。 テーブルのサイズが小さくなるよう列ストア インデックスを再構築して、テーブルを読み取るために必要なディスク I/O を削減します。 列ストアインデックスを再構築するには、 **ALTER index**ステートメントの**rebuild**オプションを使用します。  
  
 更新可能な列ストアは、まず、行ストア形式の、**開い**ている行グループに新しいデータを挿入します。これは、デルタテーブルと呼ばれることもあります。  開いている行グループがいっぱいになると、その状態は**CLOSED**に変わります。 閉じた行グループは、組ムーバーによって列ストア形式に圧縮され、状態が**圧縮**に変わります。  組ムーバーは、定期的にウェイクアップし、列ストア行グループに圧縮できる閉じた行グループがあるかどうかを確認するバックグラウンドプロセスです。  また、組ムーバーは、すべての行が削除された行グループの割り当てを解除します。 割り当てが解除された行グループは、**廃止**済みとしてマークされます。 組ムーバーをすぐに実行するには、 **ALTER INDEX**ステートメントの**再構成**オプションを使用します。  
  
 列ストア行グループは、いっぱいになると圧縮され、新しい行の受け入れを停止します。 圧縮されたグループから行が削除されると、削除された行は、保持されますが、削除済みとしてマークされます。 圧縮されたグループに対する更新は、圧縮されたグループからの削除、および OPEN 状態のグループへの挿入として実装されます。  
  
## <a name="permissions"></a>アクセス許可  
 
  **VIEW SERVER STATE** アクセス許可が必要です。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、 **pdw_nodes_column_store_row_groups**テーブルを他のシステムテーブルに結合して、特定のテーブルに関する情報を返します。 計算済みの `PercentFull` 列は、行グループの効率の推定値を示します。 1つのテーブルに関する情報を検索するには、WHERE 句の前にあるコメントハイフンを削除し、テーブル名を指定します。  
  
```  
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
AND CSRowGroups.index_id = NI.index_id      
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

次[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]の例では、クラスター化列ストアのパーティションごとの行と、開いている、閉じた、または圧縮された行グループに含まれる行の数をカウントします。  

```
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
JOIN sys.pdw_nodes_tables pt
ON rg.object_id = pt.object_id AND rg.pdw_node_id = pt.pdw_node_id AND pt.distribution_id = rg.distribution_id
JOIN sys.pdw_table_mappings tm
ON pt.name = tm.physical_name
INNER JOIN sys.tables t
ON tm.object_id = t.object_id
INNER JOIN sys.schemas s
ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Transact-sql&#41;&#40;列ストアインデックスの作成](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [pdw_nodes_column_store_segments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [pdw_nodes_column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
