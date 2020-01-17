---
title: ロジスティック回帰モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- content queries [DMX]
ms.assetid: 7c8e13a3-5c67-46c2-abfa-4881e6ef9c62
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d156a8f015a45ca257bf4f988cf69d229eafe5f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084227"
---
# <a name="logistic-regression-model-query-examples"></a>ロジスティック回帰モデルのクエリ例
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、分析で検出されたパターンの詳細情報を取得できます。予測クエリでは、モデル内のパターンを使用して新しいデータによる予測を行うことができます。  
  
 ここでは、Microsoft ロジスティック回帰アルゴリズムに基づいたモデルに対するクエリの作成方法について説明します。  
  
 **コンテンツ クエリ**  
  
 [データ マイニング スキーマ行セットを使用してモデル パラメーターを取得する](#bkmk_Query1)  
  
 [DMX を使用してモデルに関する追加の詳細情報を検索する](#bkmk_Query2)  
  
 **予測クエリ**  
  
 [連続値の予測を作成する](#bkmk_Query3)  
  
 [不連続値の予測を作成する](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> ロジスティック回帰モデルに関する情報を取得する  
 ロジスティック回帰モデルは、Microsoft ニューラル ネットワーク アルゴリズムでパラメーターの特殊なセットを使用して作成されます。そのため、ロジスティック回帰モデルには、ニューラル ネットワーク モデルと同じ情報がいくつか含まれますが、ニューラル ネットワーク モデルほど複雑ではありません。 モデル コンテンツの構造および各種類のノードに格納されている情報の種類については、「 [ロジスティック回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-logistic-regression-models.md)」を参照してください。  
  
 クエリのシナリオで作業を進めるには、中級者向けデータ マイニング チュートリアルの次のセクションで説明したロジスティック回帰モデルを作成できます。[レッスン 5: ニューラル ネットワーク モデルとロジスティック回帰モデルを構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)します。  
  
 また、「 [基本的なデータ マイニング チュートリアル](../../tutorials/basic-data-mining-tutorial.md)」のマイニング構造 Targeted Mailing を使用することもできます。  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:データ マイニング スキーマ行セットを使用してモデル パラメーターを取得する  
 データ マイニング スキーマ行セットに対してクエリを実行すると、モデルに関するメタデータを取得できます (作成された日時、最後に処理された日時、基になるマイニング構造の名前、予測可能な属性として使用されている列の名前など)。 次の例では、モデルが最初に作成されたときに使用されたパラメーター、モデルの名前と種類、およびモデルが作成された日付が返されます。  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 サンプルの結果 :  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:DMX を使用してモデルに関する追加の詳細情報を検索する  
 次のクエリは、ロジスティック回帰モデルに関する基本的な情報を返します。 ロジスティック回帰モデルは、入力として使用される値を表すマージナル統計ノード (NODE_TYPE = 24) がある点など、多くの点でニューラル ネットワーク モデルに似ています。 このサンプル クエリでは、Targeted Mailing モデルを使用し、入れ子になったテーブル NODE_DISTRIBUTION から入力値を取得することにより、すべての入力値を取得します。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 結果の一部 :  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Age|Missing|0|0|0|1|  
|Age|45.43491192|17484|1|126.9544114|3|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Commute Distance|Missing|0|0|0|1|  
|Commute Distance|5-10 Miles|3033|0.173472889|0|4|  
  
 実際のクエリではさらに多くの行が返されますが、このサンプルでは、入力に関して提供される情報の種類の例を示しています。 不連続入力については、可能性のある各値を表に示しています。 Age などの連続値入力については、完全な一覧を示すことはできないので、入力を平均として分離しています。 マージナル統計ノードでの情報の使用方法の詳細については、「[ロジスティック回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-logistic-regression-models.md)」を参照してください。  
  
> [!NOTE]  
>  結果は見やすくするためにフラット化されていますが、プロバイダーが階層的な行セットをサポートしている場合は、1 つの列で入れ子になったテーブルを返すことができます。  
  
## <a name="prediction-queries-on-a-logistic-regression-model"></a>ロジスティック回帰モデルに対する予測クエリ  
 すべての種類のマイニング モデルで [Predict (DMX)](/sql/dmx/predict-dmx) 関数を使用して、モデルに新しいデータを提供し、新しい値に基づいて予測を作成できます。 また、予測が正しい確率など、予測に関する追加情報を返す関数も使用できます。 ここでは、ロジスティック回帰モデルでの予測クエリの例をいくつか紹介します。  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:連続値の予測を作成する  
 ロジスティック回帰は入力と予測の両方について連続属性の使用をサポートしているため、データ内のさまざまな要素を相互に関連付けるモデルを簡単に作成できます。 予測クエリを使用して、これらの要素間のリレーションシップを調査できます。  
  
 次のサンプル クエリは、中級者向けチュートリアルの Call Center モデルに基づいており、金曜日の午前のシフトについてのサービス グレードを予測する単一クエリを作成します。 [PredictHistogram (DMX)](/sql/dmx/predicthistogram-dmx) 関数は入れ子になったテーブルを返します。このテーブルには、予測される値の有効性の理解に関連する統計が含まれます。  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 サンプルの結果 :  
  
 **サービス グレードを予測**:0.102601830123659  
  
 **結果**  
  
|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 入れ子になった NODE_DISTRIBUTION テーブルの確率、サポート、および標準偏差値の詳細については、「 [ロジスティック回帰モデルのマイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-for-logistic-regression-models.md)」を参照してください。  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4:不連続値の予測を作成する  
 ロジスティック回帰は、バイナリ結果を構成する要素を分析するシナリオでよく使用されます。 チュートリアルで使用されているモデルは連続値 **ServiceGrade**を予測しますが、現実のシナリオでは、サービス グレードがいくつかの分離した目標値を満たすかどうかを予測するモデルを設定することが必要になります。 または、連続値を使用して予測を出力し、後で予測された出力を **Good**、 **Fair**、または **Poor**にグループ化することもできます。  
  
 次のサンプルは、予測可能な属性をグループ化する方法をどのように変更するかを示しています。 これを行うには、マイニング構造のコピーを作成し、目的の列の分離方法を変更して、値が連続的ではなく、グループ化されるようにします。  
  
 次の手順は、Call Center データの Service Grade 値のグループ化を変更する方法を示しています。  
  
##### <a name="to-create-a-discretized-version-of-the-call-center-mining-structure-and-models"></a>Call Center のマイニング構造およびモデルの分離バージョンを作成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のソリューション エクスプローラーで、 **[マイニング構造]** を展開します。  
  
2.  Call Center.dmm を右クリックして、 **[コピー]** を選択します。  
  
3.  **[マイニング構造]** を右クリックし、 **[貼り付け]** をクリックします。 Call Center 1 という名前の新しいマイニング構造が追加されます。  
  
4.  新しいマイニング構造を右クリックし、 **[名前の変更]** をクリックします。 新しい名前として「 **Call Center Discretized**」と入力します。  
  
5.  新しいマイニング構造をダブルクリックしてデザイナーで開きます。 すべてのマイニング モデルがコピーされ、拡張子 1 が付いていることに注目してください。 ここでは、名前をそのままにします。  
  
6.  **[マイニング構造]** タブで、Service Grade の列を右クリックし、 **[プロパティ]** をクリックします。  
  
7.  変更、`Content`プロパティから**Continuous**に**Discretized**します。 変更、`DiscretizationMethod`プロパティを**クラスター**します。 Discretization BucketCount に「 **3**」と入力します。  
  
    > [!NOTE]  
    >  これらのパラメーターは、プロセスを説明するために使用されており、有効なモデルを生成するとは限りません。  
  
8.  **[マイニング モデル]** メニューの **[構造および全モデルの処理]** をクリックします。  
  
 次のサンプル クエリは、この分離モデルに基づいており、指定した曜日のサービス グレードと、各予測出力の確率を予測します。  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 期待される結果:  
  
 **予測**  
  
|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 予測結果は、指定どおりに 3 つのカテゴリにグループ化されています。ただし、このグループ化は、データの実際の値のクラスタリングに基づくものであり、ビジネスの目標として設定できる任意の値に基づくものではありません。  
  
## <a name="list-of-prediction-functions"></a>予測関数の一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 これに加え、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ロジスティック回帰アルゴリズムでは、次の表に示す関数もサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|あるノードがモデル内の別のノードの子であるかどうかを示します。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|指定された状態の調整済みの確率を返します。|  
|[PredictHistogram (DMX)](/sql/dmx/predicthistogram-dmx)|指定された列に対して、予測された値、または値のセットを返します。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|指定された状態の確率を返します。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|予測された値の標準偏差を返します。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|指定された状態に対するサポート値を返します。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|指定された列の分散を返します。|  
  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムに共通の関数の一覧については、「[一般的な予測関数 (DMX)](/sql/dmx/general-prediction-functions-dmx)」を参照してください。 特定の関数の構文については、「[データ マイニング拡張機能 (DMX) 関数リファレンス](/sql/dmx/data-mining-extensions-dmx-function-reference)」を参照してください。  
  
> [!NOTE]  
>  ニューラル ネットワーク モデルとロジスティック回帰モデルの場合、[PredictSupport (DMX)](/sql/dmx/predictsupport-dmx) 関数はモデル全体のトレーニング セットのサイズを表す 1 つの値を返します。  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング クエリ](data-mining-queries.md)   
 [Microsoft ロジスティック回帰アルゴリズム](microsoft-logistic-regression-algorithm.md)   
 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](microsoft-logistic-regression-algorithm-technical-reference.md)   
 [ロジスティック回帰モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-logistic-regression-models.md)   
 [レッスン 5: ニューラル ネットワーク モデルとロジスティック回帰モデルを構築&#40;中級者向けデータ マイニング チュートリアル&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
