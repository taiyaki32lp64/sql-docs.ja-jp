---
title: BottomPercent (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbcf9086cedc9221c39832bd0b7d55e5f0814c7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016916"
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)


  セットを昇順で並べ替え、累積合計が、指定した割合以上になるは最小値を持つタプルのセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *[パーセント]*  
 返される組の割合を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **BottomPercent**関数セットを昇順を並べ替え、指定されたセットに対して評価される指定数値式の合計を計算します。 関数は、合計値の累積比率は、少なくとも指定した割合の最小値を持つ要素を返します。 この関数は、累積合計が、指定したパーセンテージでは、少なくともセットの最小サブセットを返します。 要素は大きい方から順に返されます。  
  
> [!IMPORTANT]  
>  **BottomPercent**関数は、このような[TopPercent](../mdx/toppercent-mdx.md)関数を常に階層を解除します。 詳細については、注文を参照してください。 関数。  
  
## <a name="example"></a>例  
 次の例を返します、Bike カテゴリについて、最小ディメンション メンバーのセットの Geography 階層、地理的な場所にある City レベルの 2003 会計年度のメジャーが 15% 以上の Reseller Sales Amount を使用して累積合計が、累積合計 (販売数の最小セットのメンバーで始まる)。  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
