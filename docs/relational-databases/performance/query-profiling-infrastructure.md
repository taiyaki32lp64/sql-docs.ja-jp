---
title: クエリ プロファイリング インフラストラクチャ | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query profiling
- lightweight query profiling
- lightweight profiling
- lwp
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 40c2c30ff3d44b41d4ddcac4cc9fe0954a06d72e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257674"
---
# <a name="query-profiling-infrastructure"></a>クエリ プロファイリング インフラストラクチャ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] では、クエリ実行プランのランタイム情報にアクセスする機能を提供しています。 パフォーマンスの問題が発生したときに最も重要なアクションの 1 つは、実行中のワークロードとリソース使用量が促進される仕組みを正確に把握することです。 そのためには、[実際の実行プラン](../../relational-databases/performance/display-an-actual-execution-plan.md)にアクセスすることが重要です。

クエリの完了は、実際のクエリ プランの利用における前提条件ですが、データが 1 つの[クエリ プラン演算子](../../relational-databases/showplan-logical-and-physical-operators-reference.md)から別のクエリ プラン演算子に移動するので、[ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)からリアルタイムの分析情報をクエリ実行プロセスに提供できます。 ライブ クエリ プランには、全体的なクエリ進捗状況と演算子レベルのランタイム実行統計が表示されます。生成された行の数、経過時間、演算子の進捗状況などです。このデータはクエリの完了を待つことなくリアルタイムで利用できるため、これらの実行統計は、長時間実行されるクエリや、不明確で決して終わることのないクエリなど、クエリ パフォーマンスの問題のデバッグで非常に役立ちます。

## <a name="the-standard-query-execution-statistics-profiling-infrastructure"></a>標準クエリ実行統計プロファイリング インフラストラクチャ

実行プラン、つまり行数、CPU、および I/O の使用状況に関する情報を収集するには、*クエリ実行統計プロファイル インフラストラクチャ*、すなわち標準プロファイリングを有効にする必要があります。 次の**ターゲット セッション**の実行プラン情報収集メソッドでは、標準プロファイリング インフラストラクチャが活用されます。

- [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) 
- [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)
- [ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で *[ライブ クエリ統計を含む]* ボタンをクリックすると、標準プロファイリング インフラストラクチャを活用できます。    
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の上位バージョンで、[軽量プロファイリング インフラストラクチャ](#lwp)が有効になっていると、[利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)を通じて表示したとき、または [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV を直接クエリしたときに、標準プロファイリングではなく、ライブ クエリ統計によって利用されます。 

次の**すべてのセッション**のグローバルな実行プラン情報収集メソッドでは、標準プロファイリング インフラストラクチャが活用されます。

-  ***query_post_execution_showplan*** 拡張イベント。 拡張イベントを有効にする方法については、「 [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)」を参照してください。  
- [SQL トレース](../../relational-databases/sql-trace/sql-trace.md)と [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md) の **Showplan XML** トレース イベント。 このトレース イベントの詳細については、「[Showplan XML イベント クラス](../../relational-databases/event-classes/showplan-xml-event-class.md)」を参照してください。

*query_post_execution_showplan* イベントを使用する拡張イベント セッションの実行時に、[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV も入力されます。これによって、すべてのセッションのライブ クエリ統計が有効になり、[利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)を使用することや、DMV に直接クエリを実行することができます。 詳細については、「 [Live Query Statistics](../../relational-databases/performance/live-query-statistics.md)」を参照してください。

## <a name="lwp"></a>軽量クエリ実行統計プロファイリング インフラストラクチャ

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 および [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降で、新しい*軽量クエリ実行統計プロファイリング インフラストラクチャ*、すなわち**軽量プロファイリング**が導入されました。 

> [!NOTE]
> 軽量プロファイリングでは、ネイティブ コンパイル ストアド プロシージャはサポートされていません。  

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v1"></a>軽量クエリ実行統計プロファイリング インフラストラクチャ v1

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 から [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])。 
  
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 および [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降で、軽量プロファイリングの導入により、実行プランに関する情報を収集するパフォーマンスのオーバーヘッドが軽減されました。 標準プロファイリングと異なり、軽量プロファイリングでは CPU のランタイム情報が収集されません。 ただし、軽量プロファイリングでも行数と I/O の使用状況の情報は収集されます。

軽量プロファイリングを活用する新しい***query_thread_profile*** 拡張イベントも導入されました。 この拡張イベントでは、演算子ごとの実行統計が示されるため、各ノードおよびスレッドのパフォーマンスについて、より多くの分析情報を提供できます。 この拡張イベントを使用するサンプル セッションは、次の例のように構成できます。

```sql
CREATE EVENT SESSION [NodePerfStats] ON SERVER
ADD EVENT sqlserver.query_thread_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

> [!NOTE]
> クエリ プロファイリングのパフォーマンス オーバーヘッドの詳細については、ブログの投稿「[Developers Choice:Query progress - anytime, anywhere (開発者の選択: クエリの進行状況 - いつでも、どこでも)](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)」をご覧ください。 

*query_thread_profile* イベントを使用する拡張イベント セッションの実行時に、[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV も軽量プロファイリングを使用して入力されます。これによって、[利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)を使用することや、DMV に直接クエリを実行することができます。

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v2"></a>軽量クエリ実行統計プロファイリング インフラストラクチャ v2

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 から [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])。 

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 には、オーバーヘッドが最小限の軽量プロファイリングの改訂版が含まれます。 軽量プロファイリングも、*適用対象*の前述のバージョンで、[トレース フラグ 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を使用してグローバルに有効にできます。 送信中の要求にクエリ実行プランを返すために、新しい DMF [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) が導入されました。

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 と [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11 以降で、軽量プロファイリングがグローバルで有効でない場合、新しい [USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)引数 **QUERY_PLAN_PROFILE** を使用して、任意のセッションで、クエリ レベルで軽量プロファイリングを有効にできます。 この新しいヒントを含むクエリが終了すると、新しい ***query_plan_profile*** 拡張イベントも出力され、*query_post_execution_showplan* 拡張イベントに類似した実際の実行プラン XML が提供されます。 

> [!NOTE]
> *query_plan_profile* 拡張イベントではまた、クエリ ヒントが使用されない場合でも、軽量プロファイリングが活用されます。 

*query_plan_profile* 拡張イベントを使用したサンプル セッションは下の例のように構成できます。

```sql
CREATE EVENT SESSION [PerfStats_LWP_Plan] ON SERVER
ADD EVENT sqlserver.query_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v3"></a>軽量クエリ実行統計プロファイリング インフラストラクチャ v3

**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] には、すべての実行の行数情報を収集する軽量プロファイリングの新しい改訂版が含まれます。 軽量プロファイリングは、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] で既定で有効であり、トレース フラグ 7412 は機能しません。 軽量プロファイリングは、LIGHTWEIGHT_QUERY_PROFILING [データベース スコープ構成](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md): `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = OFF;` を使用して、データベース レベルで無効にできます。

ほとんどのクエリで最後の既知の実際の実行プランと同等のものが返されるように、*最後のクエリ プランの統計*と呼ばれる新しい DMF [sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) が導入されました。 最後のクエリ プランの統計は、LAST_QUERY_PLAN_STATS [データベース スコープ構成](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md): `ALTER DATABASE SCOPED CONFIGURATION SET LAST_QUERY_PLAN_STATS = ON;` を使用して、データベース レベルで有効にすることができます。

新しい *query_post_execution_plan_profile* 拡張イベントでは、標準プロファイリングを使用する *query_post_execution_showplan* とは異なり、軽量プロファイリングに基づいて、実際の実行プランと同等のものが収集されます。 *query_post_execution_plan_profile* 拡張イベントを使用したサンプル セッションは下の例のように構成できます。

```sql
CREATE EVENT SESSION [PerfStats_LWP_All_Plans] ON SERVER
ADD EVENT sqlserver.query_post_execution_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

#### <a name="example-1---extended-event-session-using-standard-profiling"></a>例 1: 標準プロファイリングを使用した拡張イベント セッション

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>例 2: 軽量プロファイリングを使用した拡張イベント セッション

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

## <a name="query-profiling-infrastruture-usage-guidance"></a>クエリ プロファイリング インフラストラクチャの使用に関するガイダンス
以下の表は、標準プロファイリングと軽量プロファイリングをグローバル (サーバー レベル) または単一セッションで有効にするためのアクションをまとめたものです。 そのアクションを使用できる最も古いバージョンも記載されています。 

|スコープ|標準プロファイリング|軽量プロファイリング|
|---------------|---------------|---------------|
|グローバル|`query_post_execution_showplan` XE を使用する xEvent セッション。[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降|トレース フラグ 7412。[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降|
|グローバル|`Showplan XML` トレース イベントを使用する SQL トレースおよび SQL Server Profiler。SQL Server 2000 以降|`query_thread_profile` XE を使用する xEvent セッション。[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降|
|グローバル|-|`query_post_execution_plan_profile` XE を使用する xEvent セッション。[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降|
|Session|`SET STATISTICS XML ON` を使用。SQL Server 2000 以降|`query_plan_profile` XE を使用する xEvent イベント セッションと共に `QUERY_PLAN_PROFILE` クエリ ヒントを使用。[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11 以降|
|Session|`SET STATISTICS PROFILE ON` を使用。SQL Server 2000 以降|-|
|Session|SSMS 内で[[ライブ クエリ統計]](../../relational-databases/performance/live-query-statistics.md) ボタンをクリック。[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降|-|

## <a name="remarks"></a>解説

> [!IMPORTANT]
> [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) を参照するストアド プロシージャの監視の実行中にランダムにアクセス違反が発生する可能性があるため、[KB 4078596](https://support.microsoft.com/help/4078596) が [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] と [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] にインストールされていることを確認してください。

軽量プロファイリング v2 以降では、低オーバーヘッドでもあることから、CPU バインドされていない任意のサーバーで軽量プロファイリングを**継続的に**実行できます。データベースの専門家は、利用状況モニターを使用するか、`sys.dm_exec_query_profiles` に直接クエリを実行するなどして、いつでも処理中の実行から、ランタイム統計を含むクエリ プランを取得できます。

クエリ プロファイリングのパフォーマンス オーバーヘッドの詳細については、ブログの投稿「[Developers Choice:Query progress - anytime, anywhere (開発者の選択: クエリの進行状況 - いつでも、どこでも)](https://techcommunity.microsoft.com/t5/SQL-Server/Developers-Choice-Query-progress-anytime-anywhere/ba-p/385004)」をご覧ください。 

> [!NOTE]
> 軽量プロファイリングを利用する拡張イベントでは、標準プロファイリング インフラストラクチャが既に有効になっている場合は、標準プロファイルの情報を使用します。 たとえば、`query_post_execution_showplan` を使用する拡張イベント セッションが実行されており、`query_post_execution_plan_profile` を使用する別のセッションが開始されたとします。 2 番目のセッションは、標準プロファイルからの情報を使用し続けます。

## <a name="see-also"></a>参照  
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)     
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [拡張イベントを使用したシステムの使用状況の監視](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)      
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
 [実際の実行プラン](../../relational-databases/performance/display-an-actual-execution-plan.md)    
 [ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)      
