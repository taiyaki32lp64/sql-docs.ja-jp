---
title: GRANT (可用性グループのアクセス許可の許可)
description: Always On 可用性グループに対する権限を許可します。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0a9954e823ae66017c3a6105f0f0ec27964b7043
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246172"
---
# <a name="grant-availability-group-permissions-transact-sql"></a>可用性グループの権限の許可 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Always On 可用性グループに対する権限を許可します。  
  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 可用性グループに対して許可できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 ON AVAILABILITY GROUP **::** _availability_group_name_  
 権限を許可する可用性グループを指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 TO \<server_principal>  
 権限を許可する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_Windows_login*  
 Windows ログインから作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_certificate*  
 証明書にマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 *SQL_Server_login_from_AsymKey*  
 非対称キーにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前を指定します。  
  
 WITH GRANT OPTION  
 権限が許可されたプリンシパルが、この権限を他のプリンシパルにも許可できることを示します。  
  
 AS *SQL_Server_login*  
 このクエリを実行するプリンシパルが権限を許可する権利を取得した、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。  
  
## <a name="remarks"></a>解説  
 サーバー スコープの権限を許可できるのは、現在のデータベースが **master** のときだけです。  
  
 可用性グループに関する情報は、[sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) カタログ ビューで表示できます。 サーバー権限に関する情報は [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) カタログ ビュー、サーバー プリンシパルに関する情報は [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューでそれぞれ確認できます。  
  
 可用性グループは、サーバー レベルでセキュリティ保護可能なリソースです。 次の表に、可用性グループで許可できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|可用性グループの権限|権限が含まれる可用性グループ権限|権限が含まれるサーバー権限|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 すべての [!INCLUDE[ssDE](../../includes/ssde-md.md)] 権限を示した一覧表については、[データベース エンジンの権限ポスター](https://aka.ms/sql-permissions-poster)に関するページをご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 可用性グループに対する CONTROL 権限、またはサーバーに対する ALTER ANY AVAILABILITY GROUP 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>A. 可用性グループの VIEW DEFINITION 権限を許可する  
 次の例では、可用性グループ `MyAg` での `VIEW DEFINITION` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `ZArifin` に対して許可します。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. GRANT OPTION を指定して TAKE OWNERSHIP 権限を許可する  
 次の例では、可用性グループ `TAKE OWNERSHIP` での `MyAg` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー `PKomosinski` に許可します。ここでは `GRANT OPTION` を使用します。  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. 可用性グループの CONTROL 権限を許可する  
 次の例では、可用性グループ `CONTROL` での `MyAg` 権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー `PKomosinski` に対して許可します。 CONTROL によって、ログインは可用性グループを (その可用性グループの所有者でない場合でも) 完全に制御できます。 所有権の変更については、「[ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)」をご覧ください。  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [REVOKE (可用性グループの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [DENY (可用性グループの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ カタログ ビュー (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [アクセス許可 (データベース エンジン)](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
