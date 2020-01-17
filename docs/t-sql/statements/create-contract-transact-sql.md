---
title: CREATE CONTRACT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2e7dbdb8ea5a422b91f290478eeca4dfc9b21cbc
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064639"
---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新しいコントラクトを作成します。 コントラクトは、[!INCLUDE[ssSB](../../includes/sssb-md.md)] のメッセージ交換で使用されるメッセージ型を定義し、またメッセージ交換のどちら側がその型のメッセージを送信できるかを決定するものです。 各メッセージ交換は、コントラクトに従います。 発信側サービスでは、メッセージ交換の開始時に、そのメッセージ交換用のコントラクトを指定します。 ターゲット サービスでは、メッセージ交換を受け入れるコントラクトを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *contract_name*  
 作成するコントラクトの名前です。 新しいコントラクトは現在のデータベースで作成され、AUTHORIZATION 句で指定するプリンシパルによって所有されます。 サーバー名、データベース名、スキーマ名は指定できません。 *contract_name* には、最大 128 文字までを指定できます。  
  
> [!NOTE]  
>  *contract_name* のキーワード ANY を使用するコントラクトは作成しないでください。 CREATE BROKER PRIORITY でコントラクト名に ANY を指定した場合、優先度はすべてのコントラクトに適用されます。 名前が ANY のコントラクトに限定されません。  
  
 AUTHORIZATION *owner_name*  
 コントラクトの所有者を、指定したデータベース ユーザーまたはロールに設定します。 現在のユーザーが **dbo** または **sa** の場合、*owner_name* には、任意の有効なユーザーまたはロールの名前を指定できます。 それ以外の場合、*owner_name* には、現在のユーザーの名前、現在のユーザーが持つ借用権限に対応するユーザーの名前、または現在のユーザーが所属するロールの名前を指定する必要があります。 この句を省略すると、コントラクトは現在のユーザーに属します。  
  
 *message_type_name*  
 コントラクトの一部として含まれる、メッセージ型の名前です。  
  
 SENT BY  
 指定したメッセージ型のメッセージを送信できるエンドポイントを指定します。 コントラクトには、サービスが特定のメッセージ交換で使用できるメッセージが記録されています。 各メッセージ交換は、2 つのエンドポイントの間で行われます。1 つは*発信側*エンドポイントで、メッセージ交換を開始するサービスです。もう 1 つは*発信先*エンドポイントで、発信側のメッセージの送信先となるサービスです。  
  
 INITIATOR  
 メッセージ交換の発信側だけが、指定したメッセージ型のメッセージを送信できることを示します。 メッセージ交換を開始するサービスをメッセージ交換の*発信側*といいます。  
  
 TARGET  
 メッセージ交換のターゲットだけが、指定したメッセージ型のメッセージを送信できることを示します。 別のサービスによって開始されたメッセージ交換を受け入れるサービスをメッセージ交換の*発信先*といいます。  
  
 ANY  
 指定した型のメッセージを、発信側と発信先の両方から送信できることを示します。  
  
 [ DEFAULT ]  
 コントラクトで、既定のメッセージ型のメッセージがサポートされることを示します。 既定では、すべてのデータベースに DEFAULT という名前のメッセージ型が含まれます。 このメッセージ型では、NONE の検証を使用します。 この句のコンテキストでは、DEFAULT はキーワードとして扱われないため、識別子として区切り記号で区切る必要があります。 Microsoft SQL Server では、DEFAULT メッセージ型を指定する DEFAULT コントラクトも提供されています。  
  
## <a name="remarks"></a>Remarks  
 コントラクトのメッセージ型の順序は重要ではありません。 発信先が最初のメッセージを受信した後は、メッセージ交換のいずれの側からも、[!INCLUDE[ssSB](../../includes/sssb-md.md)] を介して、その側の許可されているメッセージをいつでも送信できるようになります。 たとえば、メッセージ交換の発信側でメッセージ型 **//Adventure-Works.com/Expenses/SubmitExpense** が許可されている場合、この発信側は [!INCLUDE[ssSB](../../includes/sssb-md.md)] を介して、メッセージ交換中に任意の数だけ **SubmitExpense** メッセージを送信できます。  
  
 コントラクトのメッセージ型と方向は変更できません。 コントラクトの AUTHORIZATION を変更するには、ALTER AUTHORIZATION ステートメントを使用します。  
  
 コントラクトでは、発信側がメッセージを送信することを許可する必要があります。 コントラクトに、SENT BY ANY または SENT BY INITIATOR のメッセージ型のうち少なくとも 1 つが含まれていないと、CREATE CONTRACT ステートメントは失敗します。  
  
 コントラクトに関係なく、サービスは常にメッセージ型 `https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`、`https://schemas.microsoft.com/SQL/ServiceBroker/Error`、`https://schemas.microsoft.com/SQL/ServiceBroker/EndDialog` を受信できます。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、アプリケーションへのシステム メッセージにこれらのメッセージ型が使用されます。  
  
 コントラクトは一時オブジェクトとして指定できません。 # で始まるコントラクト名は許可されますが、永続的オブジェクトになります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、**db_ddladmin** 固定データベース ロールまたは **db_owner** 固定データベース ロールのメンバーと **sysadmin** 固定サーバー ロールのメンバーがコントラクトを作成できます。  
  
 コントラクトの REFERENCES 権限は、既定ではコントラクトの所有者、**db_ddladmin** 固定データベース ロールまたは **db_owner** 固定データベース ロールのメンバー、**sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
 CREATE CONTRACT ステートメントを実行するには、指定されているすべてのメッセージ型に対する REFERENCES 権限が必要です。  
  
## <a name="examples"></a>使用例  
 **A.コントラクトを作成する**  
  
 次の例では、3 つのメッセージ型に基づいて経費の払い戻しのコントラクトを作成します。  
  
```sql  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>参照  
 [DROP CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
