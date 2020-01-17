---
title: sys.server_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_events_TSQL
- sys.server_events_TSQL
- server_events
- sys.server_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_events catalog view
ms.assetid: 996f6c9b-6426-4847-95d9-6b77541422be
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3613c3da1138a6ec17394a5b6615d78d0a941e56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133149"
---
# <a name="sysserverevents-transact-sql"></a>sys.server_events (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー レベルのイベント通知またはサーバー レベルの DDL トリガーが起動されるイベントごとに 1 行のデータを保持します。 列**object_id**と**型**サーバー イベントを一意に識別します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|起動するには、サーバー レベルのイベント通知またはサーバー レベル DDL トリガーの ID。|  
|**type**|**int**|起動するには、イベント通知または DDL トリガーを原因となるイベントの種類。|  
|**type_desc**|**nvarchar(60)**|DDL トリガーまたはイベント通知を起動させるイベントの説明です。|  
|**event_group_type**|**int**|トリガーまたはイベント通知が作成されるイベント グループ、またはイベント グループを作成していない場合は null です。|  
|**event_group_type**|**nvarchar(60)**|トリガーまたはイベント通知が作成されるイベント グループの説明またはイベント グループを作成していない場合は null|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
