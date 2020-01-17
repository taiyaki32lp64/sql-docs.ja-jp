---
title: PredictHistogram (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fdc63d1c93d1290c701233cb94f71f157c771182
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893850"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定された列の予測のためのヒストグラムを表すテーブルを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>適用対象  
 スカラー列参照またはクラスター列参照。 [!INCLUDE[msCoName](../includes/msconame-md.md)]アソシエーションアルゴリズムを除くすべてのアルゴリズムの種類で使用できます。  
  
## <a name="return-type"></a>戻り値の型  
 テーブルです。  
  
## <a name="remarks"></a>コメント  
 ヒストグラムでは、統計列が生成されます。 返されるヒストグラムの列構造は、 **PredictHistogram**関数で使用される列参照の型によって異なります。  
  
## <a name="scalar-columns"></a>スカラー列  
 スカラー列参照 > の場合、PredictHistogram 関数が返すヒストグラムは、次の列で構成されます。 \<  
  
-   予測されている値。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニングアルゴリズムでは、 **$ProbabilityVariance**はサポートされていません。 アルゴリズムの場合、この列[!INCLUDE[msCoName](../includes/msconame-md.md)]には常に0が格納されます。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニングアルゴリズムでは、 **$ProbabilityStdev**はサポートされていません。 アルゴリズムの場合、この列[!INCLUDE[msCoName](../includes/msconame-md.md)]には常に0が格納されます。  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability**列は[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、データマイニング仕様の[!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB の拡張機能です。  
  
## <a name="cluster-columns"></a>クラスター列  
 \<クラスター列参照 > に対して**PredictHistogram**関数が返すヒストグラムは、次の列で構成されます。  
  
-   **$Cluster**(クラスター名を表します)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>使用例  
 次の例では、単一クエリの自転車の購入者列の予測された状態を返します。 このクエリでは、 **PredictHistogram**関数を使用して取得された調整済みの確率に基づいて、自転車購入者属性の上位2つの最も可能性の高い状態が返されます。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>関連項目  
 [クラスター &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
