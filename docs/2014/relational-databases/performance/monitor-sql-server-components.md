---
title: SQL Server コンポーネントの監視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c0534bf3a12aa81a9fc84d0e2c4f82a189748a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150751"
---
# <a name="monitor-sql-server-components"></a>SQL Server コンポーネントの監視
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では動的な環境でサービスを提供しているため、監視することは重要です。 アプリケーションのデータは変化します。 ユーザーが必要とするアクセスの種類は変化します。 ユーザーの接続方法も変化します。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアクセスするアプリケーションの種類が変わる可能性もあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、手動によるシステム レベルのチューニングを必要最低限に抑えるために、メモリやディスク領域などシステム レベルのリソースが自動的に管理されています。 管理者は、SQL Server を監視することにより、パフォーマンスの傾向を特定して、変更が必要かどうかを判断することができます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントを効果的に監視するには、次の手順に従います。  
  
1.  監視目的を決定します。  
  
2.  適切なツールを選択します。  
  
3.  監視するコンポーネントを決定します。  
  
4.  これらのコンポーネントに対するメトリックを選択します。  
  
5.  サーバーを監視します。  
  
6.  データを分析します。  
  
 これらの手順を順番に説明します。  
  
## <a name="determine-your-monitoring-goals"></a>監視目的の決定  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を効果的に監視するには、監視する理由を明確にする必要があります。 監視する理由には、次のようなものがあります。  
  
-   パフォーマンスのベースラインを設定する。  
  
-   長期にわたるパフォーマンスの変化を特定する。  
  
-   具体的なパフォーマンスの問題を診断する。  
  
-   最適化するコンポーネントまたはプロセスを特定する。  
  
-   いくつかのクライアント アプリケーションのパフォーマンスに対する影響を比較する。  
  
-   現在のユーザー利用状況を監査する。  
  
-   サーバーの負荷耐性をテストする。  
  
-   データベース アーキテクチャをテストする。  
  
-   メンテナンス スケジュールをテストする。  
  
-   バックアップ プランおよび復元プランをテストする。  
  
-   ハードウェア構成の変更時期を判断する。  
  
## <a name="select-the-appropriate-tool"></a>適切なツールの選択  
 監視の理由が決まったら、監視に適切なツールを選択する必要があります。 Windows オペレーティング システムおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、トランザクションを集中的に使用する環境のサーバーを監視できる、ツールの完全なセットが用意されています。 これらのツールを使用すると、SQL Server データベース エンジンのインスタンスや SQL Server Analysis Services のインスタンスの状態を明確に把握することができます。  
  
 Windows で提供されている、サーバーで実行中のアプリケーションを監視するためのツールは次のとおりです。  
  
-   システム モニター。このツールを使用すると、メモリ、ディスク、プロセッサの使用状況などのアクティビティに関するデータをリアルタイムに収集して参照できます。  
  
-   パフォーマンス ログと警告  
  
-   タスク マネージャー  
  
 Windows Server または Windows ツールの詳細については、Windows のマニュアルを参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で提供されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のコンポーネントを監視するためのツールは、次のとおりです。  
  
-   SQL トレース (SQL Trace)  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]  
  
-   Distributed Replay Utility  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 利用状況モニター  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] グラフィカルなプラン表示  
  
-   ストアド プロシージャ  
  
-   データベース コンソール コマンド (DBCC)  
  
-   組み込み関数  
  
-   トレース フラグ  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監視ツールを使用する方法の詳細については、「 [パフォーマンス監視およびチューニング ツール](performance-monitoring-and-tuning-tools.md)」を参照してください。  
  
## <a name="identify-the-components-to-monitor"></a>監視するコンポーネントの決定  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス監視の 3 つ目の手順は、監視するコンポーネントを決定することです。 たとえば、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用してサーバーをトレースする場合、特定のイベントに関するデータを収集するようにトレースを定義することができます。 また、状況に適用しないイベントをトレースの対象から除外することもできます。  
  
## <a name="select-metrics-for-monitored-components"></a>監視するコンポーネントのメトリックの選択  
 監視するコンポーネントが決定したら、監視するコンポーネントのメトリックを決めます。 たとえば、トレースに含めるイベントを選択したら、それらのイベントの特定のデータのみを含めるように選択することができます。 トレースに関連のあるデータのみに制限すると、トレースを実行するのに必要なシステム リソースを最小限に抑えられます。  
  
## <a name="monitor-the-server"></a>サーバーの監視  
 サーバーを監視するには、データを収集するように構成した監視ツールを実行します。 たとえば、トレースを定義したら、トレースを実行して、サーバーで発生したイベントのデータを収集できます。  
  
## <a name="analyze-the-data"></a>データの分析  
 トレースが終了したら、データを分析して、監視の目的を達成できたかどうかを判断します。 達成できていない場合は、サーバーの監視に使用したコンポーネントやメトリックを変更します。  
  
 イベント データのキャプチャおよびその使用に関するプロセスは、次のとおりです。  
  
1.  フィルターを適用して、収集するイベント データを制限します。  
  
     イベント データを制限することで、監視シナリオに関連するイベントに集中した処理をシステムが行えるようになります。 たとえば、実行速度の遅いクエリを監視する場合は、アプリケーションによって実行されたクエリの中で、特定のデータベースに対して実行時間が 30 秒以上かかるクエリだけを監視するフィルターを使用します。 詳細については、「[トレース フィルターの設定 &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)」および「[トレース内のイベントへのフィルターの適用 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)」を参照してください。  
  
2.  イベントを監視 (キャプチャ) します。  
  
     監視機能を有効にすると、指定したアプリケーション、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス、またはオペレーティング システムのデータのキャプチャがすぐに開始されます。 たとえば、システム モニターでディスクの使用状況を監視している場合、ディスクの読み取りや書き込みなどのイベント データがキャプチャされ、そのデータが画面に表示されます。 詳細については、「[リソースの利用状況の監視 &#40;システム モニター&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)」を参照してください。  
  
3.  キャプチャしたイベント データを保存します。  
  
     キャプチャしたイベント データを保存すると、後で、そのデータを解析したり、Distributed Replay Utility または [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して再生することができます。 キャプチャしたイベント データは、データの生成元ツールで、再度読み込んで解析することができるファイルに保存されます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにイベント データを保存することができます。 パフォーマンス ベースラインを作成する際は、キャプチャしたイベント データを保存することが重要です。 最近キャプチャしたイベント データを比較して、パフォーマンスが最適かどうかを判断する場合、保存したパフォーマンス ベースライン データを使用します。 詳細については、「 [SQL Server プロファイラーのテンプレートと権限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)」を参照してください。  
  
4.  イベントをキャプチャするように指定された設定を含むトレース テンプレートを作成します。  
  
     トレース テンプレートには、データをキャプチャするときに使用するイベント自体、イベント データ、およびフィルターに関する指定が含まれます。 このテンプレートを使用すると、イベント、イベント データ、およびフィルターを再定義することなく、後で特定のイベント セットを監視することができます。 たとえば、デッドロックの数やこれらのデッドロックに関係するユーザーの数を頻繁に監視する場合、これらのイベント、イベント データ、およびイベント フィルターを定義するテンプレートを作成して、その定義を保存しておくと、次にデッドロックを監視するときにフィルターを再適用できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、この処理にトレース テンプレートが使用されます。 詳細については、「[トレース定義の既定値の設定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)」および「[トレース テンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)」を参照してください。  
  
5.  キャプチャしたイベント データを分析します。  
  
     分析するには、キャプチャして保存したイベント データを、データのキャプチャに使用したアプリケーションで読み込みます。 たとえば、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] でキャプチャしたトレースは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] で再度読み込んで、参照および分析することができます。 詳細については、「 [SQL Server Profiler を使用したトレースの表示と分析](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)」をご覧ください。  
  
     イベント データの分析では、どのようなイベントがなぜ発生したのかを判断します。 分析した情報に基づいて、メモリを増設する、インデックスを変更する、Transact-SQL ステートメントやストアド プロシージャのコードの問題を解決するなど、行った分析の種類に応じてパフォーマンスの向上を実現する変更を加えることができます。 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーを使用して、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] でキャプチャしたトレースを分析し、その結果に基づいてインデックスの推奨設定を作成できます。  
  
6.  キャプチャしたイベント データを再生します。  
  
     イベントの再生では、データをキャプチャしたデータベース環境のテスト コピーを設定して、キャプチャしたイベントを実際のシステムで発生したとおりに再生できます。 この機能は、Distributed Replay Utility または [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]でのみ提供されます。 イベントの再生速度は、実際に発生したときと同じ速度にすることができます。また、システムに負荷を与えるためにできる限り高速にしたり、多くの場合に行われるように、一度に 1 ステップずつ再生して、各イベントの発生後にシステムを分析することもできます。 テスト環境で実稼動システムとまったく同じイベントを分析できるので、実稼動システムへの悪影響を防ぐことができます。 詳細については、「 [トレースの再生](../../tools/sql-server-profiler/replay-traces.md)」を参照してください。  
  
  
