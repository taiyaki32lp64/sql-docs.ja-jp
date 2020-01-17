---
title: 折れ線グラフ (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 194e6679-890d-4a3e-a756-130d32ef7e29
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 20e9e6626bbd08eebfe69a04f63ed882979b34d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580156"
---
# <a name="line-charts-report-builder-and-ssrs"></a>折れ線グラフ (レポート ビルダーおよび SSRS)
  折れ線グラフでは、1 本の線で結ばれた点のセットとして系列が表示されます。 折れ線グラフは、継続的に発生する大量のデータを表す場合に使用されます。 折れ線グラフにデータを追加する方法の詳細については、「 [グラフ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)」を参照してください。  
  
 次の図は、3 つの系列を含む折れ線グラフを示しています。  
  
 ![折れ線グラフ](../../reporting-services/report-design/media/rs-linechart.gif "折れ線グラフ")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>バリエーション  
  
-   **平滑線**: 直線ではなく曲線を使用した折れ線グラフ。  
  
-   **階段状折れ線**: 直線ではなく階段状折れ線を使用した折れ線グラフ。 階段状折れ線は、はしごや階段の段のように見える線を使用して点を結びます。  
  
-   **スパークライン グラフ**: 折れ線グラフの一種で、テーブルまたはマトリックスのセルに線系列のみが表示されます。 詳細については、「 [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="data-considerations-for-line-charts"></a>折れ線グラフのデータに関する注意点  
  
-   既定の折れ線グラフの視覚的な効果を高めるには、系列の罫線の幅を 3 に変更したり、影のオフセットを 1 にしたりすることを検討してください。 こうすると、太い折れ線グラフが作成されます。 グラフの種類を折れ線グラフから他の種類に変更する場合は、これらのプロパティを元の値に戻す必要があります。  
  
-   データセット内に空の値がある場合、折れ線グラフでは、グラフ上で連続性を維持するために、プレースホルダーの線の形式で空のポイントが追加されます。 この線が表示されないようにする場合は、横棒グラフや縦棒グラフなど、連続性のない種類のグラフを使用してデータセットを表示することを検討してください。  
  
-   折れ線グラフでは、線を描画するために少なくとも 2 つのポイントが必要です。  データセットにデータ ポイントが 1 つしかない場合、折れ線グラフは 1 つのデータ ポイント マーカーとして表示されます。  
  
-   線で描画される系列は、グラフ領域内であまり場所を取りません。  そのため、折れ線グラフは、縦棒グラフなどの他の種類のグラフと組み合わせることがよくあります。 ただし、折れ線グラフは、横棒、極座標、円、または図形のグラフと組み合わせることはできません。  
  
## <a name="see-also"></a>参照  
 [横棒グラフ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [縦棒グラフ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [グラフ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [グラフの種類 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [面グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)   
 [グラフ内の空のデータ ポイントおよび NULL データ ポイント (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
