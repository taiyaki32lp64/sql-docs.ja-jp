---
title: PredictProbability (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd8365b2d3aac82c184af549ef21952fd4c8e649
ms.sourcegitcommit: 75fe364317a518fcf31381ce6b7bb72ff6b2b93f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2019
ms.locfileid: "68893904"
---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定された状態の確率を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>適用対象  
 スカラー列。  
  
## <a name="return-type"></a>戻り値の型  
 スカラー値です。  
  
## <a name="remarks"></a>Remarks  
 予測された状態が省略されている場合、省略した状態バケットを除いて、確率が最も高い状態が使用されます。 欠落している状態バケットを含めるには、\<予測された状態の > を**INCLUDE_NULL**に設定します。 欠落状態の確率を返すには、\<予測状態 > を NULL に設定します。  
  
> [!NOTE]  
>  一部のマイニングモデルには確率値が指定されていないため、この関数を使用することはできません。 また、特定のターゲット値の確率値は異なる方法で計算されます。また、クエリを実行するモデルの種類によっては、解釈が異なる場合があります。 特定の種類のモデルに対する確率の計算方法の詳細については、「[マイニングモデルコンテンツ&#40;Analysis Services-データマイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」の個々のアルゴリズムに関するトピックを参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、自然予測結合を使用して、個人が TM デシジョンツリーマイニングモデルに基づいた自転車購入者である可能性があるかどうかを判断し、予測の確率も決定します。 この例では、可能な値ごとに1つずつ、PredictProbability 関数が2つあります。 この引数を省略した場合、関数は最も可能性の高い値の確率を返します。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 例の結果を次に示します。  
  
|Bike Buyer|Bike Buyer = Yes|Bike Buyer = No|  
|----------------|-----------------------|----------------------|  
|@shouldalert|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Functions &#40;DMX&#41; ](../dmx/functions-dmx.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
