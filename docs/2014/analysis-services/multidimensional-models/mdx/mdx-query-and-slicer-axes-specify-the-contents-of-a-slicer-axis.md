---
title: スライサー軸 (MDX) の内容の指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slicer axis
- filtering data [MDX]
ms.assetid: c56b0a70-cdec-427f-990e-425290344e7d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12e2d2f543694a1da418f5e8eb4b900eaa123d97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074058"
---
# <a name="specifying-the-contents-of-a-slicer-axis-mdx"></a>スライサー軸の内容の指定 (MDX)
  スライサー軸は、多次元式 (MDX) の SELECT ステートメントから返されるデータを絞り込み、指定されているメンバーと重なり合うデータだけが返されるように、返されるデータを制限します。 クエリ内の見えない追加の軸であると考えることができます。 スライサー軸は、MDX の SELECT ステートメントの WHERE 句で定義します。  
  
## <a name="slicer-axis-syntax"></a>スライサー軸の構文  
 スライサー軸を明示的に指定するには、MDX の `<SELECT slicer axis clause>` を使用します。その際の構文は以下のとおりです。  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 このスライサー軸の構文で使用する `Set_Expression` には、その句を評価するためのセットとして処理される組式、またはセット式を指定できます。 セット式を指定した場合は、指定したセットが評価され、そのセット内のすべての組の結果セルが集計されます。 つまり、指定したセットに対して [Aggregate](/sql/mdx/aggregate-mdx) 関数が適用され、メジャーごとに定義されている集計関数によって各メジャーが集計されます。 また、セット式を属性階層メンバーのクロス積として表せない場合は、スライサーのセット式の外部にあるセルを NULL と見なして評価されます。  
  
> [!IMPORTANT]  
>  SQL の WHERE 句とは異なり、MDX SELECT ステートメントの WHERE 句は、クエリの ROWS 軸で返される対象を直接フィルター選択することはありません。 クエリの ROWS 軸または COLUMNS 軸に表示される対象をフィルター選択するには、たとえば FILTER、NONEMPTY、TOPCOUNT などの、さまざまな MDX 関数を使用します。  
  
### <a name="implicit-slicer-axis"></a>暗黙的なスライサー軸  
 キューブ内の階層のメンバーがクエリ軸に明示的に含まれていない場合は、その階層の既定のメンバーが暗黙的にスライサー軸に含まれます。 詳細については、「 [既定メンバーの定義](../attribute-properties-define-a-default-member.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次のクエリは、WHERE 句を含んでおらず、すべての年の Internet Sales Amount メジャーの値を返します。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 これに、WHERE 句を次のように追加します。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 クエリの行と列に返される対象は変わりませんが、各セルに返される値は変わります。 この例では、クエリがスライスされて、すべての年の、米国に住む顧客だけに関する Internet Sales Amount の値を返すようになります。WHERE 句には、異なる階層の複数のメンバーを追加できます。 次のクエリは、すべての年の、カテゴリ Bikes の製品を購入した、米国に住む顧客に関する Internet Sales Amount の値を表示します。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 同じ階層の複数のメンバーを使用する場合は、WHERE 句にセットを含める必要があります。 たとえば、次のクエリは、すべての年の、カテゴリ Bikes の製品を購入した、米国およびイギリスに住む顧客に関する Internet Sales Amount の値を表示します。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 上で説明したように、WHERE 句でセットを使用すると、セット内のすべてのメンバーに関する値が暗黙的に集計されます。 この例の場合、クエリは各セルに米国とイギリスの集計値を表示します。  
  
  
