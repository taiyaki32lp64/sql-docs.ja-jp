---
title: sp_help_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_job_TSQL
- sp_help_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_job
ms.assetid: 8a8b6104-e0e4-4d07-a2c3-f4243ee0d6fa
author: stevestein
ms.author: sstein
ms.openlocfilehash: 29870a0ffb3d2c3b1872acbb40266aef0d16b62c
ms.sourcegitcommit: 94f6a4b506dfda242fc3efb2403847e22a36d340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2019
ms.locfileid: "75546565"
---
# <a name="sp_help_job-transact-sql"></a>sp_help_job (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  自動化された操作を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用されるジョブに関する情報を返します。  
  
 
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_job { [ @job_id = ] job_id  
[ @job_name = ] 'job_name' }   
     [ , [ @job_aspect = ] 'job_aspect' ]   
     [ , [ @job_type = ] 'job_type' ]   
     [ , [ @owner_login_name = ] 'login_name' ]   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @enabled = ] enabled ]   
     [ , [ @execution_status = ] status ]   
     [ , [ @date_comparator = ] 'date_comparison' ]   
     [ , [ @date_created = ] date_created ]   
     [ , [ @date_last_modified = ] date_modified ]   
     [ , [ @description = ] 'description_pattern' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id`ジョブの識別番号を指定します。 *job_id*は**uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'`ジョブの名前。 *job_name*は**sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  特定のジョブを表示するには、 *job_id*または*job_name*のいずれかを指定する必要があります。  すべてのジョブに関する情報を返すには、 *job_id*と*job_name*の両方を省略します。
  
`[ @job_aspect = ] 'job_aspect'`表示するジョブ属性。 *job_aspect*は**varchar (9)**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**すべての**|ジョブのすべての属性情報|  
|**補足**|ジョブ情報|  
|**出荷**|スケジュール情報|  
|**よう**|ジョブ ステップ情報|  
|**ターゲット**|ターゲット情報|  
  
`[ @job_type = ] 'job_type'`レポートに含めるジョブの種類。 *job_type*は**varchar (12)**,、既定値は NULL です。 *Job_type* **ローカル**または**マルチサーバー**を指定できます。  
  
`[ @owner_login_name = ] 'login_name'`ジョブの所有者のログイン名です。 *login_name*は**sysname**,、既定値は NULL です。  
  
`[ @subsystem = ] 'subsystem'`サブシステムの名前。 *サブシステム*は**nvarchar (40)**,、既定値は NULL です。  
  
`[ @category_name = ] 'category'`カテゴリの名前。 *category*は**sysname**,、既定値は NULL です。  
  
`[ @enabled = ] enabled`有効なジョブまたは無効になっているジョブの情報を表示するかどうかを示す数値です。 *有効*になっているは**tinyint**,、既定値は NULL です。 **1**は有効なジョブを示し、 **0**は無効になっているジョブを示します。  
  
`[ @execution_status = ] status`ジョブの実行状態です。 *状態*は**int**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|アイドルまたは中断されていないジョブのみを返します。|  
|**1 で保護されたプロセスとして起動されました**|実行.|  
|**3**|スレッド待機中。|  
|**番**|再試行の間隔。|  
|**4/4**|[アイドル]。|  
|**5/5**|状態.|  
|**7**|完了操作の実行中。|  
  
`[ @date_comparator = ] 'date_comparison'`*Date_created*と*date_modified*の比較に使用する比較演算子。 *date_comparison*は**char (1)** で、=、 \<、または > にすることができます。  
  
`[ @date_created = ] date_created`ジョブが作成された日付。 *date_created*は**datetime**,、既定値は NULL です。  
  
`[ @date_last_modified = ] date_modified`ジョブが最後に変更された日付。 *date_modified*は**datetime**,、既定値は NULL です。  
  
`[ @description = ] 'description_pattern'`ジョブの説明。 *description_pattern*は**nvarchar (512)**,、既定値は NULL です。 *description_pattern*には、パターンマッチングに SQL Server ワイルドカード文字を含めることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 引数を指定しない場合、 **sp_help_job**はこの結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**一意**|ジョブの一意の ID。|  
|**originating_server**|**nvarchar (30)**|ジョブの送信元のサーバーの名前。|  
|**指定**|**sysname**|ジョブの名前。|  
|**enabled**|**tinyint**|ジョブの実行が有効かどうかを示します。|  
|**記述**|**nvarchar(512)**|ジョブの説明。|  
|**start_step_id**|**通り**|実行を開始するジョブのステップの ID。|  
|**別**|**sysname**|ジョブ カテゴリ。|  
|**責任**|**sysname**|ジョブ所有者。|  
|**notify_level_eventlog**|**通り**|どのような場合に、通知イベントを Microsoft Windows アプリケーションログに記録するかを示す**ビットマスク**。 次のいずれかの値を指定できます。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功した場合<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**notify_level_email**|**通り**|どのような場合に、ジョブの完了時に通知電子メールを送信するかを示す**ビットマスク**。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**notify_level_netsend**|**通り**|どのような場合に、ジョブの完了時にネットワークメッセージを送信するかを示す**ビットマスク**。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**notify_level_page**|**通り**|どのような場合に、ジョブの完了時にページを送信するかを示す**ビットマスク**。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**notify_email_operator**|**sysname**|通知するオペレーターの電子メール名。|  
|**notify_netsend_operator**|**sysname**|ネットワークメッセージを送信するときに使用するコンピューターまたはユーザーの名前。|  
|**notify_page_operator**|**sysname**|ページを送信するときに使用するコンピューターまたはユーザーの名前。|  
|**delete_level**|**通り**|どのような場合に、ジョブの完了時にジョブを削除するかを示す**ビットマスク**。 指定できる値は、 **notify_level_eventlog**の場合と同じです。|  
|**date_created**|**/**|ジョブが作成された日付。|  
|**date_modified**|**/**|ジョブが最後に変更された日付。|  
|**version_number**|**通り**|ジョブのバージョン (ジョブを変更するたびに自動的に更新されます)。|  
|**last_run_date**|**通り**|ジョブの実行を最後に開始した日付。|  
|**last_run_time**|**通り**|ジョブの実行を最後に開始した時刻。|  
|**last_run_outcome**|**通り**|最後に実行したときのジョブの結果:<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
|**next_run_date**|**通り**|ジョブが次に実行されるようにスケジュールされている日付。|  
|**next_run_time**|**通り**|ジョブの次回実行予定時刻。|  
|**next_run_schedule_id**|**通り**|次回の実行スケジュールの識別番号。|  
|**current_execution_status**|**通り**|現在の実行状態:<br /><br /> **1** = 実行中<br /><br /> **2** = スレッドを待機しています<br /><br /> **3** = 再試行の間隔<br /><br /> **4** = アイドル<br /><br /> **5** = 中断<br /><br /> **6** = 互換性のために残されています<br /><br /> **7** = PerformingCompletionActions|  
|**current_execution_step**|**sysname**|ジョブの現在の実行ステップ。|  
|**current_retry_attempt**|**通り**|ジョブが実行中で、ステップが再試行されている場合は、これが現在の再試行です。|  
|**has_step**|**通り**|ジョブに含まれるジョブステップの数。|  
|**has_schedule**|**通り**|ジョブのジョブ スケジュール数。|  
|**has_target**|**通り**|ジョブのターゲット サーバー数。|  
|**各種**|**通り**|ジョブの種類。<br /><br /> 1 = ローカルジョブ。<br /><br /> **2** = マルチサーバージョブ。<br /><br /> **0** = ジョブに対象サーバーがありません。|  
  
 *Job_id*または*job_name*が指定されている場合、 **sp_help_job**は、ジョブステップ、ジョブスケジュール、およびジョブ対象サーバーに対してこれらの追加の結果セットを返します。  
  
 次に、ジョブ ステップに関する結果セットを示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**step_id**|**通り**|ステップの (このジョブで) 一意の ID。|  
|**step_name**|**sysname**|ステップの名前。|  
|**サブ**|**nvarchar (40)**|ステップ コマンドを実行するサブシステム。|  
|**メニュー**|**nvarchar (3200)**|実行するコマンド。|  
|**示す**|**nvarchar(4000)**|ステップの動作を制御する値の**ビットマスク**。|  
|**cmdexec_success_code**|**通り**|**CmdExec**ステップの場合、これは成功したコマンドのプロセス終了コードです。|  
|**on_success_action**|**nvarchar(4000)**|ステップが成功した場合の対処方法:<br /><br /> **1** = 正常に終了します。<br /><br /> **2** = エラーで終了します。<br /><br /> **3** = 次の手順に進みます。<br /><br /> **4** = ステップに進みます。|  
|**on_success_step_id**|**通り**|**On_success_action**が**4**の場合は、次に実行する手順を示します。|  
|**on_fail_action**|**nvarchar(4000)**|ステップが失敗した場合に実行する動作。 値は**on_success_action**の場合と同じです。|  
|**on_fail_step_id**|**通り**|**On_fail_action**が**4**の場合は、次に実行する手順を示します。|  
|**server**|**sysname**|予約済み。|  
|**database_name**|**sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)]ステップの場合、これはコマンドを実行するデータベースです。|  
|**database_user_name**|**sysname**|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合は、コマンドを実行するデータベース ユーザー コンテキスト。|  
|**retry_attempts**|**通り**|ステップを正常に実行できない場合、コマンドを再試行する最大回数。この回数に達すると、ステップが失敗したと判断されます。|  
|**retry_interval**|**通り**|再試行の間隔 (分単位)。|  
|**os_run_priority**|**varchar (4000)**|予約済み。|  
|**output_file_name**|**varchar (200)**|コマンド出力を書き込むファイル ([!INCLUDE[tsql](../../includes/tsql-md.md)]および**CmdExec**ステップのみ)。|  
|**last_run_outcome**|**通り**|最後に実行したときのステップの結果。<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
|**last_run_duration**|**通り**|最後に実行したときのステップの経過時間 (秒単位)。|  
|**last_run_retries**|**通り**|最後にステップを実行したときにコマンドが再試行された回数。|  
|**last_run_date**|**通り**|ステップの実行を最後に開始した日付。|  
|**last_run_time**|**通り**|ステップの実行を最後に開始した時刻。|  
|**proxy_id**|**通り**|ジョブステップのプロキシ。|  
  
 これは、ジョブスケジュールの結果セットです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**通り**|すべてのジョブで一意なスケジュール識別子。|  
|**schedule_name**|**sysname**|スケジュールの名前 (このジョブでのみ一意)。|  
|**enabled**|**通り**|スケジュールがアクティブである (**1**) かどうか (**0**)。|  
|**freq_type**|**通り**|ジョブをいつ実行するかを示す値。<br /><br /> **1** = 1 回<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月、 **freq_interval**に対して相対的<br /><br /> **64** = **SQLServerAgent**サービスの開始時に実行します。|  
|**freq_interval**|**通り**|ジョブが実行された日。 値は**freq_type**の値によって異なります。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 」を参照してください。|  
|**freq_subday_type**|**通り**|**Freq_subday_interval**の単位。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 」を参照してください。|  
|**freq_subday_interval**|**通り**|ジョブの各実行間に発生する**freq_subday_type**期間の数。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 」を参照してください。|  
|**freq_relative_interval**|**通り**|スケジュールされたジョブの各月の**freq_interval**の発生。 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md) 」を参照してください。|  
|**freq_recurrence_factor**|**通り**|スケジュールされたジョブの実行間隔 (月数)。|  
|**active_start_date**|**通り**|ジョブの実行を開始する日付。|  
|**active_end_date**|**通り**|ジョブの実行を終了する日付。|  
|**active_start_time**|**通り**|Active_start_date でジョブの実行を開始する時刻 **。**|  
|**active_end_time**|**通り**|**Active_end_date**でジョブの実行を終了する時刻。|  
|**date_created**|**/**|スケジュールが作成された日付。|  
|**schedule_description**|**nvarchar(4000)**|スケジュールの英語の説明 (要求された場合)。|  
|**next_run_date**|**通り**|スケジュールによってジョブが次に実行される日付。|  
|**next_run_time**|**通り**|スケジュールによってジョブが次に実行される時刻。|  
|**schedule_uid**|**一意**|スケジュールの識別子。|  
|**job_count**|**通り**|このスケジュールを参照するジョブの数。|  
  
 次に、ジョブターゲット サーバーに関する結果セットを示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**通り**|対象サーバーの識別子。|  
|**server_name**|**nvarchar (30)**|対象サーバーのコンピューター名。|  
|**enlist_date**|**/**|対象サーバーをマスターサーバーに参加させた日付。|  
|**last_poll_date**|**/**|対象サーバーが最後にマスターサーバーをポーリングした日付。|  
|**last_run_date**|**通り**|ターゲット サーバーでジョブの実行を最後に開始した日付。|  
|**last_run_time**|**通り**|ターゲット サーバーでジョブの実行を最後に開始した時刻。|  
|**last_run_duration**|**通り**|対象サーバーで最後に実行されたときのジョブの期間。|  
|**last_run_outcome**|**tinyint**|このサーバーで最後に実行されたときのジョブの結果:<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = キャンセル<br /><br /> **5** = 不明|  
|**last_outcome_message**|**nvarchar (1024)**|この対象サーバーで最後に実行されたときのジョブからの結果メッセージ。|  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin**固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**のメンバーは、自分が所有しているジョブのみを表示できます。 **Sysadmin**、 **SQLAgentReaderRole**、および**Sqlagentoperatorrole**のメンバーは、すべてのローカルジョブとマルチサーバージョブを表示できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-list-information-for-all-jobs"></a>A. すべてのジョブの情報を一覧表示する  
 次の例では`sp_help_job` 、パラメーターを指定せずにプロシージャを実行し、 `msdb`データベースで現在定義されているすべてのジョブの情報を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-matching-a-specific-criteria"></a>B. 特定の条件に一致するジョブの情報を一覧表示する  
 次の例では、`françoisa` が所有するマルチサーバー ジョブのジョブ情報を一覧表示します。ここでは、有効でかつ、実行中のジョブが対象になります。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job   
   @job_type = N'MULTI-SERVER',  
   @owner_login_name = N'françoisa',  
   @enabled = 1,  
   @execution_status = 1 ;  
GO  
```  
  
### <a name="c-listing-all-aspects-of-information-for-a-job"></a>C. ジョブに関するすべての属性情報を一覧表示する  
 次の例では、`NightlyBackups` ジョブに関するすべての属性情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job  
    @job_name = N'NightlyBackups',  
    @job_aspect = N'ALL' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
