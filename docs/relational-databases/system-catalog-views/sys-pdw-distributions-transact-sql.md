---
title: sys.pdw_distributions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7deddb57cdc02410fe161728f45190492ac18a16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127549"
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  アプライアンス上の分布に関する情報を保持します。 配布のアプライアンスごとに 1 行が一覧表示します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|分布に関連付けられている一意の数値 id です。<br /><br /> このビューのキー。|コンピューティング ノードあたりのディストリビューションの数を乗算してアプライアンスにコンピューティング ノードの数に 1 です。|  
|pdw_node_id|**int**|このディストリビューションが上のノードの ID。|Pdw_node_id を参照してください。 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)します。|  
|NAME|**nvarchar(32)**|分散テーブルでのサフィックスとして使用される分布に関連付けられている識別子の文字列を指定します。|文字列の構成の ' A ~ Z'、' a ~ z'、' 0-9'、'_'、'-'。|  
|position|**int**|そのノード上の他のディストリビューションにそれぞれのノード内の配布の位置。|1 ノードあたりのディストリビューションの数にします。|  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse カタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
