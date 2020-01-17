---
title: DENY (Service Broker の権限の拒否) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [Service Broker]
- routes [Service Broker], permissions
- Service Broker, permissions
- DENY statement, Service Broker
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- denying permissions [SQL Server], Service Broker
- contracts [Service Broker], permissions
- services [Service Broker], permissions
ms.assetid: 7c6de71b-865c-41db-9413-ad9b3562e579
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 346044530087c40c468abe9d304231ce06220845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984424"
---
# <a name="deny-service-broker-permissions-transact-sql"></a>DENY (Service Broker の権限の拒否) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSB](../../includes/sssb-md.md)] コントラクト、メッセージ型、リモート サービス バインド、ルート、またはサービスに対する権限を拒否します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DENY permission  [ ,...n ] ON  
    {    
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 セキュリティ保護可能な [!INCLUDE[ssSB](../../includes/sssb-md.md)] に対して拒否できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 CONTRACT **::** _contract_name_  
 権限を拒否するコントラクトを指定します。 スコープ修飾子 **::** が必要です。  
  
 MESSAGE TYPE **::** _message_type_name_  
 権限を拒否するメッセージ型を指定します。 スコープ修飾子 **::** が必要です。  
  
 REMOTE SERVICE BINDING **::** _remote_binding_name_  
 権限を拒否するリモート サービス バインドを指定します。 スコープ修飾子 **::** が必要です。  
  
 ROUTE **::** _route_name_  
 権限を拒否するルートを指定します。 スコープ修飾子 **::** が必要です。  
  
 SERVICE **::** _message_type_name_  
 権限を拒否するサービスを指定します。 スコープ修飾子 **::** が必要です。  
  
 *database_principal*  
 権限を拒否するプリンシパルを指定します。 次のいずれかです。  
  
-   データベース ユーザー  
-   データベース ロール  
-   アプリケーション ロール  
-   Windows ログインにマップされているデータベース ユーザー  
-   Windows グループにマップされているデータベース ユーザー  
-   証明書にマップされているデータベース ユーザー  
-   非対称キーにマップされているデータベース ユーザー  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
CASCADE  
 このプリンシパルによって権限が許可されている他のプリンシパルに対しても、同じ権限を拒否することを示します。  
  
*denying_principal*  
 このクエリを実行するプリンシパルが権限を拒否する権利を取得した、元のプリンシパルを指定します。 次のいずれかです。  
  
-   データベース ユーザー  
-   データベース ロール  
-   アプリケーション ロール  
-   Windows ログインにマップされているデータベース ユーザー  
-   Windows グループにマップされているデータベース ユーザー  
-   証明書にマップされているデータベース ユーザー  
-   非対称キーにマップされているデータベース ユーザー  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>Remarks  
  
## <a name="service-broker-contracts"></a>Service Broker コントラクト  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] コントラクトは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、[!INCLUDE[ssSB](../../includes/sssb-md.md)] コントラクトで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|Service Broker コントラクト権限|権限が含まれる Service Broker コントラクト権限|権限が含まれるデータベース権限|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker メッセージ型  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ型は、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、[!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ型で拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|Service Broker メッセージ型権限|権限が含まれる Service Broker メッセージ型権限|権限が含まれるデータベース権限|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker リモート サービス バインド  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] リモート サービス バインドは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、[!INCLUDE[ssSB](../../includes/sssb-md.md)] リモート サービス バインドで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|Service Broker リモート サービス バインド権限|権限が含まれる Service Broker リモート サービス バインド権限|権限が含まれるデータベース権限|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker ルート  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ルートは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、[!INCLUDE[ssSB](../../includes/sssb-md.md)] ルートで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|Service Broker ルート権限|権限が含まれる Service Broker ルート権限|権限が含まれるデータベース権限|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker サービス  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、[!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|Service Broker サービス権限|権限が含まれる Service Broker サービス権限|権限が含まれるデータベース権限|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] コントラクト、メッセージ型、リモート サービス バインド、ルート、またはサービスに対する CONTROL 権限が必要です。 AS 句を使用する場合、指定されるプリンシパルは、権限の拒否対象となるセキュリティ保護可能なリソースを所有している必要があります。  
  
## <a name="see-also"></a>参照  
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE (Service Broker の権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)  
  
  
