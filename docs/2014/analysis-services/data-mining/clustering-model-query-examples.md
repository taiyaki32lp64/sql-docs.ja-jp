---
title: クラスタ リング モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- content queries [DMX]
- clustering algorithms [Analysis Services]
ms.assetid: bf2ba332-9bc6-411a-a3af-b919c52432c8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4996ba378319e442df07a4ff09af3404034474d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085718"
---
# <a name="clustering-model-query-examples"></a>クラスタリング モデルのクエリ例
  データ マイニング モデルに対するクエリを作成すると、モデルに関するメタデータを取得できます。また、分析で検出されたパターンに関する詳細を取得するためのコンテンツ クエリも作成できます。 モデル内のパターンを使用して新しいデータの予測を行う予測クエリを作成することもできます。 取得できる情報は、クエリの種類によって異なります。 たとえばコンテンツ クエリを使用すると、検出されたクラスターに関する追加情報を取得できるのに対し、予測クエリを使用すると、新しいデータ ポイントが所属する可能性が高いクラスターを調べることができます。  
  
 ここでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスタリング アルゴリズムに基づいたモデルに対するクエリの作成方法について説明します。  
  
 **コンテンツ クエリ**  
  
 [DMX を使用してモデル メタデータを取得する](#bkmk_Query1)  
  
 [スキーマ行セットからモデル メタデータを取得する](#bkmk_Query2)  
  
 [クラスターまたはクラスターのリストを取得する](#bkmk_Query3)  
  
 [クラスターの属性を取得する](#bkmk_Query4)  
  
 [システム ストアド プロシージャを使用してクラスターのプロファイルを取得する](#bkmk_Query5)  
  
 [クラスターの識別要因を取得する](#bkmk_Query6)  
  
 [クラスターに属するケースを取得する](#bkmk_Query7)  
  
 **予測クエリ**  
  
 [クラスター モデルの結果を予測する](#bkmk_Query8)  
  
 [クラスター メンバーシップを確認する](#bkmk_Query9)  
  
 [すべての可能なクラスターを確率および距離と共に取得する](#bkmk_Query10)  
  
##  <a name="bkmk_top2"></a> モデルに関する情報の入手  
 すべてのマイニング モデルでは、アルゴリズムによる学習内容が、正規化されたスキーマ (マイニング モデル スキーマ行セット) に従って公開されます。 マイニング モデル スキーマ行セットに対するクエリは、データ マイニング拡張機能 (DMX) ステートメントを使用して作成できます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、スキーマ行セットに対して直接、システム テーブルとしてクエリを実行することもできます。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:DMX を使用してモデル メタデータを取得する  
 次のクエリは、「基本的なデータ マイニング チュートリアル」で作成したクラスター モデル `TM_Clustering`に関する基本的なメタデータを返します。 クラスター モデルの親ノードで利用可能なメタデータには、モデルの名前、モデルが格納されているデータベース、モデルの子ノードの数などがあります。 このクエリでは、DMX コンテンツ クエリを使用してモデルの親ノードからメタデータを取得しています。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  CHILDREN_CARDINALITY という列名は、多次元式 (MDX) の同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Cluster Model|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|All|  
  
 アソシエーション モデル内でのこれらの列の意味については、「[クラスター モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)」を参照してください。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:スキーマ行セットからモデル メタデータを取得する  
 データ マイニング スキーマ行セットに対してクエリを実行すると、DMX コンテンツ クエリで返されたのと同じ情報を取得できます。 ただし、スキーマ行セットから返される情報にはいくつかの追加の列があります (モデルの作成時に使用されたパラメーター、モデルが最後に処理された日時、モデルの所有者など)。  
  
 次の例では、モデルが作成された日、変更された日、最後に処理された日、モデルの作成に使用されたクラスタリング パラメーター、およびトレーニング セットのサイズが返されます。 この情報は、モデルのドキュメントを作成する場合や、既存のモデルの作成に使用されたクラスタリング オプションを特定する場合に使用できます。  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [トップに戻る](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>クラスターに関する情報の入手  
 一般に、クラスター モデルに対する最も便利なコンテンツ クエリでは、 **クラスター ビューアー**を使用して参照できるのと同じ種類の情報が返されます。 こうした情報には、クラスターのプロファイル、クラスターの特性、クラスターの識別などがあります。 ここでは、この情報を取得するクエリの例を紹介します。  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:クラスターまたはクラスターの一覧を取得します。  
 すべてのクラスターはノードの種類が 5 であるため、モデル コンテンツに対してその種類のノードのみのクエリを実行することによって、簡単にクラスターのリストを取得できます。 この例のように、返されるノードを確率やサポートでフィルター処理することもできます。  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|Cluster 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 クラスターを定義する属性は、データ マイニング スキーマ行セットの 2 つの列に含まれています。  
  
-   NODE_DESCRIPTION 列には、属性のコンマ区切りのリストが含まれています。 この属性のリストは、表示のために省略されることもあります。  
  
-   NODE_DISTRIBUTION 列の入れ子になったテーブルには、クラスターのすべての属性のリストが含まれています。 使用しているクライアントで階層的な行セットがサポートされていない場合は、SELECT 列リストの前に FLATTENED キーワードを追加することによって、入れ子になったテーブルを返すことができます。 FLATTENED キーワードの使用方法の詳細については、「[SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](/sql/dmx/select-from-model-dimension-content-dmx)」を参照してください。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4:クラスターの属性を取得する  
 **クラスター ビューアー** には、すべてのクラスターについて、属性とその値の一覧を含むプロファイルが表示されます。 そのほか、モデル内のケースの母集団全体の値の分布を示すヒストグラムも表示されます。 ビューアーでモデルを参照する場合は、このヒストグラムをマイニング凡例からコピーして、簡単に Excel や Word のドキュメントに貼り付けることができます。 また、ビューアーの [クラスターの特性] ペインを使用して、異なるクラスターの属性をグラフィカルに比較することもできます。  
  
 ただし、一度に複数のクラスターの値を取得する必要がある場合は、モデルに対してクエリを実行する方が簡単です。 たとえば、モデルを参照していて、上位 2 つのクラスターは `Number Cars Owned`という属性が異なっていることに気付いた場合、 それぞれのクラスターの値を抽出することができます。  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 コードの最初の行で、上位 2 つのクラスターのみを対象とすることを指定しています。  
  
> [!NOTE]  
>  既定では、クラスターはサポートで順序付けされます。 したがって、NODE_SUPPORT 列は省略できます。  
  
 コードの 2 行目では、入れ子になったテーブル列の特定の列のみを返す下位選択ステートメントを追加しています。 さらに、入れ子になったテーブルの行を、対象の属性 ( `Number Cars Owned`) に関連する行のみに制限しています。 また、表示を簡略化するために、入れ子になったテーブルに別名を付けています。  
  
> [!NOTE]  
>  入れ子になったテーブル列である `PROBABILITY`は、MDX の予約済みキーワードと同じ名前であるため、角かっこで囲む必要があります。  
>   
>  例の結果を次に示します。  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Missing|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1.60E-05|  
|002|4|0|  
|002|Missing|0|  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> サンプル クエリ 5:ストアド プロシージャをシステムを使用して、クラスターのプロファイルを取得  
 DMX を使用して独自にクエリを作成する代わりに、より簡単な方法として、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でクラスターの操作に使用されるシステム ストアド プロシージャを呼び出すこともできます。 次の例は、内部ストアド プロシージャを使用して、ID が 002 のクラスターのプロファイルを取得する方法を示しています。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 同様に、システム ストアド プロシージャを使用して、次の例のように特定のクラスターの特性を取得することもできます。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 例の結果を次に示します。  
  
|属性|値|頻度|サポート|  
|----------------|------------|---------------|-------------|  
|Number Children at Home|0|0.999999829076798|899|  
|Region|North America|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  データ マイニング システム ストアド プロシージャは内部で使用するためのものであり、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、これらを必要に応じて変更する場合があります。 実際の運用では、DMX、AMO、または XMLA を使用してクエリを作成することをお勧めします。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query6"></a> サンプル クエリ 6:クラスターの識別要因を検索します。  
 **クラスター ビューアー** の **[クラスターの識別]** タブを使用すると、クラスターを簡単に別のクラスターと比較したり、他のすべてのケース (そのクラスターを除く全クラスター) と比較したりできます。  
  
 一方、この情報を返すクエリを作成するのは簡単ではなく、一時的な結果を格納して複数のクエリの結果を比較する追加の処理がクライアント側で必要になる場合があります。 より簡単な方法として、システム ストアド プロシージャを使用できます。  
  
 次のクエリは、ノード ID が 009 と 007 の 2 つのクラスターの主な識別要因を示す 1 つのテーブルを返します。 正の値を持つ属性ではクラスター 009 が優先され、負の値を持つ属性ではクラスター 007 が優先されます。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 例の結果を次に示します。  
  
|属性|値|[スコア]|  
|----------------|------------|-----------|  
|Region|North America|100|  
|English Occupation|Skilled Manual|94.9003803898654|  
|Region|Europe|-72.5041051379789|  
|English Occupation|手動|-69.6503163202722|  
  
 この情報は、 **[クラスターの識別]** タブの 1 つ目のドロップダウン リストでクラスター 9 を選択し、2 つ目のドロップダウン リストでクラスター 7 を選択した場合にグラフに表示されるのと同じ情報です。 クラスター 9 を他のすべてのクラスターと比較するには、次のように、2 つ目のパラメーターで空の文字列を使用します。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  データ マイニング システム ストアド プロシージャは内部で使用するためのものであり、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、これらを必要に応じて変更する場合があります。 実際の運用では、DMX、AMO、または XMLA を使用してクエリを作成することをお勧めします。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> サンプル クエリ 7:クラスターに属するケースを取得する  
 マイニング モデルでドリルスルーが有効になっている場合は、モデルで使用されたケースに関する詳細情報を返すクエリを作成できます。 さらに、マイニング構造でドリルスルーが有効になっている場合は、[StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 関数を使用して、基になる構造の列を含めることもできます。  
  
 次の例は、モデルで使用された 2 つの列 (Age および Region) と、モデルで使用されなかったもう 1 つの列 (First Name) を返します。 このクエリで返されるのは、クラスター 1 に分類されたケースだけです。  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 クラスターに属するケースを取得するには、そのクラスターの ID がわかっている必要があります。 クラスターの ID は、いずれかのビューアーでモデルを参照することによって取得できます。 また、簡単に参照できるようにクラスターの名前を変更することもできます。名前を変更した後は、その名前を ID 番号の代わりに使用できます。 ただし、クラスターに割り当てた名前はモデルを再処理すると失われるので注意してください。  
  
 [トップに戻る](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>モデルを使用して予測を行う  
 クラスターは、データの説明や把握のために使用されるのが一般的ですが、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] の実装では、クラスター メンバーシップに関する予測を行って、その予測に関連する確率を取得することもできます。 ここでは、クラスター モデルに対する予測クエリを作成する方法の例を紹介します。 表形式のデータ ソースを指定して複数のケースの予測を行うことも、単一クエリを作成して一度に 1 つずつ新しい値を渡すこともできます。 このセクションの例は、わかりやすくするためにすべて単一クエリになっています。  
  
 DMX を使用して予測クエリを作成する方法の詳細については、次を参照してください。[データ マイニング クエリ インターフェイス](data-mining-query-tools.md)します。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query8"></a> サンプル クエリ 8:クラスター モデルの結果を予測する  
 作成したクラスター モデルに予測可能な属性が含まれている場合は、そのモデルを使用して結果に関する予測を行うことができます。 ただし、予測可能列を `Predict` に設定するか `PredictOnly` に設定するかによって、モデルによる予測可能な属性の処理方法が異なります。 列の使用法を `Predict` に設定すると、その属性の値がクラスター モデルに追加され、完成したモデルに属性として表示されます。 一方、列の使用法を `PredictOnly` に設定すると、その値はクラスターの作成には使用されません。 代わりに、モデルが完成した後に、各ケースが属するクラスターに基づいて `PredictOnly` 属性の新しい値がクラスタリング アルゴリズムによって作成されます。  
  
 次のクエリでは、モデルに新しいケースを 1 つ渡しています。このケースに関する情報は Age と Gender だけです。 SELECT ステートメントでは、関心のある予測可能な属性と値のペアを指定しています。 [PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx) 関数は、それらの属性を持つケースの結果が対象の結果になる確率を返します。  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 使用法を `Predict` に設定した場合の結果の例を次に示します。  
  
|Bike Buyer|式|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 使用法を `PredictOnly` に設定し、モデルを再処理した場合の結果の例を次に示します。  
  
|Bike Buyer|式|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 この例ではモデルに大きな違いはありませんが、 値の実際の分布とモデルの予測との違いを検出することが重要になる場合もあります。 [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) 関数を使用できます。この関数は、特定のモデルについてケースの確率を返します。  
  
 PredictCaseLikelihood 関数によって返される数値は確率であるため、常に 0 と 1 の間になります。値 .5 はランダムな結果を表します。 したがって、スコアが .5 より小さい場合は、予測されたケースがそのモデルではあり得そうにないことを示し、.5 より大きい場合は、おそらくモデルに収まることを示します。  
  
 たとえば次のクエリは、新しいサンプル ケースの可能性を表す 2 つの値を返します。 正規化されていない値は、現在のモデルでの確率を表します。 NORMALIZED キーワードを使用すると、この関数によって返される可能性スコアが、"モデルを使用した場合の確率" を "モデル使用しない場合の確率" で割って調整されます。  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 例の結果を次に示します。  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5.56438372679893E-11|8.65459953145182E-68|  
  
 これらの結果の数値は科学的表記法で表されています。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query9"></a> サンプル クエリ 9:クラスター メンバーシップを確認する  
 この例では、 [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) 関数を使用して、新しいケースが属する可能性が最も高いクラスターを取得し、 [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx) 関数を使用して、そのクラスターに属する確率を取得しています。  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 例の結果を次に示します。  
  
|$CLUSTER|式|  
|--------------|----------------|  
|Cluster 2|0.397918596951617|  
  
 **注**既定で、`ClusterProbability`関数は、最も可能性の高いクラスターの確率を返します。 ただし、 `ClusterProbability('cluster name')`という構文を使用して別のクラスターを指定することもできます。 その場合は、この 2 つの予測関数の結果は互いに無関係であるため、 2 番目の列の確率スコアが、1 番目の列のクラスターとは別のクラスターのものになる場合もあることに注意してください。  
  
 [トップに戻る](#bkmk_top2)  
  
###  <a name="bkmk_Query10"></a> サンプル クエリ 10:すべての可能なクラスターを確率および距離と共に取得する  
 前の例の確率スコアはあまり高くありませんでした。 より適したクラスターがあるかどうかを調べるには、 [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx) 関数を [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) 関数と共に使用して、すべての可能なクラスターと、各クラスターに新しいケースが属する確率を含む、入れ子になったテーブルを取得することができます。 ここでは、結果を見やすくするために、FLATTENED キーワードを使用して階層的な行セットをフラット テーブルに変更しています。  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|Cluster 2|0.602081403048383|0.397918596951617|  
|Cluster 10|0.719691686785675|0.280308313214325|  
|Cluster 4|0.867772590378791|0.132227409621209|  
|Cluster 5|0.931039872200985|0.0689601277990149|  
|Cluster 3|0.942359230072167|0.0576407699278328|  
|クラスター 6|0.958973668972756|0.0410263310272437|  
|Cluster 7|0.979081275926724|0.0209187240732763|  
|クラスター 1|0.999169044818624|0.000830955181376364|  
|Cluster 9|0.999831227795894|0.000168772204105754|  
|Cluster 8|1|0|  
  
 既定では、結果は確率で順位付けされます。 この結果から、Cluster 2 は、確率はかなり低いとはいえ、新しいデータ ポイントに最適なクラスターであることがわかります。  
  
 **注:** 追加の列の `$DISTANCE`は、データ ポイントからクラスターまでの距離を表します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスタリング アルゴリズムでは、既定でスケーラブル EM クラスタリングが使用されます。スケーラブル EM クラスタリングでは、各データ ポイントに複数のクラスターが割り当てられて、可能なクラスターが順位付けされます。  一方、K-Means アルゴリズムを使用してクラスター モデルを作成した場合は、各データ ポイントに 1 つしかクラスターを割り当てることができないため、このクエリで返される行は 1 行だけになります。 [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) 関数を使用して、基になる構造の列を含めることもできます。 EM クラスタリングと K-Means クラスタリングの相違点の詳細については、「 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](microsoft-clustering-algorithm-technical-reference.md)」を参照してください。  
  
 [トップに戻る](#bkmk_top2)  
  
## <a name="function-list"></a>関数一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスタリング アルゴリズムを使用して作成されたモデルでは、次の表のような追加の関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx)|入力ケースを含んでいる可能性が最も高いクラスターを返します。|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|指定されたクラスターと入力したケース間の距離を返します。ただしクラスターが指定されていない場合は、最も可能性の高いクラスターと入力したケース間の距離を返します。<br /><br /> 入力ケースが指定されたクラスターに所属する確率を返します。|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|入力ケースが指定されたクラスターに所属する確率を返します。|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|あるノードがモデル内の別のノードの子であるかどうかを示します。|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|指定されたノードが現在のケースを含んでいるかどうかを示します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|重み付け確率を返します。|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|結合データセットのメンバーシップを予測します。|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|入力したケースが既存のモデル内に収まる確率値を返します。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|現在の予測値に関連する値のテーブルを返します。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|各ケースの Node_ID を返します。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|予測値の確率を返します。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|指定された列に対して、予測された標準偏差を返します。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|指定された状態に対するサポート値を返します。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|指定された列の分散を返します。|  
  
 特定の関数の構文については、「[データ マイニング拡張機能 &#40;DMX&#41; 関数リファレンス](/sql/dmx/data-mining-extensions-dmx-function-reference)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ](data-mining-queries.md)   
 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](microsoft-clustering-algorithm-technical-reference.md)   
 [Microsoft クラスタリング アルゴリズム](microsoft-clustering-algorithm.md)  
  
  
