---
title: Hierarchize (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8ab2c866f201c53684c316282a143b4f672cb8e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105435"
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)


  階層内の一連のメンバーを並べ替えます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 **Hierarchize**関数は階層の順序に指定されたセットのメンバーを編成します。 この関数は、常に重複部分を保持します。  
  
-   場合**POST**が指定されていない、関数は、自然な順序でレベル内のメンバーを並べ替えます。 自然な順序は、既定の並べ替え条件が指定されていない場合、階層に沿ったメンバーの順序付けします。 子メンバーは親メンバーの直後になります。  
  
-   場合**POST**が指定されている、 **Hierarchize**関数は、後の自然な順序を使用して、レベル内のメンバーを並べ替えます。 つまり、子メンバーには、その親が前になります。  
  
## <a name="example"></a>例  
 Canada メンバーを次の例ドリルします。 **Hierarchize**関数を使用して、必要な階層の順序で指定されたセット メンバーを整理、 **DrillUpMember**関数。  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 次の例の合計を返して、`Measures.[Order Quantity]`メンバーに含まれている 2003年の最初の 9 か月にわたり、`Date`ディメンションから、 **Adventure Works**キューブ。 **PeriodsToDate**関数、集計関数が動作するセット内の組を定義します。 **Hierarchize**関数は、階層の順序で、Product ディメンションのメンバーの指定されたセットのメンバーを編成します。  
  
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
  
  
