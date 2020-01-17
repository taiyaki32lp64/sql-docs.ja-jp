---
title: 序数 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b22cc6d5a609f8e1f585ccc1229e0e1cd67e1796
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055640"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)


  レベルに関連付けられた 0 から始まる序数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
## <a name="remarks"></a>コメント  
 **序数**関数は組み合わせて使用頻度、 **IIF**と**CurrentMember**条件付きで別に異なる値を表示する関数クエリ結果内の特定の各セルの序数位置に基づいて、階層レベル。 たとえば、使用することができます、**序数**関数を特定のレベルで計算を実行し、他のレベルで"N/A"の既定値を表示します。  
  
## <a name="example"></a>例  
 次の例では、Calendar 階層内の Calendar Quarter レベルの序数が返されます。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
