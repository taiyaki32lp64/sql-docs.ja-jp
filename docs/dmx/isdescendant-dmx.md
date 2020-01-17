---
title: IsDescendant (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7f6f3532165b8e958eb03cdf4954543159309a08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937711"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  現在のノードが、指定したノードから下降かどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>戻り値の型  
 ブール型です。  
  
## <a name="remarks"></a>コメント  
 **IsDescendant**でのみ使用が[SELECT FROM&#60;モデル&#62;します。コンテンツ&#40;DMX&#41; ](../dmx/select-from-model-content-dmx.md)と[SELECT FROM&#60;モデル&#62;します。DIMENSION_CONTENT &#40;DMX&#41; ](../dmx/select-from-model-dimension-content-dmx.md)クエリ。  
  
## <a name="examples"></a>使用例  
 次の例は、IsDescendant 関数に指定されたノードの子孫であるケースをすべて返します。  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
