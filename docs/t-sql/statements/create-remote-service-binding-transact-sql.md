---
title: CREATE REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2fc021cec09a7f62d05f5e435db9d6fc2597fce3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117343"
---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  バインドを作成し、リモート サービスとのメッセージ交換を開始するときに使用するセキュリティ資格情報を定義します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *binding_name*  
 作成するリモート サービス バインドの名前を指定します。 サーバー名、データベース名、スキーマ名は指定できません。 *binding_name* は有効な **sysname** とする必要があります。  
  
 AUTHORIZATION *owner_name*  
 バインドの所有者を、指定したデータベース ユーザーまたはロールに設定します。 現在のユーザーが **dbo** または **sa** の場合、*owner_name* には、任意の有効なユーザーまたはロールの名前を指定できます。 それ以外の場合、*owner_name* には、現在のユーザーの名前、現在のユーザーが持つ IMPERSONATE 権限に対応するユーザーの名前、または現在のユーザーが所属するロールの名前を指定する必要があります。  
  
 TO SERVICE '*service_name*'  
 WITH USER 句のユーザーにバインドするリモート サービスを指定します。  
  
 USER = *user_name*  
 TO SERVICE 句のリモート サービスに関連付けられた証明を所有しているデータベース プリンシパルを指定します。 この証明は、リモート サービスと交換されるメッセージの暗号化と認証に使用されます。  
  
 ANONYMOUS  
 リモート サービスと通信するときに匿名認証を使用するかどうかを指定します。 ANONYMOUS を ON にすると匿名認証が使用され、リモート データベースでの操作は、**public** 固定データベース ロールのメンバーによる操作として実行されます。 ANONYMOUS を OFF にすると、リモート データベースでの操作は、そのデータベース固有のユーザーによる操作として実行されます。 この句を指定しない場合、既定値は OFF になります。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、リモート サービス バインドを使用して、新しいメッセージ交換に使用する証明書が検索されます。 *user_name* に関連付けられている証明の公開キーは、リモート サービスに送信されるメッセージの認証とセッション キーの暗号化に使用されます。その後、暗号化されたセッション キーを使用して、メッセージ交換が暗号化されます。 *user_name* の証明は、リモート サービスをホストするデータベースに格納されているユーザーの証明と対応している必要があります。  
  
 リモート サービス バインドは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの外部にある対象サービスと通信するサービスを開始する場合にのみ必要です。 開始サービスをホストするデータベースには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの外部にあるすべての対象サービスのリモート サービス バインドが含まれている必要があります。 ただし、対象サービスをホストするデータベースには、対象サービスと通信する開始サービスのリモート サービス バインドが含まれている必要はありません。 開始サービスと対象サービスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の同じインスタンス内にある場合、リモート サービス バインドは必要ありません。 ただし、TO SERVICE に指定された *service_name* とローカル サービスの名前が一致する場所にリモート サービス バインドが存在する場合は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] ではそのバインドが使用されます。  
  
 ANONYMOUS を ON にした場合、開始サービスは、**public** 固定データベース ロールのメンバーとして対象サービスに接続します。 既定では、このロールのメンバーはデータベースに接続する権限を持ちません。 メッセージを正常に送信するには、対象のデータベースで、**public** ロールに対して、データベースへの CONNECT 権限と対象サービスへの SEND 権限が与えられている必要があります。  
  
 ユーザーが複数の証明を所有している場合は、[!INCLUDE[ssSB](../../includes/sssb-md.md)] によって現在有効な証明のうち有効期限が最も新しい証明が選択され、その証明が AVAILABLE FOR BEGIN_DIALOG としてマークされます。  
  
## <a name="permissions"></a>アクセス許可  
 リモート サービス バインドを作成する権限は、既定では、USER 句で指定されたユーザー、**db_owner** 固定データベース ロールのメンバー、**db_ddladmin** 固定データベース ロールのメンバー、**sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
 CREATE REMOTE SERVICE BINDING ステートメントを実行するには、ステートメントで指定されるプリンシパルの借用権限が必要です。  
  
 リモート サービス バインドは一時オブジェクトとして指定できません。 **#** で始まるリモート サービス バインド名は許可されますが、パーマネント オブジェクトになります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-remote-service-binding"></a>A. リモート サービス バインドを作成する  
 次の例では、サービス `//Adventure-Works.com/services/AccountsPayable` のバインドを作成します。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、データベース プリンシパル `APUser` が所有する証明を使用してリモート サービスへの認証が行われ、リモート サービスとの間でセッション暗号化キーが交換されます。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. 匿名認証を使用してリモート サービス バインドを作成する  
 次の例では、サービス `//Adventure-Works.com/services/AccountsPayable` のバインドを作成します。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、データベース プリンシパル `APUser` が所有する証明を使用して、リモート サービスとの間でセッション暗号化キーが交換されます。 Service Broker でリモート サービスへの認証は行われません。 リモート サービスをホストするデータベースでは、メッセージは **guest** ユーザーとして配信されます。  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
