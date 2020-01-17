---
title: dm_exec_dms_services (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DMS_SERVICES_TSQL
- SYS.DM_EXEC_DMS_SERVICES_TSQL
- DM_EXEC_DMS_SERVICES
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_services management view
- sys.dm_exec_dms_services management view
ms.assetid: 6ac47eef-4293-46b8-8555-07a614837504
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11e353af23c2331cd8f2bef5b439c967512e7323
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532931"
---
# <a name="sysdm_exec_dms_services-transact-sql"></a>dm_exec_dms_services (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase コンピューティングノードで実行されているすべての DMS サービスに関する情報を保持します。 サービスインスタンスごとに1つの行が表示されます。  
  
|列名|[データ型]|[説明]|範囲|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|`int`|DMS コアに関連付けられている一意の数値 id。 このビューのキー。|一意の ID。|  
|compute_node_id|`int`|この DMS サービスが実行されているノードの ID|詳細については[、 &#40;&#41;「dm_exec_compute_nodes transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)」の「 *compute_node_id* 」を参照してください。|  
|ステータス|`nvarchar(32)`|DMS サービスの現在の状態||
|compute_pool_id|`int`|プールの一意の識別子。|

## <a name="see-also"></a>参照  
 [動的管理ビューを使用した PolyBase のトラブルシューティング](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
