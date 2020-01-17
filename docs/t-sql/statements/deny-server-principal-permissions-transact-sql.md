---
title: DENY (サーバー プリンシパルの権限の拒否) (Transact-SQL) | Microsoft Docs
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
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2fc90354abf3c18a5eba7a92b7a5ffa54a84ce3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984502"
---
# <a name="deny-server-principal-permissions-transact-sql"></a>DENY (サーバー プリンシパルの権限の拒否) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに対して許可された権限を拒否します。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインで拒否できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 LOGIN **::** *SQL_Server_login*  
 拒否される権限の対象となる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 SERVER ROLE **::** *server_role*  
 拒否される権限の対象となるサーバー ロールを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 TO \<server_principal>  
 権限を許可する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたはサーバー ロールを指定します。  
  
 TO *SQL_Server_login*  
 権限を拒否する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_Windows_login*  
 Windows ログインから作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_certificate*  
 証明書にマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_AsymKey*  
 非対称キーにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *server_role*  
 サーバー ロールの名前を指定します。  
  
 CASCADE  
 このプリンシパルによって権限が許可されている他のプリンシパルに対しても、同じ権限を拒否することを示します。  
  
 AS *SQL_Server_login*  
 このクエリを実行するプリンシパルが権限を拒否する権利を取得した、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
## <a name="remarks"></a>Remarks  
 サーバー スコープの権限を拒否できるのは、現在のデータベースが master のときだけです。  
  
 サーバー権限に関する情報は、[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビューで確認できます。 サーバー プリンシパルに関する情報は、[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューで確認できます。  
  
 GRANT OPTION で権限が許可されたプリンシパルに対して権限を拒否するときに CASCADE を指定しない場合、DENY ステートメントは失敗します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインおよびサーバー ロールはサーバー レベルのセキュリティ保護可能なリソースです。 次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたはサーバー ロールで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|SQL Server ログインまたはサーバー ロールの権限|権限が含まれる SQL Server ログインまたはサーバー ロールの権限|権限が含まれるサーバー権限|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>アクセス許可  
 ログインの場合、ログインに対する CONTROL 権限、またはサーバーに対する ALTER ANY LOGIN 権限が必要です。  
  
 サーバー ロールの場合、サーバー ロールに対する CONTROL 権限、またはサーバーに対する ALTER ANY SERVER ROLE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. ログインの IMPERSONATE 権限を拒否する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `IMPERSONATE` の `WanidaBenshoof` 権限を、Windows ユーザー `AdvWorks\YoonM` から作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに対して拒否します。  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. CASCADE を指定して VIEW DEFINITION 権限を拒否する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `VIEW DEFINITION` の `EricKurjan` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `RMeyyappan` に対して拒否します。 ここでは `CASCADE` オプションを使用して、`VIEW DEFINITION` がこの権限を許可したプリンシパルに対しても、`EricKurjan` の `RMeyyappan` 権限を拒否することを指定します。  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. サーバー ロールの VIEW DEFINITION 権限を拒否する  
 次の例では、`Sales` サーバー ロールの `VIEW DEFINITION` 権限を、`Auditors` サーバー ロールに対して拒否します。  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>参照  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT (サーバー プリンシパルの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE (サーバー プリンシパルの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
