---
title: sp_post_msx_operation (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 93e9c574346ad57a6947645552616cd8db46fe85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056369"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  操作 (行) を挿入、 **sysdownloadlist**をダウンロードして実行対象サーバーのシステム テーブル。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>引数  
`[ @operation = ] 'operation'` ポストされた操作の操作の種類。 *操作*は**varchar (64)** 、既定値はありません。 有効な操作が異なります*object_type*します。  
  
|オブジェクトの種類|操作|  
|-----------------|---------------|  
|**JOB**|INSERT<br /><br /> UPDATE<br /><br /> Del<br /><br /> START<br /><br /> STOP|  
|**サーバー**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**SCHEDULE**|INSERT<br /><br /> UPDATE<br /><br /> Del|  
  
`[ @object_type = ] 'object'` 操作を投稿する対象のオブジェクトの型。 有効な種類は**ジョブ**、 **SERVER**、および**スケジュール**します。 *オブジェクト*は**varchar (64)** 、既定値は**ジョブ**します。  
  
`[ @job_id = ] job_id` 操作が適用されるジョブのジョブ識別番号。 *job_id*は**uniqueidentifier**、既定値はありません。 **0x00**すべてのジョブを示します。 場合*オブジェクト*は**SERVER**、し*job_id*は必要ありません。  
  
`[ @specific_target_server = ] 'target_server'` 指定された操作を適用するターゲット サーバーの名前。 場合*job_id*が指定されているが、 *target_server*が指定されていない、すべてのジョブ、ジョブのサーバー操作が通知されます。 *target_server*は**nvarchar (30)** 、既定値は NULL です。  
  
`[ @value = ] value` ポーリング間隔 (秒) です。 *value* のデータ型は **int**で、既定値は NULL です。 場合にのみ、このパラメーターを指定*操作*は**SET-POLL**します。  
  
`[ @schedule_uid = ] schedule_uid` 操作が適用されるスケジュールの一意の識別子。 *schedule_uid*は**uniqueidentifier**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_post_msx_operation**から実行する必要があります、 **msdb**データベース。  
  
 **sp_post_msx_operation**常に呼び出せる安全にそうである場合と、現在のサーバーがマルチ サーバーの Microsoft SQL Server エージェントの場合、最初に決定されるためかどうか*オブジェクト*はマルチ サーバー ジョブです。  
  
 操作が通知されると後に、表示される、 **sysdownloadlist**テーブル。 ジョブを作成し通知した後でそのジョブに変更を加える場合は、対象サーバー (TSX) にその変更を伝える必要があります。 これを行うには、ダウンロードの一覧を使用します。  
  
 ダウンロードの一覧は、SQL Server Management Studio を使用して管理することを強くお勧めします。 詳細については、次を参照してください。[の表示または変更するジョブ](../../ssms/agent/view-or-modify-jobs.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するユーザーに付与する必要があります、 **sysadmin**固定サーバー ロール。  
  
## <a name="see-also"></a>参照  
 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
