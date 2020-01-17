---
title: CurrentOrdinal (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 38ac7a3f4c966f9496f5ff9a0855960da8a38fb6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135881"
---
# <a name="currentordinal-mdx"></a>CurrentOrdinal (MDX)


  イテレーション中に、セット内の現在のイテレーション数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set_Expression.CurrentOrdinal  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 使用し、セットなど、反復処理するとき、 [Filter (MDX)](../mdx/filter-mdx.md)または[Generate (MDX)](../mdx/generate-mdx.md)関数の場合、 **CurrentOrdinal**関数のイテレーション数を返します。  
  
## <a name="examples"></a>使用例  
 単純な例を次に示す方法**CurrentOrdinal**で使用できる**生成**セット内の位置と、セット内の各項目の名前を含む文字列を返します。  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 CurrentOrdinal の実際の使用は、非常に複雑な計算に制限されます。 次の例では、製品の数を返しますを使用して、一意のセットで、**順序**関数を使用する前に、空の組を順序付け、**フィルター**関数。 **CurrentOrdinal**を比較し、関係を排除する関数を使用します。  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , NOT((OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          ))  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
