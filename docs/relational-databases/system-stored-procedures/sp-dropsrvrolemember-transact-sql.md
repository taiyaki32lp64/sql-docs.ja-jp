---
title: sp_dropsrvrolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 2624ed4800a247b0847adc5839346758aa50f140
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463564"
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (TRANSACT-SQL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

固定サーバー ロールから、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインや、Windows ユーザーまたはグループを削除します。

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)代わりにします。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## <a name="arguments"></a>引数

**[ @loginame = ]** '_login_'  
固定サーバー ロールから削除するログインの名前です。 *ログイン*は**sysname**、既定値はありません。 *ログイン*存在する必要があります。  

**[ @rolename = ]** '_role_'  
サーバー ロールの名前です。 *ロール*は**sysname**、既定値は NULL です。 *ロール*値は次のいずれかを指定する必要があります。  

-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin 
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 固定サーバー ロールからログインを削除するのには、sp_dropsrvrolemember のみを使用できます。 Sp_droprolemember の各を使用して、データベース ロールからメンバーを削除します。  
  
 Sa ログインは、どの固定サーバー ロールから削除できません。  
  
 sp_dropsrvrolemember は、ユーザー定義のトランザクション内で実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 Sysadmin 固定サーバー ロール、または ALTER ANY LOGIN アクセス許可の両方、サーバーと、メンバーの削除元となるロールのメンバーシップのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ログインを削除する`JackO`から、`sysadmin`固定サーバー ロール。  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember の各&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
