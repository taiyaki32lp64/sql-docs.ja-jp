---
title: (除算)(MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8dd20a0b60e105ac48a54d533055717e3f07a006
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049324"
---
# <a name="divide---mdx-operator-reference"></a>除算の MDX 演算子リファレンス


  1 つの数値を別の数値で除算する算術演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>パラメーター  
 *被除数*  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
 *除数*  
 数値の値を返す有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 優先順位の高いパラメーターのデータ型の値。  
  
## <a name="remarks"></a>コメント  
 によって返される実際の値、 **/(除算)** 演算子が 2 番目の式で除算する最初の式の商を表します。  
  
 両方の式は、同じデータ型でなければなりません。または、一方の式をもう一方の式のデータ型に暗黙的に変換できる必要があります。 場合*除数*エラー、オペレーターが発生、null 値に評価します。 両方*除数*と*被除数*評価、演算子、null の値に null 値を返します。  
  
## <a name="examples"></a>使用例  
 次の例では、この演算子の使用を示します。  
  
```  
-- This query returns the freight cost per user,  
-- for products, averaged by month.   
With Member [Measures].[Freight Per Customer] as  
    [Measures].[Internet Freight Cost]  
    /   
    [Measures].[Customer Count]  
  
SELECT   
    [Ship Date].[Calendar].[Calendar Year] Members ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
 0 以外の値または NULL 以外の値を 0 または NULL で除算すると、無限大という値が返されます。これは、値 "1.#INF" としてクエリ結果に表示されます。 ほとんどの場合、この状況を回避するために 0 除算をチェックする必要があります。 次の例では、この方法を示します。  
  
 `//Returns 1.#INF when Internet Sales Amount is zero or null`  
  
 `Member [Measures].[Reseller to Internet Ratio] AS`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `//Traps the division by zero scenario and returns null instead of 1.#INF`  
  
 `Member [Measures].[Reseller to Internet Ratio With Error Handling] AS`  
  
 `IIF([Measures].[Internet Sales Amount]=0, NULL,`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount])`  
  
 `SELECT`  
  
 `{[Measures].[Reseller to Internet Ratio],[Measures].[Reseller to Internet Ratio With Error Handling]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
## <a name="see-also"></a>関連項目  
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
