---
title: DENY (スキーマ権限の拒否) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], schemas
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- DENY statement, schemas
ms.assetid: 300a67c4-d226-4653-9e9f-7ae4d53fcf33
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bd439e528cc30c0971d1b4c824ab2375856d26e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114788"
---
# <a name="deny-schema-permissions-transact-sql"></a>DENY (スキーマ権限の拒否) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

スキーマの権限を拒否します。  
  

![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
DENY permission  [ ,...n ] } ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>引数  
*permission*  
スキーマで拒否できる権限を指定します。 これらの権限の一覧については、後の「解説」を参照してください。  
  
ON SCHEMA **::** schema *_name*  
権限を拒否するスキーマを指定します。 スコープ修飾子 **::** が必要です。  
  
*database_principal*  
権限を拒否するプリンシパルを指定します。 *database_principal* には、次のいずれかのプリンシパルを指定することができます。  
  
-   データベース ユーザー  
-   データベース ロール  
-   アプリケーション ロール  
-   Windows ログインにマップされているデータベース ユーザー  
-   Windows グループにマップされているデータベース ユーザー  
-   証明書にマップされているデータベース ユーザー  
-   非対称キーにマップされているデータベース ユーザー  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
CASCADE  
指定した *database_principal* によって権限が付与された他のプリンシパルに対する権限を拒否します。
  
*denying_principal*  
このクエリを実行するプリンシパルが権限を拒否する権利を取得した、元のプリンシパルを指定します。 *denying_principal* には、次のいずれかのプリンシパルを指定することができます。  
  
-   データベース ユーザー  
-   データベース ロール  
-   アプリケーション ロール  
-   Windows ログインにマップされているデータベース ユーザー  
-   Windows グループにマップされているデータベース ユーザー  
-   証明書にマップされているデータベース ユーザー  
-   非対称キーにマップされているデータベース ユーザー  
-   サーバー プリンシパルにマップされていないデータベース ユーザー  
  
## <a name="remarks"></a>Remarks  
スキーマは、データベース レベルでセキュリティ保護可能です。 権限の階層で親となっているデータベースに含まれています。 次の表に、スキーマで拒否できる最も限定的で制限された権限を示します。 それらを暗黙的に含む、より全般的な権限を次の表に示します。  
  
|スキーマ権限|権限が含まれるスキーマ権限|権限が含まれるデータベース権限|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|DELETE|CONTROL|DELETE|  
|EXECUTE|CONTROL|EXECUTE|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>アクセス許可  
スキーマに対する CONTROL 権限が必要です。 AS オプションを使用する場合、指定するプリンシパルはスキーマを所有している必要があります。  
  
## <a name="see-also"></a>参照  
[CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
[DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
[アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
[プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
[sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
[HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
