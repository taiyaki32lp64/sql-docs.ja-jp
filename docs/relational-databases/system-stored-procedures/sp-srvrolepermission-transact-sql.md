---
title: sp_srvrolepermission (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_srvrolepermission_TSQL
- sp_srvrolepermission
dev_langs:
- TSQL
helpviewer_keywords:
- sp_srvrolepermission
ms.assetid: 5709667f-e3e4-48a2-93ec-af5e22a2ac58
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6613c4e94ce8c802e45fe003ac73e51b3f38072b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032811"
---
# <a name="spsrvrolepermission-transact-sql"></a>sp_srvrolepermission (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  固定サーバー ロールのアクセス許可を表示します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>引数  
`[ @srvrolename = ] 'role'` 権限を返す固定サーバー ロールの名前です。 *ロール*は**sysname**、既定値は NULL です。 ロールが指定されていない場合は、すべての固定サーバー ロールの権限が返されます。 *ロール*値は次のいずれかであることができます。  
  
|値|説明|  
|-----------|-----------------|  
|**sysadmin**|システム管理者|  
|**securityadmin**|セキュリティ管理者|  
|**serveradmin**|サーバー管理者。|  
|**setupadmin**|セットアップ管理者。|  
|**processadmin**|プロセス管理者。|  
|**diskadmin**|ディスク管理者。|  
|**dbcreator**|データベース作成者。|  
|**bulkadmin**|BULK INSERT ステートメントを実行できます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ServerRole**|**sysname**|固定サーバー ロールの名前|  
|**権限**|**sysname**|アクセス許可に関連付けられている**ServerRole**|  
  
## <a name="remarks"></a>コメント  
 表示される権限には、固定サーバー ロールのメンバーが実行できる、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとその他の特別な操作が含まれます。 固定サーバー ロールの一覧を表示するには、実行**sp_helpsrvrole**します。  
  
 **Sysadmin**固定サーバー ロールは、その他のすべての固定サーバー ロールのアクセス許可を持ちます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次のクエリでは、固定サーバー ロール `sysadmin` に関連する権限が返されます。  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
