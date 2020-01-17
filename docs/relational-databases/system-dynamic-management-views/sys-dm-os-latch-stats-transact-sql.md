---
title: dm_os_latch_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_latch_stats_TSQL
- dm_os_latch_stats_TSQL
- dm_os_latch_stats
- sys.dm_os_latch_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_latch_stats dynamic management view
ms.assetid: 2085d9fc-828c-453e-82ec-b54ed8347ae5
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1a8480b7e512c697f3645006d453866963b81aa
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289403"
---
# <a name="sysdm_os_latch_stats-transact-sql"></a>dm_os_latch_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

クラス別に分類されたすべてのラッチ待機に関する情報を返します。 
  
> [!NOTE]  
> [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_latch_stats**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|latch_class|**nvarchar(120)**|ラッチクラスの名前。|  
|waiting_requests_count|**bigint**|このクラスのラッチでの待機の数。 このカウンターは、ラッチ待機の開始時にインクリメントされます。|  
|wait_time_ms|**bigint**|クラス内のラッチに対する合計待機時間 (ミリ秒単位)。<br /><br /> **注:** この列は、ラッチ待機中、およびラッチ待機の終了時に5分ごとに更新されます。|  
|max_wait_time_ms|**bigint**|メモリ オブジェクトがラッチを待機した最大時間。 この値が著しく大きい場合、内部デッドロックを示している可能性があります。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>Remarks  
 sys.dm_os_latch_stats を使用すると、別のラッチ クラスの待機数や待機時間を相対的に確認することにより、ラッチの競合の発生源を特定できます。 場合によっては、ラッチの競合を解決または減らすことができます。 ただし、[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマーサポートサービスに問い合わせる必要がある場合もあります。  
  
次のように `DBCC SQLPERF` を使用すると、sys.dm_os_latch_stats の内容をリセットできます。  
  
```sql  
DBCC SQLPERF ('sys.dm_os_latch_stats', CLEAR);  
GO  
```  
  
 これにより、すべてのカウンターが0にリセットされます。  
  
> [!NOTE]  
>  これらの統計は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動されると保存されません。 すべてのデータは、統計が最後にリセットされた後、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が開始されてから累積されます。  
  
## <a name="latches"></a>両側  
 ラッチは、さまざまな [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントによって使用される、ロックに似た内部軽量同期オブジェクトです。 ラッチは主に、バッファーやファイルアクセスなどの操作中にデータベースページを同期するために使用されます。 各ラッチは、1 つのアロケーション ユニットに関連付けられています。 
  
 ラッチが別のスレッドによって、競合するモードで保持されており、ラッチ要求がすぐに許可されない場合は、ラッチ待機が発生します。 ロックとは異なり、ラッチは、書き込み操作であっても、操作の直後に解放されます。  
  
 ラッチは、コンポーネントと使用法に基づいてクラスにグループ化されます。 特定クラスのラッチは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内に、任意の時点でいくつでも存在できます。  
  
> [!NOTE]  
> `sys.dm_os_latch_stats` は、すぐに許可されたか、待機せずに失敗したラッチ要求を追跡しません。  
  
 次の表に、さまざまなラッチクラスの簡単な説明を示します。  
  
|ラッチクラス|[説明]|  
|-----------------|-----------------|  
|ALLOC_CREATE_RINGBUF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部で使用され、割り当てリング バッファーの作成の同期を初期化します。|  
|ALLOC_CREATE_FREESPACE_CACHE|ヒープの内部空き領域キャッシュの同期を初期化するために使用されます。|  
|ALLOC_CACHE_MANAGER|内部一貫性テストの同期に使用されます。|  
|ALLOC_FREESPACE_CACHE|ヒープおよびバイナリラージオブジェクト (Blob) で使用可能な領域があるページのキャッシュへのアクセスを同期するために使用されます。 複数の接続がヒープまたは BLOB に同時に行を挿入しようとすると、このクラスのラッチの競合が発生する可能性があります。 このような競合を少なくするには、オブジェクトをパーティション分割します。 各パーティションには独自のラッチがあります。 パーティション分割では、複数のラッチに挿入が分散されます。|  
|ALLOC_EXTENT_CACHE|割り当てられていないページを含むエクステントのキャッシュへのアクセスを同期するために使用します。 このクラスのラッチの競合は、複数の接続が同じアロケーションユニット内のデータページを同時に割り当てようとしたときに発生する可能性があります。 このような競合は、このアロケーションユニットが属するオブジェクトをパーティション分割することによって減らすことができます。|  
|ACCESS_METHODS_DATASET_PARENT|並列操作中に子データセットアクセスを親データセットに同期するために使用します。|  
|ACCESS_METHODS_HOBT_FACTORY|内部ハッシュテーブルへのアクセスを同期するために使用します。|  
|ACCESS_METHODS_HOBT|HoBt のメモリ内表現へのアクセスを同期するために使用されます。|  
|ACCESS_METHODS_HOBT_COUNT|HoBt ページおよび行カウンターへのアクセスを同期するために使用します。|  
|ACCESS_METHODS_HOBT_VIRTUAL_ROOT|内部 B ツリーのルートページの抽象化へのアクセスを同期するために使用されます。|  
|ACCESS_METHODS_CACHE_ONLY_HOBT_ALLOC|作業テーブルへのアクセスを同期するために使用します。|  
|ACCESS_METHODS_BULK_ALLOC|Bulk アロケーター内でアクセスを同期するために使用します。|  
|ACCESS_METHODS_SCAN_RANGE_GENERATOR|並列スキャン中、範囲ジェネレーターへのアクセスを同期するために使用します。|  
|ACCESS_METHODS_KEY_RANGE_GENERATOR|キー範囲の並列スキャン中、先行読み取り操作へのアクセスを同期するために使用します。|  
|APPEND_ONLY_STORAGE_INSERT_POINT|高速追加専用ストレージユニットで挿入を同期するために使用されます。|  
|APPEND_ONLY_STORAGE_FIRST_ALLOC|追加専用ストレージ ユニットの最初の割り当てを同期するために使用します。|  
|APPEND_ONLY_STORAGE_UNIT_MANAGER|高速追加専用ストレージユニットマネージャー内での内部データ構造アクセスの同期に使用されます。|  
|APPEND_ONLY_STORAGE_MANAGER|高速追加専用ストレージユニットマネージャーで圧縮操作を同期するために使用されます。|  
|BACKUP_RESULT_SET|並列バックアップの結果セットを同期するために使用します。|  
|BACKUP_TAPE_POOL|バックアップテーププールの同期に使用されます。|  
|BACKUP_LOG_REDO|バックアップログの再実行操作を同期するために使用します。|  
|BACKUP_INSTANCE_ID|バックアップパフォーマンスモニターカウンターのインスタンス Id の生成を同期するために使用します。|  
|BACKUP_MANAGER|内部バックアップ マネージャーを同期するために使用します。|  
|BACKUP_MANAGER_DIFFERENTIAL|差分バックアップ操作を DBCC と同期するために使用します。|  
|BACKUP_OPERATION|データベース、ログ、ファイルバックアップなど、バックアップ操作内での内部データ構造の同期に使用されます。|  
|BACKUP_FILE_HANDLE|復元操作中にファイルを開く操作を同期するために使用します。|  
|格納|短期的なアクセスをデータベースページに同期するために使用されます。 データベースページの読み取りまたは変更を行う前に、バッファーラッチが必要です。 バッファーラッチの競合は、ホットページや低速の i/o など、いくつかの問題を示す場合があります。<br /><br /> このラッチ クラスは、ページ ラッチを使用するすべての状況に対応しています。 dm_os_wait_stats は、ページ上の i/o 操作および読み取りおよび書き込み操作によって発生するページラッチ待機の差を大きくします。|  
|BUFFER_POOL_GROW|バッファー プールの拡張操作中、内部バッファー マネージャーの同期に使用します。|  
|DATABASE_CHECKPOINT|データベース内のチェックポイントをシリアル化するために使用されます。|  
|CLR_PROCEDURE_HASHTABLE|内部使用のみです。|  
|CLR_UDX_STORE|内部使用のみです。|  
|CLR_DATAT_ACCESS|内部使用のみです。|  
|CLR_XVAR_PROXY_LIST|内部使用のみです。|  
|DBCC_CHECK_AGGREGATE|内部使用のみです。|  
|DBCC_CHECK_RESULTSET|内部使用のみです。|  
|DBCC_CHECK_TABLE|内部使用のみです。|  
|DBCC_CHECK_TABLE_INIT|内部使用のみです。|  
|DBCC_CHECK_TRACE_LIST|内部使用のみです。|  
|DBCC_FILE_CHECK_OBJECT|内部使用のみです。|  
|DBCC_PERF|内部パフォーマンスモニターカウンターを同期するために使用します。|  
|DBCC_PFS_STATUS|内部使用のみです。|  
|DBCC_OBJECT_METADATA|内部使用のみです。|  
|DBCC_HASH_DLL|内部使用のみです。|  
|EVENTING_CACHE|内部使用のみです。|  
|FCB|ファイル制御ブロックへのアクセスを同期するために使用します。|  
|FCB_REPLICA|内部使用のみです。|  
|FGCB_ALLOC|ファイル グループ内のラウンド ロビン割り当て情報へのアクセスを同期するために使用します。|  
|FGCB_ADD_REMOVE|ファイルの追加、削除、拡張、および圧縮を行うために、ファイルグループへのアクセスを同期するために使用します。|  
|FILEGROUP_MANAGER|内部使用のみです。|  
|FILE_MANAGER|内部使用のみです。|  
|FILESTREAM_FCB|内部使用のみです。|  
|FILESTREAM_FILE_MANAGER|内部使用のみです。|  
|FILESTREAM_GHOST_FILES|内部使用のみです。|  
|FILESTREAM_DFS_ROOT|内部使用のみです。|  
|LOG_MANAGER|内部使用のみです。|  
|FULLTEXT_DOCUMENT_ID|内部使用のみです。|  
|FULLTEXT_DOCUMENT_ID_TRANSACTION|内部使用のみです。|  
|FULLTEXT_DOCUMENT_ID_NOTIFY|内部使用のみです。|  
|FULLTEXT_LOGS|内部使用のみです。|  
|FULLTEXT_CRAWL_LOG|内部使用のみです。|  
|FULLTEXT_ADMIN|内部使用のみです。|  
|FULLTEXT_AMDIN_COMMAND_CACHE|内部使用のみです。|  
|FULLTEXT_LANGUAGE_TABLE|内部使用のみです。|  
|FULLTEXT_CRAWL_DM_LIST|内部使用のみです。|  
|FULLTEXT_CRAWL_CATALOG|内部使用のみです。|  
|FULLTEXT_FILE_MANAGER|内部使用のみです。|  
|DATABASE_MIRRORING_REDO|内部使用のみです。|  
|DATABASE_MIRRORING_SERVER|内部使用のみです。|  
|DATABASE_MIRRORING_CONNECTION|内部使用のみです。|  
|DATABASE_MIRRORING_STREAM|内部使用のみです。|  
|QUERY_OPTIMIZER_VD_MANAGER|内部使用のみです。|  
|QUERY_OPTIMIZER_ID_MANAGER|内部使用のみです。|  
|QUERY_OPTIMIZER_VIEW_REP|内部使用のみです。|  
|RECOVERY_BAD_PAGE_TABLE|内部使用のみです。|  
|RECOVERY_MANAGER|内部使用のみです。|  
|SECURITY_OPERATION_RULE_TABLE|内部使用のみです。|  
|SECURITY_OBJPERM_CACHE|内部使用のみです。|  
|SECURITY_CRYPTO|内部使用のみです。|  
|SECURITY_KEY_RING|内部使用のみです。|  
|SECURITY_KEY_LIST|内部使用のみです。|  
|SERVICE_BROKER_CONNECTION_RECEIVE|内部使用のみです。|  
|SERVICE_BROKER_TRANSMISSION|内部使用のみです。|  
|SERVICE_BROKER_TRANSMISSION_UPDATE|内部使用のみです。|  
|SERVICE_BROKER_TRANSMISSION_STATE|内部使用のみです。|  
|SERVICE_BROKER_TRANSMISSION_ERRORS|内部使用のみです。|  
|SSBXmitWork|内部使用のみです。|  
|SERVICE_BROKER_MESSAGE_TRANSMISSION|内部使用のみです。|  
|SERVICE_BROKER_MAP_MANAGER|内部使用のみです。|  
|SERVICE_BROKER_HOST_NAME|内部使用のみです。|  
|SERVICE_BROKER_READ_CACHE|内部使用のみです。|  
|SERVICE_BROKER_WAITFOR_MANAGER| 待機キューのインスタンスレベルのマップを同期するために使用します。 データベース ID、データベースのバージョン、およびキュー ID の組ごとに1つのキューが存在します。 このクラスのラッチの競合は、WAITFOR (RECEIVE) wait 状態での多くの接続がある場合に発生する可能性があります。WAITFOR (RECEIVE) の呼び出しWAITFOR timeout を超えています。メッセージを受信しています。WAITFOR (RECEIVE) を含むトランザクションのコミットまたはロールバックWAITFOR (RECEIVE) の待機状態にあるスレッドの数を減らすことで、競合を軽減できます。 |  
|SERVICE_BROKER_WAITFOR_TRANSACTION_DATA|内部使用のみです。|  
|SERVICE_BROKER_TRANSMISSION_TRANSACTION_DATA|内部使用のみです。|  
|SERVICE_BROKER_TRANSPORT|内部使用のみです。|  
|SERVICE_BROKER_MIRROR_ROUTE|内部使用のみです。|  
|TRACE_ID|内部使用のみです。|  
|TRACE_AUDIT_ID|内部使用のみです。|  
|trace|内部使用のみです。|  
|TRACE_CONTROLLER|内部使用のみです。|  
|TRACE_EVENT_QUEUE|内部使用のみです。|  
|TRANSACTION_DISTRIBUTED_MARK|内部使用のみです。|  
|TRANSACTION_OUTCOME|内部使用のみです。|  
|NESTING_TRANSACTION_READONLY|内部使用のみです。|  
|NESTING_TRANSACTION_FULL|内部使用のみです。|  
|MSQL_TRANSACTION_MANAGER|内部使用のみです。|  
|DATABASE_AUTONAME_MANAGER|内部使用のみです。|  
|UTILITY_DYNAMIC_VECTOR|内部使用のみです。|  
|UTILITY_SPARSE_BITMAP|内部使用のみです。|  
|UTILITY_DATABASE_DROP|内部使用のみです。|  
|UTILITY_DYNAMIC_MANAGER_VIEW|内部使用のみです。|  
|UTILITY_DEBUG_FILESTREAM|内部使用のみです。|  
|UTILITY_LOCK_INFORMATION|内部使用のみです。|  
|VERSIONING_TRANSACTION|内部使用のみです。|  
|VERSIONING_TRANSACTION_LIST|内部使用のみです。|  
|VERSIONING_TRANSACTION_CHAIN|内部使用のみです。|  
|VERSIONING_STATE|内部使用のみです。|  
|VERSIONING_STATE_CHANGE|内部使用のみです。|  
|KTM_VIRTUAL_CLOCK|内部使用のみです。|  
  
## <a name="see-also"></a>参照  
[DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)       
[オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)       
[SQL Server の Latches オブジェクト](../../relational-databases/performance-monitor/sql-server-latches-object.md)      
