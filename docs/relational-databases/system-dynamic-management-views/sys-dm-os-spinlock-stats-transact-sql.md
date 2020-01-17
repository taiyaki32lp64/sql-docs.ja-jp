---
title: sys.dm_os_spinlock_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
author: bluefooted
ms.author: pamela
ms.reviewer: maghan
manager: amitban
ms.openlocfilehash: eae0057441fe6bc356c7cea6c1e6ded829bbb9e6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265686"
---
# <a name="sysdmosspinlockstats-transact-sql"></a>sys.dm_os_spinlock_stats (TRANSACT-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

種類別に整理するすべてのスピン ロック待機に関する情報を返します。  
  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar (256)**|スピンロックの種類の名前です。|  
|競合|**bigint**|スレッドが、スピン ロックの取得を試みる、ため、現在別のスレッドがブロックされている回数には、スピンロックが保持されます。|  
|回転します。|**bigint**|スレッドの時間数では、スピンロックの取得を試みているときに、ループを実行します。|  
|spins_per_collision|**real**|競合あたりの回転の比率です。|  
|sleep_time|**bigint**|スレッドがスリープ、バックオフが発生した場合にかかったミリ秒単位の時間。|  
|バックオフ|**int**|「回転」スレッドが、スピンロックの取得に失敗して、スケジューラが得られます回数。|  


## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。    
  
## <a name="remarks"></a>コメント  
 
 sys.dm_os_spinlock_stats は、スピンロックの競合の原因を識別するために使用できます。 状況によっては、解決またはスピンロックの競合を緩和することができます。 ただし、状況もあります。 が必要になることにお問い合わせください[!INCLUDE[msCoName](../../includes/msconame-md.md)]カスタマー サポート サービス。  
  
 Sys.dm_os_spinlock_stats の内容をリセットするにを使用して`DBCC SQLPERF`次のようにします。  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 これにより、すべてのカウンターが 0 にリセットされます。  
  
> [!NOTE]  
>  これらの統計は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動されると保存されません。 すべてのデータが、前回の統計がリセットされた後、または累積的な[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]開始されました。  
  
## <a name="spinlocks"></a>スピンロック  
 スピンロックは、通常短時間保持されたデータ構造体へのアクセスをシリアル化に使用される軽量の同期オブジェクトです。 スレッドが別のスレッドによって保持されるスピン ロックで保護されているリソースにアクセスしようとすると、スレッドは、ループを実行または「起動」とすぐにラッチやその他のリソースと同様にスケジューラが生成するのではなくリソースにアクセスして、もう一度お試しください。お待ちください。 スレッドは、スピンまで、リソースが使用可能なまたは、ループが完了したら、この時点でスレッド スケジューラが、実行可能キューに戻って続けます。 この実習は、過度にスレッド コンテキストの切り替えを削減に役立ちますが、スピンロックの競合が高いとき、CPU 使用率の大幅ななることがあります。
   
 次の表には、最も一般的なスピンロックの種類のいくつかの簡単な説明が含まれています。  
  
|スピンロックの種類|説明|  
|-----------------|-----------------|  
|ABR|内部使用のみです。|
|ADB_CACHE|内部使用のみです。|
|ALLOC_CACHES_HASH|内部使用のみです。|
|APPENDONLY_STORAGE|内部使用のみです。|
|APRC_BACK_OFF_STATS|内部使用のみです。|
|APRC_EVENT_LIST|内部使用のみです。|
|APRC_QUEUE_LIST|内部使用のみです。|
|APRC_VALIDATION_QUEUE_LIST|内部使用のみです。|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|内部使用のみです。|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|内部使用のみです。|
|ASYNCSTATSLIST|内部使用のみです。|
|BACKUP|内部使用のみです。|
|BACKUP_COPY_CONTEXT|内部使用のみです。|
|BACKUP_CTX|内部使用のみです。|
|BASE_XACT_HASH|内部使用のみです。|
|BLOCKER_ENUM|内部使用のみです。|
|BPREPARTITION|内部使用のみです。|
|BPWORKFILE|内部使用のみです。|
|BUF_HASH|内部使用のみです。|
|BUF_LINK|内部使用のみです。|
|BUF_WRITE_LOG|内部使用のみです。|
|CACHEOBJ_DBG|内部使用のみです。|
|CHANNELFORCECLOSEMANAGER|内部使用のみです。|
|CHECK_AGGREGATE_STATE|内部使用のみです。|
|CLR_HOSTTASK|内部使用のみです。|
|CLR_SPIN_LOCK|内部使用のみです。|
|CMED_DATABASE|内部使用のみです。|
|CMED_HASH_SET|内部使用のみです。|
|COLUMNDATASETSESSIONLIST|内部使用のみです。|
|COLUMNSTORE_HASHTABLE|内部使用のみです。|
|COLUMNSTOREBUILDSTATE_LIST|内部使用のみです。|
|COM_INIT|内部使用のみです。|
|コミット|内部使用のみです。|
|COMPPLAN_SKELETON|内部使用のみです。|
|CONNECTION_MANAGER|内部使用のみです。|
|接続します。|内部使用のみです。|
|CSIBUILDMEM|内部使用のみです。|
|CURSOR|内部使用のみです。|
|CURSQL|内部使用のみです。|
|DATAPORTCONSUMER|内部使用のみです。|
|DATAPORTSOURCEINFOCREDIT|内部使用のみです。|
|DATAPORTSOURCEINFOQUEUE|内部使用のみです。|
|DATASET_FREELIST|内部使用のみです。|
|DBCC_CHECK|内部使用のみです。|
|DBSEEDING_OPERATION|内部使用のみです。|
|DBT_HASH|内部使用のみです。|
|DBT_IO_LIST|内部使用のみです。|
|DBTABLE|そのデータベースのプロパティを含む SQL Server 内の各データベースのインメモリ データ構造体へのアクセスを制御します。 参照してください[今回](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789)詳細についてはします。 |
|DEFERRED_WF_EXT_DROP|内部使用のみです。|
|DEK_INSTANCE|内部使用のみです。|
|DELAYED_PARTITIONED_STACK|内部使用のみです。|
|DELETEBITMAP|内部使用のみです。|
|DIAG_MANAGER|内部使用のみです。|
|DIAG_OBJECT|内部使用のみです。|
|DIGEST_CACHE|内部使用のみです。|
|DINPBUF|内部使用のみです。|
|DIRECTLOGCONSUMER|内部使用のみです。|
|DP_LIST|間接チェックポイントが有効であるデータベースのダーティ ページの一覧へのアクセスを制御します。 参照してください[今回](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510)詳細についてはします。|
|DROP|内部使用のみです。|
|DROP_TEMPO|内部使用のみです。|
|DROPPED_ALLOC_UNIT|内部使用のみです。|
|DTC_HASHTABLE|内部使用のみです。|
|DTT_LIST|内部使用のみです。|
|ENDD_LIST|内部使用のみです。|
|EXT_CACHE|内部使用のみです。|
|EXTENT_ACTIVATION|内部使用のみです。|
|FABRIC_DB_MGR_PTR|内部使用のみです。|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|内部使用のみです。|
|FABRIC_REPLICA_TRANSPORT|内部使用のみです。|
|FABRIC_TVF_DATA_CONSUMER_LIST|内部使用のみです。|
|FABRIC_TVF_LOAD_LIB|内部使用のみです。|
|FCB_REPLICA_SYNC|内部使用のみです。|
|FGCB_PRP_FILL|内部使用のみです。|
|FILE_HANDLE_CACHE|内部使用のみです。|
|FILE_TABLE|内部使用のみです。|
|FILESTREAM_CHUNKER|内部使用のみです。|
|FREE_SPACE_CACHE_ENTRY|内部使用のみです。|
|FS_CONTAINER_LIST_WITH_DELETE|内部使用のみです。|
|FS_DELETED_FOLDER_CLEANUP|内部使用のみです。|
|FSAGENT|内部使用のみです。|
|FSGHOST_STATUS|内部使用のみです。|
|FT_INIT|内部使用のみです。|
|GHOST_FREE|内部使用のみです。|
|GHOST_HASH|内部使用のみです。|
|GLOBAL_SCHEDULER_LIST|内部使用のみです。|
|GLOBAL_TRACE_FLAGS|内部使用のみです。|
|GLOBALTRANS|内部使用のみです。|
|GROUP_COMMIT_FEEDBACK_LOOP|内部使用のみです。|
|GUARDIAN|内部使用のみです。|
|HADR_AGH_X_ACCESS|内部使用のみです。|
|HADR_AR_CONTROLLER_COLLECTION|内部使用のみです。|
|HADR_AR_DB_MGR|内部使用のみです。|
|HADR_AR_TRANSPORT|内部使用のみです。|
|HADR_COMPRESSION_MGR_POOL|内部使用のみです。|
|HADR_FABRIC_FACTORY|内部使用のみです。|
|HADR_PRIORITY_QUEUE|内部使用のみです。|
|HADR_TRANSPORT_CONTROL|内部使用のみです。|
|HADR_TRANSPORT_LIST|内部使用のみです。|
|HADRSEEDINGLIST|内部使用のみです。|
|HOBT_DROPPED|内部使用のみです。|
|HOBT_HASH|内部使用のみです。|
|HTTP|内部使用のみです。|
|HTTP_CONNCACHE|内部使用のみです。|
|HTTP_ENDPOINT|内部使用のみです。|
|IDENTITY|内部使用のみです。|
|INDEX_CREATE|内部使用のみです。|
|IO_DISPENSER_PAUSE|内部使用のみです。|
|IO_RG_VOLUME_HASHTABLE|内部使用のみです。|
|IOREQ|内部使用のみです。|
|ISSRESOURCE|内部使用のみです。|
|KTM_ENLISTMENT|内部使用のみです。|
|LANG_RES_LOAD|内部使用のみです。|
|LIVE_TARGET_TVF|内部使用のみです。|
|LOCK_FREE_LIST|内部使用のみです。|
|LOCK_HASH|データベースに保持されているロックに関する情報を格納するロック マネージャーのハッシュ テーブルへのアクセスを保護します。 参照してください[今回](https://support.microsoft.com/kb/2926217)詳細についてはします。|
|LOCK_NOTIFICATION|内部使用のみです。|
|LOCK_RESOURCE_ID|内部使用のみです。|
|LOCK_RW_ABTX_HASH_SET|内部使用のみです。|
|LOCK_RW_AGDB_HEALTH_DIAG|内部使用のみです。|
|LOCK_RW_CMED_HASH_SET|内部使用のみです。|
|LOCK_RW_DPT_TABLE|内部使用のみです。|
|LOCK_RW_IN_ROW_TRACKER|内部使用のみです。|
|LOCK_RW_LOGIN_RATE_STATS|内部使用のみです。|
|LOCK_RW_PVS_PAGE_TRACKER|内部使用のみです。|
|LOCK_RW_RBIO_REQ|内部使用のみです。|
|LOCK_RW_SECURITY_CACHE|内部使用のみです。|
|LOCK_RW_TEST|内部使用のみです。|
|LOCK_RW_WPR_BUCKET|内部使用のみです。|
|LOCK_SORT_STREAM|内部使用のみです。|
|LOCK_SQLSATELLITE_MESSAGE|内部使用のみです。|
|LOG_CONSOLIDATION|内部使用のみです。|
|LOG_RG_GOVERNOR|内部使用のみです。|
|LOGCACHE_ACCESS|内部使用のみです。|
|LOGFLUSHQ|内部使用のみです。|
|LOGIOSEQ|内部使用のみです。|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|内部使用のみです。|
|LOGLC|内部使用のみです。|
|LOGLFM|内部使用のみです。|
|LOGON_TRIGGER_CACHE|内部使用のみです。|
|LOGPOOL_HASHBUCKET|内部使用のみです。|
|LOGPOOL_REFCOUNTEDOBJECT|内部使用のみです。|
|LOGPOOL_SHAREDCACHEBUFFER|内部使用のみです。|
|LOGPOOL_SIZEPERRESOURCEPOOL|内部使用のみです。|
|LPE_BATCH|内部使用のみです。|
|LPE_SESSION|内部使用のみです。|
|LPE_SXTP|内部使用のみです。|
|LSID|内部使用のみです。|
|LSLIST|内部使用のみです。|
|LSNREFLIST|内部使用のみです。|
|LSS_SYNC_DTC|内部使用のみです。|
|MD_CHANGE_NOTIFICATION|内部使用のみです。|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|内部使用のみです。|
|MDB_REMOTE_SESSION_HASH_TABLE|内部使用のみです。|
|MEM_MGR|内部使用のみです。|
|MGR_CACHE|内部使用のみです。|
|MIGRATION_BUF_LIST|内部使用のみです。|
|NETCONN_ADDRESS|内部使用のみです。|
|ONDEMAND_TASK|内部使用のみです。|
|ONE_PROC_SIM_NODE_CONTEXT|内部使用のみです。|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|内部使用のみです。|
|ONE_PROC_SIM_REPLICA_CONTEXT|内部使用のみです。|
|ONE_PROC_SIM_SERVICE_PARTITION|内部使用のみです。|
|OPT_IDX_MISS_ID|内部使用のみです。|
|OPT_IDX_MISS_KEY|内部使用のみです。|
|OPT_IDX_STATS|内部使用のみです。|
|OPT_INFO_MGR|内部使用のみです。|
|PAGE_WORKITEMLIST|内部使用のみです。|
|PAGECOPIER|内部使用のみです。|
|PARALLELREDOCACHE|内部使用のみです。|
|PARTITIONED_HEAP_FREE_LIST|内部使用のみです。|
|PROGRESS_REPORT|内部使用のみです。|
|QE_SHUTDOWN|内部使用のみです。|
|QSCAN_CACHE|内部使用のみです。|
|QUERY_EXEC_STATS|内部使用のみです。|
|QUERY_STORE_ASYNC_PERSIST|内部使用のみです。|
|QUERY_STORE_ASYNC_QUEUE_TLIST|内部使用のみです。|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|内部使用のみです。|
|QUERY_STORE_CAPTURE_POLICY_STATS|内部使用のみです。|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|内部使用のみです。|
|QUERY_STORE_CURRENT_INTERVAL|内部使用のみです。|
|QUERY_STORE_HT_CACHE|内部使用のみです。|
|QUERY_STORE_LIST|内部使用のみです。|
|QUERY_STORE_PLAN_COMP_AGG|内部使用のみです。|
|QUERY_STORE_PLAN_LIST|内部使用のみです。|
|QUERY_STORE_READ_ONLY_FLAGS|内部使用のみです。|
|QUERY_STORE_SELF_AGG|内部使用のみです。|
|QUERY_STORE_STMT_COMP_AGG|内部使用のみです。|
|QUERYEXEC|内部使用のみです。|
|QUERYSCAN|内部使用のみです。|
|RANGE_GENERATION|内部使用のみです。|
|READ_AHEAD|内部使用のみです。|
|REDOMGRSTATE|内部使用のみです。|
|REMOTE_SESSION_CACHE|内部使用のみです。|
|REMOTEBLOCKIO|内部使用のみです。|
|REMOTEOP|内部使用のみです。|
|REPL_LOGREADER_HISTORY_CACHE|内部使用のみです。|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|内部使用のみです。|
|RESMANAGER|内部使用のみです。|
|リソース|内部使用のみです。|
|RESQUEUE|内部使用のみです。|
|RFS_THREAD_QUEUE|内部使用のみです。|
|RG_TIMER|内部使用のみです。|
|ROWGROUP_VERSIONS|内部使用のみです。|
|RPCCHANNELPOOL|内部使用のみです。|
|RPCPACKAGE|内部使用のみです。|
|RPCREQUESTORCONTEXT|内部使用のみです。|
|RWLOCK_LAST|内部使用のみです。|
|SATELLITE_CONNECTION|内部使用のみです。|
|SBS_CLIENT_ENDPOINTS|内部使用のみです。|
|SBS_CLIENT_REQUESTS|内部使用のみです。|
|SBS_DISPATCH|内部使用のみです。|
|SBS_PENDING|内部使用のみです。|
|SBS_SERVER_XACT_TASK_PROXY|内部使用のみです。|
|SBS_TRANSPORT|内部使用のみです。|
|SBS_UCS_DISPATCH|内部使用のみです。|
|セキュリティ|内部使用のみです。|
|SECURITY_CACHE|内部使用のみです。|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|内部使用のみです。|
|SEMANTIC_TICACHE|内部使用のみです。|
|SEQUENCED_OBJECT|内部使用のみです。|
|SEQUEUE_SIZED_THREADSAFE|内部使用のみです。|
|SESSION_KILLER|内部使用のみです。|
|SESSION_MANAGER|内部使用のみです。|
|SESSION_SEC_CONTEXT|内部使用のみです。|
|SETRANGE_SYNC|内部使用のみです。|
|SHARABLE_SESSION_OBJECTS|内部使用のみです。|
|SLO_INFO_LIST|内部使用のみです。|
|SNI|内部使用のみです。|
|SNI_NODE_PENDING_IO_QUEUE|内部使用のみです。|
|SOAPSESSIONS|内部使用のみです。|
|SOS_ABORT_TASK|内部使用のみです。|
|SOS_ACTIVEDESCRIPTOR|内部使用のみです。|
|SOS_BLOCKALLOCPARTIALLIST|内部使用のみです。|
|SOS_BLOCKDESCRIPTORBUCKET|内部使用のみです。|
|SOS_CACHESTORE|SQL server プラン キャッシュ、一時テーブル キャッシュなどのさまざまなのインメモリ キャッシュへのアクセスを同期します。 この種類のスピンロックで多数の競合は競合では、特定のキャッシュによって、さまざまなことを意味します。 連絡先[!INCLUDE[msCoName](../../includes/msconame-md.md)]このスピンロックの種類のトラブルシューティングについてカスタマー サポート サービス。 |
|SOS_CACHESTORE_CLOCK|内部使用のみです。|
|SOS_CLOCKALG_INTERNODE_SYNC|内部使用のみです。|
|SOS_DEBUG_HOOK|内部使用のみです。|
|SOS_DESCDATABUFFERLIST|内部使用のみです。|
|SOS_LARGEPAGE_ALLOCATOR|内部使用のみです。|
|SOS_MINITHREAD|内部使用のみです。|
|SOS_NODE|内部使用のみです。|
|SOS_OBJECT_POOL|内部使用のみです。|
|SOS_OBJECT_STORE|内部使用のみです。|
|SOS_OOM_CHECK|内部使用のみです。|
|SOS_PHYS_PAGE_CACHE|内部使用のみです。|
|SOS_RESOURCE_CLERK_LIST|内部使用のみです。|
|SOS_RINGBUFFER_RECORD|内部使用のみです。|
|SOS_RW|内部使用のみです。|
|SOS_SATELLITE_USER_POOL|内部使用のみです。|
|SOS_SCHEDULER|内部使用のみです。|
|SOS_SELIST_SIZED_SLOCK|内部使用のみです。|
|SOS_SUSPEND_QUEUE|内部使用のみです。|
|SOS_SYSTHREAD|内部使用のみです。|
|SOS_SYSTHREAD_DISPATCHER|内部使用のみです。|
|SOS_TASK|内部使用のみです。|
|SOS_TLIST|内部使用のみです。|
|SOS_VM_LOW|内部使用のみです。|
|SOS_WAIT_STATS|内部使用のみです。|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|内部使用のみです。|
|SPIN_EVENT_MUTEX|内部使用のみです。|
|SPL_DISPATCHER_LIST|内部使用のみです。|
|SPL_DISPATCHER_QUEUE|内部使用のみです。|
|SPL_NONYIELD_ANALYSIS|内部使用のみです。|
|SPL_QUERY_STORE_CTX_INITIALIZED|内部使用のみです。|
|SPL_QUERY_STORE_EXEC_STATS_AGG|内部使用のみです。|
|SPL_QUERY_STORE_EXEC_STATS_READ|内部使用のみです。|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|内部使用のみです。|
|SPL_SOS_DISPATCHER|内部使用のみです。|
|SPL_TDS_PKT_QUEUE|内部使用のみです。|
|SPL_XE_BUFFER_MGR|内部使用のみです。|
|SPL_XE_DISPATCHER_QUEUE|内部使用のみです。|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|内部使用のみです。|
|SPL_XE_SESSION_EVENT_MGR|内部使用のみです。|
|SPL_XE_SESSION_MGR|内部使用のみです。|
|SPL_XE_SESSION_TARGET_MGR|内部使用のみです。|
|SPT_PROFILE|内部使用のみです。|
|SQL_MGR|内部使用のみです。|
|SQL_NORM|内部使用のみです。|
|SQLTRACE_FILE_BUFFER|内部使用のみです。|
|SRVPROC|内部使用のみです。|
|STACK_HASHER|内部使用のみです。|
|SUBLATCH|内部使用のみです。|
|SUBPDESC|内部使用のみです。|
|SUBPDESC_LIST|内部使用のみです。|
|SVC_BROKER_CTRL|内部使用のみです。|
|SVC_BROKER_DEBUG_LIST|内部使用のみです。|
|SVC_BROKER_LIST|内部使用のみです。|
|SVC_BROKER_OBJECT|内部使用のみです。|
|SYNCPOINT_RESOURCE|内部使用のみです。|
|TaskElapsedExecutionMonitor|内部使用のみです。|
|TDS_TVP|内部使用のみです。|
|TESTTEAM|内部使用のみです。|
|TESTTEAMEXPONENTIAL|内部使用のみです。|
|TESTTEAMEXPONENTIALTASTAS|内部使用のみです。|
|TESTTEAMTASTAS|内部使用のみです。|
|TMP_SESS_KEY|内部使用のみです。|
|TSQL_DEBUG|内部使用のみです。|
|TXFRM_REPL|内部使用のみです。|
|VDI_OPERATION|内部使用のみです。|
|WINFAB_REPORT_FAULT|内部使用のみです。|
|WRITE_PAGE_RECORDER|内部使用のみです。|
|X_PACKET_LIST|内部使用のみです。|
|X_PIPE|内部使用のみです。|
|X_PIPE_DEMAND|内部使用のみです。|
|X_PORT|内部使用のみです。|
|XACT_LOCK_INFO|内部使用のみです。|
|XACT_LOCKINFO_TASK|内部使用のみです。|
|XACT_WORKSPACE|内部使用のみです。|
|XCB|内部使用のみです。|
|XCB_FREE_LIST|内部使用のみです。|
|XCB_HASH|内部使用のみです。|
|XCHNG_TRACE|内部使用のみです。|
|XDES|内部使用のみです。|
|XDES_HASH|内部使用のみです。|
|XDESMGR|内部使用のみです。|
|XDESTABLELIST|内部使用のみです。|
|XE_RATE_LIMITER_STRETCHDB|内部使用のみです。|
|XE_SESSION_STORAGE|内部使用のみです。|
|XID_ARRAY|内部使用のみです。|
|XIO_BLOCKLIST|内部使用のみです。|
|XIO_REQSTR|内部使用のみです。|
|XIO_SEQNUMBUMP|内部使用のみです。|
|XIOSTATS|内部使用のみです。|
|XTP_RT_DATA_LIST|内部使用のみです。|
|XTS_MGR|内部使用のみです。|
|XVB_CSN|内部使用のみです。|
|XVB_LIST|内部使用のみです。|
 

  
## <a name="see-also"></a>関連項目  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [SQL Server で重要なドライバーの CPU 使用率のスピンロックが場合でしょうか。](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [診断および SQL Server のスピンロックの競合を解決します。](https://www.microsoft.com/download/details.aspx?id=26666)
  
  


