---
title: MSsub_identity_range (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsub_identity_range_TSQL
- MSsub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSsub_identity_range system table
ms.assetid: 26e20d28-14ed-44fc-af3b-4de386de4bb8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ec1f915e7cc70cb2d8ed0f09a9b0394dc7e09aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68221962"
---
# <a name="mssub_identity_range-transact-sql"></a>MSsub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsub_identity_range**テーブルは、サブスクリプションの id 範囲管理サポートを提供します。 このテーブルは、subscription データベースに保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|レプリケーションで管理される ID 列を持つテーブルの ID です。|  
|**range**|**bigint**|調整の際にサブスクライバーに割り当てられる連続する id 値の範囲の大きさを制御します。|  
|**last_seed**|**bigint**|現在の範囲の下限値です。|  
|**threshold**|**int**|ディストリビューション エージェントがどの時点で新しい ID 範囲を割り当てるかを制御するパーセンテージの値です。 値の比率が指定されている場合*しきい値*はディストリビューション エージェント、新しい id 範囲を作成します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
