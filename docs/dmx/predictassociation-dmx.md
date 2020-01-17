---
title: PredictAssociation (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3038bd010c5ca76ad26a301bad45ff4e1aa29460
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008063"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  結合メンバーシップを予測します。  
  
たとえば、PredictAssociation 関数を使用すると、顧客の買い物かごの現在の状態を指定した推奨事項のセットを取得します。 
  
## <a name="syntax"></a>構文  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>適用対象  
 予測可能な入れ子になったテーブル関連付けといくつかの分類アルゴリズムにはが含まれているアルゴリズムです。 入れ子になったテーブルをサポートする分類アルゴリズムには、[!INCLUDE[msCoName](../includes/msconame-md.md)]デシジョン ツリー、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes、および[!INCLUDE[msCoName](../includes/msconame-md.md)]ニューラル ネットワーク アルゴリズム。  
  
## <a name="return-type"></a>戻り値の型  
 \<テーブル式 >  
  
## <a name="remarks"></a>コメント  
 オプション、 **PredictAssociation**関数には、EXCLUDE_、INCLUDE_、INCLUSIVE、EXCLUSIVE (既定)、INPUT_ONLY、INCLUDE_STATISTICS、および INCLUDE_NODE_ID が含まれます。  
  
> [!NOTE]  
>  包括的、EXCLUSIVE、INPUT_ONLY、および INCLUDE_STATISTICS のみテーブルの列の参照とに適用されます EXCLUDE_ および INCLUDE_ はスカラー列参照に対してのみ適用します。  
  
 INCLUDE_STATISTICS はのみ返します **$Probability**と **$AdjustedProbability**します。  
  
 場合数値パラメーター *n*が指定されている、 **PredictAssociation**確率に基づく上位の n 個の最も可能性の高い値を返します。  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 含める場合 **$AdjustedProbability**、ステートメントが最上部を返す*n*値に基づいて、 **$AdjustedProbability**します。  
  
## <a name="examples"></a>使用例  
 次の例では、 **PredictAssociation**データベースの Adventure Works では、4 つの製品を返す関数が一緒に販売できる最も高い。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
次の例では、使い方入れ子になったテーブル、予測関数への入力として、SHAPE 句を使用してを示します。 SHAPE クエリでは、customerId が 1 つの列として、顧客が既にになる製品の一覧を含む 2 番目の列として入れ子になったテーブルを行セットを作成します。 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
