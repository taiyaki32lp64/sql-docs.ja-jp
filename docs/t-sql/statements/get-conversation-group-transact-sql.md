---
title: GET CONVERSATION GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GET
- CONVERSATION_GROUP_TSQL
- GET_TSQL
- GET_CONVERSATION_GROUP_TSQL
- GET CONVERSATION GROUP
- CONVERSATION GROUP
- GET CONVERSATION
- GET_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GET CONVERSATION GROUP statement
- conversations [Service Broker], groups
ms.assetid: 4da8a855-33c0-43b2-a49d-527487cb3b5c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d0ede71391f31096191255c5a8fee2051ad6f696
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252187"
---
# <a name="get-conversation-group-transact-sql"></a>GET CONVERSATION GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  次に受信するメッセージのメッセージ交換グループの識別子を返すと共に、そのメッセージが含まれるメッセージ交換のメッセージ交換グループをロックします。 メッセージ交換グループの識別子は、メッセージ自体を取得する前にメッセージ交換の状態情報を取得する場合に使用できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
[ WAITFOR ( ]  
   GET CONVERSATION GROUP @conversation_group_id  
      FROM <queue>  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<queue> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }  
```  
  
## <a name="arguments"></a>引数  
 WAITFOR  
 現在メッセージが存在しない場合、GET CONVERSATION GROUP ステートメントが、キューにメッセージが到着するのを待機するように指定します。  
  
 *\@conversation_group_id*  
 GET CONVERSATION GROUP ステートメントによって返されるメッセージ交換グループ ID が格納される変数です。 この変数は、**uniqueidentifier** 型である必要があります。 使用できるメッセージ交換グループがない場合、この変数は NULL に設定されます。  
  
 FROM  
 メッセージ交換グループを取得するキューを指定します。  
  
 *database_name*  
 メッセージ交換グループを取得するキューが含まれているデータベースの名前を指定します。 *database_name* を指定しない場合、既定では現在のデータベースが使用されます。  
  
 *schema_name*  
 メッセージ交換グループを取得するキューを所有するスキーマの名前を指定します。 *schema_name* を指定しない場合、既定では現在のユーザーに関する既定のスキーマが使用されます。  
  
 *queue_name*  
 メッセージ交換グループを取得するキューの名前を指定します。  
  
 TIMEOUT *timeout*  
 Service Broker が、キューにメッセージが到着するのを待機する時間を指定します (ミリ秒単位)。 この句は WAITFOR 句と共に使用する必要があります。 WAITFOR 句を使用するステートメントにこの句が含まれないか、*timeout* が -1 の場合、待機時間は無制限になります。 タイムアウトになると、GET CONVERSATION GROUP では *\@conversation_group_id* 変数に NULL が設定されます。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  GET CONVERSATION GROUP ステートメントがバッチまたはストアド プロシージャの最初のステートメントではない場合は、前のステートメントの後に、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのターミネータであるセミコロン ( **;** ) を指定する必要があります。  
  
 GET CONVERSATION GROUP ステートメントで指定したキューが使用できない場合、ステートメントは失敗し、[!INCLUDE[tsql](../../includes/tsql-md.md)] エラーが返されます。  
  
 このステートメントでは、以下の条件をすべて満たす、次に使用できるメッセージ交換グループが返されます。  
  
-   メッセージ交換グループを正常にロックできる。  
  
-   メッセージ交換グループに、キューで利用できるメッセージが含まれている。  
  
-   返されるメッセージ交換グループが、上記の条件を満たすすべてのメッセージ交換グループのうち、最も高い優先度を持つ。 メッセージ交換グループの優先度は、そのグループのメンバーであり、キュー内にメッセージがあるメッセージ交換のいずれかに割り当てられている最も高い優先度です。  
  
 同じトランザクション内で GET CONVERSATION GROUP を続けて呼び出すと、複数のメッセージ交換グループがロックされる場合があります。 使用できるメッセージ交換グループがない場合、このステートメントでは、メッセージ交換グループの識別子として NULL が返されます。  
  
 WAITFOR 句を指定した場合、ステートメントは指定のタイムアウト時間が経過するかメッセージ交換グループが使用できるようになるまで待機します。 ステートメントの待機中にキューが削除された場合は、その時点でエラーが返されます。  
  
 GET CONVERSATION GROUP は、ユーザー定義の関数では無効です。  
  
## <a name="permissions"></a>アクセス許可  
 メッセージ交換グループの識別子をキューから取得する場合、現在のユーザーは、そのキューに対する RECEIVE 権限を持っている必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-getting-a-conversation-group-waiting-indefinitely"></a>A. 無制限に待機して、メッセージ交換グループを取得する  
 次の例では、`@conversation_group_id` にメッセージ交換グループの識別子を設定します。このメッセージ交換グループは、`ExpenseQueue` 上にあり、次に使用できるメッセージで使用されます。 このコマンドは、メッセージが使用できるようになるまで待機します。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
WAITFOR (  
 GET CONVERSATION GROUP @conversation_group_id  
     FROM ExpenseQueue  
) ;  
```  
  
### <a name="b-getting-a-conversation-group-waiting-one-minute"></a>B. 1 分間待機して、メッセージ交換グループを取得する  
 次の例では、`@conversation_group_id` にメッセージ交換グループの識別子を設定します。このメッセージ交換グループは、`ExpenseQueue` 上にあり、次に使用できるメッセージで使用されます。 使用できるメッセージが 1 分以内に取得できない場合、GET CONVERSATION GROUP では、`@conversation_group_id` の値が変更されずに返されます。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER  
  
WAITFOR (  
    GET CONVERSATION GROUP @conversation_group_id   
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="c-getting-a-conversation-group-returning-immediately"></a>C. 待機せず、メッセージ交換グループを取得する  
 次の例では、`@conversation_group_id` にメッセージ交換グループの識別子を設定します。このメッセージ交換グループは、`ExpenseQueue` 上にあり、次に使用できるメッセージで使用されます。 使用できるメッセージがない場合、`GET CONVERSATION GROUP` ステートメントでは、`@conversation_group_id` の値が変更されずにすぐに返されます。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
GET CONVERSATION GROUP @conversation_group_id  
FROM AdventureWorks.dbo.ExpenseQueue ;  
```  
  
## <a name="see-also"></a>参照  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [MOVE CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/move-conversation-transact-sql.md)  
  
  
