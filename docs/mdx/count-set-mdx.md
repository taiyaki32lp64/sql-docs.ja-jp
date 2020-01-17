---
title: Count (セット) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047296"
---
# <a name="count-set-mdx"></a>Count (セット) (MDX)


  セット内のセルの数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 **Count (セット)** 関数を追加または使用する構文に応じて、空白のセルを除外します。 空のセルの除外またはを使用して、標準の構文を使用する場合、 **EXCLUDEEMPTY**または**INCLUDEEMPTY**フラグ、それぞれします。 代替構文を使用する場合、関数には常に空のセルが含まれます。  
  
 セットの数の空のセルを除外する、標準の構文とオプションを使用して、 **EXCLUDEEMPTY**フラグ。  
  
> [!NOTE]  
>  **Count (セット)** 関数は、既定では空のセルをカウントします。 これに対し、**カウント**関数セットをカウントする OLE DB では、既定で空白セルを除外します。  
  
## <a name="examples"></a>使用例  
 次の例では、Product ディメンションの Model Name 属性階層の子で構成されるメンバーのセット内のセルの数をカウントします。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、Product ディメンションに製品の数をカウントを使用して、 **DrilldownLevel**関数と組み合わせて、**カウント**関数。  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 次の例でを使用して、前のカレンダー四半期と比べて売上が減少した再販業者を返して、**カウント**関数と組み合わせて、**フィルター**関数とその他の数関数。 このクエリを使用して、**集計**クライアント アプリケーションでドロップダウン リストから選択のための複数の地域のメンバーの選択をサポートする関数。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>関連項目  
 [カウント&#40;ディメンション&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [カウント&#40;階層レベル&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [カウント&#40;タプル&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Aggregate (MDX)](../mdx/aggregate-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
