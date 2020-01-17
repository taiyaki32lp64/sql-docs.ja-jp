---
title: クエリのサブセレクト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c9fb5d1300b6f50f7ef0a765881896069becf0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073902"
---
# <a name="subselects-in-queries"></a>クエリのサブセレクト
  サブセレクト式とは、入れ子になった SELECT 式です。この式は、外側にある外部の SELECT が評価されているキューブ空間を制限するために使用されます。 サブセレクトにより、すべての計算が評価される新しい空間を定義できます。  
  
## <a name="subselects-by-example"></a>サブセレクトの例  
 表示させたい結果を生成するために、サブセレクトがどのように機能するかを示す例を見てみましょう。 上位 10 製品の数年間の販売動向を示す表を生成するように要求されたとします。  
  
 結果は以下の表のようになります。  
  
|||||  
|-|-|-|-|  
||Sum of Years|Year 1|[...]|  
|Sum of Top 10 Products||||  
|Product A||||  
|[...]||||  
  
 上記のようなことを実行するために、次の MDX 式を記述します。  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 次の結果を返します。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 これは必要としているものに非常に似ていますが、クエリが 10 製品ではなく 9 製品を返した点と、All Products の合計が、返された上位 9 製品ではなくすべての製品の合計を反映している点が異なります (この例の場合)。 この問題を解決するための別の例を、次の MDX クエリに示します。  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 次の結果を返します。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 これは、製品の合計のみが欠落しているので、求める結果に非常に近い形です。 この時点で、欠落している行を追加するように上記の MDX 式に手を加えることができますが、この作業は複雑になる可能性があります。  
  
 この問題を解決するために、MDX 式が評価されるキューブ空間の再定義という観点から別の方法を検討してみましょう。 '新しい' キューブに上位 10 製品のデータのみを含めたら、どうなるでしょうか。 このようなキューブにすると、上位 10 製品のみに適応するすべてのメンバーが含まれるようになり、単純なクエリでニーズを満たすようになります。  
  
 次の MDX 式は、サブセレクト ステートメントを使用して上位 10 製品のキューブ空間を再定義し、目的の結果を生成します。  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 上の式の結果は、次のようになります。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 Black, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Road-350-W Yellow, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 上記の結果は求めているものと一致します。  
  
 サブセレクトによってどのようなことが行われたかを詳細に見てみましょう。 サブセレクトは、製品からのすべてのディメンションをそのまま含む新しいキューブを返しました。ただし、製品ディメンションでは、目的の上位 10 製品に一致するようにすべてのメンバーにフィルターを適用しました。 これは、上位 10 製品という条件に一致しないすべてのデータを削除し、キューブを再構築した場合と同様な状況です。 この例を理解するためも重要なもう一つの概念は、上位 10 製品がキューブ内の他のすべてのディメンションのすべてのメンバーに対して計算されたということです。サブセレクトで他のフィルター制限が課せられなかったため、最初の SELECT は true になります。  
  
 サブセレクトは、必要に応じて複雑にできます。次の例は、上の例と似ていますが、Sales Territory ディメンションで France にフィルターを、および Sales Channel ディメンションで Internet にフィルターを適用した表を生成する方法を示しています。  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 結果は、次のようになります。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 Black, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Road-350-W Yellow, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 上記の結果は、インターネット チャネル経由でフランスで販売された上位 10 製品を示しています。  
  
## <a name="subselect-statement"></a>サブセレクト ステートメント  
 サブセレクトの BNF は次のとおりです。  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 サブセレクトは、外部選択が評価されるキューブ空間に、軸仕様およびスライサー仕様がフィルターを適用する、もう 1 つの Select ステートメントです。  
  
 メンバーが軸またはスライサー句で指定される場合、そのメンバーはその先祖および子孫と共にサブセレクトのサブキューブ空間に取り込まれます。軸句またはスライサー句で指定されていないすべての兄弟メンバーおよびその子孫は、フィルターによってサブ空間から除外されます。 このように、外部選択の空間は、前に説明した先祖および子孫と共に、軸句またはスライサー句の既存のメンバーに制限されています。  
  
 軸またはスライサー句で指定されていないすべてのディメンションのすべてのメンバーは Select の空間に属するため、これらのディメンションのすべてのメンバーのすべての子孫も、サブセレクト空間の一部になります。  
  
 サブキューブ空間のすべてのディメンションのすべてのメンバーは、新しい空間の制限の影響を反映するように再評価されます。  
  
 次の例は、上で説明したことを示したコードです。最初の MDX 式は、キューブ内のフィルターが適用されていない値の表示を支援し、2 番目の MDX 式は、サブセレクト句のフィルターの影響を示します。  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 次の値を返します。  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|米国|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 上記の例では Seattle は Washington の子であり、Portland は Oregon の子であり、Oregon および Washington は United States の子であり、United States は [Customer Geography].[All Customers] の子です。 この例で示したすべてのメンバーには、親の集計値に影響を与える、他の兄弟が存在します。たとえば、Spokane、Tacoma、および Everett は、Seattle の兄弟都市であり、すべて Washington Internet Sales Amount に影響を与えます。 Reseller Sales Amount 値は Customer Geography 属性から独立しています。このため、All 値が結果に表示されます。 次の MDX 式は、サブセレクト句に影響を与えるフィルターを示しています。  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 次の値を返します。  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 上記の結果は、Washington State の先祖および子孫のみが、外側の SELECT ステートメントが評価されたサブ空間の一部であることを示しています。Washington が指定されたのに対し、Oregon およびすべての他の兄弟州はサブセレクトで指定されなかったため、Oregon および Portland はサブキューブから削除されています。  
  
 すべてのメンバーは、Washington のフィルターを反映するように調整されました。[Customer Geography] ディメンションだけではなく、[Customer Geography] の影響を受ける他のすべてのディメンションで調整されました。 [Customer Geography] の影響を受けないすべてのディメンションは、変更されずにそのままサブキューブに残っています。  
  
 次の 2 つの MDX ステートメントは、他のディメンションのすべてのメンバーが、サブセレクトのフィルター適用の影響を受けるように調整される例を示しています。 最初のクエリは変更されない結果を表示し、2 番目のクエリはフィルター適用の影響を示しています。  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|米国|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|米国|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 上記の結果は、All Products 値が、期待どおりに Washington State の値のみに調整されたことを示しています。  
  
 サブセレクトを入れ子にできる深さに制限はありません。ただし、使用可能なメモリの制限は受けます。 最も内側のサブセレクトは、フィルターが適用され次の外側の SELECT に渡される開始サブ空間を定義します。 考慮する必要がある重要な点は、入れ子は相互的な操作でなく、入れ子が設定される順序により、異なる結果が生成される可能性があるということです。 次の例は、入れ子の順序の選択による違いを示しています。  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 結果は、次のようになります。  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Central|Northwest|Southwest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 結果は、次のようになります。  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Northwest|Southwest|イギリス|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 両方のセットの結果には、違いがあることがわかります。 最初のクエリは、上位 5 販売地域の最も販売された製品は何かという質問に対する結果を返し、2 番目のクエリは、上位 5 販売製品が最も販売された場所はどこかという質問に対する結果を返しています。  
  
### <a name="remarks"></a>コメント  
 サブセレクトには、次の制限事項と制約事項があります。  
  
-   WHERE 句はサブ空間に対してフィルターを適用しません。  
  
-   WHERE 句は、サブキューブの既定メンバーのみを変更します。  
  
-   NON EMPTY 句は軸句では使用できません。代わりに [NonEmpty &#40;MDX&#41;](/sql/mdx/nonempty-mdx) 関数式を使用します。  
  
-   HAVING 句は軸句では使用できません。代わりに [Filter &#40;MDX&#41;](/sql/mdx/filter-mdx) 関数式を使用します。  
  
-   既定で、計算されるメンバーはサブセレクト; で許可されませんただし、この制限は、セッション単位で値を割り当てることで、`SubQueries`で接続文字列プロパティ<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>または`DBPROP_MSMD_SUBQUERIES`プロパティ[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties). 参照してください[サブセレクトとサブキューブで計算されるメンバー](calculated-members-in-subselects-and-subcubes.md)の値によって計算されるメンバーの動作の詳細については`SubQueries`または`DBPROP_MSMD_SUBQUERIES`します。  
  
  
