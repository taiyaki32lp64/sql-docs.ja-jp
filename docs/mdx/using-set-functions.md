---
title: 集合関数の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 52e0c140acb944a774f5ab167bb81c662e3e32d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038054"
---
# <a name="using-set-functions"></a>集合関数の使用


  集合関数は、ディメンション、階層、レベルからセットを取得します。あるいは、それらのオブジェクト内でのメンバーの絶対位置および相対位置をトラバースすることにより、さまざまな方法でセットを構築します。  
  
 メンバー関数や組関数と同様、集合関数は、Analysis Services の多次元構造を操作するために不可欠です。 集合関数は、多次元式 (MDX) クエリから結果を取得するセット式の MDX クエリ軸を定義するために不可欠なもします。  
  
 最も一般的な集合関数の 1 つは、[Member&#40;セット&#41; &#40;MDX&#41; ](../mdx/members-set-mdx.md)関数で、すべてのディメンション、階層、またはレベルからメンバーを含むセットを取得します。 クエリ内でのこの関数の使用例を次に示します。  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 一般的に使用されるもう 1 つの関数は、 [Crossjoin &#40;MDX&#41; ](../mdx/crossjoin-mdx.md)関数。 この関数は、パラメーターとして渡されるセットのデカルト積を表す組のセットを返します。 実際には、この関数には、クエリで"クロス集計された"軸または '入れ子になった' を作成することが有効にします。  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 [Descendants&#40;MDX&#41; ](../mdx/descendants-mdx.md)関数は似ています、**Child**機能しますより強力です。 階層の 1 つまたは複数のレベルで任意のメンバーの子孫を返します。  
  
 SELECT  
  
 [Measures] です。[Internet Sales Amount]  
  
 ON Columns,  
  
 //Returns a set containing all of the Dates beneath Calendar Year  
  
 Date ディメンションの Calendar 階層に 2004  
  
 子孫 (  
  
 [Date] です。[カレンダー] です。[Calendar Year] です & [2004]。  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 [Adventure Works] から  
  
 [Order&#40;MDX&#41; ](../mdx/order-mdx.md)関数では、昇順または降順の特定の数値式に従って順序でセットの内容を注文することができます。 次のクエリでは、行の前のクエリと同じメンバーを返しますが、Internet Sales Amount メジャーに整列ようになりました。  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 このクエリも 1 つからセットを返す方法を示しています、集合関数 Descendants は、別の集合関数 Order にパラメーターとして渡すことができます。  
  
 特定の条件に従ってセットをフィルター選択非常に便利です、クエリを記述する場合は、この目的で使用することができます、[Filter ー &#40;MDX&#41; ](../mdx/filter-mdx.md)関数は、次の例で示すようにします。  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 また、他の方法でセットにフィルターを適用できるようにする、さらに高度な関数もあります。 たとえば、次のクエリの表示、 [TopCount &#40;MDX&#41; ](../mdx/topcount-mdx.md)関数がセット内の最初の n 個の項目を返します。  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 最後に、多数のなどの関数を使用して論理セットの操作を実行することは[Intersect &#40;MDX&#41;](../mdx/intersect-mdx.md)、[Union&#40;MDX&#41; ](../mdx/union-mdx.md)と[Except&#40;MDX&#41; ](../mdx/except-mdx-function.md)関数。 次のクエリでは、後者の 2 つの関数の例を示します。  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [Functions&#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)   
 [メンバー関数の使用](../mdx/using-member-functions.md)   
 [組関数の使用](../mdx/using-tuple-functions.md)  
  
  
