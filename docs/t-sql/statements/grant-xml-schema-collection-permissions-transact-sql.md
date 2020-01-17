---
title: GRANT (XML スキーマ コレクションのアクセス許可の許可)
description: XML スキーマ コレクションに対する権限を許可します。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- GRANT statement, XML schema collections
- XML schema collections [SQL Server], permissions
- granting permissions [SQL Server], XML schema collections
- schema collections [SQL Server], permissions
ms.assetid: 57e24465-cd43-45cf-bb52-eea0b49867f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5d79f02237a380a9431e8269875d93a79bd9d04
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243347"
---
# <a name="grant-xml-schema-collection-permissions-transact-sql"></a>GRANT (XML スキーマ コレクションの権限の許可) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML スキーマ コレクションに対する権限を許可します。   
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GRANT permission  [ ,...n ] ON   
    XML SCHEMA COLLECTION :: [ schema_name . ]  
    XML_schema_collection_name  
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
 XML スキーマ コレクションで許可できる権限を指定します。 権限の一覧については、後の「解説」を参照してください。  
  
 ON XML SCHEMA COLLECTION :: [ *schema_name*. ] *XML_schema_collection_name*  
 権限を許可する XML スキーマ コレクションを指定します。 スコープ修飾子 (::) が必要です。 *schema_name* が指定されていない場合、既定のスキーマが使用されます。 *schema_name* が指定されている場合、スキーマのスコープ修飾子 (.) が必要です。  
  
 \<database_principal> 、権限を許可するプリンシパルを指定します。  
  
 WITH GRANT OPTION  
 権限が許可されたプリンシパルが、この権限を他のプリンシパルにも許可できることを示します。  
  
 AS \<database_principal> このクエリを実行するプリンシパルが権限を許可する権利の派生元のプリンシパルを指定します。  
  
 *Database_user*  
 データベース ユーザーを指定します。  
  
 *Database_role*  
 データベース ロールを指定します。  
  
 *Application_role*  
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
 XML スキーマ コレクションに関する情報は、[sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) カタログ ビューで確認できます。  
  
 XML スキーマ コレクションは、スキーマ レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているスキーマに含まれています。 次の表に、XML スキーマ コレクションで許可できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|XML スキーマ コレクション権限|権限が含まれる XML スキーマ コレクション権限|権限が含まれるスキーマ権限|  
|--------------------------------------|-------------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
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
|データベース ユーザー|ユーザーに対する IMPERSONATE 権限、db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|Windows ログインにマップされているデータベース ユーザー|ユーザーに対する IMPERSONATE 権限、db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|Windows グループにマップされているデータベース ユーザー|Windows グループのメンバーシップ、db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|証明書にマップされているデータベース ユーザー|db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|非対称キーにマップされているデータベース ユーザー|db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|サーバー プリンシパルにマップされていないデータベース ユーザー|ユーザーに対する IMPERSONATE 権限、db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|データベース ロール|ロールに対する ALTER 権限、db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
|アプリケーション ロール|ロールに対する ALTER 権限、db_securityadmin 固定データベース ロールのメンバーシップ、db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップ。|  
  
## <a name="examples"></a>例  
 次の例では、XML スキーマ コレクション `EXECUTE` の `Invoices4` 権限をユーザー `Wanida` に許可します。 XML スキーマ コレクション `Invoices4` は、`AdventureWorks2012` データベースの `Sales` スキーマ内にあります。  
  
 ```
 USE AdventureWorks2012;  
 GRANT EXECUTE ON XML SCHEMA COLLECTION::Sales.Invoices4 TO Wanida;  
 GO
 ```  
  
## <a name="see-also"></a>参照  
 [DENY (XML スキーマ コレクションの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)   
 [REVOKE (XML スキーマ コレクションの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)   
 [sys.xml_schema_collections &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)   
 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

