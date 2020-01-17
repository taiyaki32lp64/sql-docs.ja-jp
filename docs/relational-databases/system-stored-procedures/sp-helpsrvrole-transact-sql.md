---
title: sp_helpsrvrole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
author: stevestein
ms.author: sstein
ms.openlocfilehash: a632e6923ab3127a363650c63533fa548d1acc12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006120"
---
# <a name="sphelpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定サーバー ロールの一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @srvrolename = ] 'role'` 固定サーバー ロールの名前です。 *ロール*は**sysname**、既定値は NULL です。 *ロール*値は次のいずれかを指定できます。  
  
|固定サーバー ロール|説明|  
|-----------------------|-----------------|  
|sysadmin|システム管理者|  
|securityadmin|セキュリティ管理者|  
|serveradmin|サーバー管理者。|  
|setupadmin|セットアップ管理者。|  
|processadmin|プロセス管理者。|  
|diskadmin|ディスク管理者。|  
|dbcreator|データベース作成者。|  
|bulkadmin|BULK INSERT ステートメントを実行できます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|サーバー ロールの名前|  
|説明|**sysname**|サーバー ロールの説明|  
  
## <a name="remarks"></a>コメント  
 固定サーバー ロールは、サーバー レベルで定義され、特定のサーバーレベルの管理操作を実行する権限が与えられます。 固定サーバー ロールは、追加、削除、または変更することはできません。  
  
 追加するサーバーの役割から削除されたメンバーを参照してくださいまたは[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)します。  
  
 すべてのログインは、public のメンバーです。 sp_helpsrvrole が public ロールを認識していないため、内部的には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリック ロールとして実装しません。  
  
 sp_helpsrvrole には、引数としてユーザー定義サーバー ロールはなりません。 ユーザー定義サーバー ロールの一覧、例を参照してください。 [ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-the-fixed-server-roles"></a>A. 固定サーバー ロールを一覧表示  
 次のクエリでは、固定サーバー ロールの一覧が返されます。  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>B. 固定の一覧とユーザー定義サーバー ロール  
 次のクエリでは、両方の固定とユーザー定義サーバー ロールの一覧を返します。  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>C. 固定サーバー ロールの説明を返す  
 次のクエリでは、`diskadmin` 固定サーバー ロールの名前と説明を返します。  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [サーバー レベルのロール](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
