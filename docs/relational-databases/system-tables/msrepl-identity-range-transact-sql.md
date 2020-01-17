---
title: MSrepl_identity_range (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_identity_range_TSQL
- MSrepl_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_identity_range system table
ms.assetid: 6e92a8e8-7667-4c98-b1c4-46735bac50d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38f5037598e240585333d246a99c29c5fd8f40fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079163"
---
# <a name="msrepl_identity_range-transact-sql"></a>MSrepl_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_identity_range**テーブル id 範囲管理サポートを提供します。 このテーブルは、パブリケーション、ディストリビューションおよびサブスクリプション データベースに保存します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリケーション データベースの名前です。|  
|**tablename**|**sysname**|テーブルの名前です。|  
|**identity_support**|**int**|自動 id 範囲処理が有効になっているかどうかを指定します。 0 は、自動 id 範囲処理が有効でないことを指定します。|  
|**next_seed**|**bigint**|ID 範囲の自動処理が有効な場合、次の範囲の開始位置を指定します。|  
|**pub_range**|**bigint**|パブリッシャーの ID 範囲の大きさ。|  
|**range**|**bigint**|調整の際にサブスクライバーに割り当てられる、連続する ID 値の大きさ。|  
|**max_identity**|**bigint**|ID 範囲の上限です。|  
|**threshold**|**int**|ID 範囲のしきい値のパーセンテージ。|  
|**current_max**|**bigint**|現在の最大値を割り当てることができますが、必ずしもを割り当てます。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
