---
title: DENY (データベース プリンシパルのアクセス許可の拒否)
description: データベース ユーザー、データベース ロール、またはアプリケーション ロールに対する権限を拒否します。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- denying permissions [SQL Server], database roles
- denying permissions [SQL Server], database users
- permissions [SQL Server], database roles
- DENY statement, database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- database permissions [SQL Server], denying
- DENY statement, application roles
- DENY statement, database users
- denying permissions [SQL Server], application roles
- application roles [SQL Server], permissions
ms.assetid: e2429a5d-e9be-4c05-be20-414d1038a63a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a3e9cb1d12dd65b813ae7cc6139a1d48925ab05f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244581"
---
# <a name="deny-database-principal-permissions-transact-sql"></a>DENY (データベース プリンシパルの権限の拒否) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ユーザー、データベース ロール、またはアプリケーション ロールに対して許可された権限を拒否します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DENY permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
    TO <database_principal> [ ,...n ]  
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
 データベース プリンシパルで拒否できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 USER ::*database_user*  
 権限を拒否するユーザーのクラスと名前を指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 ROLE ::*database_role*  
 権限を拒否するロールのクラスと名前を指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 APPLICATION ROLE ::*application_role*  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 権限を拒否するアプリケーション ロールのクラスと名前を指定します。 スコープ修飾子 ( **::** ) が必要です。  
  
 CASCADE  
 このプリンシパルによって権限が許可されている他のプリンシパルに対しても、同じ権限を拒否することを示します。  
  
 AS \<database_principal>  
 このクエリを実行するプリンシパルが権限を取り消す権利を取得した、元のプリンシパルを指定します。  
  
 *Database_user*  
 データベース ユーザーを指定します。  
  
 *Database_role*  
 データベース ロールを指定します。  
  
 *Application_role*  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 アプリケーション ロールを指定します。  
  
 *Database_user_mapped_to_Windows_User*  
 Windows ユーザーにマップされているデータベース ユーザーを指定します。  
  
 *Database_user_mapped_to_Windows_Group*  
 Windows グループにマップされているデータベース ユーザーを指定します。  
  
 *Database_user_mapped_to_certificate*  
  証明書にマップされているデータベース ユーザーを指定します。  
  
 *Database_user_mapped_to_asymmetric_key*  
  非対称キーにマップされているデータベース ユーザーを指定します。  
  
 *Database_user_with_no_login*  
 対応するサーバー レベルのプリンシパルがないデータベース ユーザーを指定します。  
  
## <a name="remarks"></a>解説  
  
## <a name="database-user-permissions"></a>データベース ユーザー権限  
 データベース ユーザーは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、データベース ユーザーで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|データベース ユーザー権限|権限が含まれるデータベース ユーザー権限|権限が含まれるデータベース権限|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>データベース ロール権限  
 データベース ロールは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、データベース ロールで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|データベース ロール権限|権限が含まれるデータベース ロール権限|権限が含まれるデータベース権限|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>アプリケーション ロール権限  
 アプリケーション ロールは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次の表に、アプリケーション ロールで拒否できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|アプリケーション ロール権限|権限が含まれるアプリケーション ロール権限|権限が含まれるデータベース権限|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 指定したプリンシパルに対する CONTROL 権限、または CONTROL 権限を暗黙的に含む上位の権限が必要です。  
  
 db_owner 固定データベース ロールのメンバーなど、データベースに対する CONTROL 権限が許可されているユーザーは、データベース内のセキュリティ保護可能なリソースに対する権限を拒否できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-denying-control-permission-on-a-user-to-another-user"></a>A. ユーザーの CONTROL 権限を別のユーザーに対して拒否する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] ユーザー `CONTROL` の `Wanida` 権限を、ユーザー `RolandX` に対して拒否します。  
  
```  
USE AdventureWorks2012;  
DENY CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-denying-view-definition-permission-on-a-role-to-a-user-to-which-it-was-granted-with-grant-option"></a>B. ロールの VIEW DEFINITION 権限を、GRANT OPTION で権限が許可されたユーザーに対して拒否する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] ロール `VIEW DEFINITION` の `SammamishParking` 権限を、データベース ユーザー `JinghaoLiu` に対して拒否します。 ユーザー `CASCADE` には、GRANT OPTION を指定して VIEW DEFINITION 権限が許可されているため、`JinghaoLiu` オプションを指定します。  
  
```  
USE AdventureWorks2012;  
DENY VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu CASCADE;  
GO  
```  
  
### <a name="c-denying-impersonate-permission-on-a-user-to-an-application-role"></a>C. ユーザーの IMPERSONATE 権限をアプリケーション ロールに対して拒否する  
 次の例では、ユーザー `IMPERSONATE` の `HamithaL` 権限を、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] のアプリケーション ロール `AccountsPayable17` に対して拒否します。  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
```  
USE AdventureWorks2012;  
DENY IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>参照  
 [GRANT (データベース プリンシパルの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)   
 [REVOKE (データベース プリンシパルの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
