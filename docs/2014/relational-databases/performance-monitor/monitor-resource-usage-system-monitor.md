---
title: リソースの利用状況の監視 (システム モニター) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8bd4676eed22cea99808d87016231dbd2ebaf4cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032116"
---
# <a name="monitor-resource-usage-system-monitor"></a>リソースの利用状況の監視 (システム モニター)
  Microsoft Windows サーバー オペレーティング システムを使用している場合は、システム モニター GUI ツールを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパフォーマンスを測定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のオブジェクトやパフォーマンス カウンターだけでなく、プロセッサ、メモリ、キャッシュ、スレッド、プロセスなどその他のオブジェクトの動作も確認できます。 これらの各オブジェクトには、それに関連したデバイス使用率、キューの長さ、遅延を測定するカウンターと、スループットおよび内部輻輳を表示するインジケーターのセットがあります。  
  
> [!NOTE]  
>  システム モニターは、Windows NT 4.0 以前に使用されていたパフォーマンス モニターの後継ツールです。  
  
## <a name="benefits-of-system-monitor"></a>システム モニターの利点  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と Windows のパフォーマンスの相関を調べるには、Windows オペレーティング システムと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のカウンターを同時に監視することをお勧めします。 たとえば、Windows のディスク I/O (入力/出力) カウンターと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Buffer Manager カウンターを同時に監視すると、システム全体の動作を把握できます。  
  
 システム モニターを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在の利用状況およびパフォーマンスに関する統計を取ることができます。 次に、システム モニターを使用して行うことができる操作を示します。  
  
-   任意の数のコンピューターのデータを同時に表示する。  
  
-   現在の利用状況を反映したグラフを表示して変更し、ユーザーが定義した頻度で更新されるカウンター値を表示する。  
  
-   さらに操作を行ったり出力したりするために、グラフ、ログ、警告ログ、およびレポートから表計算アプリケーションまたはデータベース アプリケーションにデータをエクスポートする。  
  
-   警告ログにイベントを記録し、ネットワーク警告によってユーザーに通知できるシステム警告を追加する。  
  
-   カウンター値がユーザー定義値を上回るか下回るようなケースが発生するたびに、または最初に発生したときに、あらかじめ定義しておいたアプリケーションを実行する。  
  
-   複数のコンピューターのさまざまなオブジェクトについてのデータを含むログ ファイルを作成する。  
  
-   既存の複数のログ ファイルから選択した項目を 1 つのファイルに追加していき、長期的なアーカイブを作成する。  
  
-   現在の利用状況のレポートを表示するか、既存のログ ファイルからレポートを作成する。  
  
-   グラフ、警告、ログ、またはレポートの個々の設定、あるいはワークスペースの設定全体を再利用するために保存する。  
  
    > [!NOTE]  
    >  Windows NT 4.0 以降では、パフォーマンス モニターがシステム モニターに変わっています。 ここで示したタスクには、システム モニターまたはパフォーマンス モニターのいずれかを使用できます。  
  
## <a name="system-monitor-performance"></a>システム モニターのパフォーマンス  
 パフォーマンス関連の問題を調査するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および Microsoft Windows オペレーティング システムを監視するときは、大きく分けて次の 3 点に注目することから始めます。  
  
-   ディスク利用状況  
  
-   プロセッサ使用率  
  
-   メモリ使用量  
  
 システム モニターを実行しているコンピューターを監視すると、コンピューターのパフォーマンスにわずかに影響する場合があります。 したがって、システム モニターのデータを他のディスク (またはコンピューター) に記録して監視対象のコンピューターへの影響を減らすか、リモート コンピューターからシステム モニターを実行してください。 また、監視するカウンターは関心のあるものだけに絞ります。 監視するカウンターが多すぎると、リソース使用量のオーバーヘッドが監視プロセスに上乗せされ、監視対象のコンピューターのパフォーマンスに影響を及ぼします。  
  
## <a name="system-monitor-tasks"></a>システム モニターのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|どのような状況でシステム モニターを使用するかについて示し、システム モニター使用時のパフォーマンスのオーバーヘッドについて説明します。|[システム モニターの実行](run-system-monitor.md)|  
|ディスク カウンターを監視することで、ディスクの利用状況と、SQL Server コンポーネントによって生成される I/O の量を調べる方法について説明します。|[ディスクの使用量の監視](monitor-disk-usage.md)|  
|CPU 使用率が通常の範囲内にあるかどうかを確認するために、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを監視する方法について説明します。|[CPU 使用率の監視](monitor-cpu-usage.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを監視して、メモリ使用率が通常の範囲内であることを確認する方法について説明します。|[メモリ使用率の監視](monitor-memory-usage.md)|  
|システム モニターのカウンターがしきい値に達したときに発生する警告を作成する方法について説明します。|[SQL Server データベース警告の作成](create-a-sql-server-database-alert.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを監視するためのグラフ、警告、ログ、およびレポートを作成する方法について説明します。|[グラフ、警告、ログ、およびレポートの作成](create-charts-alerts-logs-and-reports.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを実行しているコンピューターの利用状況をシステム モニターで監視する際に使用されるオブジェクトとカウンターを示します。|[SQL Server オブジェクトの使用](use-sql-server-objects.md)|  
|システム モニターでインメモリ OLTP のアクティビティを監視する際に使用されるオブジェクトとカウンターを示します。|[XTP &#40;、インメモリ OLTP&#41;パフォーマンス カウンター](../../integration-services/performance/performance-counters.md)|  
  
  
