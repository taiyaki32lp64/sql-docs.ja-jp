---
title: IIf (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b7b030776c1c18bb13307bf97db721fe472bd3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105335"
---
# <a name="iif-mdx"></a>IIf (MDX)


  ブール条件が true か false かに応じて、異なる分岐の式を評価します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>引数  
 IIf 関数は、3 つの引数を受け取る: iif (\<条件 >、 \<then 分岐 >、 \<else 分岐 >)。  
  
 *Logical_Expression*  
 評価される条件**true** (1) または**false** (0)。 有効な多次元式 (MDX) の論理式を指定する必要があります。  
  
 *Expression1 ヒント [Eager |厳密な |遅延]*  
 論理式を評価するときに使用**true**します。 Expression1 には、有効な多次元式 (MDX) を指定する必要があります。  
  
 *Expression2 ヒント [Eager |厳密な |遅延]*  
 論理式を評価するときに使用**false**します。 Expression2 には、有効な多次元式 (MDX) を指定する必要があります。  
  
## <a name="remarks"></a>コメント  
 論理式で指定された条件の評価が**false**ときに、この式の値は 0 です。 その他の値を評価する**true**します。  
  
 条件の場合は**true**、 **IIf**関数は、最初の式を返します。 それ以外の場合は、2 番目の式を返します。  
  
 指定した 2 つの式は値または MDX オブジェクトを返すことができます。 また、1 番目と 2 番目の式の型は一致しなくてもかまいません。  
  
 **IIf**関数は、検索条件に基づくメンバーのセットを作成するは推奨されません。 代わりに、使用、[フィルター](../mdx/filter-mdx.md)を論理式に対して指定されたセット内の各メンバーを評価し、メンバーのサブセットを返す関数。  
  
> [!NOTE]  
>  いずれかの式が NULL と評価される場合、その条件が満たされる場合は結果セットが NULL になります。  
  
 Hint はオプションの修飾子で、式をいつどのように評価するかを指定します。 これを使用すると、式の評価方法を指定することにより、既定のクエリ プランをオーバーライドすることができます。  
  
-   EAGER を指定すると、式は元の IIF サブ空間で評価されます。  
  
-   STRICT を指定すると、論理条件式によって作成された制限付きのサブ空間のみで式が評価されます。  
  
-   LAZY を指定すると、式はセル単位で評価されます。  
  
 EAGER と STRICT は IIF の then-else 分岐のみに適用され、LAZY はすべての MDX 式に適用されます。 MDX 式の後には、セル単位でその式を評価する HINT LAZY を指定できます。  
  
 ヒントで EAGER と STRICT を同時に使用することはできません。同じ IIF(,,) の別の式で使用することはできます。  
  
 詳細については、次を参照してください。 [IIF 関数のクエリ ヒントでは、SQL Server Analysis Services 2008](https://go.microsoft.com/fwlink/?LinkId=269540)と[実行プランおよび MDX の IIF 関数と CASE ステートメントのプラン ヒント](https://go.microsoft.com/fwlink/?LinkId=269565)します。  
  
## <a name="examples"></a>使用例  
 次のクエリの簡単な使用を示しています。 **IIF** Internet Sales Amount メジャーが大きい場合は、2 つの異なる文字列値または $10000 未満のいずれかを返す計算されるメジャー内で。  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF の一般的な使用方法では、次の例に示すように、計算されるメンバー内で "0 除算" エラーを処理します。  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 次の例に示します**IIF**行に複雑な組のセットを作成する、Generate 関数内の 2 つのセットの 1 つを返します。  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 最後に、この例では、プラン ヒントを使用する方法を示します。  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
