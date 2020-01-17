---
title: pdw_nodes_pdw_physical_databases (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 48f2a2d485f99b91b0f30a6a707a900ccbbeea96
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399916"
---
# <a name="syspdw_nodes_pdw_physical_databases-transact-sql"></a>pdw_nodes_pdw_physical_databases (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  コンピューティングノードの物理データベースごとに1行のデータを格納します。 物理データベース情報を集計して、データベースに関する詳細情報を取得します。 情報を結合するには`sys.pdw_nodes_pdw_physical_databases` 、を`sys.pdw_database_mappings`テーブル`sys.databases`とテーブルに結合します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**通り**|データベースのオブジェクト ID。 この値は、 [transact-sql&#41;ビュー &#40;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)の database_id と同じではないことに注意してください。|  
|physical_name|**sysname**|シェル/コンピューティングノード上のデータベースの物理名。 この値は、 [pdw_database_mappings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)ビューの physical_name 列の値と同じです。|  
|pdw_node_id|**通り**|ノードに関連付けられている一意の数値 id。|  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>A. 不正  
 次のクエリでは、master の各データベースの名前と ID、および各計算ノードの対応するデータベース名が返されます。  
  
```  
SELECT D.database_id AS DBID_in_master, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName   
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
### <a name="b-using-syspdw_nodes_pdw_physical_databases-to-gather-detailed-object-information"></a>B. Pdw_nodes_pdw_physical_databases を使用して詳細なオブジェクト情報を収集する  
 次のクエリは、インデックスに関する情報を表示し、データベース内のオブジェクトにオブジェクトが属しているデータベースに関する有用な情報を格納します。  
  
```  
SELECT D.name AS UserDatabaseName, D.database_id AS DBIDinMaster,  
DM.physical_name AS PhysDBName, PD.pdw_node_id AS NodeID,   
IU.object_id, IU.index_id, IU.user_seeks, IU.user_scans, IU.user_lookups, IU.user_updates  
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
JOIN sys.dm_pdw_nodes_db_index_usage_stats AS IU  
    ON PD.database_id = IU.database_id  
ORDER BY D.database_id, IU.object_id, IU.index_id, PD.pdw_node_ID;  
```  
  
### <a name="c-using-syspdw_nodes_pdw_physical_databases-to-determine-the-encryption-state"></a>C. Pdw_nodes_pdw_physical_databases を使用して暗号化の状態を確認する  
 次のクエリは、AdventureWorksPDW2012 データベースの暗号化の状態を提供します。  
  
```  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
            ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [データベース &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [pdw_database_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  

