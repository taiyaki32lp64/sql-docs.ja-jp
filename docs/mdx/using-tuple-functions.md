---
title: タプル関数の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a329c8786ce580469e4601709509ca8a2de73f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037980"
---
# <a name="using-tuple-functions"></a>タプル関数の使用


  タプル関数は、セットからタプルを取得します。 または、タプルの文字列表記を解決することでタプルを取得します。  
  
 タプル関数は、メンバー関数や集合関数と同様に、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で使用される多次元構造を操作するために不可欠です。  
  
 MDX では、次の 3 つのタプル関数がある[Current&#40;MDX&#41;](../mdx/current-mdx.md)、[Item&#40;タプル&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)と[StrToTuple &#40;MDX&#41;](../mdx/strtotuple-mdx.md). 次のクエリは、それぞれの使用方法を示しています。  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of Years and Countries`  
  
 `SET MyTuples AS  [Date].[Calendar Year].[Calendar Year].MEMBERS * [Customer].[Country].[Country].MEMBERS`  
  
 `//Returns a string representation of that set using the Current and Generate functions`  
  
 `MEMBER MEASURES.CURRENTDEMO AS GENERATE(MyTuples, TUPLETOSTR(MyTuples.CURRENT), ", ")`  
  
 `//Retrieves the fourth tuple from that set and displays it as a string`  
  
 `MEMBER MEASURES.ITEMDEMO AS TUPLETOSTR(MyTuples.ITEM(3))`  
  
 `//Creates a tuple consisting of the measure Internet Sales Amount and the country Australia from a string`  
  
 `MEMBER MEASURES.STRTOTUPLEDEMO AS STRTOTUPLE("([Measures].[Internet Sales Amount]" + ", [Customer].[Country].&[Australia])")`  
  
 `SELECT{MEASURES.CURRENTDEMO,MEASURES.ITEMDEMO,MEASURES.STRTOTUPLEDEMO} ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [Functions&#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)   
 [メンバー関数の使用](../mdx/using-member-functions.md)   
 [集合関数の使用](../mdx/using-set-functions.md)  
  
  
