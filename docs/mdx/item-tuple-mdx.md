---
title: Item (タプル) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5740095752b482430cd718d0e2bff813449d92ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105220"
---
# <a name="item-tuple-mdx"></a>Item (タプル) (MDX)


  セットからタプルを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *String_Expression1*  
 有効な文字列式は、通常文字列で表されるタプルです。  
  
 *String_Expression2*  
 有効な文字列式は、通常文字列で表されるタプルです。  
  
 *Index*  
 特定のタプルを返すセット内の位置を指定する有効な数値式です。  
  
## <a name="remarks"></a>コメント  
 **Item**関数は、指定したセットからタプルを返します。 次の 3 つの方法で **Item**関数を呼び出すことができます。  
  
-   1 つの文字列式が指定されている場合、**Item**関数は、指定されたタプルを返します。 たとえば、"([2005].Q3、[Store05])"。  
  
-   1 つ以上の文字列式が指定されている場合、**Item**関数は、指定された座標によって定義されるタプルを返します。 文字列の数は軸の数と一致している必要があり、各文字列で一意の階層を識別しなければなりません。 たとえば、"([2005].Q3、[Store05])"。  
  
-   整数が指定されている場合、**Item**関数は、*インデックス*で指定された 0 から始まる位置にあるタプルを返します。  
  
## <a name="examples"></a>使用例  
 次の例を返します ([1996], Sales)。  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 次の例では、レベル式を使用し、オーストラリアの各州におけるインターネット販売の売上高と、オーストラリアにおけるインターネット販売の合計売上高の割合を返します。 この例では、Item関数を使用して、**Ancestors**関数によって返されるセットから最初の (そして唯一のタプル) を抽出します。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
