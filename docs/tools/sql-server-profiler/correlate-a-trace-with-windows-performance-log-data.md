---
title: トレースと Windows パフォーマンス ログ データの関連付け | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 92d925158e04e11b0a00181ec0ecaf42c6ff7b37
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930098"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>トレースと Windows パフォーマンス ログ データの関連付け
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用すると、Microsoft Windows パフォーマンス ログを開き、トレースと関連付けるカウンターを選択し、選択したパフォーマンス カウンターをトレースと共に [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のグラフィカル ユーザー インターフェイスに表示できます。 トレース ウィンドウでイベントを選択すると、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] の [システム モニター] データ ウィンドウ画面の赤い縦棒で、選択したトレース イベントに関連付けられているパフォーマンス ログ データが示されます。  
  
 トレースをパフォーマンス カウンターに関連付けるには、 **StartTime** および **EndTime** data columns, および then click **で** [ファイル] [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu. パフォーマンス ログを開き、トレースに関連付けるシステム モニター オブジェクトおよびカウンターを選択します。  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>トレースとパフォーマンス ログ データとを相互に関連付けるには  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で、保存されているトレース ファイルまたはトレース テーブルを開きます。 イベント データを収集している実行中のトレースを相互に関連付けることはできません。 システム モニター データとの相関関係の精度を保証するには、 **[StartTime]** データ列と **[EndTime]** データ列の両方がトレースに含まれている必要があります。  
  
2.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **[ファイル]** メニューで、 **[パフォーマンス データのインポート]** をクリックします。  
  
3.  **[開く]** ダイアログ ボックスで、パフォーマンス ログが含まれているファイルを選択します。 パフォーマンス ログ データは、トレース データがキャプチャされたのと同じ期間にキャプチャされている必要があります。  
  
4.  **[パフォーマンス カウンター制限]** ダイアログ ボックスで、トレースと一緒に表示するシステム モニター オブジェクトとカウンターに対応するチェック ボックスをオンにします。 クリックして **OK.**  
  
5.  トレース イベント ウィンドウでイベントを選択するか、トレース イベント ウィンドウ内のいくつかの隣接する行の間を、方向キーを使用して移動します。 **[システム モニター データ]** ウィンドウ内の赤い縦棒は、選択したトレース イベントと相互に関連しているパフォーマンス ログ データを示します。  
  
6.  システム モニターのグラフで、関心のあるポイントをクリックします。 その時点に最も近い対応するトレース行が選択されます。 時間範囲を拡大するには、システム モニターのグラフでマウス ポインターをクリックしてドラッグします。  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>異なるバージョンの Windows 間で共有できるパフォーマンス ログを作成するには  
  
1.  コントロール パネルで **[管理ツール]** を開き、 **[パフォーマンス]** をダブルクリックします。  
  
2.  **[パフォーマンス]** ダイアログ ボックスで、 **[パフォーマンス ログと警告]** を展開して、 **[カウンター ログ]** を右クリックし、 **[新しいログの設定]** をクリックします。  
  
3.  カウンター ログの名前を入力し、 **[OK]** をクリックします。  
  
4.  **[全般]** タブで **[カウンターの追加]** をクリックします。  
  
5.  **[パフォーマンス オブジェクト]** ボックスで、監視するパフォーマンス オブジェクトを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パフォーマンス オブジェクトの名前は 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスの場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で始まり、名前付きインスタンスの場合は MSSQL$*instanceName*で始まります。  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス、プロセッサ時間やディスク時間などのその他の重要な値から必要なカウンターを追加します。  
  
7.  カウンターの追加を終了したら、 **[閉じる]** をクリックします。  
  
8.  **[データのサンプル間隔]** の間隔の値を設定します。 5 分程度のサンプリング間隔から始めて、必要に応じて間隔を調整します。  
  
9. **[ログ ファイル]** タブで、 **[ログ ファイルの種類]** ボックスの一覧から **[テキスト ファイル (カンマ区切り)]** を選択します。 コンマ区切りのテキストのログ ファイルは、異なるバージョンの Windows 間で共有できます。また、Microsoft Excel などのレポート ツールで後から表示できます。  
  
10. **[スケジュール]** タブで、監視スケジュールを指定します。  
  
11. **[OK]** をクリックし、パフォーマンス ログを作成します。  
