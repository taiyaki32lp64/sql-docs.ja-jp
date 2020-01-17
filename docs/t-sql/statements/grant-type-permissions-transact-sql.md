---
title: GRANT (型の権限の許可) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7695fda9dd287239f4ef88ea5c279e11a0b5abdd
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982500"
---
# <a name="grant-type-permissions-transact-sql"></a>GRANT (型の権限の許可) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  型に対する権限を許可します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GRANT permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
    TO <database_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 型で許可できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 ON TYPE **::** [ _schema_name_ **.** ] *type_name*  
 権限を許可する型を指定します。 スコープ修飾子 ( **::** ) が必要です。 *schema_name* が指定されていない場合、既定のスキーマが使用されます。 *schema_name* が指定されている場合、スキーマのスコープ修飾子 ( **.** ) が必要です。  
  
 TO \<database_principal> 権限を許可するプリンシパルを指定します。  
  
 WITH GRANT OPTION  
 権限が許可されたプリンシパルが、この権限を他のプリンシパルにも許可できることを示します。  
  
 AS \<database_principal> このクエリを実行するプリンシパルが権限を許可する権利の派生元のプリンシパルを指定します。  
  
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
  
## <a name="remarks"></a>Remarks  
 型は、スキーマ レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているスキーマに含まれています。  
  
> [!IMPORTANT]  
>  **GRANT**、**DENY,** 、**REVOKE** の各権限は、システム型には適用されません。 ユーザー定義型には権限を許可できます。 ユーザー定義型について詳しくは、「[SQL Server でのユーザー定義型の使用](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)」をご覧ください。  
  
 次の表に、型で許可できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|型権限|権限が含まれる型権限|権限が含まれるスキーマ権限|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|EXECUTE|CONTROL|EXECUTE|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 権限の許可者 (または AS オプションで指定されたプリンシパル) は、GRANT OPTION によって与えられた権限を保持しているか、権限が暗黙的に与えられる上位の権限を保持している必要があります。  
  
 AS オプションを使用している場合は、次の追加要件があります。  
  
|AS|必要な追加権限|  
|--------|------------------------------------|  
|データベース ユーザー|ユーザーに対する IMPERSONATE 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|Windows ログインにマップされているデータベース ユーザー|ユーザーに対する IMPERSONATE 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|Windows グループにマップされているデータベース ユーザー|Windows グループのメンバーシップ、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|証明書にマップされているデータベース ユーザー|**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|非対称キーにマップされているデータベース ユーザー|**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|サーバー プリンシパルにマップされていないデータベース ユーザー|ユーザーに対する IMPERSONATE 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|データベース ロール|ロールに対する ALTER 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|アプリケーション ロール|ロールに対する ALTER 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
  
## <a name="examples"></a>使用例  
 次の例では、ユーザー `VIEW DEFINITION` に対し、ユーザー定義型 `GRANT OPTION` の `PhoneNumber` 権限を、`KhalidR` を指定して許可します。 `PhoneNumber` はスキーマ `Telemarketing` にあります。  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DENY (型の権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [REVOKE (型の権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

