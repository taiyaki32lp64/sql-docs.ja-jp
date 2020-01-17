---
title: Broker イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8efa6f503f552965e3885d92626e8b5da453e29b
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494097"
---
# <a name="broker-event-category"></a>Broker イベント カテゴリ

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

**Broker** イベント カテゴリには、一般的な Service Broker イベントが含まれます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[Broker:Activation イベント クラス](../../relational-databases/event-classes/broker-activation-event-class.md)|キュー モニターがアクティブ化ストアド プロシージャを開始するときに生成されるイベント。|  
|[Broker:Connection イベント クラス](../../relational-databases/event-classes/broker-connection-event-class.md)|Service Broker によって管理されるトランスポート接続のステータスをレポートするために生成されるイベントです。|  
|[Broker:Conversation イベント クラス](../../relational-databases/event-classes/broker-conversation-event-class.md)|メッセージ交換の進行状況をレポートするために生成されるイベントです。|  
|[Broker:Conversation Group イベント クラス](../../relational-databases/event-classes/broker-conversation-group-event-class.md)|データベースがメッセージ交換グループを作成または削除すると生成されるイベントです。|  
|[Broker:Corrupted Message イベント クラス](../../relational-databases/event-classes/broker-corrupted-message-event-class.md)|データベースが破損メッセージを受信したことを報告するために生成されるイベント。|  
|[Broker:Forwarded Message Dropped イベント クラス](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)|転送された Service Broker メッセージが SQL Server によって削除されるときに生成されるイベント。|  
|[Broker:Forwarded Message Sent イベント クラス](../../relational-databases/event-classes/broker-forwarded-message-sent-event-class.md)|SQL Server によって Service Broker メッセージが転送されるときに生成されるイベント。|  
|[Broker:Message Classify イベント クラス](../../relational-databases/event-classes/broker-message-classify-event-class.md)|Service Broker がメッセージのルーティングを決定するときに生成されるイベント。|  
|[Broker:Message Drop イベント クラス](../../relational-databases/event-classes/broker-message-drop-event-class.md)|このインスタンスのサービスに配信する必要のある受信メッセージを、Service Broker が保持できないときに生成されるイベント。|  
|[Broker:Remote Message Ack イベント クラス](../../relational-databases/event-classes/broker-remote-message-ack-event-class.md)|Service Broker がメッセージの受信確認を送信または受信したときに生成されるイベント。|  
  
 Service Broker には、2 つのセキュリティ監査イベントも提供されます。 これらのイベントの詳細については、「 [Audit Broker Login イベント クラス](../../relational-databases/event-classes/audit-broker-login-event-class.md) 」と「 [Audit Broker Conversation イベント クラス](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [セキュリティ監査イベント カテゴリ](/bi-reference/trace-events/security-audit-event-category)  
  
  
