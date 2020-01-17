---
title: sys.dm_broker_forwarded_messages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87f471a91aad067dd1662f243cdbafd73d335979
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099152"
---
# <a name="sysdmbrokerforwardedmessages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各 Service Broker のメッセージを 1 行を返しますのインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]転送中です。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|このメッセージが属するメッセージ交換の ID。 NULL 値を許容します。|  
|**is_initiator**|**bit**|メッセージがメッセージ交換の発信側から送信されたものかどうかを示します。  NULL 値を許容します。<br /><br /> 0 = 発信側からでない<br /><br /> 1 = 発信側から|  
|**to_service_name**|**nvarchar(512)**|このメッセージを送信するサービスの名前。 NULL 値を許容します。|  
|**to_broker_instance**|**nvarchar(512)**|このメッセージを送信するサービスをホストするブローカーの識別子。 NULL 値を許容します。|  
|**from_service_name**|**nvarchar(512)**|このメッセージはサービスの名前です。 NULL 値を許容します。|  
|**from_broker_instance**|**nvarchar(512)**|メッセージの送信元となるサービスをホストしているブローカーの識別子。 NULL 値を許容します。|  
|**adjacent_broker_address**|**nvarchar(512)**|このメッセージを送信するネットワーク アドレスです。 NULL 値を許容します。|  
|**message_sequence_number**|**bigint**|ダイアログ ボックスで、メッセージのシーケンス番号。 NULL 値を許容します。|  
|**message_fragment_number**|**int**|ダイアログ メッセージが断片化している場合、このトランスポート メッセージに含まれるフラグメント番号。 NULL 値を許容します。|  
|**hops_remaining**|**tinyint**|メッセージが最終送信先に届くまでに再転送される回数。 メッセージが転送されるたび、この数は 1 ずつ減少します。 NULL 値を許容します。|  
|**time_to_live**|**int**|アクティブのままにするメッセージの最大時間。 この値が 0 に達すると、メッセージは破棄されます。 NULL 値を許容します。|  
|**time_consumed**|**int**|メッセージを既にアクティブにされている時間です。 メッセージが転送されるたびにメッセージを転送するにかかった時間によってこの数が増加します。 Null を許容しません。|  
|**message_id**|**uniqueidentifier**|メッセージの ID。 NULL 値を許容します。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

