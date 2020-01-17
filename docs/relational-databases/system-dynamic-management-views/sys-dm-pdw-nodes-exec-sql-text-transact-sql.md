---
title: sys.dm_pdw_nodes_exec_sql_text (Transact-sql) |Microsoft Docs
description: 指定された sql_handle によって識別される SQL バッチのテキストを返す動的管理ビュー。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: fd886217b2fb2caf0fe3f32e88b7bf0215ece1a9
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145677"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>システム pdw _nodes_dm_exec_sql_text (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

指定された*sql_handle*によって識別される SQL バッチのテキストを返します。 このテーブル値関数は、システム関数**fn_get_sql**を置き換えます。  
   
## <a name="table-returned"></a>返されたテーブル  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|ノードに関連付けられている一意の数値 ID。|
|**dbid**|**smallint**|データベースの ID。<br /><br /> 計画外および準備された SQL ステートメントの場合、ステートメントがコンパイルされたデータベースの ID。|  
|**objectid**|**int**|オブジェクトの ID。<br /><br /> アドホックおよび準備された SQL ステートメントの場合は NULL です。|  
|**number**|**smallint**|番号付きストアドプロシージャの場合、この列にはストアドプロシージャの数が返されます。 詳細については、「[sys.numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)」を参照してください。<br /><br /> アドホックおよび準備された SQL ステートメントの場合は NULL です。|  
|**encrypted**|**bit**|1: SQL テキストは暗号化されています。<br /><br /> 0: SQL テキストは暗号化されていません。|  
|**text**|**nvarchar(max)**|SQL クエリのテキスト。<br /><br /> 暗号化されたオブジェクトの場合は NULL です。|  

## <a name="remarks"></a>備考  
[sys.dm_exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15)でも同じ解説が適用されます。  
  
## <a name="permissions"></a>Permissions  
 **Sysadmin**サーバーロールが必要です。または、サーバーに対する `VIEW SERVER STATE` 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスの動的管理&#40;ビュー transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>次のステップ
 開発のヒントについては、「 [SQL Data Warehouse 開発の概要](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)」を参照してください。