---
title: REVOKE (データベース プリンシパルのアクセス許可の取り消し)
description: データベース ユーザー、データベース ロール、またはアプリケーション ロールに対する権限を取り消します。
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
- database roles [SQL Server], permissions
- REVOKE statement, roles
- database user permissions [SQL Server]
- REVOKE statement, users
- application roles [SQL Server], permissions
ms.assetid: c45e1086-c25b-48bb-a764-4a893e983db2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0353ff7b9e0778a7ef59107f5ba2876e72bbdd69
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243339"
---
# <a name="revoke-database-principal-permissions-transact-sql"></a>REVOKE (データベース プリンシパルの権限の取り消し) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベース ユーザー、データベース ロール、アプリケーション ロールに対して許可または拒否された権限を取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
       | [ ROLE :: database_role ]  
       | [ APPLICATION ROLE :: application_role ]  
    }  
    { FROM | TO } <database_principal> [ ,...n ]  
        [ CASCADE ]  
    [ AS <database_principal> ]  
  
<database_principal> ::=  
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 データベース プリンシパルで取り消すことのできる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 USER ::*database_user*  
 権限を取り消すユーザーのクラスと名前を指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 ROLE ::*database_role*  
 権限を取り消すロールのクラスと名前を指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 APPLICATION ROLE ::*application_role*  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 権限を取り消すアプリケーション ロールのクラスと名前を指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 GRANT OPTION  
 指定した権限を他のプリンシパルに許可するための権利が、取り消されることを示します。 権限自体は取り消されません。  
  
> [!IMPORTANT]  
>  指定した権限が GRANT オプションなしでプリンシパルに許可されている場合は、その権限自体が取り消されます。  
  
 CASCADE  
 このプリンシパルによって権限が許可または拒否されている他のプリンシパルからも、同じ権限が取り消されることを示します。  
  
> [!CAUTION]  
>  WITH GRANT OPTION で許可されている権限を CASCADE で取り消すと、その権限の GRANT および DENY の両方が取り消されます。  
  
 AS \<database_principal> このクエリを実行するプリンシパルが権限を取り消すには、その権限を派生元のプリンシパルを指定します。  
  
 *Database_user*  
 データベース ユーザーを指定します。  
  
 *Database_role*  
 データベース ロールを指定します。  
  
 *Application_role*  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 アプリケーション ロールを指定します。  
  
 *Database_user_mapped_to_Windows_User*  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
 Windows ユーザーにマップされているデータベース ユーザーを指定します。  
  
 *Database_user_mapped_to_Windows_Group*  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
 Windows グループにマップされているデータベース ユーザーを指定します。  
  
 *Database_user_mapped_to_certificate*  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
 証明書にマップされているデータベース ユーザーを指定します。  
  
 *Database_user_mapped_to_asymmetric_key*  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
 非対称キーにマップされているデータベース ユーザーを指定します。  
  
 *Database_user_with_no_login*  
 対応するサーバー レベルのプリンシパルがないデータベース ユーザーを指定します。  
  
## <a name="remarks"></a>解説  
  
## <a name="database-user-permissions"></a>データベース ユーザー権限  
 データベース ユーザーは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、データベース ユーザーで取り消すことができる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|データベース ユーザー権限|権限が含まれるデータベース ユーザー権限|権限が含まれるデータベース権限|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>データベース ロール権限  
 データベース ロールは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、データベース ロールで取り消すことができる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|データベース ロール権限|権限が含まれるデータベース ロール権限|権限が含まれるデータベース権限|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>アプリケーション ロール権限  
 アプリケーション ロールは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、アプリケーション ロールで取り消すことのできる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|アプリケーション ロール権限|権限が含まれるアプリケーション ロール権限|権限が含まれるデータベース権限|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 指定したプリンシパルに対する CONTROL 権限、または CONTROL 権限を暗黙的に含む上位の権限が必要です。  
  
 **db_owner** 固定データベース ロールのメンバーなど、データベースに対する CONTROL 権限が許可されているユーザーは、データベース内のセキュリティ保護可能なリソースに対する権限を許可できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-revoking-control-permission-on-a-user-from-another-user"></a>A. ユーザーに対する CONTROL 権限を別のユーザーから取り消す  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ユーザー `Wanida` に対する `CONTROL` 権限を、ユーザー `RolandX` から取り消します。  
  
```  
USE AdventureWorks2012;  
REVOKE CONTROL ON USER::Wanida FROM RolandX;  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-on-a-role-from-a-user-to-which-it-was-granted-with-grant-option"></a>B. ロールに対する VIEW DEFINITION 権限を、WITH GRANT OPTION で権限が許可されたユーザーから取り消す  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ロール `VIEW DEFINITION` に対する `SammamishParking` 権限を、データベース ユーザー `JinghaoLiu` から取り消します。 ユーザー `JinghaoLiu` には、`WITH GRANT OPTION` を指定して `VIEW DEFINITION` 権限が許可されているため、`CASCADE` オプションを指定します。  
  
```  
USE AdventureWorks2012;  
REVOKE VIEW DEFINITION ON ROLE::SammamishParking   
    FROM JinghaoLiu CASCADE;  
GO  
```  
  
### <a name="c-revoking-impersonate-permission-on-a-user-from-an-application-role"></a>C. ユーザーに対する IMPERSONATE 権限をアプリケーション ロールから取り消す  
 次の例では、ユーザー `HamithaL` に対する `IMPERSONATE` 権限を、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] アプリケーション ロール `AccountsPayable17` から取り消します。  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
```  
USE AdventureWorks2012;  
REVOKE IMPERSONATE ON USER::HamithaL FROM AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>参照  
 [GRANT (データベース プリンシパルの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)   
 [DENY (データベース プリンシパルの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

