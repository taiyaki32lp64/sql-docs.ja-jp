---
title: トレースと Windows パフォーマンス ログ データ (SQL Server Profiler) の関連付け |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], logs
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3294c9fd70ebae8eab4e76e17b2e0a21771ec26f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065048"
---
# <a name="correlate-a-trace-with-windows-performance-log-data-sql-server-profiler"></a>トレースと Windows パフォーマンス ログ データの関連付け (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] では、Microsoft Windows システム モニター カウンターを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] イベントと相互に関連付けることができます。 Windows システム モニターでは、指定されたカウンターのシステムの利用状況がパフォーマンス ログに記録されます。  
  
> [!NOTE]  
>  異なるバージョンの Windows 間でログを共有する方法の詳細については、このトピックの最後に記載されている手順を参照してください。  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>トレースとパフォーマンス ログ データとを相互に関連付けるには  
  
1.  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]で、保存されているトレース ファイルまたはトレース テーブルを開きます。 イベント データを収集している実行中のトレースを相互に関連付けることはできません。 システム モニター データとの相関関係の精度を保証するには、 **[StartTime]** データ列と **[EndTime]** データ列の両方がトレースに含まれている必要があります。  
  
2.   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] **[ファイル]** メニューで、 **[パフォーマンス データのインポート]** をクリックします。  
  
3.  **[開く]** ダイアログ ボックスで、パフォーマンス ログが含まれているファイルを選択します。 パフォーマンス ログ データは、トレース データがキャプチャされたのと同じ期間にキャプチャされている必要があります。  
  
4.  **[パフォーマンス カウンター制限]** ダイアログ ボックスで、トレースと一緒に表示するシステム モニター オブジェクトとカウンターに対応するチェック ボックスをオンにします。 **[OK]** をクリックします。  
  
5.  トレース イベント ウィンドウでイベントを選択するか、トレース イベント ウィンドウ内のいくつかの隣接する行の間を、方向キーを使用して移動します。 **[システム モニター データ]** ウィンドウ内の赤い縦棒は、選択したトレース イベントと相互に関連しているパフォーマンス ログ データを示します。  
  
6.  システム モニターのグラフで、関心のあるポイントをクリックします。 その時点に最も近い対応するトレース行が選択されます。 時間範囲を拡大するには、システム モニターのグラフでマウス ポインターをクリックしてドラッグします。  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>異なるバージョンの Windows 間で共有できるパフォーマンス ログを作成するには  
  
1.  コントロール パネルで **[管理ツール]** を開き、 **[パフォーマンス]** をダブルクリックします。  
  
2.  **[パフォーマンス]** ダイアログ ボックスで、 **[パフォーマンス ログと警告]** を展開して、 **[カウンター ログ]** を右クリックし、 **[新しいログの設定]** をクリックします。  
  
3.  カウンター ログの名前を入力し、 **[OK]** をクリックします。  
  
4.  **[全般]** タブで **[カウンターの追加]** をクリックします。  
  
5.  **[パフォーマンス オブジェクト]** ボックスで、監視するパフォーマンス オブジェクトを選択します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] パフォーマンス オブジェクトの名前は 、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスの場合は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で始まり、名前付きインスタンスの場合は MSSQL$*instanceName*で始まります。  
  
6.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス、プロセッサ時間やディスク時間などのその他の重要な値から必要なカウンターを追加します。  
  
7.  カウンターの追加を終了したら、 **[閉じる]** をクリックします。  
  
8.  **[データのサンプル間隔]** の間隔の値を設定します。 5 分程度のサンプリング間隔から始めて、必要に応じて間隔を調整します。  
  
9. **[ログ ファイル]** タブで、 **[ログ ファイルの種類]** ボックスの一覧から **[テキスト ファイル (カンマ区切り)]** を選択します。 コンマ区切りのテキストのログ ファイルは、異なるバージョンの Windows 間で共有できます。また、Microsoft Excel などのレポート ツールで後から表示できます。  
  
10. **[スケジュール]** タブで、監視スケジュールを指定します。  
  
11. **[OK]** をクリックし、パフォーマンス ログを作成します。  
  
## <a name="see-also"></a>参照  
 [SQL Server プロファイラーのテンプレートと権限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler の起動](../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
