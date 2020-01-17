---
title: sys.trigger_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc2732797551317a392b0ab55d9ecbeb28d990a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091941"
---
# <a name="systriggerevents-transact-sql"></a>sys.trigger_events (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  トリガーが起動されるイベントごとに 1 行のデータを保持します。  
  
> [!NOTE]  
>  **sys.trigger_events**イベント通知には適用されません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Sys.events から継承された列 >**|適用なし|継承、 **object_id**、**型**、 **type_desc**から列[sys.events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)します。|  
|**is_first**|**bit**|トリガーは、最初にこのイベントの起動として設定されます。|  
|**is_last**|**bit**|トリガーは、最後にこのイベントの起動として設定されます。|  
|**event_group_type**|**int**|トリガーが作成されるイベント グループ、またはイベント グループを作成していない場合は null。|  
|**event_group_type**|**nvarchar(60)**|トリガーが作成されるイベント グループの説明またはイベント グループを作成していない場合は null です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
