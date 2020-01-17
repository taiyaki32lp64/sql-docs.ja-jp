---
title: sys.server_event_notifications (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e3eaa1bdfa45e0c3e0b0412b8852e134c43c3eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124992"
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各サーバー レベルのイベント通知オブジェクトの行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|サーバー イベント通知名です。 すべてのサーバー レベルのイベント通知の間で一意です。|  
|**object_id**|**int**|オブジェクト ID 番号。 内で一意では、**マスター**データベース。|  
|**parent_class**|**tinyint**|親のクラスです。 常に 100 = サーバーです。|  
|**parent_class_desc**|**nvarchar(60)**|親のクラスの説明です。 サーバーは常にします。|  
|**parent_id**|**int**|常に 0 です。|  
|**create_date**|**datetime**|作成された日付。|  
|**modify_date**|**datetime**|オブジェクトが ALTER ステートメントを使用して最後に変更された日付です。|  
|**service_name**|**nvarchar (256)**|通知の送信先のサービスの名前です。|  
|**broker_instance**|**nvarchar(128)**|指定された通知先サービスが定義されている Service Broker です。|  
|**creator_sid**|**varbinary(85)**|イベント通知を作成するステートメントを実行するログインの SID。 WITH FAN_IN がない場合は NULL は指定イベントの通知の定義です。|  
|**principal_id**|**int**|これを所有しているサーバー プリンシパルの ID です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
