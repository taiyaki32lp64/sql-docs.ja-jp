---
title: ALTER REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b91242524f3edada4de8112558a01f09fb3310cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927223"
---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  リモート サービス バインドに関連付けられているユーザーの変更や、バインドに関する匿名認証の設定の変更を行います。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *binding_name*  
 変更するリモート サービス バインドの名前です。 サーバー名、データベース名、スキーマ名は指定できません。  
  
 WITH USER = \<*user_name>*  
 このバインド用のリモート サービスに関連付けられた証明を保持しているデータベース ユーザーを指定します。 この証明の公開キーは、リモート サービスとの間で交換されるメッセージの暗号化と認証に使用されます。  
  
 ANONYMOUS  
 リモート サービスと通信するときに匿名認証を使用するかどうかを指定します。 ANONYMOUS = ON の場合は、匿名認証が使用され、ローカル ユーザーの資格情報はリモート サービスに転送されません。 ANONYMOUS = OFF の場合は、ユーザーの資格情報が転送されます。 この句を指定しない場合、既定値は OFF になります。  
  
## <a name="remarks"></a>Remarks  
 *user_name* に関連付けられている証明の公開キーは、リモート サービスに送信されるメッセージの認証とセッション キーの暗号化に使用されます。その後、暗号化されたセッション キーを使用して、メッセージ交換が暗号化されます。 *user_name* の証明は、リモート サービスをホストするデータベースに格納されているログインの証明と対応している必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 リモート サービス バインドを変更する権限は、既定では、リモート サービス バインドの所有者、**db_owner** 固定データベース ロールのメンバー、**sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
 ALTER REMOTE SERVICE BINDING ステートメントを実行するユーザーは、ステートメントで指定されるユーザーの借用権限が必要です。  
  
 リモート サービス バインドの AUTHORIZATION を変更するには、ALTER AUTHORIZATION ステートメントを使用します。  
  
## <a name="examples"></a>使用例  
 次の例では、リモート サービス バインド `APBinding` を変更し、アカウント `SecurityAccount` からの証明を使用してメッセージを暗号化します。  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
