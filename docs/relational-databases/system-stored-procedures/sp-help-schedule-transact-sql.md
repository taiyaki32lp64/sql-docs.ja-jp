---
title: sp_help_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5a68160c8aee1bcb399513051e1f4cc35cea970
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085212"
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  スケジュールの詳細についての情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>引数  
`[ @schedule_id = ] id` 一覧表示するスケジュールの識別子。 *schedule_name*は**int**、既定値はありません。 いずれか*schedule_id*または*schedule_name*指定することがあります。  
  
`[ @schedule_name = ] 'schedule_name'` 一覧表示するスケジュールの名前。 *schedule_name*は**sysname**、既定値はありません。 いずれか*schedule_id*または*schedule_name*指定することがあります。  
  
`[ @attached_schedules_only = ] attached_schedules_only ]` ジョブに接続されているスケジュールのみを表示するかどうかを指定します。 *attached_schedules_only*は**ビット**、既定値は**0**します。 ときに*attached_schedules_only*は**0**、すべてのスケジュールが表示されます。 ときに*attached_schedules_only*は**1**ジョブにアタッチされているスケジュールのみが結果セットに含まれています。  
  
`[ @include_description = ] include_description` 結果セットに説明を含めるかどうかを指定します。 *include_description*は**ビット**、既定値は**0**します。 ときに*include_description*は**0**、 *schedule_description*結果セットの列にはプレース ホルダーが含まれています。 ときに*include_description*は**1**、結果セットのスケジュールの説明が含まれます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 このプロシージャでは、次の結果セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|スケジュールの識別番号。|  
|**schedule_uid**|**uniqueidentifier**|スケジュールの識別子。|  
|**schedule_name**|**sysname**|スケジュールの名前。|  
|**enabled**|**int**|スケジュールが有効かどうか (**1**) または有効になっていません (**0**)。|  
|**freq_type**|**int**|ジョブが実行されることを示す値。<br /><br /> **1** = 1 回<br /><br /> **4** = 毎日<br /><br /> **8** = 毎週<br /><br /> **16**毎月を =<br /><br /> **32**を基準とする、毎月を =、 **freq_interval**<br /><br /> **64** SQLServerAgent サービスの起動時に実行を = です。|  
|**freq_interval**|**int**|日のジョブを実行するとします。 値の値に依存**freq_type**します。 詳細については、次を参照してください。 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)します。|  
|**freq_subday_type**|**int**|単位**freq_subday_interval**します。 詳細については、次を参照してください。 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)します。|  
|**freq_subday_interval**|**int**|数**freq_subday_type**にジョブの各実行間に発生する期間。 詳細については、次を参照してください。 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)します。|  
|**freq_relative_interval**|**int**|定期ジョブの**freq_interval**各月にします。 詳細については、次を参照してください。 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)します。|  
|**freq_recurrence_factor**|**int**|定期ジョブの実行間隔 (月単位)。|  
|**active_start_date**|**int**|スケジュールをアクティブにした日付。|  
|**active_end_date**|**int**|スケジュールの終了日。|  
|**active_start_time**|**int**|スケジュールの開始時刻。|  
|**active_end_time**|**int**|スケジュールを終了する時刻。|  
|**date_created**|**datetime**|スケジュールを作成した日付。|  
|**schedule_description**|**nvarchar (4000)**|英語によるスケジュールの説明 (必要な場合)。|  
|**job_count**|**int**|このスケジュールを参照するジョブの数を返します。|  
  
## <a name="remarks"></a>コメント  
 パラメーターが指定されていないときに**sp_help_schedule**インスタンスのすべてのスケジュール情報を一覧表示します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーの**SQLAgentUserRole**所有しているスケジュールのみを表示できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. インスタンスのすべてのスケジュールに関する情報を一覧表示する  
 次の例では、インスタンスのすべてのスケジュールに関する情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. 特定のスケジュールに関する情報を一覧表示します。  
 次の例では、`NightlyJobs` というスケジュールに関する情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
