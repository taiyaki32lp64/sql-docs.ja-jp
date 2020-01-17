---
title: StdevP (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d4560ecbecd5db2e0f93e6910239fde27d54c028
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036867"
---
# <a name="stdevp-mdx"></a>StdevP (MDX)


  バイアスをかけた母集団の公式を使用して、セットに対して評価される数値式の母標準偏差を返します (除算*n*)。  
  
## <a name="syntax"></a>構文  
  
```  
  
StdevP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **StdevP**関数は、バイアスをかけた母集団を使用しているときに、数式、 [Stdev](../mdx/stdev-mdx.md)関数は、バイアスをかけない母集団の公式を使用します。  
  
## <a name="example"></a>例  
 次の例では、バイアスをかけた母集団の公式を使用して、2003 年度の最初の 3 か月に対して評価した、Internet Order Quantity の標準偏差を返します。  
  
```  
WITH MEMBER Measures.x AS   
   StdevP   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
