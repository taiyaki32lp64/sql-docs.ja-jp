---
title: GRANT (サーバーの権限の許可) (Transact-SQL) | Microsoft Docs
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
- GRANT statement, servers
- permissions [SQL Server], servers
- servers [SQL Server], permissions
- granting permissions [SQL Server], servers
ms.assetid: 7e880a5a-3bdc-491f-a167-7a9ed338be7f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5eeda80431c403fd1178399b4c2c3500154acd48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050793"
---
# <a name="grant-server-permissions-transact-sql"></a>GRANT (サーバーの権限の許可) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバーに対する権限を許可します。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GRANT permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ] [ WITH GRANT OPTION ]  
    [ AS <grantor_principal> ]  
  
<grantee_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
  
<grantor_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 サーバーで許可できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 TO \<grantee_principal> 権限を許可するプリンシパルを指定します。  
  
 AS \<grantor_principal> このクエリを実行するプリンシパルが権限を許可する権利の派生元のプリンシパルを指定します。  
  
 WITH GRANT OPTION  
 権限が許可されたプリンシパルが、この権限を他のプリンシパルにも許可できることを示します。  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login_mapped_to_Windows_login*  
 Windows ログインにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login_mapped_to_Windows_group*  
 Windows グループにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login_mapped_to_certificate*  
 証明書にマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login_mapped_to_asymmetric_key*  
 非対称キーにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *server_role*  
 ユーザー定義サーバー ロールを指定します。  
  
## <a name="remarks"></a>Remarks  
 サーバー スコープの権限を許可できるのは、現在のデータベースが master のときだけです。  
  
 サーバー権限に関する情報は [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビュー、サーバー プリンシパルに関する情報は [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューでそれぞれ確認できます。 サーバー ロールのメンバーシップに関する情報は、[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) カタログ ビューで確認できます。  
  
 サーバーは権限の階層の最上位となります。 次の表に、サーバーで許可できる最も限定的な権限を示します。  
  
|サーバー権限|権限が含まれるサーバー権限|  
|-----------------------|----------------------------------|  
|ADMINISTER BULK OPERATIONS|CONTROL SERVER|  
|ALTER ANY AVAILABILITY GROUP<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|CONTROL SERVER|  
|ALTER ANY CONNECTION|CONTROL SERVER|  
|ALTER ANY CREDENTIAL|CONTROL SERVER|  
|ALTER ANY DATABASE|CONTROL SERVER|  
|ALTER ANY ENDPOINT|CONTROL SERVER|  
|ALTER ANY EVENT NOTIFICATION|CONTROL SERVER|  
|ALTER ANY EVENT SESSION|CONTROL SERVER|  
|ALTER ANY LINKED SERVER|CONTROL SERVER|  
|ALTER ANY LOGIN|CONTROL SERVER|  
|ALTER ANY SERVER AUDIT|CONTROL SERVER|  
|ALTER ANY SERVER ROLE<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|CONTROL SERVER|  
|ALTER RESOURCES|CONTROL SERVER|  
|ALTER SERVER STATE|CONTROL SERVER|  
|ALTER SETTINGS|CONTROL SERVER|  
|ALTER TRACE|CONTROL SERVER|  
|AUTHENTICATE SERVER|CONTROL SERVER|  
|CONNECT ANY DATABASE<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|CONTROL SERVER|  
|CONNECT SQL|CONTROL SERVER|  
|CONTROL SERVER|CONTROL SERVER|  
|CREATE ANY DATABASE|ALTER ANY DATABASE|  
|CREATE AVAILABILITY GROUP<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|ALTER ANY AVAILABILITY GROUP|  
|CREATE DDL EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|CREATE ENDPOINT|ALTER ANY ENDPOINT|  
|CREATE SERVER ROLE<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|ALTER ANY SERVER ROLE|  
|CREATE TRACE EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|EXTERNAL ACCESS ASSEMBLY|CONTROL SERVER|  
|IMPERSONATE ANY LOGIN<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|CONTROL SERVER|  
|SELECT ALL USER SECURABLES<br /><br /> **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。|CONTROL SERVER|  
|SHUTDOWN|CONTROL SERVER|  
|UNSAFE ASSEMBLY|CONTROL SERVER|  
|VIEW ANY DATABASE|VIEW ANY DEFINITION|  
|VIEW ANY DEFINITION|CONTROL SERVER|  
|VIEW SERVER STATE|ALTER SERVER STATE|  
  
## <a name="remarks"></a>Remarks  
 次の 3 つのサーバー権限が、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] で追加されました。  
  
 **CONNECT ANY DATABASE** 権限  
 既存のあらゆるデータベースと今後作成されるすべての新規データベースに接続する必要のあるログインに、**CONNECT ANY DATABASE** を付与します。 接続以外の権限はどのデータベースにおいても一切付与されません。 **SELECT ALL USER SECURABLES** または **VIEW SERVER STATE** と組み合わせることによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス上ですべてのデータやデータベースの状態を確認する監査プロセスが可能になります。  
  
 **IMPERSONATE ANY LOGIN** 権限  
 この権限が付与されていると、中間層プロセスがデータベースに接続するときに、そこに接続するクライアントのアカウントの権限を借用できます。 この権限が拒否されていると、高い特権を持つログインが他のログインの権限を借用するのをブロックできます。 たとえば、**CONTROL SERVER** 権限を持つログインが他のログインの権限を借用するのをブロックできます。  
  
 **SELECT ALL USER SECURABLES** 権限  
 付与されていると、監査担当者などログインが、ユーザーが接続できるすべてのデータベースのデータを表示できます。 この権限が拒否されていると、オブジェクトが **sys** スキーマに含まれている場合を除き、オブジェクトへのアクセスが拒否されます。  
  
## <a name="permissions"></a>アクセス許可  
 権限の許可者 (または AS オプションで指定されたプリンシパル) は、GRANT OPTION によって与えられた権限を保持しているか、権限が暗黙的に与えられる上位の権限を保持している必要があります。 sysadmin 固定サーバー ロールのメンバーは、すべての権限を許可できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-granting-a-permission-to-a-login"></a>A. ログインに権限を許可する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `TerryEminhizer` に `CONTROL SERVER` 権限を許可します。  
  
```  
USE master;  
GRANT CONTROL SERVER TO TerryEminhizer;  
GO  
```  
  
### <a name="b-granting-a-permission-that-has-grant-permission"></a>B. GRANT 権限に関する権限を許可する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `JanethEsteves` に、`ALTER ANY EVENT NOTIFICATION` 権限を許可し、この権限を他のログインに許可する権利を与えます。  
  
```  
USE master;  
GRANT ALTER ANY EVENT NOTIFICATION TO JanethEsteves WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-a-permission-to-a-server-role"></a>C. サーバー ロールに権限を許可する  
 次の例では、`ITDevAdmin` および `ITDevelopers` という名前の 2 つのサーバー ロールを作成します。 ここでは、`ALTER ANY DATABASE` オプションを含めて、`ITDevAdmin` 権限を `WITH GRANT` ユーザー定義サーバー ロールに許可します。これにより、`ITDevAdmin` サーバー ロールは、`ALTER ANY DATABASE` 権限を再割り当てすることができます。 次に、`ITDevelopers` サーバー ロールの `ALTER ANY DATABASE` 権限を使用する権限を `ITDevAdmin` に許可します。  
  
```  
USE master;  
CREATE SERVER ROLE ITDevAdmin ;  
CREATE SERVER ROLE ITDevelopers ;  
GRANT ALTER ANY DATABASE TO ITDevAdmin WITH GRANT OPTION ;  
GRANT ALTER ANY DATABASE TO ITDevelopers AS ITDevAdmin ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [DENY (サーバーの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [REVOKE (サーバーの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [権限の階層 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

