---
title: デシジョン ツリー モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- decision tree algorithms [Analysis Services]
- content queries [DMX]
- decision trees [Analysis Services]
ms.assetid: ceaf1370-9dd1-4d1a-a143-7f89a723ef80
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 009e8d203d9262ee14702b99ad7d0e31d8a16dbb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084756"
---
# <a name="decision-trees-model-query-examples"></a>デシジョン ツリー モデルのクエリ例
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、分析で検出されたパターンの詳細情報を取得できます。予測クエリでは、モデル内のパターンを使用して新しいデータについての予測を行うことができます。 たとえば、デシジョン ツリー モデルでコンテンツ クエリを使用すると、ツリーの各レベルのケースの数に関する統計や、ケースを区別するルールを取得できます。 一方、予測クエリを使用すると、モデルを新しいデータにマップして、提案や分類などを生成することができます。 クエリを使用してモデルに関するメタデータを取得することもできます。  
  
 ここでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムに基づくモデルに対するクエリの作成方法について説明します。  
  
 **コンテンツ クエリ**  
  
 [データ マイニング スキーマ行セットからモデル パラメーターを取得する](#bkmk_Query1)  
  
 [DMX を使用してモデルのツリーについての詳細を取得する](#bkmk_Query2)  
  
 [モデルからサブツリーを取得する](#bkmk_Query3)  
  
 **予測クエリ**  
  
 [確率付きの予測を取得する](#bkmk_Query4)  
  
 [デシジョン ツリー モデルからアソシエーションを予測する](#bkmk_Query5)  
  
 [デシジョン ツリー モデルから回帰式を取得する](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> デシジョン ツリー モデルに関する情報の入手  
 デシジョン ツリー モデルのコンテンツに対して意味のあるクエリを作成するには、モデル コンテンツの構造や、各種類のノードに格納されている情報の種類を把握しておく必要があります。 詳細については、「 [デシジョン ツリー モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)」を参照してください。  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:データ マイニング スキーマ行セットからモデル パラメーターを取得する  
 データ マイニング スキーマ行セットに対してクエリを実行すると、モデルに関するメタデータを取得できます (作成された日時、最後に処理された日時、基になるマイニング構造の名前、予測可能な属性として使用されている列の名前など)。 モデルが最初に作成されたときに使用されたパラメーターを取得することもできます。  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 サンプルの結果 :  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:DMX を使用してモデル コンテンツに関する詳細を取得します。  
 次のクエリは、「 [基本的なデータ マイニング チュートリアル](../../tutorials/basic-data-mining-tutorial.md)」でモデルを構築したときに作成したデシジョン ツリーに関する基本的な情報を返します。 各ツリー構造は、それ自体のノードに格納されます。 このモデルに含まれている予測可能な属性は 1 つなので、ツリー ノードは 1 つしかありません。 しかし、デシジョン ツリー アルゴリズムを使用してアソシエーション モデルを作成した場合は、各製品に 1 つずつ、何百ものツリーがあることもあります。  
  
 このクエリでは、種類が 2 のノード (特定の予測可能な属性を表すツリーの最上位のノード) がすべて返されます。  
  
> [!NOTE]  
>  `CHILDREN_CARDINALITY` という列は、MDX の同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 例の結果を次に示します。  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|All|12939|5|  
  
 この結果からわかることは何でしょうか。 デシジョン ツリー モデルの特定のノードのカーディナリティは、そのノードの直接の子の数を表します。 このノードのカーディナリティは 5 なので、このモデルでは、対象になる母集団 (自転車を購入する可能性がある顧客) が 5 つのサブグループに分割されていることがわかります。  
  
 次の関連するクエリは、この 5 つのサブグループの子を、子ノードの属性と値の分布と共に返します。 サポート、確率、分散などの統計は、`NODE_DISTRIBUTION` という入れ子になったテーブルに格納されているため、この例では、入れ子になったテーブル列を出力するために `FLATTENED` キーワードを使用しています。  
  
> [!NOTE]  
>  入れ子になったテーブル列である `SUPPORT` は、同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 例の結果を次に示します。  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|SUPPORT|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|1|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|1|473|  
  
 これらの結果からことがわかります顧客の自転車の購入者 (`[Bike Buyer]` = 1)、1067 人の顧客が車および 473 顧客は車を 3 を必要があります。  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:モデルからサブツリーを取得する  
 実際に自転車を購入した顧客についてさらに調査する場合は、 次の例のようにクエリで [IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx) 関数を使用すると、任意のサブツリーについて追加の詳細を表示することができます。 次のクエリは、42 歳以上の顧客を含むツリーのリーフ ノード (NODE_TYPE = 4) を取得して、自転車を購入した顧客の数を返します。 このクエリでは、入れ子になったテーブルの行が Bike Buyer = 1 の行のみに制限されています。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 例の結果を次に示します。  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>デシジョン ツリー モデルを使用して予測を作成する  
 デシジョン ツリーは、分類、回帰、アソシエーションなど、さまざまなタスクに使用できるため、デシジョン ツリー モデルに対する予測クエリを作成する際にはさまざまな選択肢があります。 予測の結果を理解するには、モデルが作成された目的を把握しておく必要があります。 以下のクエリ サンプルでは、次の 3 つのシナリオについて説明します。  
  
-   分類モデルの予測を、その予測が正しい確率と共に取得して、その確率で結果をフィルター処理する  
  
-   単一クエリを作成してアソシエーションを予測する  
  
-   入力と出力が直線関係にあるデシジョン ツリーの部分の回帰式を取得する  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4:確率付きの予測を取得する  
 次のサンプル クエリでは、「 [基本的なデータ マイニング チュートリアル](../../tutorials/basic-data-mining-tutorial.md)」で作成したデシジョン ツリー モデルを使用します。 クエリは [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW のテーブル dbo.ProspectiveBuyers にあるサンプル データの新しいセットを渡して、新しいデータ セット内のどの顧客が自転車を購入するかを予測します。  
  
 このクエリでは、予測関数 [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)を使用しています。この関数は、モデルで検出された確率に関する有用な情報を含む入れ子になったテーブルを返します。 クエリの最後の WHERE 句は結果をフィルター処理して、自転車を購入する確率が 0% より大きいと予測された顧客のみを返します。  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 既定では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、入れ子になったテーブルを列ラベル **[Expression]** を使用して返します。 このラベルを変更するには、返される列に別名を付けます。 その別名 (この例の場合は **Results**) は、列見出しと、入れ子になったテーブルの値の両方に使用されます。 結果を表示するには、入れ子になったテーブルを展開する必要があります。  
  
 例の結果、Bike Buyer = 1。  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 使用しているプロバイダーが、ここに示されているような階層的な行セットをサポートしていない場合は、クエリで FLATTENED キーワードを使用すると、繰り返される列値の代わりに NULL を含むテーブルとして結果を返すことができます。 詳細については、「[入れ子になったテーブル &#40;Analysis Services - データ マイニング&#41;](nested-tables-analysis-services-data-mining.md)」または「[DMX 選択ステートメントについて](/sql/dmx/understanding-the-dmx-select-statement)」を参照してください。  
  
###  <a name="bkmk_Query5"></a> サンプル クエリ 5:デシジョン ツリー モデルからアソシエーションを予測する  
 次のサンプル クエリは、Association マイニング構造に基づいています。 このサンプルに従って作業するために、このマイニング構造に新しいモデルを追加し、アルゴリズムとして Microsoft デシジョン ツリーを選択できます。 アソシエーション マイニング構造を作成する方法の詳細については、次を参照してください。[レッスン 3。マーケット バスケット シナリオの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)します。  
  
 次のサンプル クエリは単一クエリです。このクエリは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でフィールドを選択し、それらのフィールドの値をドロップダウン リストから選択するだけで簡単に作成できます。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 期待される結果:  
  
|[モデル]|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 この結果から、Patch Kit という製品を購入した顧客に提案するのに最適な 3 つの製品がわかります。 提案を行う際に複数の製品を入力として指定することもできます。そのためには、値を入力するか、 **[単一クエリ入力]** ダイアログ ボックスを使用して値を追加または削除します。 次のサンプル クエリは、複数の値を指定して予測を行う方法を示しています。 値は、入力値を定義する SELECT ステートメント内の UNION 句で接続されています。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 期待される結果:  
  
|[モデル]|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="bkmk_Query6"></a> サンプル クエリ 6:デシジョン ツリー モデルから回帰式を取得する  
 連続属性の回帰を含むデシジョン ツリー モデルを作成すると、回帰式を使用して予測を行ったり、回帰式に関する情報を抽出したりすることができます。 回帰モデルに対するクエリの詳細については、「 [線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)」を参照してください。  
  
 デシジョン ツリー モデルに回帰ノードと、不連続属性や範囲で分割されるノードが混在している場合は、回帰ノードのみを返すクエリを作成できます。 NODE_DISTRIBUTION テーブルには、回帰式の詳細が含まれています。 この例では、見やすくするために列をフラット化して、NODE_DISTRIBUTION テーブルに別名を付けています。 しかし、このモデルでは、Income を他の連続属性に関連付けるためのリグレッサーは検出されませんでした。 このような場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、その属性の平均値とモデル内の全分散を返します。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 例の結果を次に示します。  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 回帰モデルで使用される値型と統計の詳細については、「[線形回帰モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="list-of-prediction-functions"></a>予測関数の一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムでは、次の表のような追加の関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|あるノードがモデル内の別のノードの子であるかどうかを示します。|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|指定されたノードが現在のケースを含んでいるかどうかを示します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|重み付け確率を返します。|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|結合データセットのメンバーシップを予測します。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|現在の予測値に関連する値のテーブルを返します。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|各ケースの Node_ID を返します。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|予測値の確率を返します。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|指定された列に対して、予測された標準偏差を返します。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|指定された状態に対するサポート値を返します。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|指定された列の分散を返します。|  
  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムに共通の関数の一覧については、「[一般的な予測関数 (DMX)](/sql/dmx/general-prediction-functions-dmx)」を参照してください。 特定の関数の構文については、「[データ マイニング拡張機能 &#40;DMX&#41; 関数リファレンス](/sql/dmx/data-mining-extensions-dmx-function-reference)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ](data-mining-queries.md)   
 [Microsoft デシジョン ツリー アルゴリズム](microsoft-decision-trees-algorithm.md)   
 [Microsoft デシジョン ツリー アルゴリズム テクニカル リファレンス](microsoft-decision-trees-algorithm-technical-reference.md)   
 [デシジョン ツリー モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
