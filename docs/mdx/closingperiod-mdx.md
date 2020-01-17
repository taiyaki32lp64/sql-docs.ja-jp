---
title: ClosingPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 102485ede0e52389d43bdb64742a2564aaa71419
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016794"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)


  指定されたレベルで指定されたメンバーの子孫のうち、最後の兄弟であるメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 この関数は、Time 型のディメンションに対して使用する主な対象が、どのディメンションでも使用できます。  
  
-   レベル式が指定されている場合、 **ClosingPeriod**関数は、ディメンションを指定されたレベルを含み、指定されたレベルで既定のメンバーの子孫のうち、最後の兄弟を返しますを使用します。  
  
-   レベル式もメンバー式が指定されている場合、 **ClosingPeriod**関数は、指定されたレベルで指定されたメンバーの子孫のうち、最後の兄弟を返します。  
  
-   レベル式もメンバー式が指定されている場合、 **ClosingPeriod**関数を使用して既定のレベルと、ディメンションのメンバー (存在する場合) 時の型を持つキューブでします。  
  
 **ClosingPeriod**関数は、次の MDX ステートメントと同等です。  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`。  
  
> [!NOTE]  
>  [OpeningPeriod](../mdx/openingperiod-mdx.md)機能に似ています、 **ClosingPeriod**関数点を除いて、 **OpeningPeriod**最後ではなく、最初の兄弟を返します兄弟です。  
  
## <a name="examples"></a>使用例  
 次の例では、(時間のセマンティックの種類がある) Date ディメンションの FY2007 メンバーの既定のメジャーの値を返します。 このメンバーが返されるのは、[All] レベルの最初の子孫が Fiscal Year レベルであるためです。Fiscal 階層は、階層コレクション内の最初のユーザー定義階層であるため既定の階層です。また、FY 2007 メンバーはこの階層内のこのレベルにある最後の兄弟です。  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、2006 年 11 月 30 日の既定のメジャー値を返します、Date.Date 属性階層の Date.Date.Date レベルにあるメンバー。 このメンバーは、Date.Date 属性階層の [All] レベルの子孫の最後の兄弟です。  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、December, 2003 メンバーの既定のメジャーに対応する値が返されます。これは、Calendar ユーザー定義階層の Year レベルにある 2003 メンバーの子孫の最後の兄弟です。  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、既定のメジャーの値は、6 月、年にある 2003年メンバーの子孫の最後の兄弟である 2003年メンバーのレベルを返します、Fiscal ユーザー定義階層です。  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
