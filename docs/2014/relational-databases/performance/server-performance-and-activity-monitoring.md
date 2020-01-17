---
title: サーバーのパフォーマンスと利用状況の監視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7289c18fac421bbdb5ccc0e00a3bea60b7a22d9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150615"
---
# <a name="server-performance-and-activity-monitoring"></a>サーバーのパフォーマンスと利用状況の監視
  データベースを監視する目的は、サーバーのパフォーマンスを評価することです。 適切な監視には、現在のパフォーマンスのスナップショットを定期的にキャプチャして問題の原因となっているプロセスを特定したり、長期にわたって継続的にデータを採取してパフォーマンスの傾向を追跡する作業が必要です。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows オペレーティング システムでは、データベースの現在の状態を参照したり、状態の変化に伴うパフォーマンスを追跡するためのユーティリティが用意されています。  
  
 次のセクションには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および Windows のパフォーマンスと利用状況の監視ツールの使用方法を説明するトピックが含まれています。 ここで説明する内容は次のとおりです。  
  
## <a name="in-this-section"></a>このセクションの内容  
 **Windows ツールで監視タスクを実行するには**  
  
-   [システム モニターの起動 &#40;Windows&#41;](start-system-monitor-windows.md)  
  
-   [Windows アプリケーション ログの表示 &#40;Windows&#41;](view-the-windows-application-log-windows-10.md)  
  
 **Windows ツールで SQL Server データベースの警告を作成するには**  
  
-   [SQL Server データベースの警告のセットアップ &#40;Windows&#41;](set-up-a-sql-server-database-alert-windows.md)  
  
 **SQL Server Management Studio で監視タスクを実行するには**  
  
-   [SQL Server エラー ログの表示 &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
-   [利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **Transact-SQL ストアド プロシージャを使用して SQL トレースで監視タスクを実行するには**  
  
-   [トレースの作成 &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)  
  
-   [トレース フィルターの設定 &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
-   [既存のトレースの変更 &#40;Transact-SQL&#41;](../sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [保存されているトレースの表示 &#40;Transact-SQL&#41;](../sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [フィルター情報の表示 &#40;Transact-SQL&#41;](../sql-trace/view-filter-information-transact-sql.md)  
  
-   [トレースの削除 &#40;Transact-SQL&#41;](../sql-trace/delete-a-trace-transact-sql.md)  
  
 **SQL Server Profiler を使用してトレースを作成および変更するには**  
  
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
  
 **SQL Server Profiler を使用してトレースを開始、一時停止、および停止するには**  
  
-   [サーバーへの接続後の自動的なトレースの開始 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [トレースの一時停止 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [トレースの停止 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [一時停止または停止したトレースの再開 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **SQL Server Profiler を使用してトレースを開き、トレースの表示方法を構成するには**  
  
-   [トレース ファイルを開く &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [トレース テーブルを開く &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [トレース ウィンドウの消去 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [トレース ウィンドウを閉じる &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [トレース定義の既定値の設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [トレース表示の既定値の設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **SQL Server Profiler を使用してトレースを再生するには**  
  
-   [トレース ファイルを再生する &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [トレース テーブルを再生する &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [一度に単一のイベントの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [ブレークポイントまでの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [カーソルまでの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Transact-SQL スクリプトの再生 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **SQL Server Profiler を使用してトレース テンプレートを作成、変更、および使用するには**  
  
-   [トレース テンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [トレース テンプレートの変更 &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
-   [実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [トレース テンプレートのエクスポート &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [トレース テンプレートのインポート &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **SQL Server Profiler トレースを使用してサーバーのパフォーマンスを収集および監視するには**  
  
-   [トレース中の値列またはデータ列の検索 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Deadlock Graph の保存 &#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Showplan XML イベントを個別に保存する方法 &#40;SQL Server Profiler&#41;](save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Showplan XML Statistics Profile イベントを個別に保存 &#40;SQL Server Profiler&#41;](save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [トレースからのスクリプトの抽出 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [トレースと Windows パフォーマンス ログ データの関連付け &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
