---
title: Lag (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7e95af96249b64f86bb1466283e8a1a38a32d90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905774"
---
# <a name="lag-mdx"></a>Lag (MDX)


  メンバーのレベルで指定されたメンバーの前に位置の指定した数であるメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Index*  
 メンバー位置を後退させる数を指定する有効な数値式です。  
  
## <a name="remarks"></a>コメント  
 レベル内でメンバーの位置は、属性階層の自然な順序によって決まります。 メンバーの位置の基点は 0 です。  
  
 指定した間隔が 0 の場合、 **Lag**関数は、指定されたメンバー自体を返します。  
  
 指定した間隔が負の場合、 **Lag**関数は、後続のメンバーを返します。  
  
 `Lag(1)` 同じですが、 [PrevMember](../mdx/prevmember-mdx.md)関数。 `Lag(-1)` 同じですが、 [NextMember](../mdx/nextmember-mdx.md)関数。  
  
 **Lag**機能に似ています、[リード](../mdx/lead-mdx.md)関数点を除いて、**リード**関数は方向が逆になります、 **Lag**関数。 つまり、`Lag(n)`と等価`Lead(-n)`します。  
  
## <a name="example"></a>例  
 次の例では、2001 年 12 月の値を返します。  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、2002 年 3 月の値が返されます。  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
