---
title: 面グラフ (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 245b236d-1d55-4744-b752-80bd133502aa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0c914c31f760021a10c4f26a85bcd1d995f3ef07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106483"
---
# <a name="area-charts-report-builder-and-ssrs"></a>面グラフ (レポート ビルダーおよび SSRS)
  面グラフでは、線で結ばれた点のセットとして系列が表示され、線の下の領域はすべて塗りつぶされます。 面グラフにデータを追加する方法の詳細については、「 [グラフ (レポート ビルダーおよび SSRS)](charts-report-builder-and-ssrs.md)」を参照してください。  
  
 次の図は、積み上げ面グラフの例を示しています。 このデータは積み上げ面グラフでの表示に適しています。このグラフでは、すべての系列の合計に加え、各系列が全体に占める割合も表示できるためです。  
  
 ![面グラフ](../media/areachart.gif "面グラフ")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>バリエーション  
  
-   **積み上げ面**: 複数の系列が垂直方向に積み上げられた面グラフ。 グラフに系列が 1 つしかない場合、積み上げ面グラフでも、面グラフと同じように表示されます。  
  
-   **100% 積み上げ面**: 複数の系列がグラフ領域全体を占めるように垂直方向に積み上げられた面グラフ。 グラフに系列が 1 つしかない場合、積み上げ面グラフでも、面グラフと同じように表示されます。  
  
-   **平滑面**: データ ポイントが直線ではなく平滑線で結ばれている面グラフ。 個々のデータ ポイントの値を表示するよりも傾向を表示することに関心がある場合は、面グラフではなく平滑面グラフを使用します。  
  
## <a name="data-considerations-for-area-charts"></a>面グラフのデータに関する注意点  
  
-   折れ線グラフと同様に、面グラフはデータを連続的に表示するグラフの種類の 1 つです。 このため、面グラフは、継続的に発生するデータを表す場合によく使用されます。  
  
-   100% 積み上げ面グラフは、時間の経過と共に発生するデータの割合を表す場合に役立ちます。  
  
-   系列が 1 つしかない場合、積み上げ面グラフでも、面グラフのように表示されます。  
  
-   一般的な面グラフでは、複数の系列の値が同じ場合、面が重なり、データ ポイントの重要な値がわかりにくくなる可能性があります。 この問題を解決するには、グラフの種類を積み上げ面グラフに変更します。積み上げ面グラフは、面グラフで複数の系列を示すようにデザインされています。  
  
-   積み上げ面グラフ内にギャップがある場合は、データセットに空の値が含まれている可能性があります。空の値は、積み上げ面グラフ上に空白部分として表示されます。 データセット内に空の値がある場合は、グラフ上に空のポイントを挿入することを検討してください。 空のポイントを追加すると、グラフ上の空白領域が、NULL 値または 0 を示す別の色で塗りつぶされます。 詳細については、次を参照してください。[グラフに空のポイントを追加&#40;レポート ビルダーおよび SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)します。  
  
-   面グラフの動作は、縦棒グラフや折れ線グラフとよく似ています。 複数の系列間の比較を行う場合は、縦棒グラフの使用を検討してください。 一定期間の傾向を分析する場合は、折れ線グラフの使用を検討してください。  
  
## <a name="see-also"></a>参照  
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [グラフの種類 &#40;レポート ビルダーおよび SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [折れ線グラフ &#40;レポート ビルダーおよび SSRS&#41;](line-charts-report-builder-and-ssrs.md)   
 [グラフの種類の変更 (レポート ビルダーおよび SSRS)](change-a-chart-type-report-builder-and-ssrs.md)   
 [グラフ内の空のデータ ポイントおよび NULL データ ポイント (レポート ビルダーおよび SSRS)](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
