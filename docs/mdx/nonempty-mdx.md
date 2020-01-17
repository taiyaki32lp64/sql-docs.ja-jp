---
title: NonEmpty (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45daf970f69322cad36bbe5419bf1dc8cc8009b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088341"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  指定されたセットと 2 番目のセットのクロス積に基づいて、指定されたセットから空ではない組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>引数  
 *set_expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *set_expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 この関数は、2 番目のセット内の組に対して評価するときに空でないのは最初の指定されたセット内の組を返します。 **NonEmpty**計算を関数を受け取り、重複する組を保持します。 2 番目のセットが指定されていない場合、式は、キューブ内のメジャー、属性階層のメンバーの現在の座標のコンテキストで評価されます。  
  
> [!NOTE]  
>  非推奨ではなくこの関数を使用して、 [NonEmptyCrossjoin &#40;MDX&#41; ](../mdx/nonemptycrossjoin-mdx.md)関数。  
  
> [!IMPORTANT]  
>  空以外では、組、組自体から参照されるセルの特性です。  
  
## <a name="examples"></a>使用例  
 次のクエリは、簡単な例を示しています。 **NonEmpty**、年 7 月 1 日の 2001 年に Internet Sales Amount の null 以外の値を持っているすべての顧客を返します。  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 次の例は、顧客とを使用して、購入日を含む組のセットを返します、**フィルター**関数と**空でない**各顧客が購入を行う最後の日付を検索する関数。  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
