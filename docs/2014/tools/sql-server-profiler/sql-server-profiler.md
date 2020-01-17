---
title: SQL Server Profiler |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], about SQL Server Profiler
- traces [SQL Server], SQL Server Profiler
- database monitoring [SQL Server], SQL Server Profiler
- tuning databases [SQL Server], SQL Server Profiler
- SQL Server Profiler
- server performance [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler]
- tracing [SQL Server]
- monitoring performance [SQL Server], SQL Server Profiler
- events [SQL Server], SQL Server Profiler
- SQL Server Profiler, about SQL Server Profiler
- tools [SQL Server], SQL Server Profiler
- database performance [SQL Server], SQL Server Profiler
- trace [SQL Server]
ms.assetid: 3ad5f33d-559e-41a4-bde6-bb98792f7f1a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c9b0bb789dc7571a988c434f526070546d8db454
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211047"
---
# <a name="sql-server-profiler"></a>SQL Server Profiler
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、トレースを作成および管理し、トレースの結果を分析および再生するために使用する機能の豊富なインターフェイスです。 キャプチャされたイベントはトレース ファイルに保存され、後で分析したり、問題の発生したステップを厳密に再現して診断する際に利用できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]のトレース キャプチャおよびトレース再生用の [!INCLUDE[ssDE](../../includes/ssde-md.md)] は廃止されます。 これらの機能は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の次のバージョンではサポートされますが、その後のバージョンでは削除されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のどのバージョンであるかは決定していません。 Microsoft SQL Server の Trace オブジェクトや Replay オブジェクトを含む *Microsoft.SqlServer.Management.Trace* 名前空間も非推奨とされます。 Analysis Services のワークロード用の [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は非推奨とされておらず、引き続きサポートされます。  
>   
>  以下の表に、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でトレース データのキャプチャおよび再生を行うために使用が推奨される機能を示します。  
  
||||  
|-|-|-|  
|**機能\対象のワークロード**|**リレーショナル エンジン**|**Analysis Services**|  
|**トレースのキャプチャ**|SQL Server Management Studio の拡張イベントのグラフィカル ユーザー インターフェイス|SQL Server Profiler|  
|**トレースの再生**|Distributed Replay|SQL Server Profiler|  
  
## <a name="benefits-of-sql-server-profiler"></a>SQL Server Profiler の利点  
 Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] または Analysis Services のインスタンスを監視するための SQL トレースのグラフィカル ユーザー インターフェイスです。 各イベントに関するデータをキャプチャし、ファイルやテーブルに保存して、後で分析できます。 たとえば、稼動環境を監視して、どのストアド プロシージャの実行が遅く、パフォーマンスに影響を与えているかを確認できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、次のようなアクティビティに使用します。  
  
-   問題の原因を特定するため、問題の発生したクエリを順次実行する。  
  
-   実行速度の遅いクエリを検出し、その原因を診断する。  
  
-   問題の原因となる一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをキャプチャする。 トレース ファイルに保存された内容をテスト サーバー上にレプリケートし、問題の診断に利用できます。  
  
-   ワークロードを調整するため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスを監視する。 データベース ワークロードに関してデータベースの物理設計を調整する方法については、「 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)」を参照してください。  
  
-   問題を診断するために、さまざまなパフォーマンス カウンターの関連を調べる。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行された操作の監査もサポートしています。 監査では、後でセキュリティ管理者が調査できるように、セキュリティ関連の操作を記録します。  
  
## <a name="sql-server-profiler-concepts"></a>SQL Server Profiler の概念  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用するには、ツールがどのように機能するのかを説明する用語を理解しておく必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用するときは、SQL トレースを理解しておくと役に立ちます。 詳細については、「 [SQL Trace](../../relational-databases/sql-trace/sql-trace.md)」を参照してください。  
  
 **Event**  
 イベントとは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンス内で発生するアクションです。 次に例を示します。  
  
-   ログインの接続、失敗、および接続解除。  
  
-   Transact-SQL SELECT、INSERT、UPDATE、および DELETE ステートメント。  
  
-   リモート プロシージャ コール (RPC) のバッチ ステータス。  
  
-   ストアド プロシージャの開始または終了。  
  
-   ストアド プロシージャ内のステートメントの開始または終了。  
  
-   SQL バッチの開始または終了。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに書き込まれたエラー。  
  
-   データベース オブジェクトで取得または解放されたロック。  
  
-   開かれたカーソル。  
  
-   セキュリティ権限の確認。  
  
 イベントによって生成されたデータは、すべてトレースに 1 行で表示されます。 この行の各データ列には、イベントの詳しい説明が表示されます。  
  
 **EventClass**  
 イベント クラスは、トレースできるイベントの種類を定義します。 イベント クラスには、イベントによって報告できるすべてのデータが含まれています。 イベント クラスの例を次に示します。  
  
-   **SQL:BatchCompleted**  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **Lock:Acquired**  
  
-   **Lock:Released**  
  
 **EventCategory**  
 イベント カテゴリは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]内でイベントを分類する方法を定義します。 たとえば、ロック イベント クラスはすべて、 **ロック** イベント カテゴリに分類されます。 ただし、イベント カテゴリは [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]でしか存在しません。 この用語に、エンジン イベントを分類する方法は反映されていません。  
  
 **DataColumn**  
 各データ列は、トレースでキャプチャされるイベント クラスの属性です。 収集できるデータの種類はイベント クラスによって異なるため、必ずしもすべてのデータ列がすべてのイベント クラスに使用されるわけではありません。 たとえば、 **Lock:Acquired** イベント クラスをキャプチャするトレースでは、ロックされたページ ID またはロックされた行の値が **BinaryData** データ列に格納されますが、 **Integer Data** データ列にはまったく値が格納されません。これは、キャプチャ対象のイベント クラスにこのデータ列が適合しないためです。  
  
 **テンプレート**  
 テンプレートは、トレースの既定の構成を定義します。 特に、テンプレートには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して監視するイベント クラスを指定します。 たとえば、使用するイベント、データ列、およびフィルターを指定するテンプレートを作成できます。 テンプレートは、実行するのではなく、.tdf という拡張子を付けてファイルとして保存しておきます。 保存したテンプレートは、そのテンプレートに基づいて作成したトレースの実行時にどのようなトレース データをキャプチャするかを制御します。  
  
 **トレース**  
 トレースでは、選択したイベント、データ列、およびフィルターに基づいたデータをキャプチャします。 たとえば、例外エラーを監視するトレースを作成できます。 これには、 **Exception** イベント クラスを選択し、そのデータ列である **Error**、 **State**、および **Severity** を選択します。 トレース結果で意味のあるデータを示すには、これら 3 列のデータを収集する必要があります。 このようにして構成されたトレースを実行し、サーバーで発生するすべての **Exception** イベントに関するデータを収集することができます。 トレース データは、保存することも、すぐに分析に使用することもできます。 トレースは、後日再生できます。ただし、 **Exception** イベントなど、再生不可能なイベントもあります。 また、トレースをテンプレートとして保存しておき、これに似たトレースを後日作成することもできます。  
  
 SQL Server では、SQL Server のインスタンスをトレースするために 2 とおりの方法が用意されています。つまり、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用してトレースする方法と、システム ストアド プロシージャを使用してトレースする方法です。  
  
 **[フィルター]**  
 トレースまたはテンプレートを作成する際には、指定したイベントで収集されたデータをフィルターで選択する基準を定義できます。 トレースが大きくなりすぎないようにするためには、イベント データのサブセットだけが収集されるようにフィルターを適用します。 たとえば、トレースでキャプチャする Microsoft Windows のユーザー名を特定のユーザーに限定して出力データを絞り込むことができます。  
  
 フィルターが設定されていない場合は、選択したイベント クラスのすべてのイベントがトレースに出力されます。  
  
## <a name="sql-server-profiler-tasks"></a>SQL Server Profiler のタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|特定の種類のイベントを監視することを目的として SQL Server に備わっている定義済みのテンプレートと、トレースを再生するために必要な権限を紹介します。|[SQL Server プロファイラーのテンプレートとアクセス許可](sql-server-profiler-templates-and-permissions.md)|  
|SQL Server Profiler を実行する方法について説明します。|[SQL Server Profiler の実行に必要なアクセス許可](permissions-required-to-run-sql-server-profiler.md)|  
|トレースの作成方法について説明します。|[トレースの作成 &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)|  
|トレース ファイルに含めるイベントおよびデータ列を指定する方法について説明します。|[トレース ファイルに含めるイベントとデータ列の指定 &#40;SQL Server Profiler&#41;](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)|  
|トレース結果をファイルに保存する方法について説明します。|[トレース結果のファイルへの保存 &#40;SQL Server Profiler&#41;](save-trace-results-to-a-file-sql-server-profiler.md)|  
|トレース結果をテーブルに保存する方法について説明します。|[トレース結果のテーブルへの保存 &#40;SQL Server Profiler&#41;](save-trace-results-to-a-table-sql-server-profiler.md)|  
|トレース内のイベントをフィルター処理する方法について説明します。|[トレース内のイベントへのフィルターの適用 &#40;SQL Server Profiler&#41;](filter-events-in-a-trace-sql-server-profiler.md)|  
|フィルター情報を表示する方法について説明します。|[フィルター情報の表示 &#40;SQL Server Profiler&#41;](view-filter-information-sql-server-profiler.md)|  
|フィルターを変更する方法について説明します。|[フィルターの変更 &#40;SQL Server Profiler&#41;](modify-a-filter-sql-server-profiler.md)|  
|トレース ファイルの最大ファイル サイズを設定する方法について説明します (SQL Server Profiler)。|[トレース ファイルの最大ファイル サイズの設定 &#40;SQL Server Profiler&#41;](set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)|  
|トレース テーブルの最大テーブル サイズを設定する方法について説明します。|[トレース テーブルの最大テーブル サイズの設定 &#40;SQL Server Profiler&#41;](set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)|  
|トレースの開始方法について説明します。|[トレースを開始する](start-a-trace.md)|  
|サーバーへの接続後、トレースを自動的に開始する方法について説明します。|[サーバーへの接続後の自動的なトレースの開始 &#40;SQL Server Profiler&#41;](start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)|  
|イベントの開始時刻に基づいてイベントをフィルター選択する方法について説明します。|[イベントの開始時刻に基づいたイベントのフィルター選択 &#40;SQL Server Profiler&#41;](filter-events-based-on-the-event-start-time-sql-server-profiler.md)|  
|イベントの終了時刻に基づいてイベントをフィルター選択する方法について説明します。|[イベントの終了時刻に基づいたフィルターでのイベントの選択 &#40;SQL Server Profiler&#41;](filter-events-based-on-the-event-end-time-sql-server-profiler.md)|  
|トレース内のサーバー プロセス ID (SPID) をフィルター選択する方法について説明します。|[トレースでのサーバー プロセス ID &#40;SPIDs &#41;のフィルター選択 &#40;SQL Server Profiler &#41;](filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)|  
|トレースを一時停止する方法について説明します。|[トレースの一時停止 &#40;SQL Server Profiler&#41;](pause-a-trace-sql-server-profiler.md)|  
|トレースを停止する方法について説明します。|[トレースの停止 &#40;SQL Server Profiler&#41;](stop-a-trace-sql-server-profiler.md)|  
|一時停止後または停止後にトレースを実行する方法について説明します。|[一時停止または停止したトレースの再開 &#40;SQL Server Profiler&#41;](run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)|  
|トレース ウィンドウをクリアする方法について説明します。|[トレース ウィンドウの消去 &#40;SQL Server Profiler&#41;](clear-a-trace-window-sql-server-profiler.md)|  
|トレース ウィンドウを閉じる方法について説明します。|[トレース ウィンドウを閉じる &#40;SQL Server Profiler&#41;](close-a-trace-window-sql-server-profiler.md)|  
|トレース定義の既定値を設定する方法について説明します。|[トレース定義の既定値の設定 &#40;SQL Server Profiler&#41;](set-trace-definition-defaults-sql-server-profiler.md)|  
|トレース表示の既定値を設定する方法について説明します。|[トレース表示の既定値の設定 &#40;SQL Server Profiler&#41;](set-trace-display-defaults-sql-server-profiler.md)|  
|トレース ファイルを開く方法について説明します。|[トレース ファイルを開く &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)|  
|トレース テーブルを開く方法について説明します。|[トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)|  
|トレース テーブルを再生する方法について説明します。|[トレース テーブルを再生する &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)|  
|トレース ファイルを再生する方法について説明します。|[トレース ファイルを再生する &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)|  
|一度に単一のイベントを再生する方法について説明します。|[一度に単一のイベントの再生 &#40;SQL Server Profiler&#41;](replay-a-single-event-at-a-time-sql-server-profiler.md)|  
|ブレークポイントまで再生する方法について説明します。|[ブレークポイントまでの再生 &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)|  
|カーソルまで再生する方法について説明します。|[カーソルまでの再生 &#40;SQL Server Profiler&#41;](replay-to-a-cursor-sql-server-profiler.md)|  
|Transact-SQL スクリプトを再生する方法について説明します。|[Transact-SQL スクリプトの再生 &#40;SQL Server Profiler&#41;](replay-a-transact-sql-script-sql-server-profiler.md)|  
|トレース テンプレートの作成方法について説明します。|[トレース テンプレートの作成 &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)|  
|トレース テンプレートの変更方法について説明します。|[トレース テンプレートの変更 &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)|  
|グローバル トレース オプションを設定する方法について説明します。|[グローバル トレース オプションの設定 &#40;SQL Server Profiler&#41;](set-global-trace-options-sql-server-profiler.md)|  
|トレース中に値列またはデータ列を検索する方法について説明します。|[トレース中の値列またはデータ列の検索 &#40;SQL Server Profiler&#41;](find-a-value-or-data-column-while-tracing-sql-server-profiler.md)|  
|実行中のトレースからテンプレートを作成する方法について説明します。|[実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)|  
|トレース ファイルまたはトレース テーブルからテンプレートを作成する方法について説明します。|[トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)|  
|トレースを実行するための Transact-SQL スクリプトを作成する方法について説明します。|[トレースを実行するための Transact-SQL スクリプトの作成 &#40;SQL Server Profiler&#41;](create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)|  
|トレース テンプレートをエクスポートする方法について説明します。|[トレース テンプレートのエクスポート &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)|  
|トレース テンプレートをインポートする方法について説明します。|[トレース テンプレートのインポート &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)|  
|スクリプトをトレースから抽出する方法について説明します。|[トレースからのスクリプトの抽出 &#40;SQL Server Profiler&#41;](extract-a-script-from-a-trace-sql-server-profiler.md)|  
|トレースと Windows パフォーマンス ログ データを相互に関連付ける方法について説明します。|[トレースと Windows パフォーマンス ログ データの関連付け &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)|  
|トレースに表示される列を構成する方法について説明します。|[トレースに表示される列の構成 &#40;SQL Server Profiler&#41;](organize-columns-displayed-in-a-trace-sql-server-profiler.md)|  
|SQL Server Profiler を起動する方法について説明します。|[SQL Server Profiler の起動](start-sql-server-profiler.md)|  
|トレースとトレース テンプレートを保存する方法について説明します。|[トレースとトレース テンプレートの保存](save-traces-and-trace-templates.md)|  
|トレース テンプレートの変更方法について説明します。|[トレース テンプレートを変更する](modify-trace-templates.md)|  
|トレースと Windows パフォーマンス ログ データを相互に関連付ける方法について説明します。|[トレースと Windows パフォーマンス ログ データの関連付け](correlate-a-trace-with-windows-performance-log-data.md)|  
|SQL Server Profiler を使用したトレースの表示と分析の方法について説明します。|[SQL Server Profiler を使用したトレースの表示と分析](view-and-analyze-traces-with-sql-server-profiler.md)|  
|SQL Server Profiler を使用してデッドロックを分析する方法について説明します。|[SQL Server Profiler を使用したデッドロックの分析](analyze-deadlocks-with-sql-server-profiler.md)|  
|SQL Server Profiler での SHOWPLAN 結果を使用してクエリを分析する方法について説明します。|[SQL Server Profiler での Showplan 結果を使用したクエリの分析](analyze-queries-with-showplan-results-in-sql-server-profiler.md)|  
|SQL Server Profiler でトレースにフィルターを適用する方法について説明します。|[SQL Server Profiler でのトレースへのフィルターの適用](filter-traces-with-sql-server-profiler.md)|  
|SQL Server Profiler の再生機能の使用方法について説明します。|[トレースの再生](replay-traces.md)|  
|SQL Server Profiler の状況依存ヘルプ トピックについて紹介します。|[SQL Server Profiler の F1 ヘルプ](sql-server-profiler-f1-help.md)|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] でパフォーマンスと利用状況を監視する際に使用される一連のシステム ストアド プロシージャを紹介します。|[SQL Server Profiler のストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)|  
  
## <a name="see-also"></a>関連項目  
 [Locks イベント カテゴリ](../../relational-databases/event-classes/locks-event-category.md)   
 [Sessions イベント カテゴリ](../../relational-databases/event-classes/sessions-event-category.md)   
 [Stored Procedures イベント カテゴリ](../../relational-databases/event-classes/stored-procedures-event-category.md)   
 [TSQL イベント カテゴリ](../../relational-databases/event-classes/tsql-event-category.md)   
 [サーバーのパフォーマンスと利用状況の監視](../../relational-databases/performance/server-performance-and-activity-monitoring.md)  
  
  
