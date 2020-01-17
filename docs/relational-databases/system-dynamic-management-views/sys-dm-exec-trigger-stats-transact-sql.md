---
title: sys.dm_exec_trigger_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 65e54b90fa036e738f2e1e6a28498559051011a5
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262208"
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  キャッシュされたトリガーの集計パフォーマンス統計を返します。 ビューには、トリガーごとに 1 行が含まれていて、行の有効期間は、トリガーが残っている限りキャッシュします。 トリガーがキャッシュから削除されると、対応する行がこのビューから削除します。 その時点では、パフォーマンス統計 SQL トレース イベントが発生するのような**sys.dm_exec_query_stats**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|トリガーが存在するデータベース ID。|  
|**object_id**|**int**|トリガーのオブジェクト ID 番号。|  
|**type**|**char(2)**|次のいずれかのオブジェクトの種類。<br /><br /> TA = アセンブリ (CLR) トリガー<br /><br /> TR = SQL トリガー|  
|**Type_desc**|**nvarchar(60)**|オブジェクトの種類の説明です。<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|これでのクエリと関連付けるために使用できる**sys.dm_exec_query_stats**するは、このトリガー内から実行されました。|  
|**plan_handle**|**varbinary(64)**|メモリ内のプランの識別子。 この識別子は、一時的なプランをキャッシュに保持している間だけ一定のまま。 この値で使用できる、 **sys.dm_exec_cached_plans**動的管理ビュー。|  
|**cached_time**|**datetime**|トリガーがキャッシュに追加された時刻。|  
|**last_execution_time**|**datetime**|トリガーが実行された最終時刻。|  
|**execution_count**|**bigint**|以降、トリガーが実行された回数を最後にコンパイルします。|  
|**total_worker_time**|**bigint**|コンパイルされた後に、このトリガーの実行で使用されたマイクロ秒単位での CPU 時間の合計量。|  
|**last_worker_time**|**bigint**|前回トリガーの実行に使用された CPU 時間、マイクロ秒単位で。|  
|**min_worker_time**|**bigint**|最大の CPU 時間、1 回の実行中にこのトリガーで使用された (マイクロ秒)。|  
|**max_worker_time**|**bigint**|最大の CPU 時間、1 回の実行中にこのトリガーで使用された (マイクロ秒)。|  
|**total_physical_reads**|**bigint**|コンパイルされた後に、このトリガーの実行によって実行される物理読み取りの合計数。|  
|**last_physical_reads**|**bigint**|物理読み取りの数は、トリガーが実行された最終時刻を実行します。|  
|**min_physical_reads**|**bigint**|このトリガーで 1 回の実行中に行われた物理読み取りの最小数。|  
|**max_physical_reads**|**bigint**|このトリガーで 1 回の実行中に行われた物理読み取りの最大数。|  
|**total_logical_writes**|**bigint**|コンパイルされた後に、このトリガーの実行によって実行される論理書き込みの合計数。|  
|**last_logical_writes**|**bigint**|論理書き込みの数は、トリガーが実行された最終時刻を実行します。|  
|**min_logical_writes**|**bigint**|このトリガーで 1 回の実行中に行われた論理書き込みの最小数。|  
|**max_logical_writes**|**bigint**|このトリガーで 1 回の実行中に行われた論理書き込みの最大数。|  
|**total_logical_reads**|**bigint**|コンパイルされた後に、このトリガーの実行によって実行される論理読み取りの合計数。|  
|**last_logical_reads**|**bigint**|論理読み取りの数は、トリガーが実行された最終時刻を実行します。|  
|**min_logical_reads**|**bigint**|このトリガーで 1 回の実行中に行われた論理読み取りの最小数。|  
|**max_logical_reads**|**bigint**|このトリガーで 1 回の実行中に行われた論理読み取りの最大数。|  
|**total_elapsed_time**|**bigint**|このトリガーの実行完了のマイクロ秒単位で、合計経過時間。|  
|**last_elapsed_time**|**bigint**|このトリガーの最後に完了した実行のマイクロ秒単位の経過時間。|  
|**min_elapsed_time**|**bigint**|このトリガーの実行を完了する任意のマイクロ秒単位で、最小経過時間。|  
|**max_elapsed_time**|**bigint**|このトリガーの実行を完了する任意のマイクロ秒単位で、最大経過時間。| 
|**total_spills**|**bigint**|コンパイルされた後に、このトリガーの実行によって書き込まれたページの合計数。<br /><br /> **適用対象**:以降で[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|ページの数には、トリガーが実行された最終時刻が書き込まれます。<br /><br /> **適用対象**:以降で[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|このトリガーが 1 回の実行中に書き込まれたことがこれまでのページの最小数。<br /><br /> **適用対象**:以降で[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|このトリガーが 1 回の実行中に書き込まれたことがこれまでのページの最大数。<br /><br /> **適用対象**:以降で[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**total_page_server_reads**|**bigint**|コンパイルされた後に、このトリガーの実行によって実行されるページ サーバーの読み取りの合計数。<br /><br /> **適用対象**:Azure SQL データベースのハイパー スケール|  
|**last_page_server_reads**|**bigint**|サーバーのページ読み取りの数は、トリガーが実行された最終時刻を実行します。<br /><br /> **適用対象**:Azure SQL データベースのハイパー スケール|  
|**min_page_server_reads**|**bigint**|ページ サーバーの最小数は、このトリガーが 1 回の実行中に行われたことを読み取ります。<br /><br /> **適用対象**:Azure SQL データベースのハイパー スケール|  
|**max_page_server_reads**|**bigint**|ページ サーバーの最大数は、このトリガーが 1 回の実行中に行われたことを読み取ります。<br /><br /> **適用対象**:Azure SQL データベースのハイパー スケール|  

  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開することを避けるため、接続されているテナントに属していないデータが含まれるすべての行はフィルターで除外します。  

ビュー内の統計は、クエリが完了したときに更新されます。  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="examples"></a>使用例  
 次の例では、平均経過時間で識別される上位 5 つのトリガーに関する情報を返します。  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>関連項目  
[実行関連の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
