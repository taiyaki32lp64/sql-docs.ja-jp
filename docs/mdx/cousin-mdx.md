---
title: Cousin (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a98d496467e2fd75924b0067257f192c79cdf6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047248"
---
# <a name="cousin-mdx"></a>Cousin (MDX)


  同じ相対位置として、指定した子メンバーの親メンバーの子メンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Ancestor_Member_Expression*  
 先祖メンバーを返す有効な多次元式 (MDX) メンバー式。  
  
## <a name="remarks"></a>コメント  
 この関数は、順序、レベル内のメンバーの位置では動作します。 2 つの階層が存在し、一方の階層に 4 つ、他方の階層に 5 つのレベルがあるとすると、一方の階層の 3 番目のレベルに対応する "いとこ" の位置関係に当たる子メンバーは他方の階層の 3 番目のレベルです。  
  
## <a name="examples"></a>使用例  
 次の例では、2003 会計年度の year レベルでは、その先祖に基づいて、2002 会計年度の第 4 四半期の子メンバーを取得します。 取得される子メンバーは、2003 会計年度の第 4 四半期です。  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、2004 会計年度の第 2 四半期の quarter レベルでは、その先祖に基づいて 2002 会計年度の 7 月の子メンバーを取得します。 取得される子メンバーは、2003 年 10 月の 1 か月です。  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
