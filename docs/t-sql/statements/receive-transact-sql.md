---
title: RECEIVE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RECEIVE_TSQL
- RECEIVE
dev_langs:
- TSQL
helpviewer_keywords:
- queues [Service Broker], message retrieval
- messages [Service Broker], retrieving
- RECEIVE statement
- receiving messages
- retrieving messages
ms.assetid: 878c6c14-37ab-4b87-9854-7f8f42bac7dd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e555a51cc4ab7c628dc75469aa1cfe4d7c01edcc
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211440"
---
# <a name="receive-transact-sql"></a>RECEIVE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  キューから 1 つ以上のメッセージを受信します。 キューの保有期間の設定に応じて、キューからメッセージを削除するか、キュー内のメッセージの状態を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
[ WAITFOR ( ]  
    RECEIVE [ TOP ( n ) ]   
        <column_specifier> [ ,...n ]  
        FROM <queue>  
        [ INTO table_variable ]  
        [ WHERE {  conversation_handle = conversation_handle  
                 | conversation_group_id = conversation_group_id } ]  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<column_specifier> ::=  
{    *   
  |  { column_name | [ ] expression } [ [ AS ] column_alias ]  
  |  column_alias = expression   
}     [ ,...n ]   
  
<queue> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
## <a name="arguments"></a>引数  
 WAITFOR  
 現在メッセージが存在しない場合、RECEIVE ステートメントが、キューにメッセージが到着するのを待機するように指定します。  
  
 TOP( *n* )  
 返されるメッセージの最大数を指定します。 この句を指定しない場合、ステートメントの条件に合致したすべてのメッセージが返されます。  
  
 \*  
 結果セットにキューのすべての列を含めることを指定します。  
  
 *column_name*  
 結果セットに含める列の名前です。  
  
 *式 (expression)*  
 列名、定数、関数、またはその組み合わせです。組み合わせる場合は演算子を使用します。  
  
 *column_alias*  
 結果セット内の列名を置換する別名です。  
  
 FROM  
 取得するメッセージが含まれているキューを指定します。  
  
 *database_name*  
 メッセージを受信するキューが含まれているデータベースの名前です。 *database_name* を指定しない場合、既定では現在のデータベースが使用されます。  
  
 *schema_name*  
 メッセージを受信するキューを所有するスキーマの名前です。 *schema_name* を指定しない場合、既定では現在のユーザーに関する既定のスキーマが使用されます。  
  
 *queue_name*  
 メッセージを受信するキューの名前です。  
  
 INTO *table_variable*  
 RECEIVE によってメッセージを格納するテーブル変数を指定します。 テーブル変数の列数は、メッセージ内の列数と同じである必要があります。 テーブル変数の各列のデータ型は、メッセージ内の対応する列のデータ型に暗黙的に変換できる必要があります。 INTO を指定しない場合、メッセージは結果セットとして返されます。  
  
 WHERE  
 受信するメッセージのメッセージ交換、またはメッセージ交換グループを指定します。 指定しない場合、次に使用可能なメッセージ交換グループからのメッセージが返されます。  
  
 conversation_handle = *conversation_handle*  
 受信するメッセージのメッセージ交換を指定します。 指定する *conversation_handle* は、**uniqueidentifer** 型であるか、または **uniqueidentifier** に変換可能な型である必要があります。  
  
 conversation_group_id = *conversation_group_id*  
 受信するメッセージのメッセージ交換グループを指定します。 指定する *conversation_group_id* は、**uniqueidentifer** 型であるか、または **uniqueidentifier** に変換可能な型である必要があります。  
  
 TIMEOUT *timeout*  
 ステートメントでメッセージを待機する時間をミリ秒で指定します。 この句は WAITFOR 句と共に使用する必要があります。 この句を指定しないか、タイムアウトが -**1** の場合、待機時間は無制限になります。 タイムアウトの時間を過ぎると、RECEIVE では空の結果セットが返されます。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  RECEIVE ステートメントがバッチまたはストアド プロシージャで最初のステートメントではない場合は、前のステートメントの後にセミコロン (;) を指定する必要があります。  
  
 RECEIVE ステートメントでは、キューからメッセージが読み取られ、結果セットが返されます。 結果セットには 0 以上の行が含まれ、各行には 1 つのメッセージが含まれます。 INTO 句が使用されず、*column_specifier* でローカル変数に値が割り当てられない場合、このステートメントでは呼び出し元のプログラムに結果セットが返されます。  
  
 RECEIVE ステートメントによって返されるメッセージには、さまざまなメッセージ型があります。 アプリケーションでは、**message_type_name** 列を使用して、関連付けられているメッセージ型を処理するコードに各メッセージをルーティングできます。 メッセージ型には、次の 2 種類があります。  
  
-   CREATE MESSAGE TYPE ステートメントを使用して作成されたアプリケーション定義のメッセージ型。 メッセージ交換で使用できるアプリケーション定義のメッセージ型のセットは、メッセージ交換に指定されている [!INCLUDE[ssSB](../../includes/sssb-md.md)] コントラクトで定義されます。  
  
-   状態やエラー情報を返す [!INCLUDE[ssSB](../../includes/sssb-md.md)] システム メッセージ。  
  
 キューにメッセージ保有期間が指定されていない場合、RECEIVE ステートメントでは受信したメッセージがキューから削除されます。 キューの RETENTION 設定が ON になっている場合、RECEIVE ステートメントでは **status** 列が **0** に更新され、メッセージはキューに残ります。 RECEIVE ステートメントを含むトランザクションがロールバックされる場合は、そのトランザクションでキューに行われたすべての変更もロールバックされ、キューにメッセージが戻されます。  
  
 RECEIVE ステートメントで返されるメッセージは、すべて同じメッセージ交換グループに属しています。 RECEIVE ステートメントでは、ステートメントを含むトランザクションが完了するまで、返されるメッセージのメッセージ交換グループがロックされます。 RECEIVE ステートメントでは、**status** が **1** のメッセージが返されます。 RECEIVE ステートメントで返された結果セットは暗黙的に並べ替えられます。  
  
-   複数のメッセージ交換のメッセージが WHERE 句の条件を満たす場合、RECEIVE ステートメントでは、1 つのメッセージ交換のメッセージがすべて返されてから、他のメッセージ交換のメッセージが返されます。 メッセージ交換は、優先度レベルの降順に処理されます。  
  
-   指定されたメッセージ交換に対して、RECEIVE ステートメントでは、メッセージが **message_sequence_number** の値で昇順に並べ替えられて返されます。  
  
 RECEIVE ステートメントの WHERE 句には、**conversation_handle** または **conversation_group_id** のいずれかを使用した検索条件を 1 つだけ含めることができます。 検索条件にキューの他の列を 1 つ以上含めることはできません。 **conversation_handle** または **conversation_group_id** を式にすることはできません。 返されるメッセージのセットは、WHERE 句で指定した条件によって決まります。  
  
-   **conversation_handle** を指定した場合、RECEIVE では、指定したメッセージ交換から、キュー内の使用できるメッセージがすべて返されます。  
  
-   **conversation_group_id** を指定した場合、RECEIVE では、指定したメッセージ交換グループのメンバーである任意のメッセージ交換から、キュー内の使用できるメッセージがすべて返されます。  
  
-   WHERE 句がない場合は、RECEIVE によって、次の条件を満たすメッセージ交換グループに決定されます。  
  
    -   1 つ以上のメッセージがキュー内にある。  
  
    -   別の RECEIVE ステートメントによってロックされていない。  
  
    -   上記の条件を満たすすべてのメッセージ交換グループのうち、最も高い優先度レベルを持つ。  
  
     決定後、RECEIVE によって、選択されたメッセージ交換グループのメンバーである任意のメッセージ交換から、キュー内の使用できるメッセージがすべて返されます。  
  
 WHERE 句で指定したメッセージ交換ハンドルまたはメッセージ交換グループの識別子が存在しないか、指定したキューに関連付けられていない場合、RECEIVE ステートメントではエラーが返されます。  
  
 RECEIVE ステートメントで指定したキューの状態が OFF に設定されている場合、ステートメントは失敗し、[!INCLUDE[tsql](../../includes/tsql-md.md)] エラーが返されます。  
  
 WAITFOR 句を指定した場合、ステートメントは指定のタイムアウト時間が経過するか結果セットが使用可能になるまで待機します。 ステートメントが待機しているときに、キューが削除されたり、キューの状態が OFF に設定されると、ステートメントでは直ちにエラーが返されます。 RECEIVE ステートメントでメッセージ交換グループまたはメッセージ交換ハンドルを指定したが、メッセージ交換で使用するサービスが削除されたり、他のキューに移動された場合、RECEIVE ステートメントでは [!INCLUDE[tsql](../../includes/tsql-md.md)] エラーがレポートされます。  
  
 RECEIVE は、ユーザー定義の関数では無効です。  
  
 RECEIVE ステートメントには、優先度のスタベーション防止はありません。 1 つの RECEIVE ステートメントによってメッセージ交換グループがロックされ、優先度の低いメッセージ交換から大量のメッセージが取得されると、そのグループ内の優先度の高いメッセージ交換からメッセージを受信できなくなります。 このような状態を回避するには、優先度の低いメッセージ交換からメッセージを取得する場合に、TOP 句を使用して、各 RECEIVE ステートメントによって取得されるメッセージ数を制限します。  
  
## <a name="queue-columns"></a>キューの列  
 次の表は、キューの列の一覧です。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**ステータス**|**tinyint**|メッセージの状態。 RECEIVE コマンドで返されるメッセージの状態は常に **0** です。 キューのメッセージには、次のいずれかの値が含まれます。<br /><br /> **0** = 準備完了。**1** = 受信メッセージ。**2** = 未完了。**3** = 保持されている送信済みメッセージ。|  
|**priority**|**tinyint**|メッセージに適用されているメッセージ交換の優先度レベル。|  
|**queuing_order**|**bigint**|キュー内のメッセージの順序番号。|  
|**conversation_group_id**|**uniqueidentifier**|メッセージが属するメッセージ交換グループの識別子。|  
|**conversation_handle**|**uniqueidentifier**|メッセージが属するメッセージ交換のハンドル。|  
|**message_sequence_number**|**bigint**|メッセージ交換内でのメッセージのシーケンス番号。|  
|**service_name**|**nvarchar(512)**|メッセージ交換の対象サービスの名前。|  
|**service_id**|**int**|メッセージ交換の対象サービスに関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト識別子。|  
|**service_contract_name**|**nvarchar (256)**|メッセージ交換が従うコントラクトの名前。|  
|**service_contract_id**|**int**|メッセージ交換が従うコントラクトに関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト識別子。|  
|**message_type_name**|**nvarchar (256)**|メッセージの形式を示すメッセージ型の名前。 メッセージは、アプリケーション メッセージ型か Broker システム メッセージのいずれかになります。|  
|**message_type_id**|**int**|メッセージの種類を示すメッセージ型に関する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクト識別子。|  
|**validation**|**nchar(2)**|メッセージに使用される検証。<br /><br /> **E**= 空。**N**= なし。**X**= XML。|  
|**message_body**|**varbinary(MAX)**|メッセージの内容。|  
  
## <a name="permissions"></a>アクセス許可  
 メッセージを受信するには、キューに対する RECEIVE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-receiving-all-columns-for-all-messages-in-a-conversation-group"></a>A. メッセージ交換グループにあるすべてのメッセージの、すべての列を受信する  
 次の例では、`ExpenseQueue` キューから、次に使用できるメッセージ交換グループに属している使用可能なすべてのメッセージを受信します。 このステートメントでは、メッセージが結果セットとして返されます。  
  
```  
RECEIVE * FROM ExpenseQueue ;  
```  
  
### <a name="b-receiving-specified-columns-for-all-messages-in-a-conversation-group"></a>B. メッセージ交換グループにあるすべてのメッセージを対象として、指定した列を受信する  
 次の例では、`ExpenseQueue` キューから、次に使用できるメッセージ交換グループに属している使用可能なすべてのメッセージを受信します。 このステートメントでは、列 `conversation_handle`、`message_type_name`、`message_body` を含むメッセージが結果セットとして返されます。  
  
```  
RECEIVE conversation_handle, message_type_name, message_body  
FROM ExpenseQueue ;  
```  
  
### <a name="c-receiving-the-first-available-message-in-the-queue"></a>C. キューで最初に使用可能なメッセージを受信する  
 次の例では、`ExpenseQueue` キューから、最初に使用可能なメッセージを結果セットとして受信します。  
  
```  
RECEIVE TOP (1) * FROM ExpenseQueue ;  
```  
  
### <a name="d-receiving-all-messages-for-a-specified-conversation"></a>D. 指定したメッセージ交換のすべてのメッセージを受信する  
 次の例では、`ExpenseQueue` キューから、指定したメッセージ交換に属している使用可能なすべてのメッセージを結果セットとして受信します。  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER ;  
  
SET @conversation_handle = <retrieve conversation from database> ;  
  
RECEIVE *  
FROM ExpenseQueue  
WHERE conversation_handle = @conversation_handle ;  
```  
  
### <a name="e-receiving-messages-for-a-specified-conversation-group"></a>E. 指定したメッセージ交換グループのメッセージを受信する  
 次の例では、`ExpenseQueue` キューから、指定したメッセージ交換グループに属している使用可能なすべてのメッセージを結果セットとして受信します。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id =   
    <retrieve conversation group ID from database> ;  
  
RECEIVE *  
FROM ExpenseQueue  
WHERE conversation_group_id = @conversation_group_id ;  
```  
  
### <a name="f-receiving-into-a-table-variable"></a>F. 受信したメッセージをテーブル変数に挿入する  
 次の例では、`ExpenseQueue` キューから、指定したメッセージ交換グループに属している使用可能なすべてのメッセージを受信して、テーブル変数に挿入します。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
DECLARE @procTable TABLE(  
     service_instance_id UNIQUEIDENTIFIER,  
     handle UNIQUEIDENTIFIER,  
     message_sequence_number BIGINT,  
     service_name NVARCHAR(512),  
     service_contract_name NVARCHAR(256),  
     message_type_name NVARCHAR(256),  
     validation NCHAR,  
     message_body VARBINARY(MAX)) ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database> ;  
  
RECEIVE TOP (1)  
    conversation_group_id,  
    conversation_handle,  
    message_sequence_number,  
    service_name,  
    service_contract_name,  
    message_type_name,  
    validation,  
    message_body  
FROM ExpenseQueue  
INTO @procTable  
WHERE conversation_group_id = @conversation_group_id ;  
```  
  
### <a name="g-receiving-messages-and-waiting-indefinitely"></a>G. メッセージを受信して無制限に待機する  
 次の例では、`ExpenseQueue` キューから、次に使用できるメッセージ交換グループに属している使用可能なすべてのメッセージを受信します。 このステートメントは、少なくとも 1 つのメッセージが使用可能になるまで待機し、その後すべてのメッセージ列を含む結果セットを返します。  
  
```  
WAITFOR (  
    RECEIVE *  
    FROM ExpenseQueue) ;  
```  
  
### <a name="h-receiving-messages-and-waiting-for-a-specified-interval"></a>H. メッセージを受信して指定の期間待機する  
 次の例では、`ExpenseQueue` キューから、次に使用できるメッセージ交換グループに属している使用可能なすべてのメッセージを受信します。 このステートメントは、60 秒が経過するか、少なくとも 1 つのメッセージが使用可能になるまで待機します。 少なくとも 1 つのメッセージが使用可能である場合、このステートメントはすべてのメッセージ列を含む結果セットを返します。 それ以外の場合は、空の結果セットを返します。  
  
```  
WAITFOR (  
    RECEIVE *  
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="i-receiving-messages-modifying-the-type-of-a-column"></a>I. メッセージを受信して列の型を変更する  
 次の例では、`ExpenseQueue` キューから、次に使用できるメッセージ交換グループに属している使用可能なすべてのメッセージを受信します。 メッセージ型でメッセージに XML ドキュメントが含まれることが指定されている場合、このステートメントでは、メッセージ本文が XML に変換されます。  
  
```  
WAITFOR (  
    RECEIVE message_type_name,  
        CASE  
            WHEN validation = 'X' THEN CAST(message_body as XML)  
            ELSE NULL  
         END AS message_body   
         FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="j-receiving-a-message-extracting-data-from-the-message-body-retrieving-conversation-state"></a>J. メッセージを受信し、メッセージ本文からデータを抽出して、メッセージ交換の状態を取得する  
 次の例では、`ExpenseQueue` キューから、次に使用できるメッセージ交換グループに属している、次に使用可能なメッセージを取得します。 メッセージの型が `//Adventure-Works.com/Expenses/SubmitExpense` の場合、このステートメントでは、メッセージ本文から従業員 ID とアイテム一覧が抽出されます。 また、このステートメントでは `ConversationState` テーブルからメッセージ交換の状態も取得されます。  
  
```  
WAITFOR(  
    RECEIVE   
    TOP(1)  
      message_type_name,  
      COALESCE(  
           (SELECT TOP(1) ConversationState  
            FROM CurrentConversations AS cc  
            WHERE cc.ConversationHandle = conversation_handle),  
           'NEW')  
      AS ConversationState,  
      COALESCE(  
          (SELECT TOP(1) ErrorCount  
           FROM CurrentConversations AS cc  
           WHERE cc.ConversationHandle = conversation_handle),   
           0)  
      AS ConversationErrors,  
      CASE WHEN message_type_name = N'//Adventure-Works.com/Expenses/SubmitExpense'  
          THEN CAST(message_body AS XML).value(  
                'declare namespace rpt = "https://Adventure-Works.com/schemas/expenseReport"  
                   (/rpt:ExpenseReport/rpt:EmployeeID)[1]', 'nvarchar(20)')  
         ELSE NULL  
      END AS EmployeeID,  
      CASE WHEN message_type_name = N'//Adventure-Works.com/Expenses/SubmitExpense'  
          THEN CAST(message_body AS XML).query(  
                'declare namespace rpt = "https://Adventure-Works.com/schemas/expenseReport"   
                     /rpt:ExpenseReport/rpt:ItemDetail')  
          ELSE NULL  
      END AS ItemList  
    FROM ExpenseQueue   
), TIMEOUT 60000 ;  
```  
  
## <a name="see-also"></a>参照  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [BEGIN CONVERSATION TIMER &#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)  
  
  
