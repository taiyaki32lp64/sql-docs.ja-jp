---
title: NextMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b852564510c6b5918c781e0c75e84e3b30aecd44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088359"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  指定したメンバーを含むレベルで、次のメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **NextMember**関数は、指定されたメンバーを含む同じレベルで、次のメンバーを返します。  
  
## <a name="example"></a>例  
 次の例では、July 2001 メンバーを次のメンバーとして August 2001 メンバーを返します。  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
