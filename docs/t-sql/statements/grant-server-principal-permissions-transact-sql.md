---
title: GRANT (サーバー プリンシパルの権限の許可) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- impersonate [SQL Server], granting
- granting permissions [SQL Server], logins
- permissions [SQL Server], impersonate
- permissions [SQL Server], logins
- GRANT statement, impersonation
- GRANT statement, logins
- logins [SQL Server], granting access
- granting permissions [SQL Server], impersonation
ms.assetid: 4cbed281-5e1e-4d8b-b410-4c18a6cd0205
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 81a8422cbab7eb10d0c74ad5cd758817a665eaa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050777"
---
# <a name="grant-server-principal-permissions-transact-sql"></a>GRANT (サーバー プリンシパルの権限の許可) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに対する権限を許可します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GRANT permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインで許可できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 LOGIN **::** *SQL_Server_login*  
 許可される権限の対象となる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 SERVER ROLE **::** *server_role*  
 権限を許可するユーザー定義のサーバー ロールを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 TO \<server_principal> 権限を許可する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたはサーバー ロールを指定します。  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_Windows_login*  
 Windows ログインから作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_certificate*  
 証明書にマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_AsymKey*  
 非対称キーにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *server_role*  
 ユーザー定義サーバー ロールの名前を指定します。  
  
 WITH GRANT OPTION  
 権限が許可されたプリンシパルが、この権限を他のプリンシパルにも許可できることを示します。  
  
 AS *SQL_Server_login*  
 このクエリを実行するプリンシパルが権限を許可する権利を取得した、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
## <a name="remarks"></a>Remarks  
 サーバー スコープの権限を許可できるのは、現在のデータベースが master のときだけです。  
  
 サーバー権限に関する情報は、[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビューで確認できます。 サーバー プリンシパルに関する情報は、[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューで確認できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインおよびサーバー ロールはサーバー レベルのセキュリティ保護可能なリソースです。 次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたはサーバー ロールで許可できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
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
  
### <a name="a-granting-impersonate-permission-on-a-login"></a>A. ログインの IMPERSONATE 権限を許可する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `WanidaBenshoof` の `IMPERSONATE` 権限を、Windows ユーザー `AdvWorks\YoonM` から作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに許可します。  
  
```  
USE master;  
GRANT IMPERSONATE ON LOGIN::WanidaBenshoof to [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-granting-view-definition-permission-with-grant-option"></a>B. GRANT OPTION を指定して VIEW DEFINITION 権限を許可する  
 次の例では、`GRANT OPTION` を指定して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `EricKurjan` の `VIEW DEFINITION` 権限を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `RMeyyappan` に許可します。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    WITH GRANT OPTION;  
GO   
```  
  
### <a name="c-granting-view-definition-permission-on-a-server-role"></a>C. サーバー ロールの VIEW DEFINITION 権限を許可する  
 次の例では、`Auditors` サーバー ロールに対する `Sales` サーバー ロールの `VIEW DEFINITION` を許可します。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>参照  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

