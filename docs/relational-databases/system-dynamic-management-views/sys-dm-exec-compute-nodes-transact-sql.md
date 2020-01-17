---
title: dm_exec_compute_nodes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODES_TSQL
- DM_EXEC_COMPUTE_NODES
- SYS.DM_EXEC_COMPUTE_NODES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_nodes management view
- PolyBase, views
- PolyBase management views
- dm_exec_compute_nodes management view
ms.assetid: 0de4b7a4-401f-4e2d-9ab0-c54587e05154
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44664805dc9b728ecbd48acbf38c4565601c631a
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326146"
---
# <a name="sysdm_exec_compute_nodes-transact-sql"></a>dm_exec_compute_nodes (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase データ管理で使用されるノードに関する情報を保持します。 ノードごとに1つの行が表示されます。  
  
 この DMV を使用すると、スケールアウトクラスター内のすべてのノードの一覧と、それらのロール、名前、および IP アドレスが表示されます。  
  
|列名|[データ型]|[説明]|範囲|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|ノードに関連付けられている一意の数値 id。 このビューのキー。|種類に関係なく、スケールアウトクラスター全体で一意です。|  
|型|**nvarchar(32)**|ノードの種類。|' COMPUTE '、' HEAD '|  
|name|**nvarchar(32)**|ノードの論理名。|適切な長さの任意の文字列。|  
|address|**nvarchar(32)**|このノードの IP アドレス。|IP アドレスの範囲|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューを使用した PolyBase のトラブルシューティング](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
