---
title: TopCount (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0f607f3111c150bff3d5dc562c77901a381bedc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036604"
---
# <a name="topcount-mdx"></a>TopCount (MDX)


  セットを降順で並べ替えおよび指定した数の最大値を持つ要素を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、 **TopCount**関数、順序、指定したに対して評価される数値式で指定された値に基づいて指定されたセットで指定されたセット内の組を降順で並べ替えます設定します。 セットを並べ替えて、 **TopCount**関数し、指定した数の最大値を持つタプルを返します。  
  
> [!IMPORTANT]  
>  ように、 [BottomCount](../mdx/bottomcount-mdx.md)関数の場合、 **TopCount**関数は常に、階層を解除します。  
  
 数値式が指定されていない場合、関数のセットを返しますメンバー、自然な順序で、並べ替えを行わず同様の動作、 [Head (MDX)](../mdx/head-mdx.md)関数。  
  
## <a name="examples"></a>使用例  
 次の例では、Internet Sales Amount を上位 10 日を返します。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 次の例では、Bike カテゴリについて、Geography ディメンションの Geography 階層にある City レベルのメンバーのすべての組み合わせと Date ディメンションの Fiscal 階層のすべての会計年度を含んでいるセットを、Reseller Sales Amount メジャーで (最も売上が多いメンバーが 1 番目になるように) 並べ替えて、最初の 5 つのメンバーを返します。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
