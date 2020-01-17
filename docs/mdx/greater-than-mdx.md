---
title: '&gt; (より大きい)(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bb4f04e623096857cce9dd27f0cddc77f6a59798
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906037"
---
# <a name="gt-greater-than-mdx"></a>&gt; (より大きい)(MDX)


  1 つの多次元式 (MDX) 式の値が、別の MDX 式の値よりも大きいかどうかを判別する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MDX_Expression > MDX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *MDX_Expression*  
 有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 次の条件に基づくブール値。  
  
-   **true**かどうかは、両方のパラメーターが null 以外の場合、および最初のパラメーターが 2 番目のパラメーターの値よりも大きい値です。  
  
-   **false**かどうかは、両方のパラメーターが null 以外の場合、および最初のパラメーターが同じであるか、2 番目のパラメーターの値よりも小さい値です。  
  
-   いずれか一方または両方のパラメーターが NULL 値に評価される場合は、NULL です。  
  
## <a name="examples"></a>使用例  
 次のクエリの例では、この演算子の使用を示します。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is more than 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] > .5,  
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
  
  
