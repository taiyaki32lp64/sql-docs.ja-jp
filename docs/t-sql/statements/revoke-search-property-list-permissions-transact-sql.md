---
title: REVOKE (検索プロパティ リスト アクセス許可の取り消し)
description: 検索プロパティ リストに対する権限を取り消します。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], permissions
- search property lists [SQL Server], permissions
- revoking permissions [SQL Server]
- REVOKE statement, search property list permissions
ms.assetid: a6b8b37c-0015-4596-898c-51a567659e2e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 84d15026a188bd24522195d22e70707a8803fda8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255803"
---
# <a name="revoke-search-property-list-permissions-transact-sql"></a>REVOKE (検索プロパティ リスト権限の取り消し) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  検索プロパティ リストに対する権限を取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
        SEARCH PROPERTY LIST :: search_property_list_name  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>引数  
 GRANT OPTION FOR  
 指定した権限を他のプリンシパルに許可するための権利が、取り消されることを示します。 権限自体は取り消されません。  
  
> [!IMPORTANT]  
>  指定した権限が GRANT オプションなしでプリンシパルに許可されている場合は、その権限自体が取り消されます。  
  
 *permission*  
 権限の名前を指定します。 権限とセキュリティ保護可能なリソースの有効な組み合わせについては、後の「解説」を参照してください。  
  
 ON SEARCH PROPERTY LIST **::** _search_property_list_name_  
 権限を取り消す検索プロパティ リストを指定します。 スコープ修飾子 **::** が必要です。  
  
 *database_principal*  
 権限を取り消すプリンシパルを指定します。 プリンシパルには、次のいずれかを指定することができます。  
  
-   データベース ユーザー  
  
-   データベース ロール (database role)  
  
-   アプリケーション ロール (application role)  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
 CASCADE  
 このプリンシパルによって権限が許可されている他のプリンシパルからも、同じ権限が取り消されることを示します。  
  
> [!CAUTION]  
>  WITH GRANT OPTION で許可されている権限を CASCADE で取り消すと、その権限の GRANT および DENY の両方が取り消されます。  
  
 AS *revoking_principal*  
 このクエリを実行するプリンシパルが権限を取り消す権利を取得した、元のプリンシパルを指定します。 プリンシパルには、次のいずれかを指定することができます。  
  
-   データベース ユーザー  
  
-   データベース ロール (database role)  
  
-   アプリケーション ロール (application role)  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>解説  
  
## <a name="search-property-list-permissions"></a>SEARCH PROPERTY LIST 権限  
 検索プロパティ リストは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 以下に、検索プロパティ リストで取り消すことのできる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|検索プロパティ リスト権限|権限が含まれる検索プロパティ リスト権限|権限が含まれるデータベース権限|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 フルテキスト カタログに対する CONTROL 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DENY (検索プロパティ リスト権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT (検索プロパティ リスト権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
