---
title: CoalesceEmpty (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f760220b02396591e684a83305111e487908d19b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006306"
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)


  空のセル値を指定した空でないセル値、数値または文字列に変換します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>引数  
 *Numeric_Expression1*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression2*  
 通常は、指定された数値が有効な数値式です。  
  
 *String_Expression1*  
 有効な文字列式です。通常は、文字列を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression2*  
 通常は、NULL の代わりに使用する指定した文字列値が有効な文字列式が最初のによって返される文字列式を指定します。  
  
## <a name="remarks"></a>コメント  
 1 つまたは複数の数値式が指定されている場合、 **CoalesceEmpty**関数の最初の数値式 (左右から) から空でない値に解決される数値の値を返します。 指定されている数値式に、空でない値に解決される式がない場合、この関数は、空のセル値を返します。 通常、2 番目の数値式の値は、最初の数値式から返された NULL の代わりに使用する数値を指定します。  
  
 最初の文字列値を返します 1 つまたは複数の文字列式を指定する場合の文字列が空でない値に解決できる式 (左から右へ)。 指定した文字列式のいずれも指定できますが、空でない値に解決する場合は、空のセル値を返します。 値では通常、2 番目の文字列式の値は、最初から返された NULL の代わりに使用する文字列値の文字列式です。  
  
 **CoalesceEmpty**関数では、同じ型の値を受け取ることができます。 つまり、指定した値式は、すべて 1 つの数値データ型または空のセル値に評価されるか、すべて 1 つの文字列データ型または空のセル値に評価される必要があります。 この関数の 1 回の呼び出しで、数値式と文字列式を両方含めることはできません。  
  
 空のセルの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="example"></a>例  
 次の例のクエリ、 **Adventure Works**キューブ。 この例は、カテゴリで、各製品の注文数量と注文数量の割合を返します。 **CoalesceEmpty**関数により計算されるメンバーをフォーマットするときに、ゼロ (0) として null 値が表されるようになります。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
