---
title: sp_help_jobhistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 10033b2525ba28e79bd31a73bd9e71a7cca15e42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054931"
---
# <a name="sphelpjobhistory-transact-sql"></a>sp_help_jobhistory (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マルチサーバー管理ドメインに所属するサーバーのジョブに関する情報を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ジョブの識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
`[ @step_id = ] step_id` ステップの識別番号。 *step_id*は**int**、既定値は NULL です。  
  
`[ @sql_message_id = ] sql_message_id` ジョブを実行するときに、Microsoft SQL Server によって返されるエラー メッセージの識別番号。 *sql_message_id*は**int**、既定値は NULL です。  
  
`[ @sql_severity = ] sql_severity` ジョブを実行するときに、SQL Server によって返されるエラー メッセージの重大度レベル。 *sql_severity*は**int**、既定値は NULL です。  
  
`[ @start_run_date = ] start_run_date` ジョブが開始された日付。 *start_run_date*は**int**、既定値は NULL です。 *start_run_date*必要があります形式で入力 yyyymmdd 形式で指定、YYYY は 4 桁の年、MM は 2 桁の月、DD は 2 桁の日の名前。  
  
`[ @end_run_date = ] end_run_date` ジョブが完了した日付。 *end_run_date*は**int**、既定値は NULL です。 *end_run_date*必要があります形式で入力 yyyymmdd 形式で指定、YYYY は 4 桁の年、MM は 2 桁の月、DD は 2 桁の日の名前。  
  
`[ @start_run_time = ] start_run_time` ジョブが開始された時刻。 *start_run_time*は**int**、既定値は NULL です。 *start_run_time*必要があります形式で入力 hhmmss で、HH は、1 日の 2 文字の 1 時間、MM は、1 日の 2 桁の分 SS は、1 日の 2 桁の秒。  
  
`[ @end_run_time = ] end_run_time` ジョブの実行を完了した時刻。 *end_run_time*は**int**、既定値は NULL です。 *end_run_time*必要があります形式で入力 hhmmss で、HH は、1 日の 2 文字の 1 時間、MM は、1 日の 2 桁の分 SS は、1 日の 2 桁の秒。  
  
`[ @minimum_run_duration = ] minimum_run_duration` ジョブの終了までの時間の最小長。 *minimum_run_duration*は**int**、既定値は NULL です。 *minimum_run_duration*必要があります形式で入力 hhmmss で、HH は、1 日の 2 文字の 1 時間、MM は、1 日の 2 桁の分 SS は、1 日の 2 桁の秒。  
  
`[ @run_status = ] run_status` ジョブの実行状態。 *run_status*は**int**、既定値は null の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|Failed|  
|**1**|成功しました|  
|**2**|再試行 (ステップのみ)|  
|**3**|Canceled|  
|**4**|実行中のメッセージ|  
|**5**|Unknown|  
  
`[ @minimum_retries = ] minimum_retries` ジョブが実行を再試行する最小回数。 *minimum_retries*は**int**、既定値は NULL です。  
  
`[ @oldest_first = ] oldest_first` 最初に出力された最も古いジョブを表示するかどうかです。 *oldest_first*は**int**、既定値は**0**、最初、最新のジョブを提供します。 **1**最初に、最も古いジョブを表示します。  
  
`[ @server = ] 'server'` ジョブが実行されたサーバーの名前。 *server*は**nvarchar (30)** 、既定値は NULL です。  
  
`[ @mode = ] 'mode'` SQL Server が、結果セット内のすべての列を出力するかどうか (**完全**) または列の概要。 *モード*は**varchar (7)** 、既定値は**概要**します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 実際の列の一覧は、の値によって異なります。*モード*します。 列の最も包括的なセットを次に示します、ときに返される*モード*いっぱいです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|履歴エントリの識別番号。|  
|**job_id**|**uniqueidentifier**|ジョブ識別番号。|  
|**job_name**|**sysname**|ジョブの名前。|  
|**step_id**|**int**|ステップ識別番号 (なります**0**ジョブ履歴の)。|  
|**step_name**|**sysname**|ステップ名。ジョブ履歴の場合は NULL です。|  
|**sql_message_id**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合、コマンドの実行中に最も新しく発生した [!INCLUDE[tsql](../../includes/tsql-md.md)] エラーの番号。|  
|**sql_severity**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合、コマンドの実行中に発生した最も重大な [!INCLUDE[tsql](../../includes/tsql-md.md)] エラーの重大度。|  
|**message**|**nvarchar(1024)**|ジョブまたはステップの履歴メッセージ。|  
|**run_status**|**int**|ジョブまたはステップの結果。|  
|**run_date**|**int**|日付と、ジョブまたはステップが実行を開始します。|  
|**run_time**|**int**|ジョブまたはステップが実行を開始します。|  
|**run_duration**|**int**|ジョブまたはステップを実行してからの経過時間 (HHMMSS 形式)。|  
|**operator_emailed**|**nvarchar(20)**|このジョブに関する電子メールを送信したオペレーター (ステップ履歴の場合は NULL)。|  
|**operator_netsent**|**nvarchar(20)**|このジョブに関するネットワーク メッセージを送信したオペレーター (ステップ履歴の場合は NULL)。|  
|**operator_paged**|**nvarchar(20)**|このジョブに関するページを送信したオペレーター (ステップ履歴の場合は NULL)。|  
|**retries_attempted**|**int**|ステップの再試行回数 (常にジョブ履歴の 0)。|  
|**server**|**nvarchar(30)**|サーバーのステップまたはジョブを実行します。 常に (**ローカル**)。|  
  
## <a name="remarks"></a>コメント  
 **sp_help_jobhistory**指定のスケジュールされたジョブの履歴レポートを返します。 どのパラメーターも指定しない場合は、レポートにはすべての定期ジョブの履歴が含まれます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバー、 **SQLAgentUserRole**データベース ロールは、自分が所有しているジョブの履歴のみを表示できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. ジョブのジョブ情報をすべて一覧表示  
 次の例は、すべてのジョブ情報を一覧表示、`NightlyBackups`ジョブ。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>B. 一定の条件に一致するジョブに関する情報を一覧表示する  
 次の例は、すべての列を出力しのすべてのジョブ情報が失敗したジョブとジョブ ステップのエラー メッセージで失敗しました`50100`(ユーザー定義エラー メッセージ) と重大度`20`します。  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
