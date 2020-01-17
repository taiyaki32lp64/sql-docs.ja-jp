---
title: REVOKE (アセンブリの権限の取り消し) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, assemblies
- assemblies [CLR integration], permissions
ms.assetid: f88e9da1-2c0b-4bdd-9ec5-44467707cb46
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 898037be3f55692d7c85dbe92d00dc3f305e2ec7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082383"
---
# <a name="revoke-assembly-permissions-transact-sql"></a>REVOKE (アセンブリの権限の取り消し) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アセンブリに対する権限を取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ASSEMBLY :: assembly_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>引数  
 GRANT OPTION FOR  
 指定した権限を与えるまたは拒否する許可を取り消します。 権限自体は取り消されません。  
  
> [!IMPORTANT]  
>  指定した権限が GRANT オプションなしでプリンシパルに許可されている場合は、その権限自体が取り消されます。  
  
 *permission*  
 アセンブリで取り消すことができる権限を指定します。 以下に一覧を示します。  
  
 ON ASSEMBLY **::** _assembly_name_  
 権限を取り消すアセンブリを指定します。 スコープ修飾子 **::** が必要です。  
  
 *database_principal*  
 権限を取り消すプリンシパルを指定します。 次のいずれかです。  
  
-   データベース ユーザー  
  
-   データベース ロール (database role)  
  
-   アプリケーション ロール (application role)  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
 CASCADE  
 このプリンシパルによって権限が許可または拒否されている他のプリンシパルからも、同じ権限が取り消されることを示します。  
  
> [!CAUTION]  
>  WITH GRANT OPTION で許可されている権限を CASCADE で取り消すと、その権限の GRANT および DENY の両方が取り消されます。  
  
 AS *revoking_principal*  
 このクエリを実行するプリンシパルが権限を取り消す権利を取得した、元のプリンシパルを指定します。 次のいずれかです。  
  
-   データベース ユーザー  
  
-   データベース ロール (database role)  
  
-   アプリケーション ロール (application role)  
  
-   Windows ログインにマップされているデータベース ユーザー  
  
-   Windows グループにマップされているデータベース ユーザー  
  
-   証明書にマップされているデータベース ユーザー  
  
-   非対称キーにマップされているデータベース ユーザー  
  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>Remarks  
 アセンブリは、データベース レベルのセキュリティ保護可能なリソースで、権限の階層で親となっているデータベースに含まれています。 次に、アセンブリで取り消すことのできる権限のうち最も限定的なものを、それらを暗黙的に含む一般的な権限と共に示します。  
  
|アセンブリ権限|権限が含まれるアセンブリ権限|権限が含まれるデータベース権限|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
 アセンブリに対する CONTROL 権限が必要です  
  
## <a name="see-also"></a>参照  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
