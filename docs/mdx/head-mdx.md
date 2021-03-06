---
title: Head (MDX) |Microsoft ドキュメント
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 05cfcb3c23a0369f010b8440d4a27e94ffacdb21
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740481"
---
# <a name="head-mdx"></a>Head (MDX)


  セットの先頭から、指定された数の要素を返します (重複要素も保持します)。  
  
## <a name="syntax"></a>構文  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *カウント*  
 返す組の数を指定する有効な数値式です。  
  
## <a name="remarks"></a>コメント  
 **ヘッド**関数は、指定されたセットの先頭から指定数の組を返します。 要素の順序は保持されます。 Count の既定値は 1 です。 指定した数の組が 1 より小さい場合、**ヘッド**関数は、空のセットを返します。 指定された組数がセット内の組数を超える場合は、元のセットを返します。  
  
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
  
## <a name="see-also"></a>参照  
 [末尾&#40;MDX&#41;](../mdx/tail-mdx.md)   
 [項目&#40;組&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [項目&#40;メンバー&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [ランク&#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX 関数リファレンス&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
