---
title: CREATE EVENT NOTIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_EVENT_NOTIFICATION_TSQL
- NOTIFICATION_TSQL
- EVENT
- NOTIFICATION
- CREATE EVENT NOTIFICATION
- EVENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EVENT NOTIFICATION statement
- events [SQL Server], notifications
- event notifications [SQL Server], creating
ms.assetid: dbbff0e8-9e25-4f12-a1ba-e12221d16ac2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 98e784be4bbe4e939ed4413a33d6a3ed36872558
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902814"
---
# <a name="create-event-notification-transact-sql"></a>CREATE EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース イベントやサーバー イベントに関する情報を Service Broker サービスに送信するオブジェクトを作成します。 イベント通知は [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでのみ作成されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE EVENT NOTIFICATION event_notification_name   
ON { SERVER | DATABASE | QUEUE queue_name }   
[ WITH FAN_IN ]  
FOR { event_type | event_group } [ ,...n ]  
TO SERVICE 'broker_service' , { 'broker_instance_specifier' | 'current database' }  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *event_notification_name*  
 イベント通知の名前です。 イベント通知名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に準拠している必要があり、作成先のスコープ内で一意であることが必要です (SERVER、DATABASE、または *object_name*)。  
  
 SERVER  
 イベント通知のスコープを現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに適用します。 指定した場合、FOR 句で指定したイベントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで発生するたびに、通知が行われます。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 DATABASE  
 イベント通知のスコープを現在のデータベースに適用します。 指定した場合、FOR 句で指定したイベントがデータベースで発生するたびに、通知が行われます。  
  
 QUEUE  
 通知のスコープを現在のデータベースの特定のキューに適用します。 QUEUE を指定できるのは、FOR QUEUE_ACTIVATION または FOR BROKER_QUEUE_DISABLED を指定した場合だけです。  
  
 *queue_name*  
 イベント通知を適用するキューの名前を指定します。 *queue_name* を指定できるのは、QUEUE を指定した場合だけです。  
  
 WITH FAN_IN  
 次の条件に該当するすべてのイベント通知に対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、イベントごとに 1 メッセージだけを指定のサービスに送信します。  
  
-   同じイベントで作成されたもの  
  
-   同じプリンシパルによって作成された (同じ SID で識別される) もの  
  
-   同じサービスと *broker_instance_specifier* を指定します。  
  
-   WITH FAN_IN を指定するイベント通知  
  
 たとえば、3 つのイベント通知が作成されます。 すべてのイベント通知は同じ SID によって作成され、FOR ALTER_TABLE、WITH FAN_IN、および同じ TO SERVICE 句が指定されています。 この場合、ALTER TABLE ステートメントを実行すると、これら 3 つのイベント通知で作成されたメッセージは 1 つにマージされます。 したがって、ターゲット サービスは、イベントのメッセージを 1 つだけ受信します。  
  
 *event_type*  
 イベント通知が実行されるイベントの種類の名前です。 *event_type* には、[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL イベントの種類、SQL トレース イベントの種類、または [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントの種類を指定できます。 指定できる [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL イベントの種類については、「[DDL イベント](../../relational-databases/triggers/ddl-events.md)」を参照してください。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントの種類は QUEUE_ACTIVATION と BROKER_QUEUE_DISABLED です。 詳しくは、「 [Event Notifications](../../relational-databases/service-broker/event-notifications.md)」をご覧ください。  
  
 *event_group*  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] または SQL トレース イベントの定義済みグループの名前を指定します。 イベント通知は、イベント グループに属するイベントが実行された後に実行されます。 DDL イベント グループと、対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] イベント、およびそれらを定義できるスコープの一覧については、「[DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)」を参照してください。  
  
 *event_group* は、対応するイベントの種類を**sys.events** カタログ ビューに追加した場合、CREATE EVENT NOTIFICATION ステートメントが終了したときにマクロとしても動作します。  
  
 **'** *broker_service* **'**  
 イベント インスタンスのデータを受信するターゲット サービスを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、イベント通知用に対象サービスに対して 1 つ以上のメッセージ交換が開きます。 このサービスは、同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントのメッセージ型と、メッセージの送信に使用されるコントラクトに従っている必要があります。  
  
 メッセージ交換は、イベント通知が削除されるまで開いたままになります。 特定のエラーが発生すると、メッセージ交換が予定よりも早く閉じる場合があります。 明示的にメッセージ交換の一部または全部を終了することで、ターゲット サービスでそれ以上メッセージを受信しないようにできます。  
  
 { **'** _broker\_instance\_specifier_ **'**  |  **'current database'** }  
 *broker_service* を解決する Service Broker インスタンスを指定します。 **sys.databases** カタログ ビューの **service_broker_guid** 列にクエリを実行することで、特定の Service Broker の値を取得できます。 現在のデータベースの Service Broker インスタンスを指定するには、 **'current database'** を使用します。 **'current database'** は大文字と小文字を区別しない文字列リテラルです。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] には、イベント通知用のメッセージ型とコントラクトが含まれています。 したがって、コントラクト名 (`https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`) を指定する Service Broker 開始サービスが既に存在するため、開始サービスを作成する必要はありません  
  
 イベント通知を受け取る対象サービスは、この既存のコントラクトに従う必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] ダイアログ セキュリティを構成する必要があります。 ダイアログ セキュリティは完全なセキュリティ モデルに基づいて手動で構成する必要があります。 詳しくは、「[イベント通知のダイアログ セキュリティの構成](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)」をご覧ください。  
  
 通知を有効にしたイベント トランザクションがロールバックされた場合、イベント通知の送信もロールバックされます。 トランザクションがトリガー内でコミットまたはロールバックされた場合、トリガーで定義されたアクションによってイベント通知が行われることはありません。 トレース イベントはトランザクションでバインドされないため、トレース イベントに基づくイベント通知は、イベント通知を有効にするトランザクションがロールバックされたかどうかに関係なく送信されます。  
  
 イベント通知が行われた後で、サーバーと対象サービスの間のメッセージ交換が解除された場合は、エラーがレポートされ、イベント通知は削除されます。  
  
 通知を起動したイベント トランザクションが、イベント通知送信の成功または失敗によって影響を受けることはありません。  
  
 イベント通知の送信が失敗した場合はログに記録されます。  
  
## <a name="permissions"></a>アクセス許可  
 データベース スコープ (ON DATABASE) のイベント通知を作成するには、現在のデータベースの CREATE DATABASE DDL EVENT NOTIFICATION 権限が必要です。  
  
 サーバー スコープ (ON SERVER) の DDL ステートメントのイベント通知を作成するには、サーバーの CREATE DDL EVENT NOTIFICATION 権限が必要です。  
  
 トレース イベントのイベント通知を作成するには、サーバーの CREATE TRACE EVENT NOTIFICATION 権限が必要です。  
  
 キュー スコープのイベント通知を作成するには、キューの ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
> [!NOTE]  
>  以下に示す A と B の例では、`TO SERVICE 'NotifyService'` 句の GUID ('8140a771-3c4b-4479-8ac0-81008ab17984') は、例をセットアップしたコンピューターに固有の値です。 ここで示した例の場合は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの GUID です。  
>   
>  これらの例をコピーして実行するには、この GUID をお使いのコンピューターおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの GUID に置き換える必要があります。 前述の「引数」セクションで説明したように、sys.databases カタログ ビューの service_broker_guid 列に対してクエリを実行することで **'** _broker\_instance\_specifier_ **'** を取得することができます。  
  
### <a name="a-creating-an-event-notification-that-is-server-scoped"></a>A. サーバー スコープのイベント通知を作成する  
 次の例では、[!INCLUDE[ssSB](../../includes/sssb-md.md)] を使用する対象サービスの設定で必要となるオブジェクトを作成します。 対象サービスでは、イベント通知専用の開始サービスのメッセージ型とコントラクトが参照されます。 作成後は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで `Object_Created` トレース イベントが発生するたびに通知を送信する対象サービスに対して、イベント通知が作成されます。  
  
```sql  
--Create a queue to receive messages.  
CREATE QUEUE NotifyQueue ;  
GO  
--Create a service on the queue that references  
--the event notifications contract.  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
([https://schemas.microsoft.com/SQL/Notifications/PostEventNotification]);  
GO  
--Create a route on the service to define the address   
--to which Service Broker sends messages for the service.  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
--Create the event notification.  
CREATE EVENT NOTIFICATION log_ddl1   
ON SERVER   
FOR Object_Created   
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
### <a name="b-creating-an-event-notification-that-is-database-scoped"></a>B. データベース スコープのイベント通知を作成する  
 次の例では、前の例と同じターゲット サービスに対してイベント通知を作成します。 イベント通知は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースで `ALTER_TABLE` イベントが発生した後に行われます。  
  
```sql  
CREATE EVENT NOTIFICATION Notify_ALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
### <a name="c-getting-information-about-an-event-notification-that-is-server-scoped"></a>C. サーバー スコープのイベント通知に関する情報を取得する  
 次の例では、`sys.server_event_notifications` カタログ ビューをクエリして、サーバー スコープで作成されたイベント通知 `log_ddl1` に関するメタデータを取得します。  
  
```  
SELECT * FROM sys.server_event_notifications  
WHERE name = 'log_ddl1';  
```  
  
### <a name="d-getting-information-about-an-event-notification-that-is-database-scoped"></a>D. データベース スコープのイベント通知に関する情報を取得する  
 次の例では、`sys.event_notifications` カタログ ビューをクエリして、データベース スコープで作成されたイベント通知 `Notify_ALTER_T1` に関するメタデータを取得します。  
  
```sql  
SELECT * FROM sys.event_notifications  
WHERE name = 'Notify_ALTER_T1';  
```  
  
## <a name="see-also"></a>参照  
 [イベント通知](../../relational-databases/service-broker/event-notifications.md)   
 [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)   
 [sys.server_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md)  
  
  
