---
title: OpeningPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 07f94c3ed850af10120b1de7d95941bc5c90e826
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088221"
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)


  指定したレベル、オプションで指定されたメンバーの子孫のうち、最初の兄弟を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 この関数がある主な対象は、時間ディメンションの使用がどのディメンションでも使用できます。  
  
-   レベル式が指定されている場合、 **OpeningPeriod**関数は、階層を指定されたレベルを含み、指定されたレベルで既定のメンバーの子孫のうち、最初の兄弟を返しますを使用します。  
  
-   レベル式もメンバー式が指定されている場合、 **OpeningPeriod**関数は、指定されたを含む階層内で指定されたレベルで指定されたメンバーの子孫のうち、最初の兄弟を返しますレベルです。  
  
-   レベル式もメンバー式が指定されている場合、 **OpeningPeriod**関数と Time 型の既定のレベルと、ディメンションのメンバーを使用します。  
  
> [!NOTE]  
>  [ClosingPeriod](../mdx/closingperiod-mdx.md)機能に似ています、 **OpeningPeriod**関数点を除いて、 **ClosingPeriod**関数は、1 つ目ではなく、最後の兄弟を返します兄弟です。  
  
## <a name="examples"></a>使用例  
 次の例では、(時間の種類がある) Date ディメンションの FY2002 メンバーの既定のメジャーの値を返します。 このメンバーが返されるは、Fiscal Year レベルが [All] レベルの最初の子孫であるため、階層コレクション内の最初のユーザー定義階層であり、fy 2002 メンバーが、最初の兄弟のため、Fiscal 階層は、既定の階層このレベルの階層。  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、2001 年 7 月 1 日の既定のメジャー値を返します、Date.Date 属性階層の Date.Date.Date レベルにあるメンバー。 このメンバーは、Date.Date 属性階層の [All] レベルの子孫の最初の兄弟です。  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、January, 2003 メンバーの既定のメジャーに対応する値が返されます。これは、Calendar ユーザー定義階層の Year レベルにある 2003 メンバーの子孫の最初の兄弟です。  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、July, 2002 メンバーの既定のメジャーに対応する値が返されます。これは、Fiscal ユーザー定義階層の Year レベルにある 2003 メンバーの子孫の最初の兄弟です。  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
