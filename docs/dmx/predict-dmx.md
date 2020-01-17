---
title: 予測 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb939c45d298117fa81b05d6188aa3a4c5cd7c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008163"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **Predict**予測された値、または指定された列の値のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>適用対象  
 スカラー列参照またはテーブル列の参照。  
  
## <a name="return-type"></a>戻り値の型  
 \<スカラー列参照 >  
  
 または  
  
 \<テーブルの列参照 >  
  
 戻り値の型は、この関数を適用する列の種類によって異なります。  
  
> [!NOTE]  
>  包括的、EXCLUSIVE、INPUT_ONLY、および INCLUDE_STATISTICS のみテーブルの列の参照とに適用されます EXCLUDE_ および INCLUDE_ はスカラー列参照に対してのみ適用します。  
  
## <a name="remarks"></a>コメント  
 オプションには、EXCLUDE_NULL (既定)、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE (既定)、INPUT_ONLY、および INCLUDE_STATISTICS が含まれています。  
  
> [!NOTE]  
>  タイム シリーズ モデルでは、Predict 関数では、INCLUDE_STATISTICS はサポートしません。  
  
 INCLUDE_NODE_ID パラメーターは、結果に $NODEID 列を返します。 NODE_ID は、特定のケースの予測を実行するコンテンツ ノードです。 テーブルの列に対して予測を使用する場合、このパラメーターは省略可能です。  
  
 *N*パラメーター テーブルの列に適用されます。 これには、予測の種類に基づいて返される行の数を設定します。 呼び出す、基になる列がシーケンスの場合、 **PredictSequence**関数。 基になる列が時系列の場合は、呼び出し、 **PredictTimeSeries**関数。 予測の種類が結合型を呼び出し、 **PredictAssociation**関数。  
  
 **Predict**関数は、ポリモーフィズムをサポートしています。  
  
 使用される頻度の高い代替省略形は次のとおりです。  
  
-   [Gender] は代替の**Predict**([Gender], EXCLUDE_)。  
  
-   [Products Purchases] は代替の**Predict**([Products Purchases], exclude _、排他)。  
  
    > [!NOTE]  
    >  この関数の戻り値の型は、列の参照と見なされる自体。 つまり、 **Predict**関数は、他の関数に引数として列の参照を引数として使用できます (を除き、 **Predict**関数自体)。  
  
 列を追加する INCLUDE_STATISTICS をテーブル値列の予測に渡す **$Probability**と **$Support**結果のテーブル。 これらの列には、関連付けられている入れ子になったテーブルのレコードの存在の確率がについて説明します。  
  
## <a name="examples"></a>使用例  
 次の例では、Predict 関数を使用して、一緒に販売できる可能性が最も高い Adventure Works データベースの 4 つの製品を返します。 自動的に使用して、関数は、アソシエーション ルール マイニング モデルに対して、予測するため、 **PredictAssociation**前に説明したとおりに機能します。  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 サンプルの結果 :  
  
 このクエリは、1 行の 1 つの列のデータを返します。`Expression`が、その列には、次の入れ子になったテーブルが含まれています。  
  
|モデル|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
