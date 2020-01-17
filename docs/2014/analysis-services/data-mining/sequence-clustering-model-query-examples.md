---
title: シーケンス クラスター モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d871ba87147f24fdd60c9effe5f279d9ea355db1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082920"
---
# <a name="sequence-clustering-model-query-examples"></a>Sequence Clustering Model Query Examples
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、モデルに格納されている情報の詳細を取得できます。予測クエリでは、モデル内のパターンを使用して、指定した新しいデータに基づく予測を行うことができます。 シーケンス クラスター モデルでコンテンツ クエリを使用すると、一般に、検出されたクラスターやクラスター内の遷移に関する追加情報を取得できます。 クエリを使用してモデルに関するメタデータを取得することもできます。  
  
 シーケンス クラスター モデルで予測クエリを使用すると、一般に、シーケンスと遷移、モデル内の非シーケンス属性、またはシーケンス属性と非シーケンス属性の組み合わせに基づく提案が行われます。  
  
 ここでは、Microsoft シーケンス クラスター アルゴリズムに基づいたモデルに対するクエリの作成方法について説明します。 クエリの作成に関する一般的な情報については、「 [データ マイニング クエリ](data-mining-queries.md)」を参照してください。  
  
 **Content Queries**  
  
 [データ マイニング スキーマ行セットを使用してモデル パラメーターを取得する](#bkmk_Query1)  
  
 [状態に対するシーケンス一覧を取得する](#bkmk_Query2)  
  
 [システム ストアド プロシージャを使用する](#bkmk_Query3)  
  
 **予測クエリ**  
  
 [次の状態を予測する](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> シーケンス クラスター モデルに関する情報の入手  
 マイニング モデルのコンテンツに対して意味のあるクエリを作成するには、モデル コンテンツの構造や、各種類のノードに格納されている情報の種類を把握しておく必要があります。 詳細については、「 [シーケンス クラスター モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-sequence-clustering-models.md)」を参照してください。  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:データ マイニング スキーマ行セットを使用してモデル パラメーターを取得するには  
 データ マイニング スキーマ行セットに対してクエリを実行すると、モデルに関する各種の情報を取得できます (基本的なメタデータ、モデルが作成された日時、モデルが最後に処理された日時、基になるマイニング構造の名前、予測可能な属性として使用されている列など)。  
  
 次のクエリでは、 `[Sequence Clustering]`モデルの作成とトレーニングに使用されたパラメーターが返されます。 このモデルは、「 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)」のレッスン 5 で作成できます。  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 例の結果を次に示します。  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 このモデルは、CLUSTER_COUNT の既定値 10 を使用して作成されています。 CLUSTER_COUNT にゼロ以外のクラスター数を指定した場合、アルゴリズムで取得するクラスターの概数のヒントとして、この数が使用されます。 ただし、アルゴリズムによる分析処理時に取得されるクラスター数は、これより上下する場合があります。 ここでは、アルゴリズムによって、15 個のクラスターがトレーニング データに対し最適であると判断されました。 したがって、完成したモデルのパラメーター値の一覧では、モデルの作成時に渡された値ではなく、アルゴリズムによって決定されたクラスター数が報告されます。  
  
 最適なクラスター数をアルゴリズムで決定する場合と、この動作はどのように違うのでしょうか。 試しに、同じデータを使用する別のクラスター モデルを作成し、CLUSTER_COUNT を 0 に設定してみます。 この場合、アルゴリズムでは 32 個のクラスターが検出されます。 したがって、CLUSTER_COUNT の既定値 10 を使用することによって、結果の数が制限されていることがわかります。  
  
 既定値として 10 が使用されているのは、多くの人にとって、クラスター数が少ない方が、データのグループ化を参照および理解しやすいためです。 ただし、それぞれのモデルとデータのセットは異なります。 クラスター数を増減してみて、最も正確なモデルが作成されるパラメーター値を探すようお勧めします。  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:状態に対するシーケンスの一覧を取得します。  
 マイニング モデル コンテンツには、トレーニング データで検出されたシーケンスが、最初の状態とそれに関連する 2 番目の状態の一覧の組み合わせとして格納されます。 最初の状態がシーケンスのラベルとして使用され、関連する 2 番目の状態は遷移と呼ばれます。  
  
 たとえば、次のクエリでは、モデルにある最初の状態の完全な一覧が返された後、シーケンスがクラスターにグループ化されます。  この一覧を取得するには、モデルのルート ノードを親 (PARENT_UNIQUE_NAME = 0) とするシーケンスの一覧 (NODE_TYPE = 13) を取得します。 FLATTENED キーワードによって、結果が読み取りやすくなります。  
  
> [!NOTE]  
>  PARENT_UNIQUE_NAME、Support、Probability の各列名は、同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 結果の一部 :  
  
|NODE_UNIQUE_NAME|製品 1|シーケンス サポート|シーケンス確率|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Missing|0|#######|  
|1081327|All-Purpose Bike Stand|17|0.00111|  
|1081327|Bike Wash|64|0.00418|  
|1081327|(行 4 ～ 36 は省略)|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 モデル内のシーケンスの一覧は、常にアルファベットの昇順で表示されます。 シーケンスの順序番号によって関連する遷移を検索するため、シーケンスの順序は重要です。 `Missing` の値は常に遷移 0 です。  
  
 たとえば、上の結果のモデルでは、製品 "Women's Mountain Shorts" のシーケンス番号が 37 です。 この情報を使用して、"Women's Mountain Shorts" の後に購入されたすべての製品を表示することができます。  
  
 そのためには、まず、上のクエリで NODE_UNIQUE_NAME に対して返された値を参照し、モデルのすべてのシーケンスを含むノードの ID を取得します。 この値を親ノードの ID としてクエリに渡し、このノードに含まれている遷移だけを取得します。このノードには、モデルのすべてのシーケンスの一覧が含まれています。 一方、特定のクラスターの遷移の一覧を表示するには、クラスター ノードの ID を渡します。これにより、そのクラスターに関連するシーケンスだけを表示できます。  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 例の結果を次に示します。  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 この ID のノードには、製品 "Women's Mountain Shorts" に続くシーケンス、およびサポートと確率の値の一覧が含まれます。  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 例の結果を次に示します。  
  
|t.Product2|t.P2 サポート|t.P2 確率|  
|----------------|------------------|----------------------|  
|Missing|230.7419|0.456012|  
|Classic Vest|8.16129|0.016129|  
|Cycling Cap|60.83871|0.120235|  
|Half-Finger Gloves|30.41935|0.060117|  
|Long-Sleeve Logo Jersey|86.80645|0.171554|  
|Racing Socks|28.93548|0.057185|  
|Short-Sleeve Classic Jersey|60.09677|0.118768|  
  
 このモデルでは、"Women's Mountain Shorts" に関連するさまざまなシーケンスに対するサポートが 506 です。 遷移に対するサポートの値も 506 まで加算されます。 ただし、これらの数は整数ではありません。サポートが単に各遷移を含むケースの数を表すと考えると、少々変な感じがするかもしれません。 しかし、クラスターを作成する方法では部分的なメンバーシップが計算されるため、クラスター内の任意の遷移の可能性は、その特定のクラスターに属する可能性によって重み付けされる必要があります。  
  
 たとえば、クラスターが 4 つある場合、あるシーケンスがクラスター 1 に属する可能性は 40%、クラスター 2 に属する可能性は 30%、クラスター 3 に属する可能性は 20%、クラスター 4 に属する可能性は 10% です。 アルゴリズムでは、遷移が属する可能性が最も高いクラスターが特定された後、クラスター内での確率がクラスターの事前確率によって重み付けされます。  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:システムを使用してストアド プロシージャ  
 これらのクエリ サンプルから、モデルに格納された情報が複雑であることと、必要な情報を取得するために複数のクエリを作成する必要が生じる場合があることがわかります。 ただし、Microsoft シーケンス クラスター ビューアーには、シーケンス クラスター モデルに含まれている情報をグラフィカルに表示する、一連の強力なツールが用意されています。このビューアーを使用して、モデルにクエリやドリル ダウンを実行することもできます。  
  
 Microsoft シーケンス クラスター ビューアーに表示される情報は、ほとんどの場合、モデルにクエリを実行する Analysis Services システム ストアド プロシージャを使用して作成されます。 モデル コンテンツに対するデータ マイニング拡張機能 (DMX) クエリを記述することによっても、同じ情報を取得できますが、Analysis Services システム ストアド プロシージャを使用すると、探索やモデルのテストをすばやく行うことができます。  
  
> [!NOTE]  
>  システム ストアド プロシージャは、Analysis Services サーバーによって、また Analysis Services サーバーとの対話用に Microsoft が提供するクライアントによって、内部処理に使用されます。 したがって、Microsoft はこれらを随時変更する場合があります。 ここでは便宜上、これらについて説明しますが、運用環境での使用はサポートされません。 運用環境での安定性と互換性を保つには、常に DMX を使用してクエリを記述してください。  
  
 ここでは、シーケンス クラスター モデルに対するクエリを作成するシステム ストアド プロシージャの使用例を紹介します。  
  
#### <a name="cluster-profiles-and-sample-cases"></a>クラスターのプロファイルとサンプル ケース  
 [クラスターのプロファイル] タブには、モデル内のクラスターの一覧、各クラスターのサイズ、およびクラスターに含まれる状態を示すヒストグラムが表示されます。 同様の情報を取得するクエリで使用できるシステム ストアド プロシージャには、次の 2 種類があります。  
  
-   `GetClusterProfile` では、クラスターの特性と、クラスターの NODE_DISTRIBUTION テーブルにあるすべての情報が返されます。  
  
-   `GetNodeGraph` では、[シーケンス クラスター] ビューの最初のタブに表示される、クラスターの数学グラフ表現の作成に使用できるノードとエッジが返されます。 ノードがクラスターを、エッジが重み (強さ) を表します。  
  
 次の例は、システム ストアド プロシージャ `GetClusterProfiles`を使用して、モデル内のすべてのクラスターとそのプロファイルを取得する方法を示しています。 このストアド プロシージャは、モデル内のプロファイルの完全なセットを返す、一連の DMX ステートメントを実行します。 ただし、このストアド プロシージャを使用するには、モデルのアドレスを知っている必要があります。  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 次の例は、システム ストアド プロシージャ `GetNodeGraph`でクラスター ID を指定して、特定のクラスター (クラスター 12) のプロファイルを取得する方法を示しています。クラスター ID は、通常、クラスター名に含まれる番号と同じです。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 次のクエリに示すようにクラスター ID を省略した場合、 `GetNodeGraph` では、すべてのクラスター プロファイルの順序付けされフラット化された一覧が返されます。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 **[クラスターのプロファイル]** タブには、モデルのサンプル ケースのヒストグラムも表示されます。 これらのサンプル ケースは、モデルの理想的なケースを表しています。 これらのケースは、トレーニング データと同じようにはモデルに格納されません。モデルのサンプル ケースを取得するには、特別な構文を使用する必要があります。  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 詳細については、「[SELECT FROM &#60;model&#62;.SAMPLE_CASES (DMX)](/sql/dmx/select-from-model-dmx)」を参照してください。  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>クラスターの特性とクラスターの識別  
 **[クラスターの特性]** タブには、各クラスターの主要な属性が、確率で順位付けされて表示されます。 ケースの数が、クラスターに属するとどのようなケースの分布のように、クラスター内にあります。それぞれの特性では、特定のサポートされています。 特定のクラスターの特性を確認するには、クラスターの ID を知っている必要があります。  
  
 次の例では、システム ストアド プロシージャ `GetClusterCharacteristics`を使用して、確率スコアが指定したしきい値 0.0005 よりも高い、クラスター 12 の特性をすべて取得します。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 すべてのクラスターの特性を取得するには、クラスターの ID を空のままにします。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 次の例では、システム ストアド プロシージャ `GetClusterDiscrimination` を呼び出して、クラスター 1 とクラスター 12 の特性を比較します。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 独自のクエリを DMX で記述して、2 つのクラスターの比較や、あるクラスターと他のすべてのクラスターとの比較を行う場合、まず一方のセットの特性を取得してから、対象の特定クラスターの特性を取得して、2 つのセットを比較する必要があります。 このシナリオは比較的複雑で、通常、クライアント処理を必要とします。  
  
#### <a name="states-and-transitions"></a>状態と遷移  
 Microsoft シーケンス クラスターの **[状態遷移]** タブでは、さまざまなクラスターに関する統計情報を取得および比較する複雑なクエリを、バックエンドで実行します。 これらの結果を再現するには、比較的複雑なクエリとクライアント処理とを必要とします。  
  
 ただし、 [このセクション](#bkmk_ContentQueries)のサンプル クエリ 2 で説明した DMX クエリを使用すると、シーケンスまたは個々の遷移の確率と状態を取得できます。  
  
## <a name="using-the-model-to-make-predictions"></a>モデルを使用した予測  
 シーケンス クラスター モデルの予測クエリでは、他のクラスター モデルで使用される予測関数の多くを使用できます。 さらに、特別な予測関数 [PredictSequence (DMX)](/sql/dmx/predictsequence-dmx)を使用すると、提案や次の状態についての予測を行うことができます。  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4:次の状態を予測します。  
 [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx) 関数を使用すると、ある値に対して、最も可能性の高い次の状態を予測できます。 また、複数の次の状態を予測することもできます。たとえば、顧客が購入する可能性のある上位 3 製品の一覧を取得して、推奨製品一覧を提供することができます。  
  
 次のサンプル クエリは、上位 5 つの予測とその確率を返す単一予測クエリです。 入れ子になったテーブルがモデルに含まれているため、予測の実行時には、入れ子になったテーブル `[v Assoc Seq Line Items]`を列参照として使用する必要があります。 また、入れ子になった SELECT ステートメントに示されているように、入力として値を指定するときは、ケース テーブルと入れ子になったテーブルの両方の列を結合する必要があります。  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 例の結果を次に示します。  
  
|Expression.$Sequence|Expression.Line 番号|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 1 列だけを予期したにもかかわらず、結果には 3 列が含まれています。これは、クエリが常にケース テーブルに対する列を返すためです。 ここでは結果がフラット化されています。フラット化しないと、クエリは、入れ子になったテーブル列 2 列を含む 1 つの列を返します。  
  
 $sequence 列は、予測結果を並べ替えるために、 `PredictSequence` 関数から既定で返される列です。 `[Line Number]`列は、モデルのシーケンス キーに一致させる必要がありますが、これらのキーは出力ではありません。  
  
 興味深いことに、All-Purpose Bike Stand の後の最上位に予測されたシーケンスは、Cycling Cap と Cycling Cap です。 これはエラーではありません。 顧客に対するデータの提示方法や、モデルのトレーニング時のグループ化方法によっては、このようなシーケンスが返されることは珍しくありません。 たとえば、1 人の顧客がサイクリング キャップ (赤) の次にもう 1 つサイクリング キャップ (青) を購入することがあります。また、数を指定する方法がない場合、2 つを連続して購入することもあります。  
  
 行 6 と行 7 の値はプレースホルダーです。 可能な遷移のチェーンの最後に達しても、予測結果が終了されることはなく、入力として渡された値が結果に追加されます。 たとえば、予測の数を 20 に増やした場合、行 6 ～ 20 の値はすべて同じ All-Purpose Bike Stand となります。  
  
## <a name="function-list"></a>関数一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター アルゴリズムでは、次の表に示す追加の関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[Cluster (DMX)](/sql/dmx/cluster-dmx)|入力したケースを含む可能性の最も高いクラスターを返します。|  
|[ClusterDistance (DMX)](/sql/dmx/clusterdistance-dmx)|指定されたクラスターと入力したケース間の距離を返します。ただしクラスターが指定されていない場合は、最も可能性の高いクラスターと入力したケース間の距離を返します。<br /><br /> この関数は任意の種類のクラスター モデル (EM、K-Means など) と共に使用できますが、結果はアルゴリズムによって異なります。|  
|[ClusterProbability (DMX)](/sql/dmx/clusterprobability-dmx)|入力ケースが指定されたクラスターに所属する確率を返します。|  
|[IsInNode (DMX)](/sql/dmx/isinnode-dmx)|指定されたノードが現在のケースを含んでいるかどうかを示します。|  
|[PredictAdjustedProbability (DMX)](/sql/dmx/predictadjustedprobability-dmx)|指定された状態の調整済みの確率を返します。|  
|[PredictAssociation (DMX)](/sql/dmx/predictassociation-dmx)|結合メンバーシップを予測します。|  
|[PredictCaseLikelihood (DMX)](/sql/dmx/predictcaselikelihood-dmx)|入力したケースが既存のモデル内に収まる確率値を返します。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|指定された列の予測のためのヒストグラムを表すテーブルを返します。|  
|[PredictNodeId (DMX)](/sql/dmx/predictnodeid-dmx)|ケースが分類されるノードの Node_ID を返します。|  
|[PredictProbability (DMX)](/sql/dmx/predictprobability-dmx)|指定された状態の確率を返します。|  
|[PredictSequence (DMX)](/sql/dmx/predictsequence-dmx)|指定された一連のシーケンス データに対して予測される将来のシーケンス値です。|  
|[PredictStdev (DMX)](/sql/dmx/predictstdev-dmx)|指定された列に対して、予測された標準偏差を返します。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|指定された状態に対するサポート値を返します。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|指定された列の分散を返します。|  
  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムに共通の関数の一覧については、「[一般的な予測関数 (DMX)](/sql/dmx/general-prediction-functions-dmx)」を参照してください。 特定の関数の構文については、「[データ マイニング拡張機能 &#40;DMX&#41; 関数リファレンス](/sql/dmx/data-mining-extensions-dmx-function-reference)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ](data-mining-queries.md)   
 [Microsoft シーケンス クラスタリング アルゴリズム テクニカル リファレンス](microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft シーケンス クラスター アルゴリズム](microsoft-sequence-clustering-algorithm.md)   
 [シーケンス クラスター モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
