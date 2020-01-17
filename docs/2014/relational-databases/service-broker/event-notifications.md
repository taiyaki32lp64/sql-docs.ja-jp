---
title: イベント通知 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d7c74ee9963d93d289f589115712614a745dad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68197774"
---
# <a name="event-notifications"></a>イベントの通知
  イベント通知を使用すると、イベントについての情報を [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスに送信できます。 イベント通知は、さまざまな [!INCLUDE[tsql](../../includes/tsql-md.md)] データ定義言語 (DDL) ステートメントおよび SQL トレースのイベントに応答して実行されます。イベント通知は、これらのイベントに関する情報を [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスに送信することで実行されます。  
  
 イベント通知を使用できるのは、次のような作業を行う場合です。  
  
-   データベース上で発生した変更または操作をログに記録して確認する。  
  
-   イベントに応答した操作を、同期的にではなく、非同期に実行する。  
  
 イベント通知により、DDL トリガーおよび SQL トレースに代わるプログラミングを提供できます。  
  
## <a name="event-notifications-benefits"></a>イベント通知の利点  
 イベント通知は、トランザクションのスコープの外部で非同期に実行されます。 そのため、DDL トリガーとは異なり、イベント通知をデータベース アプリケーション内部で使用して、即時トランザクションで定義されるリソースを使用しないでイベントに応答することができます。  
  
 SQL トレースとは異なり、イベント通知は、SQL トレース イベントに応答して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で操作を実行するために使用できます。  
  
 イベント データは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と共に実行されているアプリケーションで使用して、進行状況を追跡したり判断を下したりすることができます。 たとえば、 `ALTER TABLE` サンプル データベースで [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ステートメントが実行されるたびに、次のイベント通知により、特定のサービスに情報が送信されます。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>イベント通知の概念  
 イベント通知が作成されると、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] のインスタンスと指定した対象サービスの間で、1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メッセージ交換が開かれます。 メッセージ交換は通常、イベント通知がサーバー インスタンス上のオブジェクトとして存在する限り、開いたままになります。 一部のエラーでは、イベント通知が削除される前にメッセージ交換が終了する場合があります。 このようなメッセージ交換がイベント通知間で共有されることはありません。 イベント通知ごとに、独自の排他的なメッセージ交換が確立されます。 メッセージ交換を明示的に終了すると、対象のサービスがこれ以上メッセージを受信しなくなります。また、次回イベント通知が起動されてもメッセージ交換は再度開かれません。  
  
 イベント発生時の情報、影響を受けるデータベース オブジェクトの情報、関係する [!INCLUDE[ssSB](../../includes/sssb-md.md)] バッチ ステートメント、およびその他の情報を提供するイベント情報が、`xml` 型の変数として [!INCLUDE[tsql](../../includes/tsql-md.md)] サービスに配信されます。 イベント通知によって生成された XML スキーマの詳細については、「[EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)」を参照してください。  
  
### <a name="event-notifications-vs-triggers"></a>イベント通知とトリガー  
 次の表では、トリガーとイベント通知の比較対照を示します。  
  
|トリガー|イベントの通知|  
|--------------|-------------------------|  
|DML トリガーは DML (データ操作言語) イベントに応答します。 DDL トリガーは DDL (データ定義言語) イベントに応答します。|イベント通知は、DDL イベントと SQL トレース イベントのサブセットに応答します。|  
|トリガーでは、Transact-SQL または CLR (共通言語ランタイム) マネージド コードを実行できます。|イベント通知ではコードは実行されません。 代わりに、送信`xml`Service Broker サービスへのメッセージ。|  
|トリガーを起動させるトランザクションのスコープ内では、トリガーは同期的に処理されます。|イベント通知は非同期に処理され、イベント通知を発生させるトランザクションのスコープ内では実行されません。|  
|トリガーのコンシューマーは、トリガーを起動させるイベントに緊密に結び付けられます。|イベント通知のコンシューマーは、イベント通知を起動させるイベントからは切り離されます。|  
|トリガーは、ローカル サーバーで処理される必要があります。|イベント通知はリモート サーバーで処理できます。|  
|トリガーはロールバックできます。|イベント通知はロールバックできません。|  
|DML トリガー名はスキーマ スコープです。 DDL トリガー名は、データベースまたはサーバーによってスコープが設定されます。|イベント通知名は、サーバーまたはデータベースによってスコープが設定されます。 QUEUE_ACTIVATION イベントのイベント通知は、特定のキューにスコープが設定されます。|  
|DML トリガーは、トリガーが適用されるテーブルと同じ所有者に所有されます。|キュー上のイベント通知の所有者は、イベント通知が適用されるオブジェクトとは所有者が異なる場合があります。|  
|トリガーでは、EXECUTE AS 句がサポートされます。|イベント通知では、EXECUTE AS 句はサポートされません。|  
|DDL トリガー イベント情報のキャプチャは、返す EVENTDATA 関数を使用して、`xml`データ型。|イベント通知を送信する`xml`イベント情報が Service Broker サービス。 情報は、EVENTDATA 関数と同じスキーマにフォーマットされます。|  
|**sys.triggers** カタログ ビューと **sys.server_triggers** カタログ ビューに、トリガーに関するメタデータがあります。|**sys.event_notifications** カタログ ビューと **sys.server_event_notifications** カタログ ビューに、イベント通知に関するメタデータがあります。|  
  
### <a name="event-notifications-vs-sql-trace"></a>イベント通知とSQL トレース (SQL Trace)  
 次の表では、サーバー イベントを監視する場合のイベント通知と SQL トレースの使用を比較します。  
  
|SQL トレース (SQL Trace)|イベントの通知|  
|---------------|-------------------------|  
|SQL トレースでは、トランザクションに関連したパフォーマンス上のオーバーヘッドは生じません。 データのパッケージ化が効率的に行われます。|XML 形式のイベント データの作成やイベント通知の送信に関連して、パフォーマンス上のオーバーヘッドが生じます。|  
|SQL トレースは、どのトレース イベント クラスでも監視できます。|イベント通知では、トレース イベント クラスのサブセット、およびすべての DDL (データ定義言語) イベントを監視できます。|  
|トレース イベント内に生成するデータ列をカスタマイズできます。|イベント通知で返される XML 形式のイベント データのスキーマは固定です。|  
|DDL で生成されるトレース イベントは、DDL ステートメントがロールバックされるかどうかにかかわらず、常に生成されます。|対応する DDL ステートメントのイベントがロールバックされると、イベント通知は発生しません。|  
|トレース イベント データの中間フローを管理するには、トレース ファイルやトレース テーブルを設定し、管理する必要があります。|イベント通知データの中間管理は、Service Broker キューを使用して自動的に行われます。|  
|サーバーが再起動されるたびに、トレースを再起動する必要があります。|イベント通知は、登録後サーバー サイクル間で保持され、トランザクション処理されます。|  
|トレースを開始すると、それ以後は起動を制御できません。 停止時間とフィルター時間を使用して、開始時点を指定できます。 対応するトレース ファイルにポーリングすることで、トレースにアクセスできます。|イベント通知によって生成されたメッセージを受信するキューに対して WAITFOR ステートメントを使用することで、イベント通知を制御できます。 キューにポーリングすることで、イベント通知にアクセスできます。|  
|トレースを作成するために必要最低限の権限は、ALTER TRACE 権限です。 対応するコンピューター上にトレース ファイルを作成する場合にも、権限が必要です。|最低限の権限は、作成するイベント通知の種類によって異なります。 対応するキューでは、RECEIVE 権限も必要です。|  
|トレースはリモートで受信できます。|イベント通知はリモートで受信できます。|  
|トレース イベントは、システム ストアド プロシージャを使用して実装されます。|イベント通知は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] および [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを組み合わせて実装されます。|  
|プログラムからトレース イベント データにアクセスするには、対応するトレース テーブルへのクエリを実行するか、トレース ファイルを解析するか、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) TraceReader クラスを使用します。|プログラムからイベント データにアクセスするには、XML 形式のイベント データに対して XQuery を発行するか、SMO イベント クラスを使用します。|  
  
## <a name="event-notification-tasks"></a>イベント通知タスク  
  
|タスク|トピック|  
|----------|-----------|  
|イベント通知を作成して実装する方法について説明します。|[イベント通知の実装](implement-event-notifications.md)|  
|リモート サーバー上の Service Broker にメッセージを送信するイベント通知に対し、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ダイアログ セキュリティを構成する方法について説明します。|[イベント通知のダイアログ セキュリティの構成](configure-dialog-security-for-event-notifications.md)|  
|イベント通知に関する情報を取得する方法について説明します。|[イベント通知に関する情報の取得](get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>関連項目  
 [DDL トリガー](../triggers/ddl-triggers.md)   
 [DML トリガー](../triggers/dml-triggers.md)   
 [SQL トレース (SQL Trace)](../sql-trace/sql-trace.md)  
  
  
