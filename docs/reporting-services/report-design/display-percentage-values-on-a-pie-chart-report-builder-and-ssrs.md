---
title: 円グラフへのパーセンテージの表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fab9a9c5f6fbdbf3201ba597102450bad0d95629
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578200"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>円グラフへのパーセンテージの表示 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートでは、既定で凡例にカテゴリが表示されます。 凡例にパーセンテージまたはパイ スライス自体を表示することもできます。   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 「[チュートリアル: レポートへの円グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)」では、最初にサンプル データを使って試す場合に、パーセンテージをパイ スライスに追加する手順について説明します。
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>円グラフにパーセンテージをラベルとして表示するには  
  
1.  レポートに円グラフを追加します。 詳細については、「[レポートへのグラフの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
2.  デザイン画面で、円グラフを右クリックし、 **[データ ラベルの表示]** をクリックします。 円グラフの各スライス内にデータ ラベルが表示されます。  
  
3.  デザイン画面で、ラベルを右クリックし、 **[系列ラベルのプロパティ]** をクリックします。 **[系列ラベルのプロパティ]** ダイアログ ボックスが表示されます。  
  
4.  **[ラベル データ]** オプションに **#PERCENT** と入力します。  
  
5.  (省略可) ラベルに表示する小数点以下桁数を指定するには、「#PERCENT{P*n*}」と入力します。ここで、 *n* は、表示する小数点以下桁数を表します。 たとえば、小数点以下を表示しない場合は「#PERCENT{P0}」と入力します。  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>円グラフの凡例にパーセンテージを表示するには  
  
1.  デザイン画面で、円グラフを右クリックし、 **[系列のプロパティ]** をクリックします。 **[系列のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[凡例]** の **[凡例のユーザー定義テキスト]** プロパティに **#PERCENT** と入力します。  
  
## <a name="see-also"></a>参照  
* [チュートリアル: レポートへの円グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [円グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [グラフの凡例の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [円グラフの外側へのデータ ポイント ラベルの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
