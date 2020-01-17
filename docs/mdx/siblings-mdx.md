---
title: 兄弟 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8ba2dd26575ebd41f4a6c275a2668b1421dee6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036948"
---
# <a name="siblings-mdx"></a>Siblings (MDX)


  指定されたメンバー自体を含めて、メンバーの兄弟を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
### <a name="example"></a>例  
 次の例では、既定のメジャーは、兄弟を 2003 年 3 月と年 3 月の 2003 年 1 月の 2003年と February 2003 を返します。  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
