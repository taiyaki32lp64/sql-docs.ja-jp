---
title: '&gt;= (より大きいまたは等しい) (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0e8599378367dd47bd5858c09327795a25852105
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005841"
---
# <a name="gt-greater-than-or-equal-to-mdx"></a>&gt;= (より大きいまたは等しい) (MDX)


  1 つの多次元式 (MDX) 式の値が別の MDX 式の値以上かどうかを判断する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MDX_Expression >= MDX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *MDX_Expression*  
 有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 次の条件に基づくブール値。  
  
-   **true**最初のパラメーターに値より大きいか、2 番目のパラメーターの値と等しいです。  
  
-   **false**最初のパラメーターが 2 番目のパラメーターの値よりも小さい値を持つ場合です。  
  
-   **true**両方のパラメーターが null の場合、または 1 つのパラメーターが null と、その他のパラメーターが 0 の場合。  
  
## <a name="examples"></a>使用例  
 次の例では、この演算子の使用を示します。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is greater than or equal to 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] >= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
    NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[HighGPM])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
