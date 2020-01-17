---
title: REVOKE (型の権限の取り消し) (Transact-SQL) | Microsoft Docs
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
- REVOKE statement, types
- permissions [SQL Server], types
- type permissions [SQL Server]
ms.assetid: 3969c7e9-ca10-4c67-971b-25d2dfccf650
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 29bf592fcc169f112eb938af19077aa59621b843
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982901"
---
# <a name="revoke-type-permissions-transact-sql"></a>REVOKE (型の権限の取り消し) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  型に対する権限を取り消します。  
  
  ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON TYPE :: [ schema_name ]. type_name   
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
 型で取り消すことができる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 ON TYPE **::** [ *schema_name* ] **.** *type_name*  
 権限を取り消す型を指定します。 スコープ修飾子 ( **::** ) が必要です。 *schema_name* が指定されていない場合、既定のスキーマが使用されます。 *schema_name* が指定されている場合、スキーマのスコープ修飾子 ( **.** ) が必要です。  
  
 { FROM | TO } \<database_principal> 権限を取り消すプリンシパルを指定します。  
  
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
  
## <a name="remarks"></a>Remarks  
 型は、スキーマ レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているスキーマに含まれています。  
  
> [!IMPORTANT]  
>  **GRANT**、**DENY,** 、**REVOKE** の各権限は、システム型には適用されません。 ユーザー定義型には権限を許可できます。 ユーザー定義型について詳しくは、「[SQL Server でのユーザー定義型の使用](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)」をご覧ください。  
  
 次の表に、型で取り消すことができる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|型権限|権限が含まれる型権限|権限が含まれるスキーマ権限|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|EXECUTE|CONTROL|EXECUTE|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 型に対する CONTROL 権限が必要です。 AS 句を使用する場合は、指定したプリンシパルが型を所有している必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、ユーザー定義型 `PhoneNumber` に対する `VIEW DEFINITION` 権限を、ユーザー `KhalidR` から取り消します。 `CASCADE` オプションは、`KhalidR` が `VIEW DEFINITION` 権限を許可したプリンシパルからも権限を取り消すことを示します。 `PhoneNumber` はスキーマ `Telemarketing` にあります。  
  
```  
REVOKE VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    FROM KhalidR CASCADE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [GRANT (型の権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)   
 [DENY (型の権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [セキュリティ保護可能](../../relational-databases/security/securables.md)  
  
  

