---
title: REVOKE (可用性グループのアクセス許可の取り消し)
description: Always On 可用性グループに対して権限を取り消します。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- REVOKE statement, availability groups
- revoking permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 02c77378-a36d-4286-9235-d8867a2b92ad
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ceb07117a8842faa35d005dba008d15b3810040a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242611"
---
# <a name="revoke-availability-group-permissions-transact-sql"></a>可用性グループの権限の取り消し (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Always On 可用性グループに対する権限を取り消します。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON AVAILABILITY GROUP :: availability_group_name  
    { FROM | TO } < server_principal >  [ ,...n ]  
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
 可用性グループに対して取り消すことができる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 ON AVAILABILITY GROUP **::** _availability_group_name_  
 権限を取り消す可用性グループを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 { FROM | TO } \<server_principal> 取り消される権限の対象となる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
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
  
> [!IMPORTANT]  
>  WITH GRANT OPTION で許可されている権限を CASCADE で取り消すと、その権限の GRANT および DENY の両方が取り消されます。  
  
 AS *SQL_Server_login*  
 このクエリを実行するプリンシパルが権限を取り消す権利を取得した、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
## <a name="remarks"></a>解説  
 サーバー スコープの権限を取り消すことができるのは、現在のデータベースが **master** のときだけです。  
  
 可用性グループに関する情報は、[sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) カタログ ビューで表示できます。 サーバー権限に関する情報は [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビュー、サーバー プリンシパルに関する情報は [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューでそれぞれ確認できます。  
  
 可用性グループは、サーバー レベルでセキュリティ保護可能なリソースです。 次の表に、可用性グループで取り消すことができる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|可用性グループの権限|権限が含まれる可用性グループ権限|権限が含まれるサーバー権限|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 可用性グループに対する CONTROL 権限、またはサーバーに対する ALTER ANY AVAILABILITY GROUP 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-revoking-view-definition-permission-on-an-availability-group"></a>A. 可用性グループの VIEW DEFINITION 権限を取り消す  
 次の例では、可用性グループ `MyAg` での `VIEW DEFINITION` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `ZArifin` に対して取り消します。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade"></a>B. CASCADE を指定して TAKE OWNERSHIP 権限を取り消す  
 次の例では、可用性グループ `MyAg` での `TAKE OWNERSHIP` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー `PKomosinski` から取り消し、`PKomosinski` が MyAg での TAKE OWNERSHIP 権限を許可したすべてのプリンシパルから取り消します。  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
### <a name="c-revoking-a-previously-granted-with-grant-option-clause"></a>C. 以前に許可した WITH GRANT OPTION 句を取り消す  
 WITH GRANT OPTION を使用して権限が許可されていた場合、その WITH GRANT OPTION を取り消すには REVOKE GRANT OPTION FOR を使用します。 次の例では、権限を許可し、その権限の WITH GRANT の部分を取り消します。  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
REVOKE GRANT OPTION FOR CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski  
CASCADE  
GO  
```  
  
## <a name="see-also"></a>参照  
 [GRANT (可用性グループの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [DENY (可用性グループの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

