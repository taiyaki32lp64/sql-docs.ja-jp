---
title: SQL Server Profiler - ツール オプション (全般オプション ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.generaloptions.f1
helpviewer_keywords:
- General Options dialog box
ms.assetid: a888246d-ccfe-415f-bbdc-d6adafac250a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9da36f49927acd2a313bcb9f8647655731006d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089618"
---
# <a name="sql-server-profiler---tools-options-general-options-page"></a>SQL Server Profiler - ツール オプション (全般オプション ページ)
  **[全般オプション]** ダイアログ ボックスを使用すると、以下のオプションを確認または指定できます。  
  
## <a name="options"></a>および  
  
### <a name="display-options"></a>[表示オプション]  
 **[フォント名]**  
 トレースの実行中にトレース結果グリッドで使用されるフォントの名前を表示します。  
  
 **[フォント サイズ]**  
 トレースの実行中にトレース結果グリッドで使用されるフォントのサイズを表示します。  
  
 **[フォントの選択]**  
 フォント設定を変更するためのダイアログを開きます。  
  
 **[日時の値の表示に地域別設定を使用する]**  
 使用するコンピューター用に構成された地域の設定で日時の値を表示します。 このオプションを選択しない場合、日時の値は Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]が使用する固定形式 (ミリ秒を含む) で表示されます。  
  
> [!NOTE]  
>  このチェック ボックスのオン/オフを切り替えることで、 **[StartTime]** や **[EndTime]** などの時間列の表示形式が変更されます。 ただし、言語イベントまたはリモート プロシージャ コール (RPC) 内の **DateTime** 値のパラメーターは変更されません。  
  
 **[実行時間列の値をマイクロ秒で表示する]**  
 トレースの **[実行時間]** データ列の値をマイクロ秒で表示します。 既定では、 **[実行時間]** 列の値はミリ秒で表示されます。  
  
### <a name="tracing-options"></a>[トレース オプション]  
 **[接続の確立直後にトレースを開始する]**  
 接続の確立直後に既定のテンプレートを使用してトレースを開始します。  
  
 **[プロバイダーのバージョンが変更されたときに、トレース定義を更新する]**  
 プロバイダーが更新されたときに、最新のトレース定義を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に適用します。 既定ではオンになっていません。 このオプションをオンにすると、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] は、サーバーでトレース定義を問い合わせるクエリを実行し、トレース定義があればファイルをディスクに再作成します。  
  
### <a name="file-rollover-options"></a>[ファイルのロールオーバー オプション]  
 **[確認せずにすべてのロールオーバー ファイルを順に読み込む]**  
 トレース ファイルが開かれるとロールオーバー ファイルを自動的に読み込みます。 トレースの実行中に複数のファイルが作成されたときに、このオプションがオンになっている場合、すべてのロールオーバー ファイルが自動的に読み込まれます。  
  
 **[ロールオーバー ファイルを読み込む前に確認する]**  
 トレース ファイルを開いたときに、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] はロールオーバー ファイルを追加するかどうかをユーザーに確認してから追加します。  
  
 **[後続のロールオーバー ファイルを読み込まない]**  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] は、トレース ファイルを開いたときに、後続のロールオーバー ファイルを読み込みません。  
  
### <a name="replay-options"></a>[再生オプション]  
 **[再生スレッドの既定の数]**  
 同時に使用する再生スレッドの数を指定します。 使用する数を多くすると再生中のリソースも多くなりますが、再生のコンカレンシー数が増えます。  
  
 **[ヘルス モニターの既定の待機間隔 (秒)]**  
 再生の待機間隔を秒単位で指定します。 既定値は 3,600 秒 (1 時間) です。 この設定は、ヘルス モニターでスレッドが終了するまでに、このスレッドを実行できる時間の長さに影響を与えます。  
  
 **[ヘルス モニターの既定のポーリング間隔 (秒)]**  
 再生中のヘルス モニターのポーリング間隔を秒単位で指定します。 既定値は 60 秒です。 ユーザーはこの値を指定することで、終了するプロセスを決定するためにヘルス モニターがポーリングする頻度を設定できます。  
  
## <a name="see-also"></a>参照  
 [サーバーへの接続後の自動的なトレースの開始 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [トレース表示の既定値の設定 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [トレース テーブルを再生する &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [トレース ファイルを再生する &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [トレースの再生](../tools/sql-server-profiler/replay-traces.md)   
 [グローバル トレース オプションを設定&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)   
 [SQL Server プロファイラーのテンプレートと権限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
