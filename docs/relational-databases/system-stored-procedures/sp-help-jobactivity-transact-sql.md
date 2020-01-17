---
title: sp_help_jobactivity (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
author: stevestein
ms.author: sstein
ms.openlocfilehash: 95283eee1a38dbafd9824986188df565103de06c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054977"
---
# <a name="sphelpjobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのランタイム状態に関する情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ジョブの識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @session_id = ] session_id` 情報をレポートするセッション id。 *session_id*は**int**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|エージェント セッションの id 番号。|  
|**job_id**|**uniqueidentifier**|ジョブの識別子。|  
|**job_name**|**sysname**|ジョブの名前。|  
|**run_requested_date**|**datetime**|ジョブの実行が要求された日付。|  
|**run_requested_source**|**sysname**|ジョブを実行する要求のソース。 次のいずれかです。<br /><br /> **1**スケジュールに基づいて実行を =<br /><br /> **2**アラートに対する応答の実行を =<br /><br /> **3**起動時に実行を =<br /><br /> **4**ユーザーが実行を =<br /><br /> **6** = CPU アイドル スケジュールに基づいて実行|  
|**queued_date**|**datetime**|要求がキューに登録された日付。 ジョブが直接実行された場合は NULL です。|  
|**start_execution_date**|**datetime**|ジョブが実行可能なスレッドに割り当てられるとき。|  
|**last_executed_step_id**|**int**|最も最近実行されたジョブ ステップのステップの ID。|  
|**last_exectued_step_date**|**datetime**|最後にジョブ ステップを開始した日付。|  
|**stop_execution_date**|**datetime**|ジョブが停止した日付。|  
|**next_scheduled_run_date**|**datetime**|ジョブは、次にスケジュール設定する場合。|  
|**job_history_id**|**int**|ジョブの履歴テーブルでのジョブ履歴の識別子です。|  
|**message**|**nvarchar(1024)**|メッセージは、ジョブの前回の実行中に生成されます。|  
|**run_status**|**int**|ジョブの最終実行の状態が返されます。<br /><br /> **0** = 失敗エラー<br /><br /> **1** = に成功しました<br /><br /> **3** = キャンセル<br /><br /> **5** = 状態不明|  
|**operator_id_emailed**|**int**|ジョブの完了時に電子メールの通知を受けたオペレーターの ID 番号。|  
|**operator_id_netsent**|**int**|使用して通知を受けたオペレーターの ID 番号**net send**ジョブの完了時にします。|  
|**operator_id_paged**|**int**|ジョブの完了時に、ポケットベルの通知を受けたオペレーターの ID 番号。|  
  
## <a name="remarks"></a>コメント  
 このプロシージャでは、ジョブに関する現在の状態のスナップショットが生成されます。 返される結果は、要求の処理時に情報を表します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、エージェント サービスが開始されるたびにセッション id を作成します。 セッション id がテーブルに格納されている**msdb.dbo.syssessions**します。  
  
 ない場合*session_id*が指定されて、最新のセッションに関する情報を表示します。  
  
 ない場合*job_name*または*job_id*が指定されて、すべてのジョブ情報を一覧表示します。  
  
## <a name="permissions"></a>アクセス許可  
 既定のメンバーで、 **sysadmin**固定サーバー ロールは、このストアド プロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーだけ**sysadmin**他のユーザーが所有するジョブの動作状況を表示できます。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のユーザーを表示する権限を持つすべてのジョブの利用状況が一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
