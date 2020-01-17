---
title: sp_apply_job_to_targets (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 32e9f15dca77a7c99d7d4a9ae314e074876c6274
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117807"
---
# <a name="spapplyjobtotargets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つ以上のターゲット サーバー、または 1 つ以上のターゲット サーバー グループに属する複数のターゲット サーバーにジョブを適用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 指定した対象サーバーまたは対象サーバー グループに適用するジョブのジョブ識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` 関連付けられている対象サーバーを指定された適用またはサーバー グループを対象とするジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @target_server_groups = ] 'target_server_groups'` 指定したジョブが適用される対象サーバー グループのコンマ区切りの一覧。 *target_server_groups*は**nvarchar (2048)** 、既定値は NULL です。  
  
`[ @target_servers = ] 'target_servers'` 指定したジョブが適用される対象サーバーのコンマ区切りの一覧。 *target_servers*は**nvarchar (2048)** 、既定値は NULL です。  
  
`[ @operation = ] 'operation'` 指定したジョブに適用または指定した対象サーバーまたは対象サーバー グループから削除するかどうか。 *操作*は**varchar (7)** 、既定値は APPLY です。 有効な操作は**適用**と**削除**します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_apply_job_to_targets**ジョブを適用する (または削除する) 複数の対象サーバーからの簡単な方法を提供しを呼び出す代わりには、 **sp_add_jobserver** (または**sp_delete_jobserver**)各対象サーバーが必要ですに対して 1 回。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、このプロシージャを実行できます。  
  
## <a name="examples"></a>使用例  
 次の例では、`Backup Customer Information` グループのすべての対象サーバーに、先に作成した `Servers Maintaining Customer Information` ジョブを適用します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
