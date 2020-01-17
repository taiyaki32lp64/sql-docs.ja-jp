---
title: sys.dm_exec_background_job_queue (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09e760bac8e31ba9c78b9809a12f8d595b7ebd05
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263931"
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  非同期 (バックグラウンド) で実行するようスケジュール設定されたクエリ プロセッサ ジョブごとに 1 行のデータを返します。  
  
> **注:** これから **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** または **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** 、名前を使用して、 **sys.dm_pdw_nodes_exec_background_job_queue**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|ジョブがキューに追加された時刻。|  
|**job_id**|**int**|ジョブ識別子。|  
|**database_id**|**int**|ジョブが実行されるデータベース。|  
|**object_id1**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**object_id2**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**object_id3**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**object_id4**|**int**|値はジョブの種類によって異なります。 詳細については、「解説」を参照してください。|  
|**error_code**|**int**|ジョブが失敗し、再挿入された場合のエラー コード。 ジョブが中断したか、取得されていないか、完了している場合は NULL です。|  
|**request_type**|**smallint**|ジョブ要求の種類。|  
|**retry_count**|**smallint**|ジョブがキューから取得され、リソース不足またはその他の理由で再挿入された回数。|  
|**in_progress**|**smallint**|ジョブが実行を開始したかどうかを示します。<br /><br /> 1 = 開始<br /><br /> 0 = 待機中|  
|**session_id**|**smallint**|セッション識別子。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="remarks"></a>コメント  
 このビューは、統計の非同期更新ジョブに関する情報のみを返します。 統計の非同期更新の詳細については、次を参照してください。[統計](../../relational-databases/statistics/statistics.md)します。  
  
 値**object_id1**を通じて**object_id4**ジョブ要求の種類によって異なります。 次の表は、それぞれのジョブの種類の列に関する説明です。  
  
|要求の種類|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|統計の非同期更新|テーブルまたはビュー ID|統計 ID|使用しない|使用しない|  
  
## <a name="examples"></a>使用例  
 次の例では、アクティブな非同期ジョブの数を返しますのインスタンス内の各データベースのバック グラウンド キューに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [統計](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



