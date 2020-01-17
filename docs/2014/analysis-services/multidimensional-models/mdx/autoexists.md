---
title: Autoexists |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 56283497-624c-45b5-8a0d-036b0e331d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc9aa519d37b040026414ab826373357a1ddd92f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074727"
---
# <a name="autoexists"></a>Autoexists
  *autoexists* の概念を導入すると、このキューブ空間を、同じ階層から属性階層メンバーの可能なすべての組み合わせを作成した結果として存在するセルでなく、実際に存在するセルのみに限定できます。 これは、1 つの属性階層のメンバーは、同じディメンション内の別の属性階層のメンバーと共存できないためです。 SELECT ステートメントに同じディメンションの属性階層を複数使用した場合、こうした属性のメンバーは、Analysis Services が属性の式を評価する際、それ以外のすべての属性の条件を満たすよう、適切に絞り込まれます。  
  
 たとえば、Geography ディメンションの属性を指定したとします。 一方の式で City 属性のすべてのメンバーを返し、もう一方の式で Country 属性のメンバーを欧州内の国のみに限定した場合、結果として得られる City メンバーは、欧州の国に属する市区町村に限定されます。 これは、Analysis Services が備えている Autoexists という特性のためです。 Autoexists が同じディメンションの属性にのみ適用されるのは、一方の属性式で排除されたディメンション レコードが、もう一方の属性式で含められるのを防ぐように機能するためです。 ディメンション行に複数の属性式を適用した結果の共通集合と考えることもできます。  
  
## <a name="cell-existence"></a>セルの存在  
 次のセルは常に存在します。  
  
-   同じディメンション内の他の階層のメンバーの影響を受ける場合、各階層の (All) メンバー  
  
-   計算されない兄弟または計算されない兄弟の親または子孫の影響を受ける場合、計算されるメンバー  
  
## <a name="providing-non-existing-cells"></a>存在しないセルの指定  
 存在しないセルは、キューブ内に存在しないセルを要求するクエリまたは計算に対する応答としてシステムによって提供されるセルです。 たとえば、Geography ディメンションに属する City 属性階層と Country 属性階層、および Internet Sales Amount メジャーが含まれたキューブがあるとします。このキューブの空間には、共存できるメンバーのみが含まれます。 City 属性階層に都市 New York、London、Paris、Tokyo、Melbourne があり、Country 属性階層に国 United States、United Kingdom、France、Japan、Australia があるとすると、このキューブ空間に Paris と United States が交差する領域 (セル) は含まれません。  
  
 存在しないセルに対するクエリを実行すると、NULL が返されます。つまり、存在しないセルには計算を含めることができないので、この領域に書き込みを行う計算は定義できません。 たとえば、次のステートメントには、存在しないセルが含まれています。  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  このクエリでは、 [Members (セット) (MDX)](/sql/mdx/members-set-mdx) 関数を使用して列軸の Gender 属性階層のメンバーのセットを取得し、それを行軸の Customer 属性階層のメンバーの限定的なセットと交差させています。  
  
 上記のクエリを実行すると、Aaron A. Allen と Female が交差するセルに NULL が表示されます。 同様に、Abigail Clark と Male が交差するセルに NULL が表示されます。 これらのセルは存在しないため値を含めることができませんが、クエリから返される結果には、存在しないセルが表示される場合があります。  
  
 [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) 関数を使用して同一ディメンションの異なる属性階層に属するメンバーのクロス積を取得した場合、取得される組は完全なデカルト積ではなく、autoexist によって実際に存在する組のセットのみに限定されます。 たとえば、次のクエリを実行し、実行結果を確認します。  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  このクエリでは、列軸を表す axis(0) の略記である 0 を使用して、列軸を指定しています。  
  
 上のクエリを実行すると、クエリ内の各属性階層から、共存できるメンバーのセルのみが返されます。 前のクエリは、新しいを使用して書き込むこともできます * のバリアント、 [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx)関数。  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 上のクエリは、次のように記述することもできます。  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 結果セットのメタデータが異なりますが、返されるセルの値は同一です。 たとえば上のクエリで、Country 階層は (WHERE 句の) スライサー軸に移動されたので、結果セットに明示的には出現しません。  
  
 これら 3 つのクエリはいずれも、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の autoexist の効果を示しています。  
  
## <a name="deep-and-shallow-autoexists"></a>Deep および Shallow Autoexists  
 Autoexists は、式に対して深く (deep) または浅く (shallow) 適用できます。 `Deep Autoexists` では、スライサーの式、軸の下位選択式などを適用した後、可能な限り深い場所に到達するように、すべての式が評価されます。 `Shallow Autoexists` では、現在の式より前に外部の式が評価され、その結果が現在の式に渡されます。 既定の設定は deep autoexists です。  
  
 以下のシナリオとサンプルでは、さまざまな種類の Autoexists について説明します。 この例では 2 つのセットを 1 つは計算式として、もう 1 つは定数式として作成します。  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 取得される結果セットは次のとおりです。  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring 1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 取得された製品のセットは、Preferred10Products と同じであるように見えます。そこで、Preferred10Products のセットを検証してみることにします。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 次の結果から、両方のセット (Top10SellingProducts と Preferred10Products) が同一であることがわかります。  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring 1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 次の例が示しているのは、deep Autoexists の概念です。 この例では、[Mountain] グループの製品について、[Product].[Product Line] 属性で Top10SellingProducts をフィルター処理します。 どちらの属性 (スライサーおよび軸) も同じディメンション ([Product]) に属している点に注意してください。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 結果セットは、次のようになります。  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0.05%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1.62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0.05%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0.05%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0.04%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0.05%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2.56%**|  
  
 この結果セットを見ると、Top10SellingProducts のリストに、新しい製品が 7 つ出現していることがわかります。また、Mountain-200、Mountain-100、および HL Mountain Frame がリストの上位に移動しています。 その前の結果セットでは、この 3 つの値がばらばらに存在していました。  
  
 クエリのスライス条件を満たすように Top10SellingProducts のセットが評価されていることから、これを deep Autoexists といいます。 deep Autoexists では、スライサーの式、軸の下位選択式などを適用した後、可能な限り深い場所に到達するように、すべての式が評価されます。  
  
 ただし、場合によっては、次の例のように、Top10SellingProducts に対して、Preferred10Products と同等の分析を行うことができれば便利です。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 結果セットは、次のようになります。  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 上の結果では、スライスによって、Preferred10Products から、[Product].[Product Line] の [Mountain] グループに属する製品だけを含む結果が得られます。Preferred10Products は定数式であるため、これは当然の結果と言えます。  
  
 この結果セットは、Shallow Autoexists と考えることもできます。 式がスライス句よりも前に評価されるためです。 前の例では、概念をわかりやすく説明するために、定数式を使用しました。  
  
 Autoexists の動作は、`Autoexists` 接続文字列プロパティを使用することにより、セッション レベルで変更できます。 次の例は、まず、新しいセッションを開いてを追加する、 *Autoexists=3* プロパティを接続文字列にします。 この例を実行するには、新しい接続を開く必要があります。 いったん Autoexist 設定で確立された接続は、その接続が解除されるまで有効です。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 次の結果セットは、shallow Autoexists の動作を示しています。  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 Autoexists の動作は、AUTOEXISTS を使用して変更できます = [1 | 2 | 3] パラメーター、接続文字列。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)と<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>パラメーターの使用法。  
  
## <a name="see-also"></a>参照  
 [MDX の主な概念 (Analysis Services)](../key-concepts-in-mdx-analysis-services.md)   
 [キューブ空間](cube-space.md)   
 [組](tuples.md)   
 [メンバー、組、およびセットの操作 (MDX)](working-with-members-tuples-and-sets-mdx.md)   
 [表示部分の合計と非表示部分の合計](visual-totals-and-non-visual-totals.md)   
 [MDX 言語リファレンス &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [多次元式 &#40;MDX&#41; リファレンス](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
