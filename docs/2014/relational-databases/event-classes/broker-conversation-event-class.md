---
title: Broker:Conversation イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Conversation event class
ms.assetid: 784707b5-cc67-46a3-8ae6-8f8ecf4b27c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d6f29eba93e7841d2d64db57266d8f2ad859377
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664368"
---
# <a name="brokerconversation-event-class"></a>Broker:Conversation イベント クラス
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **Service Broker** メッセージ交換の進行状況を報告するために、Broker:Conversation イベントが生成されます。  
  
## <a name="brokerconversation-event-class-data-columns"></a>Broker:Conversation イベント クラスのデータ列  
  
|データ列|型|説明|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|[はい]|  
|**ClientProcessID**|`int`|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|[はい]|  
|**DatabaseID**|`int`|USE *database* ステートメントで指定されているデータベースの ID。 特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、 **DB_ID** 関数を使用して特定します。|3|[はい]|  
|**EventClass**|`int`|キャプチャされたイベント クラスの種類。 **Broker:Conversation** の場合は、常に **124**です。|27|いいえ|  
|**EventSequence**|`int`|このイベントのシーケンス番号。|51|いいえ|  
|**EventSubClass**|`nvarchar`|イベント サブクラスの種類。 各イベント クラスについての詳細情報を提供します。|21|はい|  
|**GUID**|`uniqueidentifier`|ダイアログのメッセージ交換 ID。 この ID はメッセージの一部として転送され、メッセージ交換の両側で共有されます。|54|いいえ|  
|**HostName**|`nvarchar`|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、 **HOST_NAME** 関数を使用します。|8|はい|  
|**IsSystem**|`int`|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> 0 = ユーザー<br /><br /> 1 = システム|60|いいえ|  
|**LoginSid**|`image`|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**MethodName**|`nvarchar`|このメッセージ交換が属しているメッセージ交換グループ。|47|いいえ|  
|**NTDomainName**|`nvarchar`|ユーザーが属している Windows ドメイン。|7|はい|  
|**NTUserName**|`nvarchar`|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**ObjectName**|`nvarchar`|ダイアログのメッセージ交換ハンドル。|34|いいえ|  
|**[Priority]**|`int`|メッセージ交換の優先度レベル。|5|はい|  
|**RoleName**|`nvarchar`|メッセージ交換ハンドルのロール。 **initiator** または **target**のいずれかです。|38|いいえ|  
|**ServerName**|`nvarchar`|トレースしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|26|いいえ|  
|**Severity**|`int`|(このイベントによってエラーが報告された場合) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーの重大度。|29|いいえ|  
|**SPID**|`int`|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**StartTime**|`datetime`|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**TextData**|`ntext`|メッセージ交換の現在の状態。 次のいずれかです。<br /><br /> **SO**。 送信開始状態。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でこのメッセージ交換に対して BEGIN CONVERSATION が処理されましたが、メッセージはまだ送信されていません。<br /><br /> **SI**。 受信開始状態。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の別のインスタンスで現在のインスタンスとの新しいメッセージ交換が開始されましたが、現在のインスタンスが最初のメッセージの受信を完了していません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、最初のメッセージが分割されたものであるか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で順序どおりにメッセージが受け取られなかった場合は、この状態のメッセージ交換が作成されます。 ただし、メッセージ交換で受信された最初の転送データに最初のメッセージ全体が含まれている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で CO 状態のメッセージ交換が作成されることがあります。<br /><br /> **CO**。 メッセージ交換中状態。 メッセージ交換が確立され、メッセージ交換の両側からメッセージを送信できます。 通常のサービスに関する通信の大部分は、メッセージ交換がこの状態のときに行われます。<br /><br /> **DI**。 受信切断状態。 メッセージ交換のリモート側で END CONVERSATION が発行されました。 メッセージ交換のローカル側で END CONVERSATION が発行されるまで、メッセージ交換はこの状態になります。 アプリケーションは引き続きこのメッセージ交換のメッセージを受信できます。 メッセージ交換のリモート側ではメッセージ交換が終了しているので、このメッセージ交換でアプリケーションからメッセージを送信することはできません。 アプリケーションで END CONVERSATION を発行すると、メッセージ交換は終了 (CD) 状態に移行します。<br /><br /> **DO**。 送信切断状態。 メッセージ交換のローカル側で END CONVERSATION が発行されました。 メッセージ交換のリモート側で END CONVERSATION が承認されるまで、メッセージ交換はこの状態になります。 アプリケーションはこのメッセージ交換でメッセージを送受信することはできません。 メッセージ交換のリモート側で END CONVERSATION が承認されると、メッセージの交換は終了 (CD) 状態に移行します。<br /><br /> **ER**。 エラー状態。 このエンドポイントでエラーが発生しました。 Error、Severity、State の各列に、発生した特定のエラーに関する情報が含まれています。<br /><br /> **CD**。 終了状態。 メッセージ交換のエンドポイントは解放されました。|1|はい|  
|**Transaction ID**|`bigint`|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
 次の表は、このイベント クラスのサブクラス値の一覧です。  
  
|ID|サブクラス|説明|  
|--------|--------------|-----------------|  
|1|SEND Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **で SEND ステートメントが実行されるときに、** SEND Message [!INCLUDE[ssDE](../../includes/ssde-md.md)] イベントが生成されます。|  
|2|END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **で WITH ERROR 句を指定しない END CONVERSATION ステートメントが実行されるときに、** END CONVERSATION [!INCLUDE[ssDE](../../includes/ssde-md.md)] イベントが生成されます。|  
|3|END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **で WITH ERROR 句を指定した END CONVERSATION ステートメントが実行されるときに、** END CONVERSATION WITH ERROR [!INCLUDE[ssDE](../../includes/ssde-md.md)] イベントが生成されます。|  
|4|Broker Initiated Error|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **でエラー メッセージが作成されるたびに** Broker Initiated Error [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントが生成されます。 たとえば、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] がダイアログのメッセージをルーティングできないときは、ブローカーがそのダイアログのエラー メッセージを作成し、このイベントを生成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、アプリケーション プログラムがエラーでメッセージ交換を終了しても、このイベントが生成されることはありません。|  
|5|Terminate Dialog|[!INCLUDE[ssSB](../../includes/sssb-md.md)] がダイアログを終了しました。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] はダイアログの続行を妨げる条件に反応してダイアログを終了しますが、この条件はエラーやメッセージ交換の通常の終了ではありません。 たとえば、サービスを削除すると、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] はそのサービスのダイアログをすべて終了します。|  
|6|Received Sequenced Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **でメッセージ シーケンス番号を含むメッセージを受信するときに、** Received Sequenced Message [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベント クラスが生成されます。 ユーザー定義メッセージ型はすべてシーケンス番号付きメッセージです。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、次の 2 つの場合にシーケンス番号のないメッセージが生成されます。<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] が生成するエラー メッセージにはシーケンス番号が付きません。<br /><br /> メッセージの受信確認にはシーケンス番号が付けられない場合があります。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、効率を上げるために、シーケンス番号付きメッセージにすべてのメッセージ受信確認が含められます。 ただし、アプリケーションから一定時間内にシーケンス番号付きメッセージがリモート エンドポイントに送信されなかった場合、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] はメッセージ受信確認用にシーケンス番号のないメッセージを作成します。|  
|7|Received END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメッセージ交換の相手から End Dialog メッセージを受信するときに、Received END CONVERSATION イベントが生成されます。|  
|8|Received END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **がメッセージ交換の相手側からユーザー定義エラーを受信すると、** Received END CONVERSATION WITH ERROR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントが生成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がブローカー定義エラーを受信した場合は、このイベントは生成されません。|  
|9|Received Broker Error Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **がメッセージ交換の相手側からブローカー定義エラー メッセージを受信すると、** Received Broker Error Message [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントが生成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] がアプリケーションで生成されたエラー メッセージを受信した場合は、このイベントは生成されません。<br /><br /> たとえば、現在のデータベースに転送先のデータベースへの既定のルートが含まれている場合、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ではサービス名が不明なメッセージをその転送先にルーティングします。 転送先のデータベースがメッセージをルーティングできない場合、そのデータベースのブローカーでエラー メッセージが作成され、現在のデータベースに返されます。 現在のデータベースが転送先のデータベースからブローカーが生成したエラーを受信すると、現在のデータベースで **Received Broker Error Message** イベントが生成されます。|  
|10|Received END CONVERSATION Ack|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メッセージ交換のこちら側から送信された End Dialog メッセージまたは Error メッセージの受信が相手側で確認されるときに、 **Received END CONVERSATION Ack** イベント クラスが生成されます。|  
|11|BEGIN DIALOG|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベース エンジンで BEGIN DIALOG コマンドが実行されるときに、 **BEGIN DIALOG** イベントが生成されます。|  
|12|Dialog Created|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **がダイアログのエンドポイントを作成すると** Dialog Created [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントが生成されます。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] は、現在のデータベースがダイアログの開始側か相手側かにかかわらず、新しいダイアログが確立されるたびにエンドポイントを作成します。|  
|13|END CONVERSATION WITH CLEANUP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で WITH CLEANUP 句を指定した END CONVERSATION ステートメントが実行されるときに、END CONVERSATION WITH CLEANUP イベントが生成されます。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
