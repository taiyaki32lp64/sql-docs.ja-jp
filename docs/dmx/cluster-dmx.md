---
title: クラスター (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa7df2782b8102e386c70d5e874a25f7868dbb1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071077"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  入力ケースを含んでいる可能性が最も高いクラスターを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>適用対象  
 この関数は、基本となるデータ マイニング モデルがクラスターをサポートする場合にのみ使用できます。  
  
## <a name="return-type"></a>戻り値の型  
 **クラスター**関数のパラメーターは必要ありません。  
  
 **クラスター**関数は、クラスター名のスカラー値を返します。 ただし、別の関数の引数としてこの関数を使用する場合は、する必要があります記事として、\<クラスター列参照 >。  
  
## <a name="remarks"></a>コメント  
 **クラスター**としても使用できます、`<`クラスター列参照`>`の**PredictHistogram**関数。  
  
## <a name="examples"></a>使用例  
 次のコードの例では、単一クエリを使用、 [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md)クラスター機能、TM Clustering マイニング モデルの各クラスターから個々 のケースの距離を取得して、個々 のケースが各クラスターである確率です。  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>関連項目  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
