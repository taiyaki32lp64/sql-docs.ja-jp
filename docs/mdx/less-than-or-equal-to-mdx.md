---
title: '&lt;= (に等しいまたはそれよりも小さい) (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 00021ea9c23de80f6b025963543af2cf4be2f572
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905683"
---
# <a name="lt-less-than-or-equal-to-mdx"></a>&lt;= (に等しいまたはそれよりも小さい) (MDX)


  1 つの多次元式 (MDX) 式の値が、別の MDX 式の値以下であるかどうかを判別する比較演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MDX_Expression <= MDX_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *MDX_Expression*  
 有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 次の条件に基づくブール値。  
  
-   t**rue**両方のパラメーターが null 以外の場合、最初のパラメーターは、いずれかの値を持つ場合、2 番目のパラメーターの値未満です。  
  
-   f**インクルード**両方のパラメーターが null 以外の場合、最初のパラメーターの値を持つ場合が 2 番目のパラメーターの値より大きい。  
  
-   いずれか一方または両方のパラメーターが NULL 値に評価される場合は、NULL です。  
  
## <a name="examples"></a>使用例  
 次の例では、この演算子の使用を示します。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is less than or equal to 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
