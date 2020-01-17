---
title: IsInNode (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e4c7df84bc7bf3a4804db76d952b1219100ef5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008363"
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定されたノードが現在のケースを含んでいるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>戻り値の型  
 ブール型です。  
  
## <a name="remarks"></a>コメント  
 **IsInNode**でのみ使用が[SELECT FROM&#60;モデル&#62;します。ケース&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)と[SELECT FROM&#60;モデル&#62;します。SAMPLE_CASES &#40;DMX&#41; ](../dmx/select-from-model-sample-cases-dmx.md)クエリ。  
  
## <a name="examples"></a>使用例  
 次の例では、IsInNode 関数で指定されているノードに関連付けられているモデルの作成に使用されたすべてのケースを返します。  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
