---
title: 範囲グラフ (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 48e351d3-ac5b-4eda-a4bd-32a0de206a30
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e44e658d2aaf8be9a9e591f627f60798f6ba4121
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105397"
---
# <a name="range-charts-report-builder-and-ssrs"></a>範囲グラフ (レポート ビルダーおよび SSRS)
  範囲グラフでは、同じカテゴリの複数の値によってそれぞれ定義された、一連のデータ ポイントが表示されます。 値は、マーカーの高さ (値軸) で表されます。 カテゴリのラベルは、カテゴリ軸に表示されます。 一般的な範囲グラフでは、各データ ポイントの最高値と最低値の間の領域が設定されます。  
  
 次の図は、3 つの系列の一般的な範囲グラフを示しています。  
  
 ![範囲グラフ](../media/rs-rangechart.gif "範囲グラフ")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>バリエーション  
  
-   **平滑範囲**: 平滑範囲グラフでは、直線ではなく曲線が表示されます。  
  
-   **範囲縦棒**: 範囲縦棒グラフでは、領域ではなく縦棒を使用して範囲を表示します。  
  
-   **範囲横棒**: 範囲横棒グラフでは、領域ではなく横棒を使用して範囲を表示します。  
  
## <a name="data-considerations-for-range-charts"></a>範囲グラフのデータに関する注意点  
  
-   範囲グラフでは、データ ポイントごとに 2 つの値が必要です。 これらの値は、各データ ポイントの範囲を定義する高値および低値に対応しています。  
  
-   範囲グラフが分析に役立つのは、最高値が常に最低値より大きい場合のみです。 そうでない場合は、折れ線グラフの使用を検討してください。 高値が低値より低い場合、範囲グラフでは、この 2 つの値の差の絶対値が表示されます。  
  
-   値が 1 つしか指定されていない場合、範囲グラフは、各データ ポイントに 1 つの値を持つ、標準の面グラフのように表示されます。  
  
-   範囲グラフは、データセット内の各カテゴリ グループの最小値および最大値を含むデータをグラフ化する場合によく使用されます。  
  
-   範囲グラフでは、各データ ポイントでマーカーを表示することがサポートされていません。  
  
-   一般的な範囲グラフでは、面グラフと同様に、複数の系列の値が同じ場合、系列が重なります。 このシナリオでは、一般的な範囲グラフではなく、範囲縦棒グラフまたは範囲横棒グラフを使用することが必要になる場合があります。  
  
-   ガント チャートは、範囲横棒グラフを使用して作成できます。  
  
## <a name="see-also"></a>関連項目  
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [グラフの種類 &#40;レポート ビルダーおよび SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [グラフの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)  
  
  
