---
title: REVOKE (エンドポイントの権限の取り消し) (Transact-SQL) | Microsoft Docs
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
- endpoints [SQL Server], permissions
- REVOKE statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 826f513e-9ad0-46b9-87ad-7525713638c8
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: db85df99a2b37e2d92997dce579d77d0f31f7c0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082279"
---
# <a name="revoke-endpoint-permissions-transact-sql"></a>REVOKE (エンドポイントの権限の取り消し) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  エンドポイントに対して許可または拒否された権限を取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ENDPOINT :: endpoint_name  
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 エンドポイントで許可できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 ON ENDPOINT **::** _endpoint_name_  
 権限を許可するエンドポイントを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 { FROM | TO } \<server_principal> 権限を取り消す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_Windows_login*  
 Windows ログインから作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_certificate*  
 証明書にマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_AsymKey*  
 非対称キーにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 GRANT OPTION  
 指定した権限を他のプリンシパルに許可するための権利が、取り消されることを示します。 権限自体は取り消されません。  
  
> [!IMPORTANT]  
>  指定した権限が GRANT オプションなしでプリンシパルに許可されている場合は、その権限自体が取り消されます。  
  
 CASCADE  
 このプリンシパルによって権限が許可または拒否されている他のプリンシパルからも、同じ権限が取り消されることを示します。  
  
> [!CAUTION]  
>  WITH GRANT OPTION で許可されている権限を CASCADE で取り消すと、その権限の GRANT および DENY の両方が取り消されます。  
  
 AS *SQL_Server_login*  
 このクエリを実行するプリンシパルが権限を取り消す権利を取得した、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
## <a name="remarks"></a>Remarks  
 サーバー スコープの権限を取り消すことができるのは、現在のデータベースが **master** のときだけです。  
  
 エンドポイントに関する情報は、[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) カタログ ビューで確認できます。 サーバー権限に関する情報は [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビュー、サーバー プリンシパルに関する情報は [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューでそれぞれ確認できます。  
  
 エンドポイントは、サーバー レベルのセキュリティ保護可能なリソースです。 次の表に、エンドポイントで取り消すことができる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|エンドポイント権限|権限が含まれるエンドポイント権限|権限が含まれるサーバー権限|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 エンドポイントに対する CONTROL 権限、またはサーバーに対する ALTER ANY ENDPOINT 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-revoking-view-definition-permission-on-an-endpoint"></a>A. エンドポイントの VIEW DEFINITION 権限を取り消す  
 次の例では、エンドポイント `Mirror7` での `VIEW DEFINITION` アクセス許可を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `ZArifin` から取り消します。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON ENDPOINT::Mirror7 FROM ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade-option"></a>B. CASCADE オプションを指定して TAKE OWNERSHIP 権限を取り消す  
 次の例では、エンドポイント `Shipping83` での `TAKE OWNERSHIP` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー `PKomosinski` と、`PKomosinski` が `Shipping83` の `TAKE OWNERSHIP` 権限を許可したすべてのプリンシパルから取り消します。  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON ENDPOINT::Shipping83 FROM PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [GRANT (エンドポイントのアクセス許可の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [DENY (エンドポイントの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

