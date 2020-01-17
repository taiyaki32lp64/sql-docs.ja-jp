---
title: フィルター (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132693"
---
# <a name="filter-mdx"></a>Filter (MDX)


  検索条件に基づいて、指定されたセットをフィルター処理の結果セットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Logical_Expression*  
 true または false に評価される有効な多次元式 (MDX) 論理式です。  
  
## <a name="remarks"></a>コメント  
 **フィルター**関数は、指定されたセット内の各組に対して指定された論理式を評価します。 論理式の評価が指定されたセット内の各組で構成されるセットを返します**true**します。 評価される組がない場合**true**空のセットが返されます。  
  
 **フィルター**関数の動作のような方法で、 [IIf](../mdx/iif-mdx.md)関数。 **IIf**関数は、2 つのオプションのいずれかのみを返します MDX 論理式の評価に基づき、while、**フィルター**関数を指定した検索条件を満たす組のセットを返します。 実際には、**フィルター**関数が実行される`IIf(Logical_Expression, Set_Expression.Current, NULL)`セット、および返します内の組ごとに、その結果セットします。  
  
## <a name="examples"></a>使用例  
 次の例は、Internet Sales Amount が $10000 より大きい日付だけを返すクエリの Rows 軸で、フィルター関数の使用を示しています。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 フィルター関数は、計算されるメンバーの定義内でも使用できます。 次の例の合計を返して、`Measures.[Order Quantity]`メンバーに含まれている 2003年の最初の 9 か月にわたり、`Date`ディメンションから、 **Adventure Works**キューブ。 **PeriodsToDate**関数セット内の組を定義する、**集計**関数は動作します。 **フィルター**関数は、前の期間の Reseller Sales Amount メジャーの値が小さいものに返される組を限定します。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
