---
title: TopPercent (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8c92a4b6a76cb9d15048d6f058038363970cb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036593"
---
# <a name="toppercent-mdx"></a>TopPercent (MDX)


  セットを降順で並べ替えし、を指定した割合以上になる最も高い値と組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *[パーセント]*  
 返される組の割合を指定する有効な数値式です。  
  
> [!IMPORTANT]  
>  *割合*正の値を指定する必要がある負の値がエラーを生成します。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **TopPercent**関数セットを降順に並べ替え、指定されたセットに対して評価される指定数値式の合計を計算します。 次に、合計値の累積割合が指定されている割合以上になるように、最も値の大きい方から要素を返します。 この関数は、累積合計が、指定したパーセンテージでは、少なくともセットの最小サブセットを返します。 要素は大きい方から順に返されます。  
  
> [!WARNING]  
>  場合*Numeric_Expression*し、負の値を返します**TopPercent**のみ (1 つの行を返します。  
>   
>  この動作の詳細なプレゼンテーションの 2 番目の例を参照してください。  
  
> [!IMPORTANT]  
>  ように、 [BottomPercent](../mdx/bottompercent-mdx.md)関数の場合、 **TopPercent**関数は常に、階層を解除します。  
  
## <a name="example"></a>例  
 次の例では、Bike カテゴリについて、再販業者の売上の上位 10% を支援する最適な都市を返します。 結果は降順に並べ替え、売上の最高値を持つ都市が先頭に並べ替えられます。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 上記の式では、次の結果を生成します。  
  
||Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|3,508,904.84 ドル|  
|London|1,521,530.09 ドル|  
|Seattle|1,209,418.16 ドル|  
|Paris|1,170,425.18 ドル|  
  
 元のデータのセットは、次のクエリで取得でき、588 行を返します。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
## <a name="example"></a>例  
 次のチュートリアルが負の値での影響を理解できますが、 *Numeric_Expression*します。 まず、この動作を実行できる、いくつかのコンテキストを構築します。  
  
 次のクエリでは、再販業者 'Sales Amount'、'Total Product Cost' および' Gross Profit'、利益の順序を降順でのテーブルを返します。 利益には負の値しかないので、損失の少ないものが上位に表示されます。  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 上記のクエリは、次の結果を返します。見やすくするために、中間部の行は削除してあります。  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring 2000 青、50|157,444.56 ドル|163,112.57 ドル|(5,668.01 $)|  
|Touring 2000 青、46|321,027.03 ドル|333,021.50 ドル|(11,994.47 $)|  
|Touring-3000 Blue, 62|87,773.61 ドル|100,133.52 ドル|(12,359.91 $)|  
|[...]|...|...|[...]|  
|Touring 1000 の黄色の場合、46|1,016,312.83 ドル|1,234,454.27 ドル|(218,141.44 $)|  
|Touring-1000 Yellow, 60|1,184,363.30 ドル|1,443,407.51 ドル|(259,044.21 $)|  
  
 このとき、利益で上位 100% の自転車を提示するように求められた場合、クエリは次のように記述されます。  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 クエリ要求 100% (100%;) のすべての行を返す必要があることを意味することに注意してください。 ただし、負の値であるため、 *Numeric_Expression* 、1 行のみが返されます。  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring 2000 青、50|157,444.56 ドル|163,112.57 ドル|(5,668.01 $)|  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
