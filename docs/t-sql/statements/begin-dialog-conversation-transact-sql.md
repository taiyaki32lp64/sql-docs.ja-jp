---
title: BEGIN DIALOG CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DIALOG CONVERSATION
- DIALOG
- BEGIN_DIALOG_TSQL
- BEGIN_DIALOG_CONVERSATION_TSQL
- DIALOG_CONVERSATION_TSQL
- DIALOG_TSQL
- BEGIN DIALOG
- BEGIN DIALOG CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker]
- beginning dialogs
- dialogs [Service Broker], beginning
- BEGIN DIALOG CONVERSATION statement
- cryptography [SQL Server], conversations
- opening conversations
- encryption [SQL Server], conversations
- starting conversations
ms.assetid: 8e814f9d-77c1-4906-b8e4-668a86fc94ba
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c456b6e34dba77b7e35cc24e8af673662725a2bb
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211374"
---
# <a name="begin-dialog-conversation-transact-sql"></a>BEGIN DIALOG CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  あるサービスから別のサービスに対してダイアログを開始します。 ダイアログとは、2 つのサービスの間で順序どおりにメッセージを 1 回だけ交換する (exactly-once-in-order) メッセージ交換のことです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
BEGIN DIALOG [ CONVERSATION ] @dialog_handle  
   FROM SERVICE initiator_service_name  
   TO SERVICE 'target_service_name'  
       [ , { 'service_broker_guid' | 'CURRENT DATABASE' }]   
   [ ON CONTRACT contract_name ]  
   [ WITH  
   [  { RELATED_CONVERSATION = related_conversation_handle   
      | RELATED_CONVERSATION_GROUP = related_conversation_group_id } ]   
   [ [ , ] LIFETIME = dialog_lifetime ]   
   [ [ , ] ENCRYPTION = { ON | OFF }  ] ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 **@** _dialog_handle_  
 システムで生成される、新しいダイアログ用のダイアログ ハンドルを格納する変数です。この値は、BEGIN DIALOG CONVERSATION ステートメントによって返されます。 この変数は、**uniqueidentifier** 型である必要があります。  
  
 FROM SERVICE *initiator_service_name*  
 ダイアログを開始するサービスを指定します。 現在のデータベースにあるサービスの名前を指定する必要があります。 発信先サービスから返されるメッセージ、およびこのメッセージ交換用に Service Broker によって作成されるメッセージは、発信側サービス用に指定したキューで受信されます。  
  
 TO SERVICE **'**_target_service_name_**'**  
 ダイアログの発信先となるサービスを指定します。 *target_service_name* の型は **nvarchar(256)** です。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ではバイト単位の比較を使用して、*target_service_name* 文字列を照合します。 つまり、この場合、大文字小文字は区別され、現在の照合順序は考慮されません。  
  
 *service_broker_guid*  
 発信先サービスをホストするデータベースを指定します。 発信先サービスの 1 つのインスタンスが複数のデータベースでホストされる場合に、特定のデータベースと通信するには、*service_broker_guid* を指定します。  
  
 *service_broker_guid* は **nvarchar(128)** 型です。 データベースの *service_broker_guid* を検索するには、データベースで次のクエリを実行します。  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID() ;  
```  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 **'** CURRENT DATABASE **'**  
 メッセージ交換で現在のデータベースの *service_broker_guid* を使用することを指定します。  
  
 ON CONTRACT *contract_name*  
 メッセージ交換が従うコントラクトを指定します。 コントラクトは、現在のデータベース内に存在している必要があります。 発信先サービスで、指定したコントラクトに従った新しいメッセージ交換が受け入れられない場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] ではそのメッセージ交換に関するエラー メッセージが返されます。 この句を省略すると、メッセージ交換は **DEFAULT** という名前のコントラクトに従います。  
  
 RELATED_CONVERSATION **=**_related_conversation_handle_  
 新しいダイアログを追加する既存のメッセージ交換グループを指定します。 この句が存在する場合、新しいダイアログは、*related_conversation_handle* で指定したダイアログと同じメッセージ交換グループに属することになります。 *related_conversation_handle* は、**uniqueidentifier** 型に暗黙的に変換できる型である必要があります。 *related_conversation_handle* が既存のダイアログを参照していない場合、ステートメントは失敗します。  
  
 RELATED_CONVERSATION_GROUP **=**_related_conversation_group_id_  
 新しいダイアログを追加する既存のメッセージ交換グループを指定します。 この句が存在する場合、新しいダイアログは、*related_conversation_group_id* で指定したメッセージ交換グループに追加されます。 *related_conversation_group_id* は、**uniqueidentifier** 型に暗黙的に変換できる型である必要があります。 *related_conversation_group_id* が既存のメッセージ交換グループを参照していない場合、Service Broker では、指定した *related_conversation_group_id* で新しいメッセージ交換グループが作成され、そのメッセージ交換グループに新しいダイアログが関連付けられます。  
  
 LIFETIME **=**_dialog_lifetime_  
 ダイアログを開いたままにする最長時間を指定します。 ダイアログを正常に完了するには、有効期間の終了までに、双方のエンドポイントが明示的にダイアログを終了する必要があります。 *dialog_lifetime* の値は秒単位で表す必要があります。 有効期間は **int** 型です。LIFETIME 句を指定しない場合、ダイアログの有効期間は **int** データ型の最大値になります。  
  
 ENCRYPTION  
 このダイアログで送受信したメッセージを [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの外部に送信する場合に、暗号化するかどうかを指定します。 暗号化が必要なダイアログは、*セキュリティで保護されたダイアログ*です。 ENCRYPTION = ON の状態で、暗号化のサポートに必要な証明書が構成されていない場合は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってメッセージ交換に関するエラー メッセージが返されます。 ENCRYPTION = OFF の状態で、*target_service_name* に対してリモート サービス バインドが構成されている場合は、暗号化が使用されます。それ以外の場合、メッセージは暗号化されずに送信されます。 この句を指定しない場合、既定値の ON が使用されます。  
  
> [!NOTE]  
>  同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにあるサービス間で交換されるメッセージは暗号化されません。 ただし、メッセージ交換を行うサービスが異なるデータベースにある場合は、暗号化したメッセージ交換を行うために、データベースのマスター キーと暗号化の証明書が必要になります。 これらを用意しておくと、メッセージ交換中にデータベースの 1 つが別のインスタンスに移動した場合でも、メッセージ交換を続行できます。  
  
## <a name="remarks"></a>Remarks  
 すべてのメッセージはメッセージ交換の一部になります。 したがって、発信先サービスにメッセージを送信するには、発信側サービスで、発信先サービスとのメッセージ交換を開始する必要があります。 BEGIN DIALOG CONVERSATION ステートメントで指定する情報は、手紙の住所に似ています。[!INCLUDE[ssSB](../../includes/sssb-md.md)] ではこの情報を使用して、正しいサービスにメッセージを配信します。 TO SERVICE 句で指定するサービスは、メッセージの送信先アドレスです。 FROM SERVICE 句で指定するサービスは、メッセージの返信先アドレスです。  
  
 メッセージ交換の発信先で BEGIN DIALOG CONVERSATION を呼び出す必要はありません。 発信側からメッセージ交換の最初のメッセージが届くと、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって発信先データベースにメッセージ交換が作成されます。  
  
 ダイアログを開始すると、発信側サービスのデータベースにメッセージ交換のエンドポイントは作成されますが、発信先サービスをホストしているインスタンスへのネットワーク接続は作成されません。 最初のメッセージが送信されるまでは、[!INCLUDE[ssSB](../../includes/sssb-md.md)] でダイアログの発信先との通信は確立されません。  
  
 BEGIN DIALOG CONVERSATION ステートメントで、関連するメッセージ交換または関連するメッセージ交換グループを指定しなかった場合は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって、新しいメッセージ交換用の新しいメッセージ交換グループが作成されます。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、メッセージ交換のグループ化を任意に行うことはできません。 メッセージ交換グループのすべてのメッセージ交換に対しては、FROM 句を使って、メッセージ交換の発信側または発信先のサービスを指定する必要があります。  
  
 BEGIN DIALOG CONVERSATION コマンドを実行すると、返された *dialog_handle* が含まれているメッセージ交換グループがロックされます。 コマンドに RELATED_CONVERSATION_GROUP 句が含まれている場合、*dialog_handle* のメッセージ交換グループは、*related_conversation_group_id* パラメーターで指定したメッセージ交換グループになります。 コマンドに RELATED_CONVERSATION 句が含まれている場合、*dialog_handle* のメッセージ交換グループは、指定した *related_conversation_handle* に関連付けられているメッセージ交換グループになります。  
  
 BEGIN DIALOG CONVERSATION は、ユーザー定義の関数では無効です。  
  
## <a name="permissions"></a>アクセス許可  
 ダイアログを開始するには、現在のユーザーに、コマンドの FROM 句で指定したサービス用のキューに対する RECEIVE 権限と、指定したコントラクトの REFERENCES 権限が与えられている必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-beginning-a-dialog"></a>A. ダイアログを開始する  
 次の例では、ダイアログ メッセージ交換を開始し、`@dialog_handle.` にダイアログの識別子を格納します。`//Adventure-Works.com/ExpenseClient` サービスはダイアログの発信側で、`//Adventure-Works.com/Expenses` サービスはダイアログの発信先です。 このダイアログはコントラクト `//Adventure-Works.com/Expenses/ExpenseSubmission` に従います。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="b-beginning-a-dialog-with-an-explicit-lifetime"></a>B. 有効期間を明示してダイアログを開始する  
 次の例では、ダイアログ メッセージ交換を開始し、`@dialog_handle` にダイアログの識別子を格納します。 `//Adventure-Works.com/ExpenseClient` サービスはダイアログの発信側で、`//Adventure-Works.com/Expenses` サービスはダイアログの発信先です。 このダイアログはコントラクト `//Adventure-Works.com/Expenses/ExpenseSubmission` に従います。 `60` 秒以内に END CONVERSATION コマンドを使用してダイアログを閉じなかった場合は、ブローカーによってダイアログが終了され、エラーが返されます。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH LIFETIME = 60 ;  
```  
  
### <a name="c-beginning-a-dialog-with-a-specific-broker-instance"></a>C. 特定のブローカー インスタンスとのダイアログを開始する  
 次の例では、ダイアログ メッセージ交換を開始し、`@dialog_handle` にダイアログの識別子を格納します。 `//Adventure-Works.com/ExpenseClient` サービスはダイアログの発信側で、`//Adventure-Works.com/Expenses` サービスはダイアログの発信先です。 このダイアログはコントラクト `//Adventure-Works.com/Expenses/ExpenseSubmission` に従います。 ここでは、ブローカーによって、このダイアログから GUID `a326e034-d4cf-4e8b-8d98-4d7e1926c904.` で指定されたブローカーにメッセージがルートされます。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses',   
              'a326e034-d4cf-4e8b-8d98-4d7e1926c904'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="d-beginning-a-dialog-and-relating-it-to-an-existing-conversation-group"></a>D. ダイアログを開始し、そのダイアログを既存のメッセージ交換グループに関連付ける  
 次の例では、ダイアログ メッセージ交換を開始し、`@dialog_handle` にダイアログの識別子を格納します。 `//Adventure-Works.com/ExpenseClient` サービスはダイアログの発信側で、`//Adventure-Works.com/Expenses` サービスはダイアログの発信先です。 このダイアログはコントラクト `//Adventure-Works.com/Expenses/ExpenseSubmission` に従います。 ここでは、ブローカーによって、新しいメッセージ交換グループが作成されるのではなく、`@conversation_group_id` で指定したメッセージ交換グループにダイアログが関連付けられます。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION_GROUP = @conversation_group_id ;  
```  
  
### <a name="e-beginning-a-dialog-with-an-explicit-lifetime-and-relating-the-dialog-to-an-existing-conversation"></a>E. 有効期間を明示してダイアログを開始し、そのダイアログと既存のメッセージ交換を関連付ける  
 次の例では、ダイアログ メッセージ交換を開始し、`@dialog_handle` にダイアログの識別子を格納します。 `//Adventure-Works.com/ExpenseClient` サービスはダイアログの発信側で、`//Adventure-Works.com/Expenses` サービスはダイアログの発信先です。 このダイアログはコントラクト `//Adventure-Works.com/Expenses/ExpenseSubmission` に従います。 新しいダイアログは、`@existing_conversation_handle` が属するメッセージ交換グループと同じメッセージ交換グループに属します。 `600` 秒以内に END CONVERSATION コマンドを使用してダイアログを閉じなかった場合は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によってダイアログが終了され、エラーが返されます。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
DECLARE @existing_conversation_handle UNIQUEIDENTIFIER  
  
SET @existing_conversation_handle = <retrieve conversation handle from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION = @existing_conversation_handle  
   LIFETIME = 600 ;  
```  
  
### <a name="f-beginning-a-dialog-with-optional-encryption"></a>F. 暗号化のオプションを指定してダイアログを開始する  
 次の例では、ダイアログを開始し、`@dialog_handle` にダイアログの識別子を格納します。 `//Adventure-Works.com/ExpenseClient` サービスはダイアログの発信側で、`//Adventure-Works.com/Expenses` サービスはダイアログの発信先です。 このダイアログはコントラクト `//Adventure-Works.com/Expenses/ExpenseSubmission` に従います。 この例のメッセージ交換では、暗号化が利用できない場合に、暗号化していないメッセージをネットワークを介して送信できます。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH ENCRYPTION = OFF ;  
```  
  
## <a name="see-also"></a>参照  
 [BEGIN CONVERSATION TIMER &#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [MOVE CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/move-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
