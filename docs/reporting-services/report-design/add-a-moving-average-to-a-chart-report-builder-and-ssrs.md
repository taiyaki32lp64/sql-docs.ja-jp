---
title: グラフへの移動平均の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 166cf9c1-0750-4866-8381-542e4fbfe65a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 58dae055e89d2c1be50c7bbc515298cfadf9fd60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574994"
---
# <a name="add-a-moving-average-to-a-chart-report-builder-and-ssrs"></a>グラフへの移動平均の追加 (レポート ビルダーおよび SSRS)
移動平均は、定義された期間にわたって計算される、系列内のデータの平均です。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 改ページされたレポートでは、移動平均をグラフに表示すると、重要な傾向を特定することができます。  

![レポート-ビルダー-列のグラフのチュートリアル](../../reporting-services/media/report-builder-column-chart-tutorial.png)
  
 移動平均式は、技術的分析で最も一般的に使用される価格指標です。 他にも、平均値、中央値、標準偏差など、多くの式をグラフ上の系列から算出することができます。 移動平均を指定する場合、各式には、指定する必要のあるパラメーターが 1 つ以上設定されていることがあります。  
 
 「[チュートリアル: レポートへの縦棒グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)」では、サンプル データを使って試す場合に、移動平均をグラフに追加する手順について説明します。
  
 デザイン モードで移動平均式を追加した際に、追加される線系列は、視覚的なプレースホルダーにすぎません。 グラフでは、レポート処理中に各式のデータ ポイントが計算されます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、傾向線の組み込みサポートは提供されていません。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-calculated-moving-average-to-a-series-on-the-chart"></a>計算される移動平均をグラフ上の系列に追加するには  
  
1.  **[値]** 領域内のフィールドを右クリックし、 **[計算系列の追加]** をクリックします。 **[計算系列のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **[式]** ボックスの一覧の **[移動平均]** を選択します。  
  
3.  移動平均の期間を表す整数値を **[期間]** に指定します。  
  
    > [!NOTE]  
    >  期間は、移動平均の計算に使用する日数です。 x 軸で日付/時刻値が指定されていない場合、期間は、移動平均の計算に使用されるデータ ポイント数で表されます。 データ ポイントが 1 つしか存在しない場合は、移動平均式による計算は行われません。 移動平均の計算は、2 番目のポイントから開始されます。 **[最初のポイントから開始する]** チェック ボックスをオンにすると、移動平均の計算は最初のポイントから開始されます。 データ ポイントが 1 つしか存在しない場合、計算された移動平均のポイントは、元の系列の最初のポイントと同じになります。  
  
## <a name="see-also"></a>参照  
* [チュートリアル: レポートへの縦棒グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [グラフの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
*  [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
*  [空のポイントのグラフへの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
  
