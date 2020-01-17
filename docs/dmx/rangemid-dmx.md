---
title: RangeMid (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ee926e04dc5b845be152e96150c99cb17182a7c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042107"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  離散化列に対して検出される予測バケットの中点を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>適用対象  
 離散化スカラー列。  
  
## <a name="return-type"></a>戻り値の型  
 スカラー値です。  
  
## <a name="remarks"></a>コメント  
 使用すると[SELECT FROM&#60;モデル&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)、 **RangeMin**、 **RangeMid**、および**RangeMax**関数、指定されたバケットの実際の境界値を返します。 たとえば、離散化列で予測を実行する場合、クエリは予測されたバケット数を離散化列に返します。 **RangeMin**、 **RangeMid**、および**RangeMax**関数が、予測が指定したバケットを説明します。 ときに、 **RangeMid** PREDICTION JOIN ステートメントを使用して関数を使用すると、スカラー列参照は不連続列および予測可能な列のみを保持できます。  
  
## <a name="examples"></a>使用例  
 次の例では、TM Decision Tree マイニング モデルの Yearly Income 連続列の最小、最大、平均値を返します。  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [関数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
