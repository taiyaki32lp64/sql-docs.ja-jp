---
title: パフォーマンス監視およびチューニング ツール | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tools [SQL Server], monitoring performance
- monitoring server performance [SQL Server], tools
- monitoring performance [SQL Server], tools
- database performance [SQL Server], tools
- tuning databases [SQL Server], tools
- database monitoring [SQL Server], tools
- performance [SQL Server], monitoring tools
- server performance [SQL Server], tools
ms.assetid: 31529dfe-68e7-49f7-b3c2-39fcecf33a95
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d900593848561bba17e186f48632bf299fe9a7cd
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962405"
---
# <a name="performance-monitoring-and-tuning-tools"></a>パフォーマンス監視およびチューニング ツール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベントを監視したり、物理データベース デザインをチューニングしたりするための広範なツール セットが用意されています。 どのツールを選択するかは、実行する監視またはチューニングの種類や、監視するイベントによって異なります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の監視およびチューニング用のツールは次のとおりです。  
  
|ツール|[説明]|  
|----------|-----------------|  
|[組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)|組み込み関数では、サーバーが起動してからの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の利用状況に関するスナップショット統計が表示されます。この統計は、あらかじめ定義された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カウンターに格納されます。 たとえば、 **\@\@CPU_BUSY** には、CPU が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コードを実行している時間が格納されます。 **\@\@CONNECTIONS** には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続数または接続試行数が格納されます。 **\@\@PACKET_ERRORS** には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続で発生するネットワーク パケット数が格納されます。|  
|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|DBCC (データベース コンソール コマンド) ステートメントによって、パフォーマンス統計とデータベースの論理的および物理的一貫性を確認できます。|  
|[データベース エンジン チューニング アドバイザー (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md)|データベース エンジン チューニング アドバイザーでは、チューニングするデータベースに対して実行した [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのパフォーマンス効果が分析されます。 データベース エンジン チューニング アドバイザーでは、インデックス、インデックス付きビュー、およびパーティションを追加、削除、または変更するための推奨設定が提供されます。|  
|[Database Experimentation Assistant (DEA)](https://www.microsoft.com/download/details.aspx?id=54090)|Database Experimentation Assistant (DEA) は、SQL Server の新しい A/B テスト ソリューションです。 これは、特定のワークロードに対してターゲット バージョンの [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] を評価する場合に役立ちます。 以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョン ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降) から任意の新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードすると、DEA で比較分析メトリックを使用できるようになります。|
|エラー ログ|Windows アプリケーション イベント ログでは、Windows Server と Windows オペレーティング システム全体で発生しているイベントと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント、およびフルテキスト検索で発生しているイベントの全般的な概要が示されます。 他のツールでは提供されない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベントに関する情報が含まれています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に関連する問題のトラブルシューティングでエラー ログの情報を使用できます。|  
|[拡張イベント](../../relational-databases/extended-events/extended-events.md)|拡張イベントは軽量なパフォーマンス監視システムであり、使用されるパフォーマンス リソースはごくわずかです。 拡張イベントには、セッション データを容易かつ迅速に作成、変更、表示、分析するためのグラフィカル ユーザー インターフェイスが 3 つ用意されています (新規セッション ウィザード、[新しいセッション]、XE Profiler)。|  
|[実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|実行関連の DMV によって、実行関連情報を確認できます。|
|[ライブ クエリ統計 (LQS)](../../relational-databases/performance/live-query-statistics.md)|クエリ実行ステップに関するリアルタイムの統計情報を表示します。 このデータはクエリの実行中に利用できるため、これらの実行統計はクエリ パフォーマンス問題のデバッグで非常に役立ちます。|  
|[リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|システム モニターでは、使用中のバッファー マネージャー ページ要求の数などのリソース使用量が主に追跡され、イベントを監視するための定義済みオブジェクトおよびカウンターやユーザー定義カウンターを使用して、サーバーのパフォーマンスおよび利用状況を監視できます。 システム モニター (Microsoft Windows NT 4.0 の場合はパフォーマンス モニター) は、イベントに関するデータではなく、メモリの使用量、アクティブなトランザクションの数、ブロックされたロックの数、CPU の利用状況など、イベントの数と比率を収集します。 特定のカウンターにしきい値を設定して、オペレーターに通知する警告を生成できます。<br /><br /> システム モニターは Microsoft Windows Server および Windows オペレーティング システムで機能します。 システム モニターでは、Windows NT 4.0 以降で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをリモートまたはローカルで監視できます。<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] とシステム モニターの重要な違いは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ではデータベース エンジンのイベントが監視されるのに対し、システム モニターではサーバー プロセスに関連したリソース使用量が監視されることです。|  
|[利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の利用状況モニターは、現在のアクティビティのカスタム ビューの場合に便利であり、次の情報をグラフィカルに表示します。<br /><br />- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで実行中のプロセス<br />- ブロックされているプロセス<br />- ロック<br />- ユーザーの利用状況|  
|[パフォーマンス ダッシュボード](../../relational-databases/performance/performance-dashboard.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 内のパフォーマンス ダッシュボードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にパフォーマンスのボトルネックが存在するかどうかを迅速に特定するのに役立ちます。|  
|[クエリ調整アシスタント (QTA)](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|クエリ調整アシスタント (QTA) 機能を利用して、推奨されるワークフローに従うことで、新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンへのアップグレード時のパフォーマンスの安定性を維持できます。これについては、「[クエリ ストアの使用シナリオ](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)」の「*新しい SQL Server にアップグレードするときにパフォーマンスの安定性を維持する*」セクションに記載されています。 |  
|[クエリ ストア](../..//relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|クエリ ストア機能を使用すると、クエリ プランの選択やパフォーマンスを把握できます。 これにより、クエリ プランの変更によって生じるパフォーマンスの違いがすばやくわかるようになり、パフォーマンス上のトラブルシューティングを簡略化できます。 クエリのストアは、自動的にクエリ、プラン、および実行時統計の履歴をキャプチャし、確認用に保持します。 データは時間枠で区分されるため、データベースの使用パターンを表示して、サーバー上でクエリ プランが変わった時点を確認することができます。|
|[SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャは次のとおりです。<br /><br /> [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)<br />[sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)<br />[sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)<br />[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)<br />[sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay では、複数のコンピューターを使用してトレース データを再生し、ミッションクリティカルなワークロードをシミュレートできます。|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、バッチまたはトランザクションの開始などのエンジン プロセス イベントが追跡され、サーバーおよびデータベースの利用状況 (デッドロック、致命的なエラー、ログインの利用状況など) を監視できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルまたはファイルにキャプチャして、後で分析できます。また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でキャプチャしたイベントをステップごとに再生して、何が起こったかを正確に確認することもできます。|  
|[システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)|次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム ストアド プロシージャでは、多くの監視タスクの強力な代替方法が提供されています。<br /><br /> [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md):<br />                    このシステム ストアド プロシージャは、現在実行中のステートメントとそのステートメントがブロックされているかどうかなど、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーおよびプロセスに関するスナップショット情報を報告します。<br /><br /> [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md):<br />                    このシステム ストアド プロシージャは、オブジェクト ID、インデックス ID、ロックの種類、ロックを適用する種類またはリソースなど、ロックに関するスナップショット情報を報告します。<br /><br /> [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md): <br />                    このシステム ストアド プロシージャは、テーブルまたはデータベース全体が使用している現在のディスク容量の推定値を表示します。<br /><br /> [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):<br />                    CPU 使用量、I/O 使用量、 **sp_monitor** を最後に実行してからのアイドル時間などの統計データを表示します。|  
|[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)|トレース フラグでは、サーバー内の特定の利用状況に関する情報が示されます。このトレース フラグを使用して、問題やデッドロック チェーンなどのパフォーマンスの問題を診断します。|  
  
## <a name="choosing-a-monitoring-tool"></a>監視ツールの選択  
 どの監視ツールを使用するかは、監視対象のイベントまたは利用状況によって決まります。  
  
|イベントまたは利用状況|拡張イベント|SQL Server プロファイラー|Distributed Replay|システム モニター|利用状況モニター|Transact-SQL|エラー ログ|パフォーマンス ダッシュボード|  
|-----------------------|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|----------------|   
|傾向分析|はい|はい||はい|||||  
|キャプチャしたイベントの再生||可 (1 台のコンピューターから)|可 (複数のコンピューターから)||||||  
|アドホック監視|可<sup>1</sup>|はい|||はい|はい|はい|はい|  
|警告の生成||||はい|||||  
|グラフィック インターフェイス|はい|はい||はい|はい||はい|はい|  
|カスタム アプリケーション内での使用|はい|はい<sup>2</sup>||||はい|||  
  
 <sup>1</sup> [SQL Server Management Studio XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md) の使用    
 <sup>2</sup> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] システム ストアド プロシージャの使用。  
  
## <a name="windows-monitoring-tools"></a>Windows 監視ツール  
 Windows オペレーティング システムおよび Windows Server 2003 では、次の監視ツールが提供されています。  
  
|ツール|[説明]|  
|----------|-----------------|  
|タスク マネージャー|システム上で実行中のプロセスやアプリケーションの概要を示します。|  
|ネットワーク モニター エージェント|ネットワーク トラフィックを監視します。|  
  
 Windows オペレーティング システムまたは Windows Server ツールの詳細については、Windows のマニュアルを参照してください。  
  
  
