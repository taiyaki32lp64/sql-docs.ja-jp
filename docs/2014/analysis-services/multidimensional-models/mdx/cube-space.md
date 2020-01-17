---
title: キューブ空間 |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c3a012b4-9ca0-4fb8-9c26-5ecc0e2e2b2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b663f86b16576360083050c5709433eed7d4dc4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074710"
---
# <a name="cube-space"></a>キューブ空間
  キューブ空間は、そのキューブのメジャーを伴った、キューブの属性階層のメンバーから構成されます。 したがって、キューブ空間はキューブ内のすべての属性階層のメンバーとキューブのメジャーの組み合わせによって決まり、キューブの最大サイズを定義します。 重要なのは、この空間には属性階層メンバーで考えられるすべての組み合わせが含まれるということです。現実世界において不可能と考えられるような組み合わせ (たとえば、都市を Paris、国を England、Spain、Japan、India などに指定する) も含まれます。  
  
## <a name="autoexists-and-cube-space"></a>Autoexists とキューブ空間  
 *autoexists* の概念を導入すると、このキューブ空間を、実際に存在するセルのみに限定できます。 あるディメンション内の属性階層のメンバーは、同じディメンション内の別の属性階層のメンバーと共存できない場合があります。  
  
 たとえば、City 属性階層、Country 属性階層、および Internet Sales Amount メジャーが含まれたキューブがあるとします。このキューブの空間には、共存できるメンバーのみが含まれます。 City 属性階層に都市 New York、London、Paris、Tokyo、Melbourne があり、Country 属性階層に国 United States、United Kingdom、France、Japan、Australia があるとすると、このキューブ空間に Paris と United States が交差する領域 (セル) は含まれません。  
  
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
  
 上のクエリを実行すると、クエリ内の各属性階層から、共存できるメンバーのセルのみが返されます。 前のクエリは、新しいを使用して書き込むこともできます * のバリアント、 [ \* (クロス積) (MDX)](/sql/mdx/crossjoin-mdx)関数。  
  
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
  
## <a name="user-defined-hierarchies-and-cube-space"></a>ユーザー定義階層とキューブ空間  
 このトピックのここまでの例では、属性階層を使用してキューブ空間内の位置を定義していました。 キューブ空間内の位置は、ディメンション内の属性階層を基に定義したユーザー定義階層を使用して定義することもできます。 ユーザー定義階層は、ユーザーによるキューブ データの参照を容易にするための、属性階層の階層です。  
  
 たとえば、上のセクションの `CROSSJOIN` クエリは、次のようにも記述できます。  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 先ほど属性階層を使用して定義していたキューブ空間内の位置を、このクエリでは、Customer ディメンション内の Customer Geography ユーザー定義階層で定義しています。 属性階層とユーザー定義階層のどちらを使用しても、キューブ空間内の同じ場所を定義できます。  
  
##  <a name="AttribRelationships"></a> 属性リレーションシップとキューブ空間  
 関連する属性間に属性リレーションシップを定義すると、(適切な集計が円滑に作成されるようになり) クエリのパフォーマンスが向上するだけでなく、属性階層のメンバーと共に出現する、関連する属性階層のメンバーに影響を及ぼします。 たとえば、City 属性階層のメンバーが含まれた組を定義した場合、その組に Country 属性階層のメンバーが明示的に定義されていなくても、関連する Country 属性階層のメンバーが Country 属性階層の既定メンバーであると予測できます。 ただしこれは、City 属性階層と Country 属性階層の間に属性リレーションシップが定義されている場合に限ります。  
  
 次の例は、関連する属性階層に所属する、クエリに明示的に含まれていないメンバーを返します。  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  注意、`WITH`でキーワードを使用して、 [CurrentMember (MDX)](/sql/mdx/current-mdx)と[Name (MDX)](/sql/mdx/members-string-mdx)クエリで使用するための計算されるメンバーを作成する関数。 詳細については、「[MDX の基本的なクエリ &#40;MDX&#41;](mdx-query-the-basic-query.md)」を参照してください。  
  
 上のクエリでは、State 属性階層の各メンバーに関連付けられた Country 属性階層のメンバーの名前が返されます。 City 属性と Country 属性の間には属性リレーションシップが定義されているので、予測どおりに Country メンバーが返されます。 ところが、次のクエリで示すように、同一ディメンションの属性階層間に属性リレーションシップが定義されていない場合は、(All) メンバーが返されます。  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 上のクエリでは、Education と City の間に属性リレーションシップが定義されていないので、(All) メンバー ("All Customers") が返されます。 したがって、Education メンバーが明示的に指定されていない場合、City 属性階層が含まれている組の Education 属性階層の既定のメンバーは Education 属性階層の (All) メンバーになります。  
  
## <a name="calculation-context"></a>計算コンテキスト  
  
## <a name="see-also"></a>参照  
 [MDX の主な概念 (Analysis Services)](../key-concepts-in-mdx-analysis-services.md)   
 [組](tuples.md)   
 [Autoexists](autoexists.md)   
 [メンバー、組、およびセットの操作 &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [表示部分の合計と非表示部分の合計](visual-totals-and-non-visual-totals.md)   
 [MDX 言語リファレンス &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [多次元式 &#40;MDX&#41; リファレンス](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
