---
title: Ytd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125759"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  以降で最初の兄弟、という制約の指定したメンバーで終わる、指定されたメンバーと同じレベルのメンバーの兄弟のセットを返します、*年*時間ディメンション内のレベル。  
  
## <a name="syntax"></a>構文  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 メンバー式が指定されていない、既定値は最初の階層の現在のメンバーの種類のレベルを持つ*年*型の最初の次元の*時間*メジャー グループ内。  
  
 **Ytd**関数のショートカット関数では、 [PeriodsToDate](../mdx/periodstodate-mdx.md)関数レベルの基になる属性階層の Type プロパティに設定されている*年*します。 つまり、`Ytd(Member_Expression)`と等価`PeriodsToDate(Year_Level_Expression,Member_Expression)`します。 Type プロパティ設定されている場合、この関数は動作しないことに注意してください*FiscalYears*します。  
  
## <a name="example"></a>例  
 次の例の合計を返して、`Measures.[Order Quantity]`に含まれている 2003 年の最初の 8 月にわたり、メンバー、`Date`ディメンションから、 **Adventure Works**キューブ。  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **Ytd**つまり指定すると、パラメーターのない組み合わせで頻繁に使用が、 [CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md)関数は、のようにに、レポートでは、年度累計の累積合計を表示は、次のクエリ:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
