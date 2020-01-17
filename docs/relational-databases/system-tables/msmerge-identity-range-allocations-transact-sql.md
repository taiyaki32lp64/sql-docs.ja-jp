---
title: MSmerge_identity_range_allocations (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
author: stevestein
ms.author: sstein
ms.openlocfilehash: de0325925bb1ad1626987361435056ff21a26be6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072653"
---
# <a name="msmerge_identity_range_allocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range_allocations** id 範囲の割り当て、パブリッシャーとサブスクライバーの両方にパブリッシュされたアーティクルの履歴を追跡するテーブルを使用します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**nvarchar(128)**|パブリケーション データベースの名前です。|  
|**publication**|**nvarchar(128)**|パブリケーションの名前を指定します。|  
|**article**|**nvarchar(128)**|アーティクルの名前です。|  
|**subscriber**|**nvarchar(128)**|サブスクライバーの名前。|  
|**subscriber_db**|**nvarchar(128)**|サブスクリプション データベースの名前。|  
|**is_pub_range**|**bit**|Id 範囲がパブリッシャーに割り当てられているかどうかを示します。|  
|**ranges_allocated**|**tinyint**|割り当てられている ID 範囲の数です。|  
|**range_begin**|**numeric(38)**|範囲の開始値。|  
|**range_end**|**numeric(38)**|範囲の最後の値。|  
|**next_range_begin**|**numeric(38)**|次の範囲で割り当てられる開始値です。|  
|**next_range_end**|**numeric(38)**|割り当てられる次の範囲の最後の値。|  
|**max_used**|**numeric(38)**|使用されている最大 ID 値です。|  
|**time_of_allocation**|**datetime**|時刻、割り当てが行われた場合。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
