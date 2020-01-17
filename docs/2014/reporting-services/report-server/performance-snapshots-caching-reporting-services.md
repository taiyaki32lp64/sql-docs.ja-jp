---
title: パフォーマンス、スナップショット、キャッシュ (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a5fa14ad158d2b937ecd8c7fa706460ec8ee1aca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103600"
---
# <a name="performance-snapshots-caching-reporting-services"></a>パフォーマンス、スナップショット、キャッシュ (Reporting Services)
  レポート サーバーのパフォーマンスには、ハードウェア、レポートに同時にアクセスするユーザー数、レポートのデータ量、出力形式など、さまざまな要因が絡み合って影響を与えます。 環境に固有のパフォーマンス要因を把握し、期待した結果を得るための対策を講じるには、ベースライン データを用意し、テストを実行する必要があります。 ツールとガイドラインの詳細については、MSDN の次の記事を参照してください。[Reporting Services のパフォーマンスの最適化](https://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx)と[Visual Studio 2005 を使用して、SQL Server 2005 Reporting Services レポート サーバーのロード テストを実行する](https://go.microsoft.com/fwlink/?LinkID=77519)します。  
  
 考慮する必要がある一般的な原則は次のとおりです。  
  
-   レポートの処理と表示には、多くのメモリを必要とします。 搭載メモリ量ができるだけ多いコンピューターを選択してください。  
  
-   レポート サーバーとレポート サーバー データベースを別個のコンピューターでホストした方が、1 台のハイエンド コンピューターで両方をホストするよりも、パフォーマンスが高くなる傾向があります。  
  
-   すべてのレポートの処理速度が低下している場合は、複数のレポート サーバー インスタンスで単一のレポート サーバー データベースをサポートするスケールアウト配置を検討します。 最適な結果を得るには、負荷分散ソフトウェアを使用して、配置全体に対して要求を均等に分散させるようにします。  
  
-   ある特定のレポートの処理速度だけが低下しているとき、そのレポートを要求時に実行する場合は、レポート データセット クエリをチューニングします。 また、キャッシュできる共有データセットの使用、レポートのキャッシュ、またはスナップショットとしてのレポートの実行を検討してください。  
  
-   特定の形式のすべてのレポートの処理速度が低下している場合 (PDF 形式で表示している場合など)、ファイル共有配信を検討するか、メモリを増設する、または、異なる形式を選択するようにします。  
  
-   レポート処理の所要時間など、使用状況のメトリックを調べるには、レポート サーバーの実行ログを参照します。 詳細については、次を参照してください。[レポート サーバー実行ログと ExecutionLog3 ビュー](report-server-executionlog-and-the-executionlog3-view.md)します。  
  
-   メモリ管理構成設定をチューニングすることによってパフォーマンスの問題を緩和する方法の詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レポート サーバーのパフォーマンスの監視](monitoring-report-server-performance.md)  
 サーバー上の処理負荷を追跡する際に使用できるパフォーマンス オブジェクトについて説明します。  
  
 [レポート処理プロパティの設定](set-report-processing-properties.md)  
 要求時にキャッシュから、またはスケジュールに従ってレポート スナップショットとして、実行するレポートを構成する方法を説明します。  
  
 [レポート サーバー アプリケーションで利用可能なメモリの構成](../report-server/configure-available-memory-for-report-server-applications.md)  
 既定のメモリ管理動作をオーバーライドする方法を説明します。  
  
 [レポートのキャッシュ (SSRS)](caching-reports-ssrs.md)  
 レポート サーバー上でのレポートのキャッシュの動作を説明します。  
  
 [共有データセットのキャッシュ &#40;SSRS&#41;](cache-shared-datasets-ssrs.md)  
 レポート サーバー上での共有データセットのキャッシュの動作を説明します。  
  
 [サイズの大きなレポートの処理](process-large-reports.md)  
 サイズの大きいレポートを構成および配布する際の推奨事項を記載しています。  
  
 [レポートおよび共有データセット処理のタイムアウト値の設定 &#40;SSRS&#41;](setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 クエリとレポート処理にタイムアウトを設定する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [Manage a Running Process](../subscriptions/manage-a-running-process.md)   
 [レポート実行の確認](verifying-a-report-run.md)  
  
  
