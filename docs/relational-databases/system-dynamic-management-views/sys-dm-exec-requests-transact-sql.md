---
title: dm_exec_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: sstein
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_requests_TSQL
- sys.dm_exec_requests
- dm_exec_requests_TSQL
- dm_exec_requests
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_requests dynamic management view
ms.assetid: 4161dc57-f3e7-4492-8972-8cfb77b29643
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 20257eb1a91b35dd45e1b4fc79f84533c64b2561
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74307996"
---
# <a name="sysdm_exec_requests-transact-sql"></a>dm_exec_requests (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]実行されている各要求に関する情報を返します。 要求の詳細については、「[スレッドおよびタスクアーキテクチャガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|この要求が関連付けられているセッションの ID。 NULL 値は許可されません。|  
|request_id|**通り**|要求の ID。 セッションのコンテキスト内で一意です。 NULL 値は許可されません。|  
|start_time|**/**|要求が到着したときのタイムスタンプ。 NULL 値は許可されません。|  
|status|**nvarchar (30)**|要求の状態。 これは次のいずれかです。<br /><br /> 背景<br />実行中<br />実行可能<br />休止中<br />Suspended<br /><br /> NULL 値は許可されません。|  
|command|**nvarchar (32)**|現在処理中のコマンドの種類。 一般的なコマンドの種類には次のものがあります。<br /><br /> SELECT<br />INSERT<br />UPDATE<br />DELETE<br />BACKUP LOG<br />BACKUP DATABASE<br />DBCC<br />FOR<br /><br /> 要求のテキストを取得するには、対応する sql_handle と共に、要求に対して sys.dm_exec_sql_text を使用します。 内部システムプロセスは、実行するタスクの種類に基づいて、コマンドを設定します。 タスクには次のものが含まれます。<br /><br /> LOCK MONITOR<br />CHECKPOINTLAZY<br />WRITER<br /><br /> NULL 値は許可されません。|  
|sql_handle|**varbinary (64)**|クエリが含まれているバッチまたはストアドプロシージャを一意に識別するトークンです。 NULL 値が許可されます。|  
|statement_start_offset|**通り**|現在実行中のバッチまたはストアド プロシージャに含まれる、現在実行中のステートメントが開始されるまでの文字数。 sql_handle、statement_end_offset、sys.dm_exec_sql_text 動的管理関数と共に使用して、要求に対して現在実行中のステートメントを取得できます。 NULL 値が許可されます。|  
|statement_end_offset|**通り**|現在実行中のバッチまたはストアドプロシージャ内で現在実行中のステートメントが終了するまでの文字数。 sql_handle、statement_end_offset、sys.dm_exec_sql_text 動的管理関数と共に使用して、要求に対して現在実行中のステートメントを取得できます。 NULL 値が許可されます。|  
|plan_handle|**varbinary (64)**|現在実行中のバッチのクエリ実行プランを一意に識別するトークンです。 NULL 値が許可されます。|  
|database_id|**smallint**|要求の実行対象データベースの ID。 NULL 値は許可されません。|  
|user_id|**通り**|要求を送信したユーザーの ID。 NULL 値は許可されません。|  
|connection_id|**一意**|要求を受信した接続の ID。 NULL 値が許可されます。|  
|blocking_session_id|**smallint**|要求をブロックしているセッションの ID。 この列が NULL または0に等しい場合は、要求がブロックされていないか、ブロックしているセッションのセッション情報が使用できない (または識別できません)。<br /><br /> -2 = ブロックしているリソースは、孤立した分散トランザクションが所有しています。<br /><br /> -3 = ブロックしているリソースは、遅延復旧トランザクションが所有しています。<br /><br /> -4 = 内部ラッチの状態遷移のため、ブロックしているラッチの所有者のセッション ID を現時点で特定できませんでした。|  
|wait_type|**nvarchar (60)**|要求が現在ブロックされている場合の待機の種類。 NULL 値が許可されます。<br /><br /> 待機の種類の詳細については、「 [sys. dm_os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。|  
|wait_time|**通り**|要求が現在ブロックされている場合の現時点での待機時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|last_wait_type|**nvarchar (60)**|要求がブロックされていた場合の最後の待機の種類。 NULL 値は許可されません。|  
|wait_resource|**nvarchar(256)**|要求が現在ブロックされている場合の現在待機中のリソース。 NULL 値は許可されません。|  
|open_transaction_count|**通り**|この要求に対して開いているトランザクションの数。 NULL 値は許可されません。|  
|open_resultset_count|**通り**|この要求に対して開いている結果セットの数。 NULL 値は許可されません。|  
|transaction_id|**bigint**|要求が実行されるトランザクションの ID。 NULL 値は許可されません。|  
|context_info|**varbinary (128)**|セッションの CONTEXT_INFO 値。 NULL 値が許可されます。|  
|percent_complete|**real**|次のコマンドで完了した作業の割合。<br /><br /> ALTER INDEX REORGANIZE<br />ALTER DATABASE の AUTO_SHRINK オプション<br />BACKUP DATABASE<br />DBCC CHECKDB<br />DBCC CHECKFILEGROUP<br />DBCC CHECKTABLE<br />DBCC INDEXDEFRAG<br />DBCC SHRINKDATABASE<br />DBCC SHRINKFILE<br />RECOVERY<br />RESTORE DATABASE<br />ROLLBACK<br />TDE の暗号化<br /><br /> NULL 値は許可されません。|  
|estimated_completion_time|**bigint**|内部のみ。 NULL 値は許可されません。|  
|cpu_time|**通り**|要求で使用される CPU 時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|total_elapsed_time|**通り**|要求を受信してから経過した総時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|scheduler_id|**通り**|この要求のスケジュールを設定しているスケジューラの ID。 NULL 値は許可されません。|  
|task_address|**varbinary (8)**|要求に関連付けられたタスクに割り当てられるメモリ アドレス。 NULL 値が許可されます。|  
|reads|**bigint**|要求で実行された読み取りの数。 NULL 値は許可されません。|  
|writes|**bigint**|要求で実行された書き込みの数。 NULL 値は許可されません。|  
|logical_reads|**bigint**|要求で実行された論理読み取りの数。 NULL 値は許可されません。|  
|text_size|**通り**|要求の TEXTSIZE 設定。 NULL 値は許可されません。|  
|言語|**nvarchar(128)**|要求の言語設定。 NULL 値が許可されます。|  
|date_format|**nvarchar (3)**|要求の DATEFORMAT 設定。 NULL 値が許可されます。|  
|date_first|**smallint**|要求の DATEFIRST 設定。 NULL 値は許可されません。|  
|quoted_identifier|**bit**|1 = 要求に対して QUOTED_IDENTIFIER が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|arithabort|**bit**|1 = 要求に対して ARITHABORT 設定が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|ansi_null_dflt_on|**bit**|1 = 要求に対して ANSI_NULL_DFLT_ON 設定が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|ansi_defaults|**bit**|1 = 要求に対して ANSI_DEFAULTS 設定が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|ansi_warnings|**bit**|1 = 要求に対して ANSI_WARNINGS 設定が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|ansi_padding|**bit**|1 = 要求に対して ANSI_PADDING 設定が ON です。<br /><br /> それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|ansi_nulls|**bit**|1 = 要求に対して ANSI_NULLS 設定が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|concat_null_yields_null|**bit**|1 = 要求に対して CONCAT_NULL_YIELDS_NULL 設定が ON です。 それ以外の場合は0になります。<br /><br /> NULL 値は許可されません。|  
|transaction_isolation_level|**smallint**|この要求に対するトランザクションの作成に使用された分離レベル。 NULL 値は許可されません。<br /> 0 = Unspecified<br /> 1 = ReadUncomitted<br /> 2 = ReadCommitted<br /> 3 = Repeatable<br /> 4 = Serializable<br /> 5 = Snapshot|  
|lock_timeout|**通り**|要求のロック タイムアウトまでの時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|deadlock_priority|**通り**|要求の DEADLOCK_PRIORITY 設定。 NULL 値は許可されません。|  
|row_count|**bigint**|この要求によってクライアントに返された行の数。 NULL 値は許可されません。|  
|prev_error|**通り**|要求の実行中に発生した最後のエラー。 NULL 値は許可されません。|  
|nest_level|**通り**|要求で実行されているコードの現在の入れ子レベル。 NULL 値は許可されません。|  
|granted_query_memory|**通り**|要求でのクエリの実行に割り当てられたページ数。 NULL 値は許可されません。|  
|executing_managed_code|**bit**|特定の要求で、ルーチン、データ型、トリガーなどの共通言語ランタイム オブジェクトが現在実行されているかどうかを示します。 共通言語ランタイム オブジェクトが共通言語ランタイム内から [!INCLUDE[tsql](../../includes/tsql-md.md)] を実行した場合でも、共通言語ランタイム オブジェクトがスタックにある間は、このパラメーターが必ず設定されます。 NULL 値は許可されません。|  
|group_id|**通り**|このクエリが属しているワークロードグループの ID。 NULL 値は許可されません。|  
|query_hash|**binary (8)**|クエリで計算され、同様のロジックを持つクエリを識別するために使用される、バイナリのハッシュ値です。 クエリ ハッシュを使用して、リテラル値だけが異なるクエリの全体的なリソース使用率を決定できます。|  
|query_plan_hash|**binary (8)**|クエリ実行プランで計算され、同様のクエリ実行プランを識別するために使用される、バイナリのハッシュ値です。 クエリ プラン ハッシュを使用して、同様の実行プランを持つクエリの累積コストを確認できます。|  
|statement_sql_handle|**varbinary (64)**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降。<br /><br /> 個々のクエリの SQL ハンドル。<br /><br />データベースに対してクエリストアが有効になっていない場合、この列は NULL になります。 |  
|statement_context_id|**bigint**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降。<br /><br /> Query_context_settings の外部キー (省略可能)。<br /><br />データベースに対してクエリストアが有効になっていない場合、この列は NULL になります。 |  
|dop |**通り** |**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降。<br /><br /> クエリの並列処理の次数。 |  
|parallel_worker_count |**通り** |**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降。<br /><br /> 並列クエリの場合は、予約済みの並列ワーカーの数。  |  
|external_script_request_id |**一意** |**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降。<br /><br /> 現在の要求に関連付けられている外部スクリプト要求 ID。 |  
|is_resumable |**bit** |**適用対象**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]以降。<br /><br /> 要求が再開可能なインデックス操作であるかどうかを示します。 |  
|page_resource |**binary (8)** |**適用対象**:[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]<br /><br /> 列に`wait_resource`ページが含まれている場合は、ページリソースの8バイトの16進数表現。 詳細については、「 [sys. fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)」を参照してください。 |  
|page_server_reads|**bigint**|**適用対象**: Azure SQL Database ハイパースケール<br /><br /> この要求によって実行されたページサーバーの読み取り回数。 NULL 値は許可されません。|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>コメント 

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部のコード (拡張ストアド プロシージャや分散クエリなど) を実行するには、スレッドを非プリエンプティブ スケジューラの制御外で実行する必要があります。 このとき、ワーカーはプリエンプティブ モードに切り替えられます。 この動的管理ビューによって返される時刻値には、プリエンプティブモードで費やされた時間は含まれません。

[行モード](../../relational-databases/query-processing-architecture-guide.md#row-mode-execution)で並列要求を実行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]場合、は、割り当てられたタスクを完了するワーカースレッドを調整するワーカースレッドを割り当てます。 この DMV では、コーディネーターのスレッドのみが要求に対して表示されます。 列の**読み取り**、**書き込み**、 **logical_reads**、 **row_count**は、コーディネータースレッドに対して更新され**ません**。 列**wait_type**、 **wait_time**、 **last_wait_type**、 **wait_resource**、および**granted_query_memory**は、コーディネータースレッドに対して**のみ更新**されます。 詳細については、「[スレッドおよびタスクのアーキテクチャ ガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。

## <a name="permissions"></a>アクセス許可
ユーザーがサーバーに`VIEW SERVER STATE`対する権限を持っている場合、ユーザーにはのインスタンスで実行中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのセッションが表示されます。それ以外の場合、ユーザーには現在のセッションのみが表示されます。 `VIEW SERVER STATE`Azure SQL Database で許可することは`sys.dm_exec_requests`できません。したがって、は常に現在の接続に限定されます。
  
## <a name="examples"></a>例  
  
### <a name="a-finding-the-query-text-for-a-running-batch"></a>A. 実行中のバッチのクエリテキストの検索

 次の例では、`sys.dm_exec_requests` をクエリして目的のクエリを検索し、その `sql_handle` を出力結果からコピーします。  

```sql
SELECT * FROM sys.dm_exec_requests;  
GO  
```  

次に、ステートメントテキストを取得するために、 `sql_handle`コピーした`sys.dm_exec_sql_text(sql_handle)`をシステム関数と共に使用します。  

```sql
SELECT * FROM sys.dm_exec_sql_text(< copied sql_handle >);  
GO  
```

### <a name="b-finding-all-locks-that-a-running-batch-is-holding"></a>B. 実行中のバッチが保持しているすべてのロックを検索する

次の例では、 **dm_exec_requests**を照会して、興味深いバッチ`transaction_id`を見つけて、出力からコピーします。

```sql
SELECT * FROM sys.dm_exec_requests;  
GO
```

次に、ロック情報を検索するには`transaction_id` 、システム関数**sys. dm_tran_locks**と共にコピーされたを使用します。  

```sql
SELECT * FROM sys.dm_tran_locks
WHERE request_owner_type = N'TRANSACTION'
    AND request_owner_id = < copied transaction_id >;
GO  
```

### <a name="c-finding-all-currently-blocked-requests"></a>C. 現在ブロックされているすべての要求を検索しています

次の例では、 **sys. dm_exec_requests**を照会して、ブロックされた要求に関する情報を検索します。  

```sql
SELECT session_id ,status ,blocking_session_id  
    ,wait_type ,wait_time ,wait_resource
    ,transaction_id
FROM sys.dm_exec_requests
WHERE status = N'suspended';  
GO  
```  

### <a name="d-ordering-existing-requests-by-cpu"></a>D. CPU による既存の要求の順序付け

```sql
SELECT 
   req.session_id
   , req.start_time
   , cpu_time 'cpu_time_ms'
   , object_name(st.objectid,st.dbid) 'ObjectName' 
   , substring
      (REPLACE
        (REPLACE
          (SUBSTRING
            (ST.text
            , (req.statement_start_offset/2) + 1
            , (
               (CASE statement_end_offset
                  WHEN -1
                  THEN DATALENGTH(ST.text)  
                  ELSE req.statement_end_offset
                  END
                    - req.statement_start_offset)/2) + 1)
       , CHAR(10), ' '), CHAR(13), ' '), 1, 512)  AS statement_text  
FROM sys.dm_exec_requests AS req  
   CROSS APPLY sys.dm_exec_sql_text(req.sql_handle) as ST
   ORDER BY cpu_time desc;
GO
```

## <a name="see-also"></a>参照
[動的管理ビューと動的管理関数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
[実行関連の動的管理ビューおよび関数](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)      
[dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)     
[dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)     
[dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)    
[dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)      
[SQL Server、SQL Statistics オブジェクト](../../relational-databases/performance-monitor/sql-server-sql-statistics-object.md)     
[クエリ処理のアーキテクチャガイド](../../relational-databases/query-processing-architecture-guide.md#DOP)       
[スレッドおよびタスクのアーキテクチャガイド](../../relational-databases/thread-and-task-architecture-guide.md)    
