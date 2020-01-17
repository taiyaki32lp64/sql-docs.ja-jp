---
title: sys.dm_pdw_nodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 61593522e09ed86ec10f08a6ad8ff7a941a2e10e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899345"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  内のノードのすべてに関する情報を保持[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]します。 アプライアンス内のノードごとに 1 行が一覧表示します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ノードに関連付けられている一意の数値 id。<br /><br /> このビューのキー。|種類に関係なく、アプライアンスにわたって一意です。|  
|type|**nvarchar(32)**|ノードの型。|' COMPUTE'、'コントロール'、'管理'|  
|NAME|**nvarchar(32)**|ノードの論理名です。|適切な長さの文字列は任意です。|  
|address|**nvarchar(32)**|このノードの IP アドレス。|0 ~ 255 の形式。0 ~ 255 です。0 ~ 255 です。0 ~ 255 です。|  
|is_passive|**int**|ノードを実行する仮想マシンが割り当てられているサーバーで実行されているかは、予備のサーバーにフェールオーバーしたかどうかを示します。|0 - ノード VM は元のサーバーで実行されています。<br /><br /> 1-ノード VM は、予備のサーバーで実行しています。|  
|領域 (region)|**nvarchar(32)**|ノードが実行されているリージョンです。|' PDW'、'HDINSIGHT'|  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
