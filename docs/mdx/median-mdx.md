---
title: 中央値 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b6f941e269bb9948dd39ba52db0ea4d0961c029a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033856"
---
# <a name="median-mdx"></a>Median (MDX)


  セットに対して評価される数値式の中央値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、指定された数値式は、セット全体が評価され、その評価から得られる中央値を返します。 数値式が指定されていない場合、指定したセットは、セットのメンバーの現在のコンテキストでが評価され、評価から中央値を返します。  
  
 中央値とは、順番に並べられた数値のセットの中央に位置する値です (セット内の数値の合計を、セット内にある数値の数で除算する平均値とは異なります)。 中央値は、セット内の値の少なくとも半数が、その値以下になるような最小の値を選択することによって決まります。 セット内の値の数が奇数の場合、中央値は 1 つの値になります。 セット内の値の数が偶数の場合は、中央に位置する 2 つの値の合計を 2 で除算した値が返されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、数値セットの中央値が計算される際、NULL 値は無視されます。  
  
## <a name="example"></a>例  
 次の例では、各四半期、サブカテゴリごとおよび国ご Adventure Works キューブ内の中央値の月単位の売上を返します。  
  
```  
WITH MEMBER Measures.x AS Median   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
