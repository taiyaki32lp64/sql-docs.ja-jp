---
title: Count (タプル) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 486c68e1947bfad67bc0288751d03c6042cd7f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047269"
---
# <a name="count-tuple-mdx"></a>Count (タプル) (MDX)


  タプルの次元数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Expression*  
 タプルを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 タプルの次元数を返します。  
  
## <a name="example"></a>例  
 次のクエリで計算されるメジャーが、タプルにある階層の数は、値 2 を返します`([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])`:  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [カウント&#40;ディメンション&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [カウント&#40;階層レベル&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
