---
title: Intersect (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f253dad526c509edff5c837b61ae2faae07d5758
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105364"
---
# <a name="intersect-mdx"></a>Intersect (MDX)


  必要に応じて重複部分を保持、2 つの入力セットの積集合を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 **Intersect**関数は、2 つのセットの積集合を返します。 既定では、関数は、積集合の両方のセットから重複を削除します。 指定された 2 つのセットの次元は同一である必要があります。  
  
 省略可能な**すべて**フラグは、重複部分を保持します。 場合**すべて**が指定されている、 **Intersect**関数は、通常どおり、積の要素と交差しているし、2 番目のセットに一致する重複している最初のセット内の重複は各交差しています。 指定された 2 つのセットの次元は同一である必要があります。  
  
## <a name="example"></a>例  
 次のクエリは 2003 年と 2004 年を返します。2 つのメンバーは指定された両方のセットに示されます。  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 次のクエリでは、指定された 2 つのセットには、異なる階層のメンバーが含まれているために失敗します。  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
