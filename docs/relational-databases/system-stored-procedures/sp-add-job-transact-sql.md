---
title: sp_add_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7752b8fcb453f545c357c529774d570e41201ed1
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381910"
---
# <a name="sp_add_job-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  SQL エージェントサービスによって実行される新しいジョブを追加します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
 > [!IMPORTANT]  
 > [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。
 
## <a name="syntax"></a>構文  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>引数  
ジョブの名前 `[ @job_name = ] 'job_name'` ます。 名前は一意である必要があり、パーセント ( **%** ) 文字を含めることはできません。 *job_name*は**nvarchar (128)** ,、既定値はありません。  
  
`[ @enabled = ] enabled` は、追加されたジョブの状態を示します。 *有効*になっているは**tinyint**,、既定値は 1 (有効) です。 **0**の場合、ジョブは無効になり、スケジュールに従って実行されません。ただし、手動で実行することもできます。  
  
ジョブの説明を `[ @description = ] 'description'` します。 *説明*は**nvarchar (512)** ,、既定値は NULL です。 *Description*を省略した場合、"説明はありません" が使用されます。  
  
ジョブに対して実行する最初のステップの識別番号を `[ @start_step_id = ] step_id` します。 *step_id*は**int**,、既定値は1です。  
  
ジョブのカテゴリを `[ @category_name = ] 'category'` します。 *category*は**sysname**,、既定値は NULL です。  
  
ジョブカテゴリを指定するための言語に依存しないメカニズムを `[ @category_id = ] category_id` します。 *category_id*は**int**,、既定値は NULL です。  
  
`[ @owner_login_name = ] 'login'`、ジョブを所有するログインの名前を指定します。 *login*は**sysname**で、既定値は NULL です。これは現在のログイン名として解釈されます。 **\@owner_login_name**の値を設定または変更できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。 **Sysadmin**ロールのメンバーでないユーザーが **\@owner_login_name**の値を設定または変更した場合、このストアドプロシージャの実行は失敗し、エラーが返されます。  
  
このジョブの Microsoft Windows アプリケーションログにエントリを配置するタイミングを示す値を `[ @notify_level_eventlog = ] eventlog_level` します。 *eventlog_level*は**int**,、これらの値のいずれかを指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0**|Never|  
|**1**|成功時|  
|**2** (既定値)|失敗時|  
|**3**|毎回|  
  
このジョブの完了時に電子メールを送信するタイミングを示す値を `[ @notify_level_email = ] email_level` します。 *email_level*は**int**,、既定値は**0**,、しないことを示します。 *email_level*は*eventlog_level*と同じ値を使用します。  
  
このジョブの完了時にネットワークメッセージを送信するタイミングを示す値を `[ @notify_level_netsend = ] netsend_level` します。 *netsend_level*は**int**,、既定値は**0**,、しないことを示します。 *netsend_level*は*eventlog_level*と同じ値を使用します。  
  
このジョブの完了時にページを送信するタイミングを示す値を `[ @notify_level_page = ] page_level` します。 *page_level*は**int**,、既定値は**0**,、しないことを示します。 *page_level*は*eventlog_level*と同じ値を使用します。  
  
*email_level*に達したときに電子メールを送信する相手の電子メール名を `[ @notify_email_operator_name = ] 'email_name'` します。 *email_name*は**sysname**,、既定値は NULL です。  
  
このジョブの完了時にネットワークメッセージを送信するオペレーターの名前を `[ @notify_netsend_operator_name = ] 'netsend_name'` します。 *netsend_name*は**sysname**,、既定値は NULL です。  
  
このジョブの完了時にページを `[ @notify_page_operator_name = ] 'page_name'` するユーザーの名前を指定します。 *page_name*は**sysname**,、既定値は NULL です。  
  
ジョブをいつ削除するかを示す値を `[ @delete_level = ] delete_level` します。 *delete_value*は**int**,、既定値は 0,、しないことを意味します。 *delete_level*は*eventlog_level*と同じ値を使用します。  
  
> [!NOTE]  
>  *Delete_level*が**3**の場合、ジョブに定義されているスケジュールに関係なく、ジョブは1回だけ実行されます。 また、ジョブが自分自身を削除した場合、そのジョブのすべての履歴も削除されます。  
  
ジョブが正常に作成された場合は、ジョブに割り当てられているジョブ識別番号を `[ @job_id = ] _job_idOUTPUT` します。 *job_id*は、 **uniqueidentifier**型の出力変数で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 **\@originating_server**は sp_add_job に存在しますが **、** [引数] の下には表示されません。 **\@originating_server**は、内部使用のために予約されています。  
  
 **Sp_add_job**を実行してジョブを追加した後、 **sp_add_jobstep**を使用して、ジョブのアクティビティを実行するステップを追加できます。 **sp_add_jobschedule**を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントサービスがジョブを実行するために使用するスケジュールを作成できます。 **Sp_add_jobserver**を使用して、ジョブを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを設定し、 **sp_delete_jobserver** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスからジョブを削除します。  
  
 マルチサーバー環境の1つ以上の対象サーバーでジョブを実行する場合は、 **sp_apply_job_to_targets**を使用して、ジョブの対象サーバーまたは対象サーバーグループを設定します。 対象サーバーまたは対象サーバーグループからジョブを削除するには、 **sp_remove_job_from_targets**を使用します。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 このストアドプロシージャを実行するには、 **sysadmin**固定サーバーロールのメンバーであるか、 **msdb**データベースに格納されている次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベースロールのいずれかが付与されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらの固定データベースロールに関連付けられている特定の権限の詳細については、「 [SQL Server エージェント固定データベースロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **\@owner_login_name**の値を設定または変更できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。 **Sysadmin**ロールのメンバーでないユーザーが **\@owner_login_name**の値を設定または変更した場合、このストアドプロシージャの実行は失敗し、エラーが返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-adding-a-job"></a>A. ジョブの追加  
 この例では、`NightlyBackups`という名前の新しいジョブを追加します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>b. ポケットベル、電子メール、および net send の情報を含むジョブの追加  
 この例では、ジョブが失敗した場合に `François Ajenstat` (ポケットベル、電子メール、またはネットワークのポップアップメッセージ) を通知する `Ad hoc Sales Data Backup` という名前のジョブを作成し、正常に完了したときにジョブを削除します。  
  
> [!NOTE]  
>  この例では、`François Ajenstat` という名前のオペレーターと `françoisa` という名前のログインが既に存在することを前提としています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [transact-sql &#40;  の&#41; sp_add_schedule](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_add_jobstep](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_add_jobserver](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_delete_job](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_remove_job_from_targets](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_help_job](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_update_job](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
