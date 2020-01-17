---
title: 再生オプション (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
- health monitor [SQL Server]
- Replay Configuration dialog box
ms.assetid: 58761a25-a84f-4a90-9c61-97700bc5ad9c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e91a501a899a6ba2b18790ac2da6e7c45b270b07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025745"
---
# <a name="replay-options-sql-server-profiler"></a>再生オプション (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、キャプチャされたトレースを再生するには、 **[構成の再生]** ダイアログ ボックスで、以下の再生オプションを指定します。 このダイアログ ボックスを表示するには、再生するトレース ファイルまたはトレース テーブルを [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で開き、 **[再生]** メニューの **[開始]** をクリックします。 トレースの再生に必要な権限の詳細については、「 [SQL Server Profiler の実行に必要な権限](sql-server-profiler.md)」を参照してください。  
  
 このトピックでは、 **[構成の再生]** ダイアログ ボックスで指定できるオプションについて説明します。  
  
> [!NOTE]  
>  (アクティブなコンカレント接続が多数ある、またはスループットが高い) 集中型の OLTP アプリケーションを再生する場合は、Distributed Replay Utility を使用することをお勧めします。 Distributed Replay Utility では、複数のコンピューターからのトレース データを再生し、ミッションクリティカルなワークロードをより正確にシミュレートできます。 詳細については、「 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)」を参照してください。  
  
## <a name="basic-replay-options"></a>基本再生オプション  
 **[再生サーバー]**  
 このサーバーは、トレースを再生する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前になります。 このサーバーは、「 [再生を実行するための必要条件](replay-requirements.md)」に記載されている再生の要件を満たしている必要があります。  
  
 **[ファイルに保存]**  
 トレースの再生結果を後で閲覧できるように書き込む出力ファイルを指定します。 既定では、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] によってトレースの再生結果が画面だけに表示されます。  
  
 **[テーブルに保存]**  
 トレースの再生結果を後で閲覧できるように書き込むデータベース テーブルを指定します。  
  
 **[再生スレッドの数]**  
 同時に使用する再生スレッドの数を指定します。 数が多いと、再生時に消費するリソース量は高くなりますが、再生時間は短縮されます。 複数のスレッドを使用する場合、イベントの順序が完全には維持されません。  
  
 **[トレースされた順番にイベントを再生します。このオプションはデバッグを有効にします。]**  
 トレースごとにステップ実行などのデバッグ方法を使用できるようにします。 このオプションを選択しなかった場合、イベントの再生順序がキャプチャ時の順序になるとは保証されません。  
  
 **[複数のスレッドを使用してイベントを再生します。このオプションはパフォーマンスを最適にし、デバッグを無効にします。]**  
 パフォーマンスを最適化し、デバッグを無効にします。 イベントは、特定のサーバー プロセス ID (SPID) に対して記録された順序で再生されますが、SPID の順序は保証されません。  
  
 **[再生結果を表示する]**  
 再生結果を表示します。 既定のオプションです。 再生するトレースのサイズが非常に大きい場合は、このオプションを無効にしてディスク領域を節約できます。  
  
> [!NOTE]  
>  最高のパフォーマンスを得るためには、[複数のスレッドを使用してイベントを再生します。このオプションはパフォーマンスを最適にし、デバッグを無効にします。] を選択し、[再生結果を表示する] を選択しないことをお勧めします。  
  
## <a name="advanced-replay-options"></a>再生オプションの詳細設定  
 **[システム SPID を再生する]**  
 すべての SPID を再生します。 既定のオプションです。  
  
 **[1 つの SPID のみ再生する]**  
 一覧から選択した SPID 番号のみを再生します。  
  
 **[日時により再生を制限する]**  
 **[開始時刻]** および **[終了時刻]** で指定された期間のトレースを再生します。  
  
 **[ヘルス モニターの待機間隔]**  
 ヘルス モニターにより終了されるまでの、プロセスに実行を許可する時間を設定します。  
  
 **[ヘルス モニターのポーリング間隔]**  
 ヘルス モニターがプロセスの終了を確認するためにポーリングする頻度を指定します。  
  
 **[SQL Server のブロックされるプロセスの監視を有効にする]**  
 ブロックされるプロセス モニターが、ブロックされているプロセスまたはブロックしているプロセスを検索する頻度を設定します。  
  
## <a name="about-the-health-monitor"></a>ヘルス モニターについて  
 ヘルス モニターは、トレースの再生に伴うシミュレートされたプロセスを監視するアプリケーション スレッドです。これらのプロセスのうち、再生内でブロックされているプロセスを終了します。 **[再生の構成]** ダイアログ ボックスの **[再生オプションの詳細設定]** タブで、ブロックされているプロセスを終了するまでにヘルス モニターが待機する時間を秒単位で指定できます (**[ヘルス モニターの待機間隔]**)。 この間隔が 0 に設定されていると、ヘルス モニターは、再生されているトレース中のブロックしているシミュレートされたプロセスを終了しません。  
  
## <a name="see-also"></a>参照  
 [トレースの再生](replay-traces.md)   
 [再生を実行するための必要条件](replay-requirements.md)   
 [トレースの再生に関する注意点 &#40;SQL Server Profiler&#41;](considerations-for-replaying-traces-sql-server-profiler.md)  
  
  
