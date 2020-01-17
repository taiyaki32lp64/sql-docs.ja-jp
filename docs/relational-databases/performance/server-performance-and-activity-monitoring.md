---
title: サーバーのパフォーマンスと利用状況の監視 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 073095217dc08f2f11605f8b0e7b5da11035e34a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113345"
---
# <a name="server-performance-and-activity-monitoring"></a>サーバーのパフォーマンスと利用状況の監視
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベースを監視する目的は、サーバーのパフォーマンスを評価することです。 適切な監視には、現在のパフォーマンスのスナップショットを定期的にキャプチャして問題の原因となっているプロセスを特定したり、長期にわたって継続的にデータを採取してパフォーマンスの傾向を追跡する作業が必要です。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows オペレーティング システムでは、データベースの現在の状態を参照したり、状態の変化に伴うパフォーマンスを追跡するためのユーティリティが用意されています。  
  
 次のセクションには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および Windows のパフォーマンスと利用状況の監視ツールの使用方法を説明するトピックが含まれています。 ここで説明する内容は次のとおりです。  
  
## <a name="to-perform-monitoring-tasks-with-windows-tools"></a>Windows ツールで監視タスクを実行するには 
  
-   [システム モニターの起動 &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
-   [Windows アプリケーション ログの表示 &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
## <a name="to-create-sql-server-database-alerts-with-windows-tools"></a>Windows ツールで SQL Server データベースの警告を作成するには  
  
-   [SQL Server データベースの警告のセットアップ &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)  

## <a name="to-perform-monitoring-tasks-with-extended-events"></a>拡張イベントで監視タスクを実行するには  
 
 -   [拡張イベント](../../relational-databases/extended-events/extended-events.md)
 
 -   [クイック スタート:SQL Server の拡張イベント](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
 
 -   [オブジェクト エクスプローラーでのイベント セッションの管理](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)
 
 -   [拡張イベント セッションの変更](../../relational-databases/extended-events/alter-an-extended-events-session.md)
 
 -   [既存の SQL トレース スクリプトから拡張イベント セッションへの変換](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)
 
 -   [SQL トレースのイベント クラスと等価な拡張イベントを確認する](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)
   
## <a name="to-perform-monitoring-tasks-with-sql-server-management-studio"></a>SQL Server Management Studio で監視タスクを実行するには  
  
-   [SQL Server エラー ログの表示 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
-   [利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)  

-   [クエリ ストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)

## <a name="to-perform-monitoring-tasks-with-sql-trace-and-sql-server-profiler"></a>SQL Trace および SQL Server Profiler を使用して監視タスクを実行するには

> [!IMPORTANT]
> 次のセクションでは、SQL トレースと [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用する方法について説明します。  
> SQL トレースと [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、非推奨です。 Microsoft SQL Server の Trace や Replay オブジェクトを含む *Microsoft.SqlServer.Management.Trace* 名前空間も非推奨とされます。   
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
> 代わりに拡張イベントを使用します。 [拡張イベント](../../relational-databases/extended-events/extended-events.md)について詳しくは、「[クイック スタート:SQL Server 拡張イベント](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)」および [SSMS XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md) に関するページをご覧ください。

> [!NOTE] 
> Analysis Services のワークロード用の [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は非推奨とされず、引き続きサポートされます。

### <a name="to-perform-monitoring-tasks-with-sql-trace-by-using-transact-sql-stored-procedures"></a>Transact-SQL ストアド プロシージャを使用して SQL トレースで監視タスクを実行するには  
  
-   [トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
-   [トレース フィルターの設定 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
-   [既存のトレースの変更 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [保存されているトレースの表示 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [フィルター情報の表示 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)  
  
-   [トレースの削除 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/delete-a-trace-transact-sql.md)  
  
### <a name="to-create-and-modify-traces-by-using-sql-server-profiler"></a>SQL Server Profiler を使用してトレースを作成および変更するには  
  
-   [トレースの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [グローバル トレース オプションの設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [トレース ファイルに含めるイベントとデータ列の指定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [トレースを実行するための Transact-SQL スクリプトの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [トレース結果のファイルへの保存 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [トレース ファイルの最大ファイル サイズの設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [トレース結果のテーブルへの保存 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [トレース テーブルの最大テーブル サイズの設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [トレース内のイベントへのフィルターの適用 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [フィルター情報の表示 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [フィルターの変更 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [イベントの開始時刻に基づいたイベントのフィルター選択 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [イベントの終了時刻に基づいたフィルターでのイベントの選択 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [トレースでのサーバー プロセス ID &#40;SPIDs&#41; のフィルター選択 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [トレースに表示される列の構成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
### <a name="to-start-pause-and-stop-traces-by-using-sql-server-profiler"></a>SQL Server Profiler を使用してトレースを開始、一時停止、および停止するには  
  
-   [サーバーへの接続後の自動的なトレースの開始 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [トレースの一時停止 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [トレースの停止 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [一時停止または停止したトレースの再開 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
### <a name="to-open-traces-and-configure-how-traces-are-displayed-by-using-sql-server-profiler"></a>SQL Server Profiler を使用してトレースを開き、トレースの表示方法を構成するには  
  
-   [トレース ファイルを開く &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [トレース テーブルを開く &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [トレース ウィンドウの消去 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [トレース ウィンドウを閉じる &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [トレース定義の既定値の設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [トレース表示の既定値の設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
### <a name="to-replay-traces-by-using-sql-server-profiler"></a>SQL Server Profiler を使用してトレースを再生するには  
  
-   [トレース ファイルを再生する &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [トレース テーブルを再生する &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [一度に単一のイベントの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [ブレークポイントまでの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [カーソルまでの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Transact-SQL スクリプトの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
### <a name="to-create-modify-and-use-trace-templates-by-using-sql-server-profiler"></a>SQL Server Profiler を使用してトレース テンプレートを作成、変更、および使用するには  
  
-   [トレース テンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [トレース テンプレートの変更 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
-   [実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [トレース テンプレートのエクスポート &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [トレース テンプレートのインポート &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
### <a name="to-use-sql-server-profiler-traces-to-collect-and-monitor-server-performance"></a>SQL Server Profiler トレースを使用してサーバーのパフォーマンスを収集および監視するには  
  
-   [トレース中の値列またはデータ列の検索 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Deadlock Graph の保存 &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Showplan XML イベントを個別に保存する方法 &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Showplan XML Statistics Profile イベントを個別に保存 &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [トレースからのスクリプトの抽出 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [トレースと Windows パフォーマンス ログ データの関連付け &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
