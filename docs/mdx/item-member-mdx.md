---
title: Item (メンバー) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d7afa88f9d6239c8da7cb9c406ef11f0764f8dcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905908"
---
# <a name="item-member-mdx"></a>Item (メンバー) (MDX)


  指定されたタプルからメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Expression*  
 タプルを返す有効な多次元式 (MDX) 式です。  
  
 *Index*  
 返されるタプル内の位置によって、特定のメンバーを指定する有効な数値式です。  
  
## <a name="remarks"></a>コメント  
 **Item**関数が、指定されたタプルからメンバーを返します。 指定した 0 から始まる位置にあるメンバーを返します*インデックス*します。  
  
## <a name="example"></a>例  
 次の例では、列の `[2003]` タプルに含まれる最初のアイテムである `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` メンバーを返します。  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
