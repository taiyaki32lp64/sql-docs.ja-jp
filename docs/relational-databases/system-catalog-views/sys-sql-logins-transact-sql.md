---
title: sys.sql_logins (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 362ccc5c85523b3d37cb792a42e8be4cd87d7510
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109001"
---
# <a name="syssqllogins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] authentication ログインごとに 1 行のデータが返ります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**|--|継承**sys.server_principals**します。|  
|**is_policy_checked**|**bit**|パスワード ポリシーが確認されるかどうかを示します。|  
|**is_expiration_checked**|**bit**|パスワードの期限が確認されるかどうかを示します。|  
|**password_hash**|**varbinary(256)**|SQL ログイン パスワードのハッシュ。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、保存されたパスワード情報は salt 化パスワードの SHA-512 を使用して計算されます。|  
  
 このビューが継承する列の一覧は、次を参照してください。 [sys.server_principals &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)します。  
  
## <a name="remarks"></a>コメント  
 両方を表示する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証のログインと Windows 認証ログインを参照してください。 [sys.server_principals &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)します。  
  
 含まれる場合にデータベース ユーザーが有効で、ログインのない、接続を作成することができます。 これらのアカウントを識別するために、次を参照してください。 [sys.database_principals &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 すべて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証ログインは、独自のログイン名と sa ログインを参照できます。 他のログインを参照するには、ALTER ANY LOGIN、またはログインに対する権限が必要です。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
