---
title: DENY (サーバーの権限の拒否) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], servers
- denying permissions [SQL Server], servers
- servers [SQL Server], permissions
- DENY statement, servers
ms.assetid: 68d6b2a9-c36f-465a-9cd2-01d43a667e99
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: de59423c368bc966fab3958fbeb4b04888f4e2a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114776"
---
# <a name="deny-server-permissions-transact-sql"></a>DENY (サーバーの権限の拒否) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  サーバーの権限を拒否します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DENY permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ]  
    [ CASCADE ]  
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
 サーバー上で拒否できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 CASCADE  
 指定したプリンシパル、およびこのプリンシパルによって権限が許可されている他のすべてのプリンシパルに対しても、同じ権限を拒否することを示します。 GRANT OPTION を使用してプリンシパルに権限が与えられている場合に必要となります。 
  
 TO \<server_principal>  
 権限を拒否するプリンシパルを指定します。  
  
 AS \<grantor_principal>  
 このクエリを実行するプリンシパルが権限を拒否する権利を取得した、元のプリンシパルを指定します。
AS <principal> 句は、権限の拒否者として記録されるプリンシパルは、ステートメントを実行しているユーザー以外のプリンシパルでなければならないことを示すために使います。 たとえば、ユーザー Mary の principal_id は 12、ユーザー Raul の principal_id は 15 であるものとします。 Mary が `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` を実行します。ステートメントは実際にはユーザー 13 (Mary) によって実行されましたが、sys.database_permissions テーブルでは、DENY ステートメントの grantor_prinicpal_id は 15 (Raul) であることが示されます。
  
このステートメントで AS を使っても、別のユーザーを偽装できることは意味しません。    
  
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
 サーバー ロールを指定します。  
  
## <a name="remarks"></a>Remarks  
 サーバー スコープの権限を拒否できるのは、現在のデータベースが master のときだけです。  
  
 サーバー権限に関する情報は [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビュー、サーバー プリンシパルに関する情報は [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューでそれぞれ確認できます。 サーバー ロールのメンバーシップに関する情報は、[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) カタログ ビューで確認できます。  
  
 サーバーは権限の階層の最上位となります。 次の表に、サーバー上で拒否できる最も限定的な権限を示します。  
  
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
 CONTROL SERVER 権限またはセキュリティ保護可能なリソースの所有権が必要です。 AS 句を使用する場合、指定されたプリンシパルは、権限が拒否されるセキュリティ保護可能なリソースを所有している必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-denying-connect-sql-permission-to-a-sql-server-login-and-principals-to-which-the-login-has-regranted-it"></a>A. SQL Server ログインと、このログインが権限を許可したプリンシパルに対して CONNECT SQL 権限を拒否する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `CONNECT SQL` と、このログインが権限を許可したプリンシパルに対して、`Annika` 権限を拒否します。  
  
```  
USE master;  
DENY CONNECT SQL TO Annika CASCADE;  
GO  
```  
  
### <a name="b-denying-create-endpoint-permission-to-a-sql-server-login-using-the-as-option"></a>B. AS オプションを使用して、SQL Server ログインに対して CREATE ENDPOINT 権限を拒否する  
 次の例では、ユーザー `CREATE ENDPOINT` に対して `ArifS` 権限を拒否します。 この例では `AS` オプションを使って、このステートメントを実行するプリンシパルに権限を許可した、元のプリンシパルとして `MandarP` を指定します。  
  
```  
USE master;  
DENY CREATE ENDPOINT TO ArifS AS MandarP;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [DENY (サーバーの権限の拒否) (Transact-SQL)](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [REVOKE (サーバーの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [権限の階層 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
