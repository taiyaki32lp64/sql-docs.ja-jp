---
title: ALTER SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2307a80d3a40599aed4762077b188baac0533967
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070271"
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

サーバー ロールのメンバーシップを変更、またはユーザー定義のサーバー ロールの名前を変更します。 固定サーバー ロールの名前は変更できません。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>引数  
*server_role_name*  
変更するサーバー ロールの名前を指定します。  
  
ADD MEMBER *server_principal*  
指定されたサーバー プリンシパルをサーバー ロールに追加します。 *server_principal* には、ログインまたはユーザー定義サーバー ロールを指定できます。 *server_principal* に、固定サーバー ロール、データベース ロール、または sa を指定することはできません。  
  
DROP MEMBER *server_principal*  
指定されたサーバー プリンシパルをサーバー ロールから削除します。 *server_principal* には、ログインまたはユーザー定義サーバー ロールを指定できます。 *server_principal* に、固定サーバー ロール、データベース ロール、または sa を指定することはできません。  
  
WITH NAME **=** _new_server_role_name_  
ユーザー定義サーバー ロールの新しい名前を指定します。 サーバー内に存在しない名前を指定してください。  
  
## <a name="remarks"></a>Remarks  
ユーザー定義サーバー ロールの名前を変更しても、ロールの ID 番号、所有者、権限は変わりません。  
  
ロールのメンバーシップの変更では、`ALTER SERVER ROLE` は sp_addsrvrolemember と sp_dropsrvrolemember を置き換えます。 これらのストアド プロシージャは非推奨です。  
  
サーバー ロールを確認するには、`sys.server_role_members` カタログ ビューおよび `sys.server_principals` カタログ ビューに対してクエリを実行します。  
  
ユーザー定義サーバー ロールの所有者を変更するには、[ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md) を使います。  
  
## <a name="permissions"></a>アクセス許可  
ユーザー定義サーバー ロールの名前を変更するには、サーバーに対する `ALTER ANY SERVER ROLE` 権限が必要です。  
  
**固定サーバー ロール**  
  
固定サーバー ロールにメンバーを追加するには、その固定サーバー ロールのメンバーであるか、`sysadmin` 固定サーバー ロールのメンバーである必要があります。  
  
> [!NOTE]  
>  `CONTROL SERVER` 権限と `ALTER ANY SERVER ROLE` 権限では、固定サーバー ロールに対して `ALTER SERVER ROLE` を実行することはできません。また、`ALTER` 権限は固定サーバー ロールに対して許可できません。  
  
**ユーザー定義サーバー ロール**  
  
ユーザー定義サーバー ロールにメンバーを追加するには、`sysadmin` 固定サーバー ロールのメンバーであるか、`CONTROL SERVER` または `ALTER ANY SERVER ROLE` 権限を持っている必要があります。 または、そのロールに対する `ALTER` 権限を持っている必要があります。  
  
> [!NOTE]  
>  固定サーバー ロールとは異なり、ユーザー定義サーバー ロールのメンバーには、同じロールにメンバーを追加する権限がもともとありません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-name-of-a-server-role"></a>A. サーバー ロールの名前を変更する  
次の例では、`Product` という名前のサーバー ロールを作成し、そのサーバー ロールの名前を `Production` に変更します。  
  
```  
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>B. ドメイン アカウントをサーバー ロールに追加する  
次の例では、`adventure-works\roberto0` という名前のドメイン アカウントを `Production` という名前のユーザー定義サーバー ロールに追加します。  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>C. SQL Server ログインをサーバー ロールに追加する  
次の例では、`Ted` という名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを `diskadmin` 固定サーバー ロールに追加します。  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>D. サーバー ロールからドメイン アカウントを削除する  
次の例では、`Production` という名前のユーザー定義サーバー ロールから `adventure-works\roberto0` という名前のドメイン アカウントを削除します。  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>E. サーバー ロールから SQL Server ログインを削除する  
次の例では、`diskadmin` 固定サーバー ロールから `Ted` という名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを削除します。  
  
```  
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>F. ログインをユーザー定義サーバー ロールに追加する権限をログインに許可する  
次の例では、`Ted` が他のログインを `Production` という名前のユーザー定義サーバー ロールに追加できるようにします。  
  
```  
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>G. ロールのメンバーシップを表示するには  
ロールのメンバーシップを表示するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[サーバー ロール (メンバー)]** ページを使用するか、次のクエリを実行します。  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>H. 基本構文  
次の例では、ログイン `Anna` をサーバー ロール `LargeRC` に追加します。  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>I. リソース クラスからログインを削除する。  
次の例では、サーバー ロール `LargeRC` から Anna のメンバーシップを削除します。  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>参照  
[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
