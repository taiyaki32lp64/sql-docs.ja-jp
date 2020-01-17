---
title: dbo.sysjobactivity (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 52d929496bf3db83dc63cdde6d86bf1a2ee1a3f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902219"
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの利用状況と状態を記録します。  このテーブルに格納されます、 **msdb**データベース。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|格納されているセッションの ID、 **syssessions**テーブルに、 **msdb**データベース。|  
|**job_id**|**uniqueidentifier**|ジョブの ID。|  
|**run_requested_date**|**datetime**|日付と、ジョブの実行が要求された時刻。|  
|**run_requested_source**|**sysname(nvarchar(128))**|ジョブの実行要求の発生元。<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|ジョブがキューに格納された日時。 場合は、ジョブを直接実行すると、この列は NULL です。|  
|**start_execution_date**|**datetime**|日付と時刻のジョブがスケジュールされて実行されます。|  
|**last_executed_step_id**|**int**|実行された最後のジョブ ステップの ID。|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|日付と最後のジョブ ステップの実行が開始された時刻。|  
|**stop_execution_date**|**datetime**|日付と時刻のジョブが実行を終了したこと。|  
|**job_history_id**|**int**|内の行を識別するために使用される、 **sysjobhistory**テーブル。|  
|**next_scheduled_run_date**|**datetime**|[次へ] の日付と時間、ジョブのスケジュールを設定します。|  

## <a name="example"></a>例
この例では、すべての SQL Server エージェント ジョブの実行時の状態を返します。  [!INCLUDE[tsql](../../includes/tsql-md.md)] で次の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を実行します。
```sql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>関連項目  
 [dbo.sysjobhistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
