---
title: Current (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 821d517419b90df44b7943a1e0edde12ef667b6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047124"
---
# <a name="current-mdx"></a>Current (MDX)


  イテレーション中に、セットから現在の組を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 反復処理中に各ステップでは、操作対象の組は、Currentの組が。 **Current**関数は、その組を返します。 この関数はのみ有効な反復処理中に、セットに対して。  
  
 セットを反復処理する MDX 関数には、[Generate](../mdx/generate-mdx.md) 関数があります。  
  
> [!NOTE]  
>  この関数は、セットの別名を使用するか名前付きセットを定義することによって名前が付けられたセットに対してのみ使用できます。  
  
## <a name="examples"></a>使用例  
 次の例は、**Generate** 内で **Current** 関数を使用する方法を示します: 

  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
