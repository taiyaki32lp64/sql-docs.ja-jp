---
title: GRANT (データベース スコープの資格情報の許可) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- GRANT DATABASE SCOPED CREDENTIAL
- GRANT_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], database scoped credential
- permissions [SQL Server], database scoped credential
- database scoped credential [SQL Server], permissions
- GRANT statement, database scoped credentials
ms.assetid: 501f2c8a-6aeb-41af-bf0b-974d17af33c0
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3d820e8740740335a576385a7c971d1e0fe5eb5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942947"
---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>GRANT (データベース スコープの資格情報の権限の許可) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  データベース スコープの資格情報に対する権限を許可します。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>引数  
 *permission*  
 データベース スコープの資格情報で許可できる権限を指定します。 以下に一覧を示します。  
  
 ON DATABASE SCOPED CREDENTIAL **::** _credential_name_  
 権限を許可するデータベース スコープの資格情報を指定します。 スコープ修飾子 "::" が必要です。  
  
 *database_principal*  
 権限を許可するプリンシパルを指定します。 次のいずれかです。  
  
-   データベース ユーザー  
-   データベース ロール (database role)  
-   アプリケーション ロール (application role)  
-   Windows ログインにマップされているデータベース ユーザー  
-   Windows グループにマップされているデータベース ユーザー  
-   証明書にマップされているデータベース ユーザー  
-   非対称キーにマップされているデータベース ユーザー  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
GRANT OPTION  
 権限が許可されたプリンシパルが、この権限を他のプリンシパルにも許可できることを示します。  
  
AS *granting_principal*  
 このクエリを実行するプリンシパルが権限を許可する権利を取得した、元のプリンシパルを指定します。 次のいずれかです。  
  
-   データベース ユーザー  
-   データベース ロール (database role)  
-   アプリケーション ロール (application role)  
-   Windows ログインにマップされているデータベース ユーザー  
-   Windows グループにマップされているデータベース ユーザー  
-   証明書にマップされているデータベース ユーザー  
-   非対称キーにマップされているデータベース ユーザー  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>Remarks  
 データベース スコープの資格情報は、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次に、データベース スコープの資格情報で許可できる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に一覧で示します。  
  
|データベース スコープの資格情報の権限|権限が含まれるデータベース スコープの資格情報の権限|権限が含まれるデータベース権限|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 権限の許可者 (または AS オプションで指定されたプリンシパル) は、GRANT OPTION によって与えられた権限を保持しているか、権限が暗黙的に与えられる上位の権限を保持している必要があります。  
  
 AS オプションを使用する場合は、次の追加要件があります。  
  
|AS *granting_principal*|必要な追加権限|  
|------------------------------|------------------------------------|  
|データベース ユーザー|ユーザーに対する IMPERSONATE 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|Windows ログインにマップされているデータベース ユーザー|ユーザーに対する IMPERSONATE 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|Windows グループにマップされているデータベース ユーザー|Windows グループのメンバーシップ、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|証明書にマップされているデータベース ユーザー|**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|非対称キーにマップされているデータベース ユーザー|**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|サーバー プリンシパルにマップされていないデータベース ユーザー|ユーザーに対する IMPERSONATE 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|データベース ロール|ロールに対する ALTER 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
|アプリケーション ロール|ロールに対する ALTER 権限、**db_securityadmin** 固定データベース ロールのメンバーシップ、**db_owner** 固定データベース ロールのメンバーシップ、または **sysadmin** 固定サーバー ロールのメンバーシップ。|  
  
 オブジェクトの所有者は、所有するオブジェクトの権限を許可できます。 セキュリティ保護可能なリソースに対して CONTROL 権限があるプリンシパルは、そのリソースの権限を許可できます。  
  
 **sysadmin** 固定サーバー ロールのメンバーなど、CONTROL SERVER 権限が許可されているユーザーは、サーバー内のセキュリティ保護可能なリソースに対する権限を許可できます。 **db_owner** 固定データベース ロールのメンバーなど、データベースに対する CONTROL 権限が許可されているユーザーは、データベース内のセキュリティ保護可能なリソースに対する権限を許可できます。 スキーマに対する CONTROL 権限が許可されているユーザーは、スキーマ内のオブジェクトに対する権限を許可できます。  
  
## <a name="see-also"></a>参照  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE (データベース スコープの資格情報の取り消し) (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [DENY (データベース スコープの資格情報の拒否) (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
