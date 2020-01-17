---
title: dbo.sysjobsteps (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
author: stevestein
ms.author: sstein
ms.openlocfilehash: 13cf57e181c3fbb1371c10b554eb9da344a951d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004735"
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって実行されるジョブ内の各ステップに関する情報を格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの ID。|  
|**step_id**|**int**|ジョブ ステップの ID。|  
|**step_name**|**sysname**|ジョブ ステップの名前です。|  
|**subsystem**|**nvarchar(40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがジョブ ステップを実行するために使用するサブシステムの名前。|  
|**command**|**nvarchar(max)**|によって実行されるコマンド**サブシステム**します。|  
|**flags**|**int**|予約済み。|  
|**additional_parameters**|**ntext**|予約済み。|  
|**cmdexec_success_code**|**int**|によって返されるエラー レベル値**CmdExec**サブシステム ステップが成功を示します。|  
|**on_success_action**|**tinyint**|ステップが正常に実行されたときに実行するアクション。|  
|**on_success_step_id**|**int**|ステップが正常に実行されたときに実行する次のステップの ID。|  
|**on_fail_action**|**tinyint**|ステップが正常に実行されない場合に実行するアクション。|  
|**on_fail_step_id**|**int**|ステップが正常に実行されないときに実行する次のステップの ID。|  
|**server**|**sysname**|予約済み。|  
|**database_name**|**sysname**|データベースの名前**コマンド**場合に実行されます**サブシステム**TSQL です。|  
|**database_user_name**|**sysname**|手順を実行するときにアカウントが使用するデータベース ユーザーの名前です。|  
|**retry_attempts**|**int**|ステップが失敗した場合に行う再試行の数。|  
|**retry_interval**|**int**|再試行間の待機時間の長さ。|  
|**os_run_priority**|**int**|予約済み。|  
|**output_file_name**|**nvarchar(200)**|ステップの出力ファイルの名前が保存された**サブシステム**が TSQL、PowerShell、または**CmdExec**_します。_|  
|**last_run_outcome**|**int**|ジョブ ステップの前回の実行結果。<br /><br /> **0** = に失敗しました<br /><br /> **1** = に成功しました<br /><br /> **2** = 再試行<br /><br /> **3** = キャンセル<br /><br /> **5** = unknown|  
|**last_run_duration**|**int**|実行時間 (hhmmss) のステップの前回の実行時。|  
|**last_run_retries**|**int**|ジョブ ステップの前回の実行で再試行の回数。|  
|**last_run_date**|**int**|ステップの実行を最後に開始した日付 (yyyymmdd)。|  
|**last_run_time**|**int**|時刻 (hhmmss) に、最後に実行を開始します。|  
|**proxy_id**|**int**|ジョブ ステップのプロキシ。|  
|**step_uid**|**uniqueidentifier**|ジョブ ステップの識別子。|  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
