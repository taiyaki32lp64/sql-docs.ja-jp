---
title: 最大 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ad4bc2bf41caacbafb5bf36b5e95263ab2f85d22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098535"
---
# <a name="max-mdx"></a>Max (MDX)


  セットに対して評価される数値式の最大値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Max( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 数値式を指定した場合、この数値式がセットに対して評価されてから、その評価で得られる最大値が返されます。 数値式を指定しなかった場合、指定したセットがそのセットのメンバーの現在のコンテキストで評価されてから、その評価で得られる最大値が返されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、数値セットの最大値が計算される際、NULL 値は無視されます。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブ内の四半期、サブカテゴリ、および国ごとに毎月の売上高の最大値を返します。  
  
```  
WITH MEMBER Measures.x AS Max   
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
  
  
