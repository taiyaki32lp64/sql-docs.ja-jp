---
title: Head (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906009"
---
# <a name="head-mdx"></a>Head (MDX)


  重複部分を保持しながら、セット内の最初の指定数の要素を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
## <a name="remarks"></a>コメント  
 **ヘッド**関数は、指定されたセットの先頭から指定数の組を返します。 要素の順序は保持されます。 Count の既定値は 1 です。 指定数の組が 1 未満の場合、**ヘッド**関数は空のセットを返します。 指定された組数がセット内の組数を超える場合は、元のセットを返します。  
  
## <a name="example"></a>例  
 次の例では、階層とは無関係に、Reseller Gross Profit に基づいて、売上が上位 5 番目までの製品のサブカテゴリを返します。 **ヘッド**関数を使用してを使用して結果を並べ替えてから、結果の最初の 5 つのセットのみを返す、**順序**関数。  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [末尾&#40;MDX&#41;](../mdx/tail-mdx.md)   
 [項目&#40;タプル&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [項目&#40;メンバー&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [ランク&#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
