---
title: dbo.sysjobhistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
author: stevestein
ms.author: sstein
ms.openlocfilehash: 85710deec2e7ab5e79ed7a514e3b625c6232484e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902199"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで実行予定のジョブに関する情報を格納します。
  
> [!NOTE]
> 基になるプロセスのケースがいくつかのジョブ ステップが完了するし、表に、通常が含まれていないレコードが現在進行中のジョブ ステップの専用ほとんどの場合、データが更新された*は*で情報を提供実行中のジョブ ステップ。

このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|行の一意識別子。|  
|**job_id**|**uniqueidentifier**|ジョブ ID。|  
|**step_id**|**int**|ジョブ ステップの ID。|  
|**step_name**|**sysname**|ステップの名前。|  
|**sql_message_id**|**int**|任意の ID[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ジョブが失敗したかどうかにエラー メッセージが返されます。|  
|**sql_severity**|**int**|いずれかの重要度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エラー。|  
|**message**|**nvarchar (4000)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーのテキスト (存在する場合)。|  
|**run_status**|**int**|ジョブ実行のステータス。<br /><br /> **0** = に失敗しました<br /><br /> **1** = に成功しました<br /><br /> **2** = 再試行<br /><br /> **3** = キャンセル<br /><br />**4** = 実行中|  
|**run_date**|**int**|日付と、ジョブまたはステップ実行を開始しました。 進行中の場合は、履歴に書き込まれた日付/時刻です。|  
|**run_time**|**int**|ジョブまたはステップが実行を開始した時刻。|  
|**run_duration**|**int**|ジョブまたはステップの実行の経過時間**HHMMSS**形式。|  
|**operator_id_emailed**|**int**|ジョブが完了したときに通知を受けたオペレーターの ID。|  
|**operator_id_netsent**|**int**|メッセージによって、ジョブが完了したときに通知を受けたオペレーターの ID。|  
|**operator_id_paged**|**int**|ジョブの終了時にポケットベルの通知を受けるオペレーターの ID。|  
|**retries_attempted**|**int**|ジョブまたはステップの再試行回数。|  
|**server**|**sysname**|ジョブが実行されたサーバーの名前です。|  
  
  ## <a name="example"></a>例
 次[!INCLUDE[tsql](../../includes/tsql-md.md)]クエリに変換されます、 **run_time の期限**と**run_duration**列以上のユーザー フレンドリな形式にします。  スクリプトを実行[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
