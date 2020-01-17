---
title: sp_update_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5428ae9130646db662c6c960f777c6a7dfe25000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084892"
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ジョブの属性を変更します。  
  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 更新するジョブの識別番号。 *job_id*は**uniqueidentifier**します。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は**nvarchar (128)** します。  
  
> **注:** いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @new_name = ] 'new_name'` ジョブの新しい名前。 *新しい名前*は**nvarchar (128)** します。  
  
`[ @enabled = ] enabled` ジョブが有効になっているかどうかを指定します (**1**) または有効になっていません (**0**)。 *有効になっている*は**tinyint**します。  
  
`[ @description = ] 'description'` ジョブの説明。 *説明*は**nvarchar (512)** します。  
  
`[ @start_step_id = ] step_id` ジョブで実行する最初のステップの識別番号。 *step_id*は**int**します。  
  
`[ @category_name = ] 'category'` ジョブのカテゴリ。 *カテゴリ*は**nvarchar (128)** します。  
  
`[ @owner_login_name = ] 'login'` ジョブを所有するログインの名前。 *ログイン*は**nvarchar (128)** のメンバーのみ、 **sysadmin**固定サーバー ロールは、ジョブの所有権を変更できます。  
  
`[ @notify_level_eventlog = ] eventlog_level` このジョブの Microsoft Windows アプリケーション ログにエントリを配置する場合を指定します。 *eventlog_level*は**int**、これらの値のいずれかを指定できます。  
  
|[値]|説明 (動作)|  
|-----------|----------------------------|  
|**0**|しない|  
|**1**|成功した場合|  
|**2**|エラー発生時|  
|**3**|常に|  
  
`[ @notify_level_email = ] email_level` このジョブの完了時に電子メールを送信するタイミングを指定します。 *email_level*は**int**します。*email_level*として同じ値を使用して*eventlog_level*します。  
  
`[ @notify_level_netsend = ] netsend_level` このジョブの完了時にネットワーク メッセージを送信するタイミングを指定します。 *netsend_level*は**int**します。*netsend_level*として同じ値を使用して*eventlog_level*します。  
  
`[ @notify_level_page = ] page_level` このジョブの完了時にページを送信するタイミングを指定します。 *page_level*は**int**します。*page_level*として同じ値を使用して*eventlog_level*します。  
  
`[ @notify_email_operator_name = ] 'operator_name'` 電子メールを送信するときにオペレーターの名前*email_level*に到達します。 *email_name*は**nvarchar (128)** します。  
  
`[ @notify_netsend_operator_name = ] 'netsend_operator'` ネットワーク メッセージを送信するオペレーターの名前。 *netsend_operator*は**nvarchar (128)** します。  
  
`[ @notify_page_operator_name = ] 'page_operator'` ページを送信するオペレーターの名前。 *page_operator*は**nvarchar (128)** します。  
  
`[ @delete_level = ] delete_level` ジョブを削除するかを指定します。 *delete_value*は**int**します。*delete_level*として同じ値を使用して*eventlog_level*します。  
  
`[ @automatic_post = ] automatic_post` 予約されています。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_update_job**から実行する必要があります、 **msdb**データベース。  
  
 **sp_update_job**パラメーター値が提供される設定のみを変更します。 パラメーターを省略すると、現在の設定は保持されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーだけ**sysadmin**このストアド プロシージャを使用して、他のユーザーによって所有されているジョブの属性を編集できます。  
  
## <a name="examples"></a>使用例  
 次の例では、名前、説明、およびジョブの有効な状態の変更`NightlyBackups`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
