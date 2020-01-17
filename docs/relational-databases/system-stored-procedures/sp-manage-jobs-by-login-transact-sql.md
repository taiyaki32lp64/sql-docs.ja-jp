---
title: sp_manage_jobs_by_login (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_manage_jobs_by_login
- sp_manage_jobs_by_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_manage_jobs_by_login
ms.assetid: 832ec15a-6e92-4eb5-8c4a-af4dba79fbaa
author: stevestein
ms.author: sstein
ms.openlocfilehash: ebc71c304939a977ac34cc2fad819edd463614fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894991"
---
# <a name="spmanagejobsbylogin-transact-sql"></a>sp_manage_jobs_by_login (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたログインに属するジョブを再割り当てまたは削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_manage_jobs_by_login  
     [ @action = ] 'action'  
     [, [@current_owner_login_name = ] 'current_owner_login_name']  
     [, [@new_owner_login_name = ] 'new_owner_login_name']  
```  
  
## <a name="arguments"></a>引数  
`[ @action = ] 'action'` 指定されたログインに対して実行するアクション。 *アクション*は**varchar (10)** 、既定値はありません。 ときに*アクション*は**削除**、 **sp_manage_jobs_by_login**によって所有されているすべてのジョブを削除*current_owner_login_name*します。 ときに*アクション*は**再割り当て**に割り当てられているすべてのジョブ*new_owner_login_name*します。  
  
`[ @current_owner_login_name = ] 'current_owner_login_name'` 現在のジョブ所有者のログイン名。 *current_owner_login_name* is **sysname**, with no default.  
  
`[ @new_owner_login_name = ] 'new_owner_login_name'` 新しいジョブ所有者のログイン名。 場合にのみ、このパラメーターを使用して、*アクション*は**再割り当て**します。 *new_owner_login_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するユーザーに付与する必要があります、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、 `danw` からのすべてのジョブを `françoisa`に再割り当てします。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_manage_jobs_by_login  
    @action = N'REASSIGN',  
    @current_owner_login_name = N'danw',  
    @new_owner_login_name = N'françoisa' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
