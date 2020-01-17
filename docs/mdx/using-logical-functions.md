---
title: 論理関数の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 723d481bc858d7d1db4a63cbb32ab5614eddbb55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097166"
---
# <a name="using-logical-functions"></a>論理関数の使用


  論理関数は、オブジェクトよぶ式に対して論理演算または比較を実行し、ブール値を返します。 論理関数は、essential の多次元式 (MDX) メンバーの位置を決定します。  
  
 最もよく使用される論理関数は、 **IsEmpty**関数。 使用方法の詳細については、 **IsEmpty**関数を参照してください[空の値を操作](../mdx/working-with-empty-values.md)します。  
  
 次のクエリを使用する方法を示しています、 **IsLeaf**と**IsAncestor**関数。  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [関数&#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)  
  
  
