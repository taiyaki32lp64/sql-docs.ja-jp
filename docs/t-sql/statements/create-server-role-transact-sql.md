---
title: CREATE SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SERVER_ROLE_TSQL
- CREATE SERVER ROLE
- SERVER ROLE
- CREATE_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE
- SERVER ROLE, CREATE
- CREATE SERVER ROLE statement
- ROLE
- user-defined server roles [SQL Server]
- roles, server
ms.assetid: 30c92f80-f7f6-4a84-ae89-16e69add0de6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 89f1338f2e127742a3e76b4b2dbc2f2ae5e8b8ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117126"
---
# <a name="create-server-role-transact-sql"></a>CREATE SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  新しいユーザー定義サーバー ロールを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE SERVER ROLE role_name [ AUTHORIZATION server_principal ]  
```  
  
## <a name="arguments"></a>引数  
 *role_name*  
 作成するサーバー ロールの名前を指定します。  
  
 AUTHORIZATION *server_principal*  
 新しいサーバー ロールを所有するログインです。 ログインを指定しない場合、サーバー ロールは CREATE SERVER ROLE を実行するログインが所有します。  
  
## <a name="remarks"></a>Remarks  
 サーバー ロールは、サーバー レベルのセキュリティ保護可能なリソースです。 サーバー ロールを作成した後は、GRANT、DENY、および REVOKE を使って、ロールのサーバー レベルの権限を構成します。 サーバー ロールのログインを追加または削除するには、[ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md) を使用します。 サーバー ロールを削除するには、[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md) を使用します。 詳細については、「[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)」を参照してください。  
  
 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) および [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) カタログ ビューに対してクエリを実行することで、サーバー ロールを確認できます。  
  
 データベース レベルのセキュリティ保護可能なリソースに対する権限をサーバー ロールに付与することはできません。 データベース ロールを作成するには、「[CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)」を参照してください。  
  
 権限システムの設計の詳細については、「 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE SERVER ROLE 権限、または sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
 さらに、ログインのための *server_principal* に対する IMPERSONATE 権限、 *server_principal*として使用されるサーバー ロールのための ALTER 権限、または server_principal として使用される Windows グループのメンバーシップも必要です。  
  
 これによりを追加するには、オブジェクトの種類のサーバーの役割設定とイベントの種類を Audit Server Principal Management イベントが発生します。  
  
 AUTHORIZATION オプションを使用してサーバー ロールの所有権を割り当てる場合は、次の権限も必要です。  
  
-   サーバー ロールの所有権を別のログインに割り当てるには、そのログインに対する IMPERSONATE 権限が必要です。  
  
-   サーバー ロールの所有権を別のサーバー ロールに割り当てるには、割り当て先のサーバー ロールのメンバーシップまたはそのサーバー ロールに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-server-role-that-is-owned-by-a-login"></a>A. ログインが所有するサーバー ロールを作成する  
 次の例では、ログイン `buyers` が所有するサーバー ロール `BenMiller` を作成します。  
  
```  
USE master;  
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-server-role-that-is-owned-by-a-fixed-server-role"></a>B. 固定サーバー ロールが所有するサーバー ロールを作成する  
 次の例では、固定サーバー ロール `auditors` が所有するサーバー ロール `securityadmin` を作成します。  
  
```  
USE master;  
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  
