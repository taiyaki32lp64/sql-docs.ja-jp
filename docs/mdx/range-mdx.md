---
title: :(範囲)(MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6afc3a73b958062bd6472153b2452bc0e3fa6cfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020621"
---
# <a name="-range-mdx"></a>:(範囲)(MDX)


  自然な順序で並べたセットを返すセット演算を実行します。指定された 2 つのメンバーが終端になり、その 2 つのメンバーの間にあるすべてのメンバーがセットのメンバーに含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>パラメーター  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="return-value"></a>戻り値  
 指定されたメンバーと指定したメンバーの間のすべてのメンバーを含むセット。  
  
## <a name="remarks"></a>コメント  
 両方のパラメーターに、ディメンションの同じレベルと同じ階層にあるメンバーを指定する必要があります。 両方のパラメーターは、同じメンバーを指定する場合、 **:(範囲)** 演算子が指定されたメンバーのみを含むセットを返します。 最初のパラメーターが Null の場合は、セットには、最大の 2 番目のパラメーターで指定されたメンバーのレベルの開始およびそのメンバーを含むすべてのメンバーが含まれます。 2 番目のパラメーターが Null の場合は、セットには、最大、最初のパラメーターで指定し、同じレベルの最後のメンバーを含むメンバーからすべてのメンバーが含まれます。  
  
 MDX にこのセット演算子と等価な関数はありません。  
  
## <a name="examples"></a>使用例  
 次の例では、この演算子の使用を示します。  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
