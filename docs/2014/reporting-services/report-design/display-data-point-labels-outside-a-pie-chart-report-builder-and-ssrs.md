---
title: 円グラフの外側へのデータ ポイント ラベルの表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb726adbb523f679fd9d59e3e51b2dc1291e6247
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106048"
---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>円グラフの外側へのデータ ポイント ラベルの表示 (レポート ビルダーおよび SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、円グラフのラベル付けは、データのいくつかのスライスのみにラベルが表示されるように最適化されています。 円グラフに含まれるスライスが多すぎると、ラベルが重なる可能性があります。 1 つの解決策として、円グラフの外側にラベルを表示する方法があります。これにより、長いデータ ラベル用に領域を確保できます。 ラベルがまだ重なっていることが判明した場合は、3D を有効にすることでラベル用の領域をさらに確保することができます。 これにより、円グラフの直径が小さくなり、グラフの周囲でさらに領域が確保されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>円グラフの内側にデータ ポイント ラベルを表示するには  
  
1.  レポートに円グラフを追加します。 詳細については、「[レポートへのグラフの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
2.  デザイン画面で、グラフを右クリックし、 **[データ ラベルの表示]** をクリックします。  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>円グラフの外側にデータ ポイント ラベルを表示するには  
  
1.  円グラフを作成し、データ ラベルを表示します。  
  
2.  プロパティ ペインを開きます。  
  
3.  デザイン画面で、円グラフをクリックしてプロパティ ペインの **[カテゴリ]** プロパティを表示します。  
  
4.  **[CustomAttributes]** ノードを展開します。 円グラフの属性の一覧が表示されます。  
  
5.  **[PieLabelStyle]** プロパティを **Outside**に設定します。  
  
6.  設定、`PieLineColor`プロパティを**黒**します。 PieLineColor プロパティでは、各データ ポイント ラベルの引き出し線を定義します。  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>円グラフの外側に表示されるラベルの重なりを防ぐには  
  
1.  外側にラベルを設定した円グラフを作成します。  
  
2.  デザイン画面で、円グラフの外側でグラフの罫線の内側を右クリックし、 **[グラフ領域のプロパティ]** をクリックします。 **[グラフ領域のプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[3D オプション]** タブで、 **[3D の有効化]** を選択します。  
  
4.  ラベル用の領域を確保するようにグラフを 2 次元で表示する場合は、 **[回転]** プロパティと **[傾斜]** プロパティを **0**に設定します。  
  
## <a name="see-also"></a>参照  
 [円グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [円グラフの小さいスライスをまとめる &#40;レポート ビルダーおよび SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [円グラフへのパーセンテージの表示 &#40;レポート ビルダーおよび SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
