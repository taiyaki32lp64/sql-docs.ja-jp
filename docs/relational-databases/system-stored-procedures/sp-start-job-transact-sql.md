---
title: sp_start_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b3015651dc263d95aa80e6108db2e8017e112d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032831"
---
# <a name="spstartjob-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブをすぐに実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_name = ] 'job_name'` 開始するジョブの名前。 いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。 *job_name*は**sysname**、既定値は NULL です。  
  
`[ @job_id = ] job_id` 開始するジョブの識別番号。 いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'` ジョブを開始する対象サーバーです。 *server_name*は**nvarchar (128)** 、既定値は NULL です。 *server_name*ジョブが現在対象となる対象のサーバーのいずれかを指定する必要があります。  
  
`[ @step_name = ] 'step_name'` ジョブの実行を開始するステップの名前。 ローカル ジョブにのみ適用されます。 *step_name*は**sysname**、既定値は NULL  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 このストアド プロシージャは、 **msdb**データベース。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーの**SQLAgentUserRole**と**SQLAgentReaderRole**自分が所有するジョブだけを開始できます。 メンバーの**SQLAgentOperatorRole**他のユーザーによって所有されているものも含め、すべてのローカル ジョブを開始できます。 メンバーの**sysadmin**すべてローカル ジョブおよびマルチ サーバー ジョブを開始できます。  
  
## <a name="examples"></a>使用例  
 次の例では、という名前のジョブを開始する`Weekly Sales Data Backup`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
