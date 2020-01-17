---
title: レポートおよび共有データセット処理のタイムアウト値の設定 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fdbca5818e3430c0445444f3fb98b426e5f8a79c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103208"
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>レポートおよび共有データセット処理のタイムアウト値の設定 (SSRS)
  タイムアウト値を指定して、システム リソースの使用に制限を設定できます。 レポート サーバーでは、2 つのタイムアウト値がサポートされます。  
  
-   埋め込みデータセットのクエリ タイムアウト値は、レポート サーバーがデータベースからの応答を待機する秒数です。 この値はレポートの中で定義されます。  
  
-   共有データセットのクエリ タイムアウト値は、レポート サーバーがデータベースからの応答を待機する秒数です。 この値は共有データセット定義の一部であり、レポート サーバー上で共有データセットを管理するときに変更できます。  
  
-   レポート実行タイムアウト値は、レポート処理を停止するまでに続行できる最大秒数です。 この値はシステムレベルで定義されます。 この設定は、レポートごとに変えることができます。  
  
 タイムアウト エラーの大半は、クエリ処理中に発生します。 タイムアウト エラーが発生する場合は、クエリ タイムアウト値を増やしてください。 レポート実行タイムアウト値はクエリ タイムアウト値より大きい値になるように調整してください。レポート実行タイムアウト値には、クエリとレポート処理の両方が完了するのに十分な時間を設定する必要があります。  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>レポートの埋め込みデータセットに対するクエリ タイムアウトの設定  
 クエリ タイムアウト値は、レポートの作成中、埋め込みデータセットを定義するときに指定します。 タイムアウト値は、レポート定義の `Timeout` 要素の中にレポートと一緒に格納されます。 既定では、この値は 30 秒に設定されます。 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  
  
 パブリッシュ済みレポートのプロパティを変更する権限を持っているユーザーは、レポート定義ファイルを編集することでこの値を再設定できます。  
  
 また、データ ドリブン サブスクリプションのクエリ タイムアウト値を指定することもできます。 クエリのタイムアウト値は、[データ ドリブン サブスクリプション] ページで指定します。 ここで指定した値によって、サブスクライバーのデータ ソースからデータを取得する際に、クエリ処理が完了するまでのレポート サーバーが待機する時間が決定されます。  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>共有データセットに対するクエリ タイムアウトの設定  
 クエリ タイムアウト値は、共有データセットを作成または管理するときに、レポート サーバー上で秒単位で指定します。 既定でこの値は 0 秒に設定されています。0 秒を指定すると、タイムアウト値を指定していない場合と同じ意味になります。 詳細については、「 [共有データセットの管理](../report-data/manage-shared-datasets.md)」を参照してください。  
  
## <a name="setting-a-report-execution-time-out"></a>レポート実行タイムアウトの設定  
 レポート実行タイムアウト値を設定して、レポート サーバーがレポート処理に使用する時間を制限することができます。 レポート実行タイムアウト値は、レポート マネージャーで指定できます。 [サイトの設定] ページですべてのレポートの既定値を設定してから、特定のレポートの [実行] プロパティ ページでその値をオーバーライドできます。 既定では、この値は 1,800 秒に設定されます。 詳細については、「 [レポート処理プロパティの設定](set-report-processing-properties.md)」を参照してください。  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>レポート実行タイムアウト値の評価方法  
 レポート サーバーでは、60 秒ごとに実行中のジョブが評価されます。 レポート サーバーでは、60 秒ごとに、レポート実行タイムアウト値に対して実際の処理時間が比較されます。 レポートの処理時間がレポート実行タイムアウト値を超えた場合、レポートの処理が停止します。  
  
 タイムアウト値を 60 秒未満に指定した場合、サイクルの静止期間、つまりレポート サーバーで実行中のジョブが評価されていない期間に、レポートが、開始から終了まで完全に実行されることがあります。 たとえば、実行に 20 秒かかるレポートのタイムアウト値を 10 秒に設定した場合、レポートの実行が 60 秒サイクルの早期に開始されると、レポートは完全に処理されます。  
  
> [!NOTE]  
>  RSReportServer.config ファイルの `RunningRequestsDbCycle` 設定で、実行中のジョブが評価される頻度を変更できます。  
  
## <a name="see-also"></a>参照  
 [処理オプションの設定 (Reporting Services の SharePoint 統合モード)](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](reporting-services-report-server-native-mode.md)   
 [Manage a Running Process](../subscriptions/manage-a-running-process.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)  
  
  
