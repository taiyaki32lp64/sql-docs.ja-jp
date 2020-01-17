---
title: 円グラフの小さいスライスをまとめる (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8718570c6a370368eaf227280245607b182eba25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581628"
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>円グラフの小さいスライスをまとめる (レポート ビルダーおよび SSRS)
スライスが多すぎる円グラフは、煩雑に見えることがあります。 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートで円グラフの多数の小さいスライスを 1 つのスライスにまとめる方法を説明します。
 
 小さいスライスを 1 つのスライスにまとめるには、まず小さいスライスを収集するためのしきい値を円グラフに対する比率と固定値のどちらで表すかを決定します。 
 
 最初にサンプル データを使って試してみたい場合は、「[チュートリアル: レポートへの円グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)」で小さいスライスを 1 つのスライスにまとめる手順が説明されています。
 
 ![report-builder-pie-chart-other-slice](../../reporting-services/report-design/media/report-builder-pie-chart-other-slice.png)
  
 小さいスライスは、1 つ目の円グラフでまとめられたスライスから切り離し、2 つ目の円グラフにまとめることもできます。 2 つ目の円グラフは元の円グラフの右側に描画されます。  
  
 じょうごグラフまたはピラミッド グラフのスライスを 1 つのスライスに結合することはできません。  
  
 
## <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>円グラフの小さいスライスを 1 つのスライスにまとめるには  
  
1.  プロパティ ペインを開きます。  
  
2.  デザイン画面で、円グラフの任意のスライスをクリックします。 系列のプロパティが [プロパティ] ペインに表示されます。  
  
3.  **[全般]** セクションで、 **[CustomAttributes]** ノードを展開します。  
  
4.  [CollectedStyle] プロパティを **[SingleSlice]** に設定します。  

    ![report-builder-pie-chart-single-slice-property](../../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
  
5.  収集されるしきい値としきい値の種類を設定します。 次の例は、収集されるしきい値を設定する一般的な方法です。  
  
    -   **比率で設定します。** たとえば、円グラフ上の 10% 未満の小さいスライスを 1 つのスライスにまとめるには、次の手順を実行します。  
  
         [CollectedThresholdUsePercent] プロパティを **True**に設定します。  
  
         [CollectedThreshold] プロパティを **10**に設定します。  
  
        > [!NOTE]  
        >  [CollectedStyle] を **[SingleSlice]** に、[CollectedThreshold] を **100** より大きい値に、[CollectedThresholdUsePercent] を **[True]** に設定した場合、グラフではパーセンテージを計算できないため、例外がスローされます。 この問題を解決するには、[CollectedThreshold] を **100** 未満の値に設定します。  
  
    -   **データ値で設定します。** たとえば、円グラフ上の 5,000 未満の小さいスライスを 1 つのスライスにまとめるには、次の手順を実行します。  
  
         [CollectedThresholdUsePercent] プロパティを **False**に設定します。  
  
         [CollectedThreshold] プロパティを **5000**に設定します。  
  
6.  [CollectedLabel] プロパティを、収集されたスライスに表示されるテキスト ラベルを表す文字列に設定します。  
  
7.  (省略可) CollectedSliceExploded、CollectedColor、CollectedLegendText および CollectedToolTip の各プロパティを設定します。 これらのプロパティでは、1 つのスライスの外観、色、ラベルのテキスト、凡例のテキスト、およびツールヒントを変更します。  
  
## <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>小さいスライスをまとめた 2 つ目の円グラフにするには  
  
1.  上記の手順 1. ～ 3. を実行します。  
  
2.  [CollectedStyle] プロパティを **[CollectedPie]** に設定します。  
  
3.  [CollectedThreshold] プロパティを、小さいスライスを 1 つのスライスにまとめる基準となるしきい値を表す値に設定します。 [CollectedStyle] プロパティが **CollectedPie**に設定された場合、[CollectedThresholdUsePercent] プロパティは常に **True**に設定され、収集されるしきい値は常に比率で表されます。  
  
4.  (省略可) CollectedColor、CollectedLabel、CollectedLegendText および CollectedToolTip の各プロパティを設定します。 "Collected" という名前を持つその他すべてのプロパティは、まとめられた円に適用されません。  
  
> [!NOTE]  
>  2 つ目の円グラフは、データの中の小さいスライスに基づいて計算され、プレビューのみに表示されます。 この円グラフはデザイン画面には表示されません。  
  
> [!NOTE]  
>  2 つ目の円グラフの書式は設定できません。 このため、円スライスを収集する際は最初の方法を使用することを強くお勧めします。  
  
## <a name="see-also"></a>参照  
* [チュートリアル: レポートへの円グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [円グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [グラフでのデータ ポイントの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
*  [円グラフの外側へのデータ ポイント ラベルの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
*  [円グラフへのパーセンテージの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)     
  
