---
title: PredictSupport (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 701d8fb43b468f6bbd33fbff9ff7cfc8deb386f9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893837"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定された状態に対するサポート値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>適用対象  
 スカラー列。  
  
## <a name="return-type"></a>戻り値の型  
 スカラー列参照 *\<* *>* によって指定された型のスカラー値。  
  
## <a name="remarks"></a>コメント  
 予測された状態が省略されている場合、省略した状態バケットを除いて、最も予測可能性が高い状態が使用されます。 欠落している状態バケットを含めるに\<は、予測された状態 > を**INCLUDE_NULL**に設定します。  
  
 欠落状態のサポートを返すには、予測さ\<れた状態 > を NULL に設定します。  
  
> [!NOTE]  
>  サポートされている値の計算方法は異なります。つまり、クエリの対象となるモデルに応じてこの値の解釈は異なる場合があります。 特定の種類のモデルのサポートを計算する方法の詳細については、「[マイニングモデルコンテンツ&#40;Analysis Services-データマイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」の個々のアルゴリズムの種類を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、単一クエリを使用して、個人が自転車購入者であるかどうかを予測します。また、TM デシジョンツリーマイニングモデルに基づく予測のサポートも決定します。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
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
 [データマイニング拡張&#40;機能&#41; DMX 関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;関数&#41;](../dmx/functions-dmx.md)   
 [一般的な予測&#40;関数 DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
