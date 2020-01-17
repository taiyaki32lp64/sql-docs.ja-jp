---
title: sp_remove_job_from_targets (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1ba55c2744d1fad0b6453e0f1d1cd2ea96934bfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006969"
---
# <a name="spremovejobfromtargets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したジョブを指定したターゲット サーバーまたはターゲット サーバー グループから削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 指定した対象サーバーまたは対象サーバー グループを削除するジョブのジョブ識別番号。 いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` 指定した対象サーバーまたは対象サーバー グループを削除するジョブの名前。 いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。 *job_name*は**sysname**、既定値は NULL です。  
  
`[ @target_server_groups = ] 'target_server_groups'` 指定されたジョブから削除する対象サーバー グループのコンマ区切りの一覧。 *target_server_groups*は**nvarchar (1024)** 、既定値は NULL です。  
  
`[ @target_servers = ] 'target_servers'` 指定されたジョブから削除する対象サーバーのコンマ区切りの一覧。 *target_servers*は**nvarchar (1024)** 、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>使用例  
 次の例では、削除前に作成した`Weekly Sales Backups`からジョブ、`Servers Processing Customer Orders`対象サーバーのグループとの間、`SEATTLE1`と`SEATTLE2`サーバー。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_remove_job_from_targets  
    @job_name = N'Weekly Sales Backups',  
    @target_server_groups = N'Servers Processing Customer Orders',   
    @target_servers = N'SEATTLE2,SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_apply_job_to_targets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
