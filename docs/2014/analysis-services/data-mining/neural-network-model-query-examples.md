---
title: ニューラル ネットワーク モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a249a83aba62c7881be024caa3931cb5ad07204
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083291"
---
# <a name="neural-network-model-query-examples"></a>Neural Network Model Query Examples
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、分析で検出されたパターンの詳細情報を取得できます。予測クエリでは、モデル内のパターンを使用して新しいデータについての予測を行うことができます。 たとえば、ニューラル ネットワーク モデルのコンテンツ クエリでは、非表示層の数などのモデル メタデータを取得できます。 また、予測クエリでは、入力に基づいて分類を提示し、必要に応じて各分類の確率を提供することもできます。  
  
 ここでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムに基づくモデルに対するクエリの作成方法について説明します。  
  
 **コンテンツ クエリ**  
  
 [DMX を使用してモデル メタデータを取得する](#bkmk_Query1)  
  
 [スキーマ行セットからモデル メタデータを取得する](#bkmk_Query2)  
  
 [モデルの入力属性を取得する](#bkmk_Query3)  
  
 [非表示層から重みを取得する](#bkmk_Query4)  
  
 **予測クエリ**  
  
 [単一予測を作成する](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>ニューラル ネットワーク モデルに関する情報の入手  
 すべてのマイニング モデルでは、アルゴリズムによる学習内容が、正規化されたスキーマ (マイニング モデル スキーマ行セット) に従って公開されます。 この情報から、基本的なメタデータ、分析で検出された構造、処理の際に使用されたパラメーターなど、モデルに関する詳細情報を得ることができます。 モデル コンテンツに対するクエリは、データ マイニング拡張機能 (DMX) ステートメントを使用して作成できます。  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:DMX を使用してモデル メタデータを取得する  
 次のクエリは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムを使用して作成されたモデルに関するいくつかの基本的なメタデータを返します。 ニューラル ネットワーク モデルの親ノードには、モデルの名前、モデルが格納されているデータベースの名前、および子ノードの数だけが含まれます。 ただし、マージナル統計ノード (NODE_TYPE = 24) によって、この基本的なメタデータと、モデルで使用される入力列に関するいくつかの派生した統計が提供されます。  
  
 次のサンプル クエリは、「 [中級者向けデータ マイニング チュートリアル](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)」で作成した `Call Center Default NN`というマイニング モデルを基にしています。 このモデルは、コール センターからのデータを使用して、人員配置と電話/注文/案件数との間に存在する可能性がある相関関係を探索します。 この DMX ステートメントは、ニューラル ネットワーク モデルのマージナル統計ノードからデータを取得します。 関心のある入力属性の統計が入れ子になったテーブル NODE_DISTRIBUTION に格納されているため、このクエリには FLATTENED キーワードが含まれています。 ただし、使用しているクエリ プロバイダーが階層的な行セットをサポートしている場合は、FLATTENED キーワードを使用する必要はありません。  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  入れ子になったテーブル列の名前 `[SUPPORT]` および `[PROBABILITY]` は、同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
 例の結果を次に示します。  
  
|MODEL_CATALOG|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|案件あたりの平均時間|Missing|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|案件あたりの平均時間|< 64.7094100096|11|0.407407407|5|  
  
 ニューラル ネットワーク モデルのコンテキストにおけるスキーマ行セットの列の意味については、「 [ニューラル ネットワーク モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)というマイニング モデルを基にしています。  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:スキーマ行セットからモデル メタデータを取得する  
 データ マイニング スキーマ行セットに対してクエリを実行すると、DMX コンテンツ クエリで返されたのと同じ情報を取得できます。 ただし、スキーマ行セットから返される情報にはいくつかの追加の列があります 次のサンプル クエリは、モデルが作成された日、変更された日、および最後に処理された日を返します。 また、予測可能列 (モデル コンテンツから簡単に取得することはできません)、およびモデルの作成に使用されたパラメーターも返します。 この情報は、モデルのドキュメントを作成する場合に使用できます。  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 例の結果を次に示します。  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Average Time Per Issue,<br /><br /> Grade Of Service,<br /><br /> Number Of Orders|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:モデルの入力属性を取得する  
 モデルの作成に使用された入力属性と値のペアを取得するには、入力層 (NODE_TYPE = 18) の子ノード (NODE_TYPE = 20) に対してクエリを実行します。 次のクエリは、ノード記述から入力属性の一覧を返します。  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 例の結果を次に示します。  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Average Time Per Issue=64.7094100096 - 77.4002099712|  
|Day Of Week=Fri.|  
|Level 1 Operators|  
  
 ここでは結果からいくつかの代表的な行のみを示していますが、 NODE_DESCRIPTION で提供される情報が入力属性のデータ型によって少しずつ異なることがわかります。  
  
-   属性が不連続値または分離された値の場合は、属性とその値または分離された範囲が返されます。  
  
-   属性が連続する数値データ型の場合は、NODE_DESCRIPTION に属性名のみが含まれます。 ただし、入れ子になった NODE_DISTRIBUTION テーブルを取得して平均を求めたり、NODE_RULE を返して数値範囲の最小値と最大値を取得したりすることは可能です。  
  
 次のクエリは、入れ子になった NODE_DISTRIBUTION テーブルに対してクエリを実行して、属性とその値を別々の列に返す方法を示しています。 連続属性の場合、属性の値は平均で表されます。  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 例の結果を次に示します。  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|案件あたりの平均時間|64.7094100096 - 77.4002099712|  
|Day Of Week|Fri.|  
|Level 1 Operators|3.2962962962963|  
  
 範囲の最小値と最大値は NODE_RULE 列に格納され、次の例のように XML フラグメントとして表現されます。  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4:非表示層から重みを取得する  
 ニューラル ネットワーク モデルのモデル コンテンツは、ネットワーク内の任意のノードに関する詳細を取得しやすい構造になっています。 さらに、ノードの ID 番号の情報からも、ノードの種類間のリレーションシップを識別できます。  
  
 次のクエリは、非表示層の特定のノードに格納された係数を取得する方法を示しています。 非表示層は、メタデータのみを含むオーガナイザー ノード (NODE_TYPE = 19)、および属性と値のさまざまな組み合わせの係数を含む複数の子ノード (NODE_TYPE = 22) で構成されます。 このクエリは、係数のノードだけを返します。  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 例の結果を次に示します。  
  
|NODE_UNIQUE_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 ここに示した結果の一部は、ニューラル ネットワーク モデルのコンテンツで非表示ノードが入力ノードにどのように関係しているかを示しています。  
  
-   非表示層のノードの一意な名前は、常に 70000000 で始まります。  
  
-   入力層のノードの一意な名前は、常に 60000000 で始まります。  
  
 したがって、これらの結果から、ID 70000000200000000 で表されるノードには 6 つの異なる係数 (VALUETYPE = 7) が渡されていることがわかります。 係数の値は、ATTRIBUTE_VALUE 列に含まれています。 どの入力属性の係数かは、ATTRIBUTE_NAME 列のノード ID を使用して判断できます。 たとえば、ノード ID 6000000000000000a は、入力属性と値を参照します。 `Day of Week = 'Tue.'` ノード ID を使用してクエリを作成したり、 [Microsoft 汎用コンテンツ ツリー ビューアー](../microsoft-generic-content-tree-viewer-data-mining.md)を使用してノードを参照したりすることができます。  
  
 同様に、出力層 (NODE_TYPE = 23) のノードの NODE_DISTRIBUTION テーブルに対してクエリを実行すると、各出力値の係数を確認できます。 ただし、出力層では、ポインターが非表示層のノードを参照します。 詳細については、「 [ニューラル ネットワーク モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)というマイニング モデルを基にしています。  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>ニューラル ネットワーク モデルを使用した予測の作成  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムでは、分類と回帰の両方がサポートされています。 これらのモデルで予測関数を使用して、新しいデータを提供したり、単一予測またはバッチ予測を作成したりすることができます。  
  
###  <a name="bkmk_Query5"></a> サンプル クエリ 5:単一予測を作成する  
 ニューラル ネットワーク モデルに対する予測クエリを作成する最も簡単な方法は、予測クエリ ビルダーを使用することです。このビルダーは、 **および** のデータ マイニング デザイナーの [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [マイニング予測] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]タブで使用できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク ビューアーでモデルを参照し、関心のある属性をフィルター選択して傾向を表示します。その後、 **[マイニング予測]** タブに切り替えて、クエリを作成し、それらの傾向について新しい値を予測できます。  
  
 たとえば、コール センター モデルを参照して、注文数とその他の属性の相関関係を表示できます。 これを行うには、モデルを開き、ビューアーでの**入力**、 **\<すべて >** します。  次に、 **[出力]** で **[注文数]** を選択します。 **[値 1]** で最も注文が多い範囲を選択し、 **[値 2]** で最も注文が少ない範囲を選択します。 これにより、モデルで注文数と相関関係があるすべての属性がひとめでわかります。  
  
 ビューアーで結果を参照すると、特定の曜日に注文数が少ないこと、およびオペレーターの増員と売上の向上に相関関係がありそうなことがわかります。 この場合、モデルに対する予測クエリを使用して "what if" 仮説を試し、注文数が少ない曜日にレベル 2 のオペレーターを増員すると注文が増加するかどうかを確認できます。 これを行うには、次のようなクエリを作成します。  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 例の結果を次に示します。  
  
|Predicted Orders|確率|  
|----------------------|-----------------|  
|364|0.9532...|  
  
 この予測された売上高は火曜日の現在の売上高の範囲より高くなり、予測の確率は非常に高い値を示しています。 ただし、バッチ処理を使用して複数の予測を作成し、モデルに対してさまざまな仮説を試す必要がある場合もあります。  
  
> [!NOTE]  
>  Excel 2007 用データ マイニング アドインで提供されるロジスティック回帰ウィザードを使用すると、サービス グレードを特定のシフトのターゲット レベルまで引き上げるにはレベル 2 のオペレーターが何人必要になるかなど、複雑な質問に対する回答を簡単に求めることができます。 データ マイニング アドインは、無料でダウンロードできます。これらのアドインには、ニューラル ネットワークまたはロジスティック回帰アルゴリズムに基づいたウィザードが含まれています。 詳細については、「 [Office 2007 用データ マイニング アドイン](https://go.microsoft.com/fwlink/?LinkID=117790) 」の Web サイトを参照してください。  
  
## <a name="list-of-prediction-functions"></a>予測関数の一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムでは、このアルゴリズムに固有の予測関数はありませんが、次の表のような関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|あるノードがニューラル ネットワーク グラフ内の別のノードの子であるかどうかを示します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|重み付け確率を返します。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|現在の予測値に関連する値のテーブルを返します。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|予測値の分散を返します。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|予測値の確率を返します。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|予測された値の標準偏差を返します。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|ニューラル ネットワーク モデルとロジスティック回帰モデルの場合、モデル全体のトレーニング セットのサイズを表す 1 つの値を返します。|  
  
 特定の関数の構文については、「[データ マイニング拡張機能 &#40;DMX&#41; 関数リファレンス](/sql/dmx/data-mining-extensions-dmx-function-reference)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md)   
 [ニューラル ネットワーク モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [レッスン 5: ニューラル ネットワーク モデルとロジスティック回帰モデルを構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
