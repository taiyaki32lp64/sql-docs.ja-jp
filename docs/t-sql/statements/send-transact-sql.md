---
title: SEND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9a6c6993252ccad0335b177c31c9d20b40f520a5
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211430"
---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

1 つ以上の既存のメッセージ交換を使用してメッセージを送信します。  
  
![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
ON CONVERSATION *conversation_handle [.. @conversation_handle_n]*  
メッセージが属するメッセージ交換を指定します。 *conversation_handle* には、有効なメッセージ交換識別子が含まれている必要があります。 同じメッセージ交換ハンドルを複数回使用することはできません。  
  
MESSAGE TYPE *message_type_name*  
送信したメッセージのメッセージ型を指定します。 このメッセージ型は、これらのメッセージ交換で使用されるサービス コントラクトに含まれている必要があります。 これらのコントラクトによって、メッセージ型をメッセージ交換の発信側から送信できます。 たとえば、メッセージ交換の対象サービスは、SENT BY TARGET または SENT BY ANY としてコントラクトに指定されるメッセージのみを送信できます。 この句が省略されると、メッセージは DEFAULT のメッセージ型になります。  
  
*message_body_expression*  
メッセージ本文を表す式を指定します。 *message_body_expression* は省略可能です。 ただし、*message_body_expression* を指定する場合は、**varbinary(max)** に変換できる型の式にする必要があります。 この式が NULL になることはありません。 この句が省略されると、メッセージ本文は空になります。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  SEND ステートメントがバッチまたはストアド プロシージャで最初のステートメントではない場合は、前のステートメントの後にセミコロン (;) を指定する必要があります。  
  
SEND ステートメントは、1 つ以上の [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ交換の一方のエンドポイントにあるサービスからもう一方のエンドポイントにあるサービスに、メッセージを送信します。 次に RECEIVE ステートメントを使用して、送信されたメッセージを、ターゲット サービスに関連付けられたキューから取得します。  
  
ON CONVERSATION 句に指定されるメッセージ交換ハンドルのソースは、次の 3 つのうちいずれかです。  
  
- 別のサービスから受信したメッセージに対する応答ではないメッセージを送信する場合、メッセージ交換を作成した BEGIN DIALOG ステートメントから返されるメッセージ交換ハンドルを使用します。  
  
- 別のサービスから以前に受信したメッセージに対して応答のメッセージを送信する場合、元のメッセージを返した RECEIVE ステートメントから返されるメッセージ交換ハンドルを使用します。  
  
- メッセージ交換ハンドルを提供する BEGIN DIALOG ステートメントや RECEIVE ステートメントが含まれたコードとは別のコードに、SEND ステートメントが含まれていることがあります。 そのような場合、メッセージ交換ハンドルは、SEND ステートメントが含まれたコードに渡される状態情報のデータ アイテムのいずれかである必要があります。  
  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の別のインスタンス内のサービスに送信されるメッセージは、リモート インスタンスのサービス キューに送信できるようになるまでの間、現在のデータベースの転送キューに格納されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の同じインスタンス内のサービスに送信されるメッセージは、それらのサービスに関連付けられたキューに直接配置されます。 ローカル メッセージを転送先サービス キューに直接配置できない条件がある場合は、その条件が解決されるまで転送キューに格納されることがあります。 これが発生するのは、特定のエラーが発生した場合や、転送先サービス キューが非アクティブな場合などです。 **sys.transmission_queue** システム ビューを使用すると、転送キュー内のメッセージを表示できます。  
  
SEND はアトミック ステートメントです。 メッセージ交換がエラー状態の場合などに、複数のメッセージ交換でメッセージを送信する SEND ステートメントが失敗した場合、メッセージは転送キューまたは転送先サービス キューに格納されません。  
  
Service Broker は、同じ SEND ステートメントを使用して複数のメッセージ交換で送信されるメッセージの格納と転送を最適化します。  
  
インスタンスの転送キュー内のメッセージは、次の内容に基づいて順番に転送されます。  
  
- 関連するメッセージ交換エンドポイントの優先度レベル。  
  
- 優先度レベル内では、メッセージ交換における送信順序。  
  
メッセージ交換の優先度で指定された優先順位は、HONOR_BROKER_PRIORITY データベース オプションが ON に設定されている場合にのみ、転送キュー内のメッセージに割り当てられます。 HONOR_BROKER_PRIORITY データベース オプションが OFF に設定されている場合、そのデータベースの転送キューに配置されたすべてのメッセージには、既定の優先度レベル 5 が割り当てられます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の同じインスタンス内のサービス キューにメッセージが直接配置される場合、SEND には優先順位が割り当てられません。  
  
SEND ステートメントは、メッセージを送信する各メッセージ交換を個別にロックし、メッセージ交換ごとの順序でメッセージが配信されるようにします。  
  
SEND はユーザー定義の関数では無効です。  
  
## <a name="permissions"></a>アクセス許可  
メッセージを送信するには、現在のユーザーは、メッセージを送信するすべてのサービスのキューに対する RECEIVE 権限を持っている必要があります。  
  
## <a name="examples"></a>使用例  
次の例では、ダイアログを開始し、ダイアログ上の XML メッセージを送信します。 メッセージを送信するために、この例では xml オブジェクトを **varbinary(max)** に変換します。  
  
```sql
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
次の例では、3 つのダイアログを開始し、各ダイアログ上の XML メッセージを送信します。  
  
```sql
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService'  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>参照  
[BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
[END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
[RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)   
[sys.transmission_queue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  
