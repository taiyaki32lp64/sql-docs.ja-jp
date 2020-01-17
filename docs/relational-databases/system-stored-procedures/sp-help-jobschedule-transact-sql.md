---
title: sp_help_jobschedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 72e321b74f3e949030a6d599c082acf36db12687
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054910"
---
# <a name="sphelpjobschedule-transact-sql"></a>sp_help_jobschedule (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  によって使用されるジョブのスケジュールに関する情報を返します[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]自動化された操作を実行します。  
 
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ジョブの識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]
> いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。

`[ @schedule_name = ] 'schedule_name'` ジョブのスケジュール アイテムの名前。 *schedule_name*は**sysname**、既定値は NULL です。  
  
`[ @schedule_id = ] schedule_id` ジョブのスケジュール アイテムの識別番号。 *schedule_id*は**int**、既定値は NULL です。  
  
`[ @include_description = ] include_description` スケジュールの説明を結果セットに含めるかどうかを指定します。 *include_description*は**ビット**、既定値は**0**します。 ときに*include_description*は**0**スケジュールの説明が結果セットに含まれません。 ときに*include_description*は**1**、結果セットのスケジュールの説明が含まれます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|スケジュールの識別番号。|  
|**schedule_name**|**sysname**|スケジュールの名前。|  
|**enabled**|**int**|スケジュールが有効かどうか (**1**) または有効になっていません (**0**)。|  
|**freq_type**|**int**|ジョブが実行されることを示す値。<br /><br /> **1** = 1 回<br /><br /> **4** = 毎日<br /><br /> **8** = 毎週<br /><br /> **16**毎月を =<br /><br /> **32**を基準とする、毎月を =、 **freq_interval**<br /><br /> **64** = の場合に実行**SQLServerAgent**サービスの開始。|  
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
|**schedule_description**|**nvarchar (4000)**|内の値から派生したスケジュールの説明**msdb.dbo.sysschedules**します。 ときに*include_description*は**0**、このコラムには、説明が要求されていないことを示すテキストが含まれています。|  
|**next_run_date**|**int**|スケジュールで次にジョブを実行する日付。|  
|**next_run_time**|**int**|スケジュールで次にジョブを実行する時刻。|  
|**schedule_uid**|**uniqueidentifier**|スケジュールの識別子。|  
|**job_count**|**int**|ジョブの数が返されます。|  
  
> **注: sp_help_jobschedule**から値を返します、**では**と**dbo.sysschedules**システム テーブル**msdb**します。 **sysjobschedules** 20 分ごとに更新します。 このストアド プロシージャによって返される値に影響を与える可能性があります。  
  
## <a name="remarks"></a>コメント  
 パラメーター **sp_help_jobschedule**特定の組み合わせでのみ使用できます。 場合*schedule_id*が指定されても*job_id*も*job_name*を指定できます。 それ以外の場合、 *job_id*または*job_name*でパラメーターを使用できる*schedule_name*します。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーの**SQLAgentUserRole**自分が所有するジョブのスケジュールのプロパティだけを表示できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. 特定のジョブのジョブ スケジュールを返す  
 次の例は、という名前のジョブのスケジュール情報を返します`BackupDatabase`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. 特定のスケジュールのジョブ スケジュールを返す  
 次の例では、`NightlyJobs` という名前のスケジュールと、`RunReports` という名前のジョブの情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. ジョブのスケジュールと特定のスケジュールのスケジュールの説明を取得します。  
 次の例では、`NightlyJobs` という名前のスケジュールと、`RunReports` という名前のジョブの情報を返します。 返される結果には、スケジュールの説明が含まれています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
