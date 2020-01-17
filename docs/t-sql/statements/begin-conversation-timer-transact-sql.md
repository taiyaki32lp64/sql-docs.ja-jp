---
title: BEGIN CONVERSATION TIMER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONVERSATION
- BEGIN_CONVERSATION_TSQL
- TIMER_TSQL
- TIMER
- CONVERSATION TIMER
- CONVERSATION_TIMER_TSQL
- BEGIN CONVERSATION TIMER
- BEGIN_CONVERSATION_TIMER_TSQL
- CONVERSATION_TSQL
- BEGIN CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN CONVERSATION TIMER statement
- DialogTimer message
- dialogs [Service Broker], beginning
- timeouts [Service Broker]
- timer messages [Service Broker]
- conversations [Service Broker], timers
- starting timers [Service Broker]
- https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer message
ms.assetid: 98e49b3f-a38f-4180-8171-fa9cb30db4cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65fbd94bac320994f9c1917e634210febd2ba878
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211218"
---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  タイマーを開始します。 タイムアウトになると、[!INCLUDE[ssSB](../../includes/sssb-md.md)] はメッセージ交換のローカル キューに型 `https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer` のメッセージを入れます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 BEGIN CONVERSATION TIMER **(**_conversation\_handle_**)**  
 メッセージ交換を定刻に指定します。 *conversation_handle* は型 **uniqueidentifier** にする必要があります。  
  
 TIMEOUT  
 メッセージをキューに配置する前に待機する時間を、秒単位で指定します。  
  
## <a name="remarks"></a>Remarks  
 メッセージ交換タイマーによって、特定の時間が経過すると、メッセージ交換でメッセージを受信する方法がアプリケーションに提供されます。 タイマーが時間切れになる前にメッセージ交換で BEGIN CONVERSATION TIMER を呼び出すと、タイムアウトが新しい値に設定されます。 メッセージ交換の有効期間とは異なり、メッセージ交換の送信側と受信側に個別のメッセージ交換タイマーがあります。 **DialogTimer** メッセージは、リモート側のメッセージ交換に影響することなくローカル キューに届きます。 したがって、タイマー メッセージはアプリケーションでどのような目的にも使用できます。  
  
 たとえばメッセージ交換タイマーを使用すると、アプリケーションで、期限の切れた応答に対する待機時間を短くすることができます。 アプリケーションが 30 秒以内にダイアログを完了するようにする場合、そのダイアログのメッセージ交換タイマーを 60 秒 (30 秒に 30 秒の猶予時間を加えたもの) に設定できます。 ダイアログが 60 秒後もまだ開いている場合、アプリケーションはそのダイアログのキューでタイムアウト メッセージを受信します。  
  
 また、アプリケーションはメッセージ交換タイマーを使用して、特定の時間にアクティブ化を要求できます。 たとえば、数分ごとにアクティブな接続数を報告するサービス、またはオープンな予約発注数を毎晩報告するサービスを作成できます。 このサービスでは、メッセージ交換タイマーを希望する時間に終了するように設定します。タイマーが終了すると、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって **DialogTimer** メッセージが送信されます。 **DialogTimer** メッセージにより、[!INCLUDE[ssSB](../../includes/sssb-md.md)] でキュー用のアクティブ化ストアド プロシージャが開始します。 このストアド プロシージャによって、メッセージがリモート サービスに送信され、メッセージ交換タイマーが再開します。  
  
 BEGIN CONVERSATION TIMER は、ユーザー定義の関数では無効です。  
  
## <a name="permissions"></a>アクセス許可  
 メッセージ交換タイマーの設定権限は、既定では、メッセージ交換用サービスに対する SEND 権限を持つユーザー、**sysadmin** 固定サーバー ロールのメンバー、**db_owner** 固定データベース ロールのメンバーに与えられています。  
  
## <a name="examples"></a>使用例  
 次の例では、`@dialog_handle` で指定されるダイアログに 2 分間のタイムアウトを設定します。  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>参照  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  
