---
title: Rank (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1081cacd0676f4eb0512780e9ddc7641edb99ca1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037069"
---
# <a name="rank-mdx"></a>Rank (MDX)


  指定されたセット内の指定された組のランクを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、**Rank**関数が、組に対して指定された数値式を評価することによって、指定された組のランクを決定します。 数値式が指定されている場合、**Rank**関数は、セットに重複する値のタプルに同じランクを割り当てます。 このように重複する値に同じランクを割り当てる動作は、セット内の後続の組のランクに影響を与えます。 セットを次の組を構成、`{(a,b), (e,f), (c,d)}`します。 タプル`(a,b)`組と同じ値を持つ`(c,d)`します。 場合、組`(a,b)`1 の場合は、両方のランクを持つ`(a,b)`と`(c,d)`のランクは 1 になります。 ただし、`(e,f)` のランクは 3 になります。 ランクが 2 の組はこのセットには存在できません。  
  
 数値式が指定されていない場合、**Rank**関数は、指定された組の 1 から始まる序数位置を返します。  
  
 **Rank**関数には、セットが順序付けしません。  
  
## <a name="example"></a>例  
 次の例を使用して、顧客と購入日を含む組のセットを返します、**フィルター**、 **NonEmpty**、**項目**、および**ランク**各顧客が購入を行う最後の日付を検索する関数。  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、**Order**関数ではなく、**ランク**City 階層のメンバーにランクの関数は、Reseller Sales Amount メジャーに基づいており、ランクの順序で表示されます。 使用して、**順序**City 階層のメンバーのセットを関数の最初の注文を 1 回だけ実行し、並べ替えた順で表示される前に後で線形スキャンには、並べ替え。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [Order &#40;MDX&#41;](../mdx/order-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
