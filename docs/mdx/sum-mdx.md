---
title: Sum (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb4e9d55ef2228404dd9113170066e4a3612a0a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036676"
---
# <a name="sum-mdx"></a>Sum (MDX)


  指定されたセットに対して評価される数値式の合計を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 有効な多次元式 (MDX) セット式です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、指定された数値式がセットに対して評価し、合計されます。 数値式を指定しなかった場合、指定したセットがセットのメンバーの現在のコンテキストで評価されてから、合計が算出されます。 SUM 関数を数値式ではない式に適用した場合、結果は不確定になります。  
  
> [!NOTE]  
>  Analysis Services では、数値セットの合計が計算される際、NULL 値は無視されます。  
  
## <a name="examples"></a>使用例  
 次の例では、2001 年と 2002 年、Product.Category 属性階層のすべてのメンバーの再販業者の売上金額の合計を返します。  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、2002 年 7 月のインターネット販売にかかる運賃をその月の 20 日まで合計して返しています。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 次の例は、WITH MEMBER キーワードおよび**合計**の Canada と United States メンバーに対する Reseller Sales Amount メジャーの合計を格納する、メジャー ディメンションの計算されるメンバーを定義する関数、Geography ディメンション内の country 属性階層。  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 多くの場合、**合計**関数を併用、 **CURRENTMEMBER**関数または関数と同様**YTD**階層の currentmember に応じて異なるセットを返します。 たとえば、次のクエリは、年度の初めから ROWS 軸に表示されている日付までのすべての日付の Internet Sales Amount メジャーの合計を返します。  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
