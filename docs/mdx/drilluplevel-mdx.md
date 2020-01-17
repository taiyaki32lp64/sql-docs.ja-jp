---
title: DrillupLevel (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ef2f94eb843b3ffbfbb67eb6ca01f2114522e024
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049221"
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)


  セットのメンバーのうち、指定されたレベルの下位に属するメンバーをドリル アップします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
## <a name="remarks"></a>コメント  
 **DrillupLevel**指定されたセットに含まれるメンバーに基づいて、関数の戻り値のメンバーのセットは階層化されています。 順序指定されたセット内のメンバーは保持されます。  
  
 レベル式が指定されている場合、 **DrillupLevel**関数は、指定されたレベルより上位にあるメンバーのみを取得してセットを構築します。 レベル式が指定されて、指定されたセットで表される、指定されたレベルのメンバーが存在しない場合は、指定したセットが返されます。  
  
 レベル式が指定されていない場合、指定されたセット内で参照されている最初のディメンションの最下位レベルより 1 つ上のレベルにあるメンバーだけを取得してセットを構築します。  
  
## <a name="example"></a>例  
 次の例は、最初のセットから Subcategory レベルより上位にあるメンバーのセットを返します。  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
