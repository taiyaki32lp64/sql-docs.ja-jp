---
title: グラフ、警告、ログ、およびレポートの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f36f1a3df7eae3fd363aa5e2bc4b5ae13f36ae2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032407"
---
# <a name="create-charts-alerts-logs-and-reports"></a>グラフ、警告、ログ、およびレポートの作成
  システム モニターを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを監視するためのグラフ、警告、ログ、およびレポートを作成できます。  
  
## <a name="charts"></a>グラフ  
 グラフを使用すると、CPU 使用率やディスク I/O など、選択したオブジェクトとカウンターの現在のパフォーマンスを監視できます。 システム モニターのオブジェクトやカウンターのさまざまな組み合わせをグラフに追加できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のオブジェクトやカウンターをグラフに追加することもできます。  
  
 各グラフは、監視する情報のサブセットを示します。 たとえば、1 つのグラフでメモリ使用率の統計を追跡して、もう 1 つのグラフでディスク I/O 統計を追跡できます。  
  
 グラフを使用すると、次の作業に役立ちます。  
  
-   コンピューターまたはアプリケーションが遅い原因または非効率な原因を調査します。  
  
-   システムを継続的に監視して、断続的なパフォーマンスの問題を検出します。  
  
-   処理容量を増加させる必要があるかどうかを判断します。  
  
-   線グラフで傾向を表示します。  
  
-   ヒストグラムで比較します。  
  
 現在発生しているイベントを監視する場合など、ローカル コンピューターまたはリモート コンピューターを短い時間、リアルタイムで監視するのにグラフは便利です。  
  
## <a name="alerts"></a>オブジェクト エクスプローラーには  
 システム モニターで警告を使用すると、特定のイベントを追跡して、要求に応じてそのイベントを通知できます。 警告ログは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のオブジェクトに対して選択したカウンターとインスタンスについて現在のパフォーマンスを監視できます。 カウンターが指定した値を超えたときに、ログはそのイベントの日付と時刻を記録します。 イベントはネットワーク警告を生成することもできます。 また、イベントが初めて発生したとき、またはイベントが発生するたびに、特定のプログラムを実行できます。 たとえば、警告はすべてのシステム管理者に対して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのディスク容量が不足していることを示すネットワーク メッセージを送信できます。  
  
## <a name="logs"></a>ログ  
 ログを使用すると、選択したオブジェクトとコンピューターの現在の利用状況について情報を記録し、後にその情報を表示および分析することができます。 複数のシステムからデータを収集して、1 つのログ ファイルに記録することもできます。 たとえば、さまざまなコンピューターで選択したオブジェクトのパフォーマンスについて情報を蓄積するために、さまざまなログを作成して、後に分析のために使用できます。 ファイル名を付けて選択した設定を保存すれば、比較のために同様の情報についてもう 1 つのログを作成するときに再使用できます。  
  
 ログ ファイルには、トラブルシューティングやプランニングに役立つ豊富な情報が記録されています。 現在の利用状況に関するグラフ、警告、およびレポートが即時のフィードバックを与えるのに対して、ログ ファイルは、長期間にわたってカウンターを追跡できます。 このため、情報をより徹底的に検査し、システムのパフォーマンスを文書化することができます。  
  
## <a name="reports"></a>[レポート]  
 レポートを使用すると、選択したオブジェクトに対して、絶えず変化し続けるカウンター値とインスタンス値を表示できます。 値は、各インスタンスの列に表示されます。 レポート間隔を調整したり、スナップショットを印刷したり、データをエクスポートすることもできます。 raw 番号を表示する必要がある場合には、レポートを使用します。  
  
 グラフ、警告、ログ、およびレポートの作成、または Windows オブジェクトとカウンターの詳細については、Windows のマニュアルを参照してください。  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
