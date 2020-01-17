---
title: query_store_wait_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6bff80fbe2b5022e12eca58de42192a3a1bb18d1
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190372"
---
# <a name="sysquery_store_wait_stats-transact-sql"></a>query_store_wait_stats (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  クエリの待機情報に関する情報を格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|Plan_id、runtime_stats_interval_id、execution_type、および wait_category の待機統計を表す行の識別子。 これは、過去の実行時統計の間隔に対してのみ一意です。 現在アクティブな間隔では、plan_id によって参照されるプランの待機統計を表す複数の行があり、execution_type によって表される実行の種類と wait_category によって表される待機カテゴリが含まれている場合があります。 通常、1つの行は、ディスクにフラッシュされる待機統計を表し、他の行はメモリ内の状態を表します。 このため、各間隔の実際の状態を取得するには、メトリックを集計し、plan_id、runtime_stats_interval_id、execution_type、および wait_category でグループ化する必要があります。 |  
|**plan_id**|**bigint**|外部キー。 [Query_store_plan &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)に結合します。|  
|**runtime_stats_interval_id**|**bigint**|外部キー。 [Query_store_runtime_stats_interval &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)に結合します。|  
|**wait_category**|**tinyint**|待機の種類は次の表を使用して分類され、待機時間はこれらの待機カテゴリ間で集計されます。 この問題を解決するには、異なる待機カテゴリで異なるフォローアップ分析が必要ですが、同じカテゴリの待機の種類は同様のトラブルシューティングエクスペリエンスをもたらし、待機に加えて影響を受けるクエリを提供します。このような調査の大半は正常に完了しました。|
|**wait_category_desc**|**nvarchar(128)**|[待機カテゴリ] フィールドの説明テキストを表示するには、次の表を確認してください。|
|**execution_type**|**tinyint**|クエリ実行の種類を決定します。<br /><br /> 0-通常の実行 (正常に完了)<br /><br /> 3-クライアントが開始した実行中止<br /><br /> 4-例外が実行を中止しました|  
|**execution_type_desc**|**nvarchar(128)**|実行の種類のフィールドの説明テキストです。<br /><br /> 0-標準<br /><br /> 3-中止<br /><br /> 4-例外|  
|**total_query_wait_time_ms**|**bigint**|集計`CPU wait`間隔および待機カテゴリ内のクエリプランの合計時間 (ミリ秒単位で報告)。|
|**avg_query_wait_time_ms**|**点**|集計間隔と待機カテゴリ内の実行ごとのクエリプランの平均待機時間 (ミリ秒単位で報告)。|
|**last_query_wait_time_ms**|**bigint**|集計間隔および待機カテゴリ内のクエリプランの最後の待機時間 (ミリ秒単位で報告)。|
|**min_query_wait_time_ms**|**bigint**|集計`CPU wait`間隔および待機カテゴリ内のクエリプランの最小時間 (ミリ秒単位で報告)。|
|**max_query_wait_time_ms**|**bigint**|集計`CPU wait`間隔および待機カテゴリ内のクエリプランの最大時間 (ミリ秒単位で報告)。|
|**stdev_query_wait_time_ms**|**点**|`Query wait`集計間隔および待機カテゴリ内のクエリプランの標準偏差 (ミリ秒単位で報告されます)。|

## <a name="wait-categories-mapping-table"></a>待機カテゴリマッピングテーブル

"%" はワイルドカードとして使用されます
  
|整数値|待機のカテゴリ|カテゴリには待機の種類が含まれます|  
|-----------------|---------------|-----------------|  
|**0**|**知ら**|Unknown の中から 1 つ以上を指定します |  
|**1 で保護されたプロセスとして起動されました**|**CPU**|SOS_SCHEDULER_YIELD|
|**3**|**ワーカースレッド**|THREADPOOL|
|**番**|**ロック**|LCK_M_%|
|**4/4**|**ラッチ**|LATCH_%|
|**5/5**|**バッファーラッチ**|PAGELATCH_%|
|**6**|**バッファー IO**|PAGEIOLATCH_%|
|**7**|**Asp.net***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR%、SQLCLR%|
|**9**|**ミラーリング**|DBMIRROR|
|**種類**|**取引**|XACT%、DTC%、TRAN_MARKLATCH_%、MSQL_XACT_%、TRANSACTION_MUTEX|
|**11**|**アイドル**|SLEEP_%、LAZYWRITER_SLEEP、SQLTRACE_BUFFER_FLUSH、SQLTRACE_INCREMENTAL_FLUSH_SLEEP、SQLTRACE_WAIT_ENTRIES、FT_IFTS_SCHEDULER_IDLE_WAIT、XE_DISPATCHER_WAIT、REQUEST_FOR_DEADLOCK_SEARCH、LOGMGR_QUEUE、ONDEMAND_TASK_QUEUE、CHECKPOINT_QUEUE、XE_TIMER_EVENT|
|**12**|**事前**|PREEMPTIVE_%|
|**第**|**Service Broker**|BROKER_% **(BROKER_RECEIVE_WAITFOR ではありません)**|
|**14**|**Tran Log IO**|LOGMGR、LOGMGR、LOGMGR_RESERVE_APPEND、LOGMGR_FLUSH、LOGMGR_PMM_LOG、CHKPT.、WRITELOG|
|**最大**|**ネットワーク IO**|ASYNC_NETWORK_IO、NET_WAITFOR_PACKET、PROXY_NETWORK_IO、EXTERNAL_SCRIPT_NETWORK_IOF|
|**まで**|**次数**|CXPACKET、EXCHANGE、HT%、BMP%、BP%|
|**a3**|**量**|RESOURCE_SEMAPHORE、CMEMTHREAD、CMEMPARTITIONED、EE_PMOLOCK、MEMORY_ALLOCATION_EXT、RESERVED_MEMORY_ALLOCATION_EXT、MEMORY_GRANT_UPDATE|
|**18**|**ユーザーの待機**|WAITFOR、WAIT_FOR_RESULTS、BROKER_RECEIVE_WAITFOR|
|**21**|**トレース**|TRACEWRITE、SQLTRACE_LOCK、SQLTRACE_FILE_BUFFER、SQLTRACE_FILE_WRITE_IO_COMPLETION、SQLTRACE_FILE_READ_IO_COMPLETION、SQLTRACE_PENDING_BUFFER_WRITERS、SQLTRACE_SHUTDOWN、QUERY_TRACEOUT、TRACE_EVTNOTIFF|
|**20@@**|**フルテキスト検索**|FT_RESTART_CRAWL、フルテキスト GATHERER、MSSEARCH、FT_METADATA_MUTEX、FT_IFTSHC_MUTEX、FT_IFTSISM_MUTEX、FT_IFTS_RWLOCK、FT_COMPROWSET_RWLOCK、FT_MASTER_MERGE、FT_PROPERTYLIST_CACHE、FT_MASTER_MERGE_COORDINATOR、PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC|
|**22**|**その他のディスク IO**|ASYNC_IO_COMPLETION、IO_COMPLETION、BACKUPIO、WRITE_COMPLETION、IO_QUEUE_LIMIT、IO_RETRY|
|**×**|**レプリケーション**|SE_REPL_%、REPL_%、HADR_% **(HADR_THROTTLE_LOG_RATE_GOVERNOR ではありません)**、PWAIT_HADR_%、REPLICA_WRITES、FCB_REPLICA_WRITE、FCB_REPLICA_READ、PWAIT_HADRSIM|
|**23**|**ログレートガバナー**|LOG_RATE_GOVERNOR、POOL_LOG_RATE_GOVERNOR、HADR_THROTTLE_LOG_RATE_GOVERNOR、INSTANCE_LOG_RATE_GOVERNOR|

**コンパイル**待機カテゴリは現在サポートされていません。

## <a name="permissions"></a>アクセス許可

 
  `VIEW DATABASE STATE` アクセス許可が必要です。  
  
## <a name="see-also"></a>参照

- [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
- [query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
- [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
- [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
- [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
- [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
- [クエリストアを使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Transact-sql&#41;&#40;カタログビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [Transact-sql&#41;&#40;のストアドプロシージャのクエリストア](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
