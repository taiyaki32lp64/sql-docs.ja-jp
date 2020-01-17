---
title: Broker イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9918aca57caaef0dc460e810f5ed5ca2d1106ac3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663811"
---
# <a name="broker-event-category"></a>Broker イベント カテゴリ
  **Broker** イベント カテゴリには、一般的な Service Broker イベントが含まれます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Broker:Activation イベント クラス](broker-activation-event-class.md)|キュー モニターがアクティブ化ストアド プロシージャを開始するときに生成されるイベント。|  
|[Broker:Connection イベント クラス](broker-connection-event-class.md)|Service Broker によって管理されるトランスポート接続のステータスをレポートするために生成されるイベントです。|  
|[Broker:Conversation イベント クラス](broker-conversation-event-class.md)|メッセージ交換の進行状況をレポートするために生成されるイベントです。|  
|[Broker:Conversation Group イベント クラス](broker-conversation-group-event-class.md)|データベースがメッセージ交換グループを作成または削除すると生成されるイベントです。|  
|[Broker:Corrupted Message イベント クラス](broker-corrupted-message-event-class.md)|データベースが破損メッセージを受信したことを報告するために生成されるイベント。|  
|[Broker:Forwarded Message Dropped イベント クラス](broker-forwarded-message-dropped-event-class.md)|転送された Service Broker メッセージが SQL Server によって削除されるときに生成されるイベント。|  
|[Broker:Forwarded Message Sent イベント クラス](broker-forwarded-message-sent-event-class.md)|SQL Server によって Service Broker メッセージが転送されるときに生成されるイベント。|  
|[Broker:Message Classify イベント クラス](broker-message-classify-event-class.md)|Service Broker がメッセージのルーティングを決定するときに生成されるイベント。|  
|[Broker:Message Drop イベント クラス](broker-message-drop-event-class.md)|このインスタンスのサービスに配信する必要のある受信メッセージを、Service Broker が保持できないときに生成されるイベント。|  
|[Broker:Remote Message Ack イベント クラス](broker-remote-message-ack-event-class.md)|Service Broker がメッセージの受信確認を送信または受信したときに生成されるイベント。|  
  
 Service Broker には、2 つのセキュリティ監査イベントも提供されます。 これらのイベントの詳細については、「 [Audit Broker Login イベント クラス](audit-broker-login-event-class.md) 」と「 [Audit Broker Conversation イベント クラス](audit-broker-conversation-event-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ監査イベント カテゴリ](https://docs.microsoft.com/bi-reference/trace-events/security-audit-event-category)  
  
  
