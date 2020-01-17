---
title: グラフ内の空のデータ ポイントおよび NULL データ ポイント (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: faddd29d-4cc1-4c2c-8e29-d3d9918fe22a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ed869c3aa283dbede50b37e74b7c8c4ee5580bc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579158"
---
# <a name="empty-and-null-data-points-in-charts-report-builder-and-ssrs"></a>グラフ内の空のデータ ポイントおよび NULL データ ポイント (レポート ビルダーおよび SSRS)

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートで、グラフに空または null の値を持つフィールドがある場合、そのグラフが適切に表示されないことがあります。 グラフでは、指定したグラフの種類によって空の値の処理方法が異なります。  
  
-   グラフの種類が線形のグラフ (横棒グラフ、縦棒グラフ、散布図、折れ線グラフ、面グラフ、または範囲グラフ) の場合、空の値は、空白 (すきま) としてグラフに表示されます。 空のポイントを示すには、空のポイントのプレースホルダーを追加する必要があります。 詳細については、「[空のポイントのグラフへの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
-   グラフの種類が連続性のある線形のグラフ (面グラフ、横棒グラフ、縦棒グラフ、折れ線グラフ、散布図) の場合、空のデータ ポイントが、系列の連続性を維持するようにグラフに追加されます。  
  
-   グラフの種類が線形のグラフ以外 (極座標グラフ、円グラフ、ドーナツ グラフ、じょうごグラフ、またはピラミッド グラフ) の場合、空の値はグラフに表示されません。  
  
-   図形グラフでは、NULL 値が省略されます。  
  
 空のデータ ポイント付きのグラフについては、サンプル レポートに例が含まれています。 このサンプル レポートおよびその他のサンプル レポートをダウンロードする方法の詳細については、 [レポート ビルダーおよびレポート デザイナーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=198283)に関するページを参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="removing-empty-or-null-values"></a>空の値または NULL 値の削除  
 重要なデータを見やすくするには、空の値をデータセットから削除することを検討してください。 NULL 値をフィルター処理するには、クエリで NOT IS NULL 句を使用することができます。 また、0 以外の値だけが表示されるように指定するフィルター式を追加することもできます。 詳細については、「 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)」を参照してください。  
  
## <a name="fields-with-no-values-in-a-chart"></a>グラフ内の値がないフィールド  
 返されたデータセット内の値が含まれていないフィールドについては、データ ポイントを含まない空のグラフが表示されますが、系列の名前 (通常はフィールド名) は凡例項目として追加されます。  
  
 この動作は、返されたデータセット内のデータが 0 行である場合とは異なります (この状況は、レポートがパラメーター化されており、選択した値によって空の結果セットが返される場合に発生します)。 データセット クエリによって返されるデータが 0 行の場合は、表示できるデータがないことを示すメッセージが実行時に表示されます。 **[プロパティ]** ペインでレポートの NoDataMessage キャプションを変更することによって、このメッセージをカスタマイズできます。 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  

## <a name="next-steps"></a>次の手順

[グラフ](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[グラフの書式設定](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[レポートにグラフを追加する](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)   
[グラフのトラブルシューティング](../../reporting-services/report-design/troubleshoot-charts-report-builder-and-ssrs.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
