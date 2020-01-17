---
title: Qtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8856b28d8eec76d2bc262c4209b007c0a7fa04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020637"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  以降で最初の兄弟、という制約の指定したメンバーで終わる、指定されたメンバーと同じレベルのメンバーの兄弟のセットを返します、*四半期*時間ディメンション内のレベル。  
  
## <a name="syntax"></a>構文  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 最初の階層の現在のメンバーの種類のレベルを持つ場合、メンバーしたは、式が指定されていない、既定値が*四半期*型の最初の次元の*時間*メジャー グループ内。  
  
 **Qtd**関数のショートカット関数では、 [PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md)関数に設定されているレベル式引数*四半期*します。 つまり、`Qtd(Member_Expression)` と `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` は機能的に等価です。  
  
## <a name="example"></a>例  
 次の例の合計を返して、`Measures.[Order Quantity]`メンバーを集計した、最初の 2 か月の 2003 年第 3 四半期に含まれている、`Date`ディメンションから、 **Adventure Works**キューブ。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
