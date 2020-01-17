---
title: タイム シリーズ モデルのクエリ例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d7451c82261e23c75b748d4b1cde473191b7749
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082748"
---
# <a name="time-series-model-query-examples"></a>Time Series Model Query Examples
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、分析で検出されたパターンの詳細情報を取得できます。予測クエリでは、モデル内のパターンを使用して新しいデータについての予測を行うことができます。 たとえば、時系列モデルでコンテンツ クエリを使用すると、検出された周期的構造に関する追加情報を取得できます。一方、予測クエリを使用すると、次の 5 ～ 10 のタイム スライスの予測などを取得できます。 クエリを使用してモデルに関するメタデータを取得することもできます。  
  
 ここでは、Microsoft Time Series アルゴリズムに基づくモデルに対してこの両方の種類のクエリを作成する方法について説明します。  
  
 **コンテンツ クエリ**  
  
 [モデルの周期性のヒントを取得する](#bkmk_Query1)  
  
 [ARIMA モデルの式を取得する](#bkmk_Query2)  
  
 [ARTxp モデルの式を取得する](#bkmk_Query3)  
  
 **予測クエリ**  
  
 [時系列データを置換する場合と拡張する場合について理解する](#bkmk_ReplaceExtend)  
  
 [EXTEND_MODEL_CASES を使用した予測の作成](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES を使用した予測の作成](#bkmk_REPLACE)  
  
 [時系列モデルで不足値を置換する](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>時系列モデルに関する情報の取得  
 モデル コンテンツのクエリを使用すると、モデルに関する基本的な情報を取得できます (モデルの作成時に使用されたパラメーターや、モデルが最後に処理された時間など)。 以下の例は、データ マイニング スキーマ行セットを使用してモデル コンテンツのクエリを実行するための基本構文を示しています。  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1:モデルの周期性のヒントを取得する  
 時系列内で検出された周期性は、ARIMA ツリーや ARTXP ツリーに対してクエリを実行することによって取得できます。 しかし、完成したモデルの周期性は、モデルの作成時にヒントとして指定した周期性と同じであるとは限りません。 モデルの作成時にパラメーターとして指定されたヒントを取得するには、次の DMX ステートメントを使用して、マイニング モデル コンテンツ スキーマ行セットに対してクエリを実行します。  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 結果の一部 :  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0.1、MINIMUM_SUPPORT = 10、PERIODICITY_HINT ={1,3}、.|  
  
 既定の周期性のヒントである {1} は、すべてのモデルで表示されます。このサンプル モデルでは、そのほかにもう 1 つ追加のヒントが作成時に使用されています。これは、最終的なモデルには存在しない可能性があります。  
  
> [!NOTE]  
>  ここでは、読みやすくするために結果が切り捨てられています。  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2:ARIMA モデルの式を取得する  
 ARIMA モデルの式を取得するには、個々のツリーの任意のノードに対してクエリを実行します。 ARIMA モデル内の各ツリーは、それぞれ異なる周期性を表します。また、複数のデータ系列がある場合は、データ系列ごとに固有の周期性ツリーのセットがあります。 したがって、特定のデータ系列の式を取得するには、まずそのツリーを特定する必要があります。  
  
 たとえば、TA プレフィックスはノードが ARIMA ツリーの一部であることを示します。一方、TS プレフィックスは ARTXP ツリーで使用されます。 モデル コンテンツにクエリを実行して NODE_TYPE 値が 27 のノードを検索することで、すべての ARIMA ルート ツリーを見つけることができます。 また、ATTRIBUTE_NAME の値を使用して、特定のデータ系列の ARIMA ルート ノードを検索することもできます。 次のクエリ例は、ヨーロッパ地域における R250 モデルの販売数量を表す ARIMA ノードを検索します。  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 このノード ID を使用すると、このツリーの ARIMA 式に関する詳細を取得できます。 次の DMX ステートメントは、データ系列に対する ARIMA 式の短い形式を取得します。 入れ子になったテーブル NODE_DISTRIBUTION の切片を取得します。 この例では、固有 ID が TA00000007 のノードを参照することで式を取得します。 ただし、場合によっては異なるノード ID を使用する必要があります。その場合は、若干異なる結果がモデルから得られる可能性があります。  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 例の結果を次に示します。  
  
|Short equation|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24....|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 この情報の意味の詳細については、「 [タイム シリーズ モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)」を参照してください。  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3:ARTXP モデルの式を取得します。  
 ARTxp モデルでは、ツリーの各レベルにさまざまな情報が格納されます。 ARTxp モデルの構造と式の意味の詳細については、「[タイム シリーズ モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)」を参照してください。  
  
 次の DMX ステートメントは、ヨーロッパにおける R250 モデルの販売数量を表す ARTxp ツリーの情報の一部を取得します。  
  
> [!NOTE]  
>  入れ子になったテーブル列の名前 VARIANCE は、同名の予約済みキーワードと区別するために角かっこで囲む必要があります。 入れ子になったテーブル列の PROBABILITY および SUPPORT は、ほとんどのケースで空白であるため、含まれていません。  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 この情報の意味の詳細については、「 [タイム シリーズ モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="creating-predictions-on-a-time-series-model"></a>時系列モデルでの予測の作成  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]以降では時系列モデルに新しいデータを追加し、モデルに新しいデータを自動的に組み込むことができます。 次の 2 つの方法のいずれかで、時系列マイニング モデルに新しいデータを追加します。  
  
-   `PREDICTION JOIN` を使用してトレーニング データに外部ソースのデータを結合します。  
  
-   単一予測クエリを使用してデータにスライスを 1 つずつ指定します。 単一予測クエリを作成する方法については、次を参照してください。[データ マイニング クエリ インターフェイス](data-mining-query-tools.md)します。  
  
###  <a name="bkmk_ReplaceExtend"></a> 置換および拡張操作の動作について  
 時系列モデルに新しいデータを追加するときは、トレーニング データを拡張するか置換するかを指定できます。  
  
-   **拡張します。** データ系列を拡張すると[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]既存のトレーニング データの最後に、新しいデータを追加します。 トレーニング ケースの数も増加します。  
  
     モデル ケースの拡張は、新しいデータを使用して継続的にモデルを更新するときに便利です。 たとえば、トレーニング セットを時間の経過と共に成長させるには、単にモデルを拡張します。  
  
     データを拡張するには、時系列モデルに `PREDICTION JOIN` を作成し、新しいデータのソースを指定し、`EXTEND_MODEL_CASES` 引数を使用します。  
  
-   **置き換えます。** データ系列のデータを置き換えるときに[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]がトレーニング済みのモデルのままで新しいデータ値を使用して、既存のトレーニング ケースの一部またはすべてを置き換えます。 このためトレーニング データのサイズは変わりませんが、ケース自体は継続的に新しいデータに置換されます。 新しいデータを十分に提供すれば、まったく新しい系列でトレーニング データを置換できます。  
  
     1 セットのケースでモデルをトレーニングし、そのモデルを別のデータ系列に適用するときは、モデル ケースの置換が便利です。  
  
     データを置換するには、時系列モデルに `PREDICTION JOIN` を作成し、新しいデータのソースを指定し、`REPLACE_MODEL_CASES` 引数を使用します。  
  
> [!NOTE]  
>  新しいデータを追加するときは履歴予測を作成することはできません。  
  
 トレーニング データを拡張するか置換するかにかかわらず、予測は常に元のトレーニング セットの最後のタイムスタンプから開始されます。 つまり、新しいデータに n 個のタイム スライスが含まれていて 1 ～ n の時間ステップの予測を要求する場合、予測は新しいデータと同じ期間になり、新しい予測は取得されません。  
  
 新しいデータと重複しない期間の新しい予測を取得するには、タイム スライス n+1 から予測を開始するか、他のタイム スライスの要求を行うようにする必要があります。  
  
 たとえば、既存のモデルに 6 か月分のデータがあるとします。 過去 3 か月間の販売成績を追加してこのモデルを拡張し、 同時に、次の 3 か月間の予測も作成したいと考えています。 新しいデータを追加したときの新しい予測のみを取得するには、開始位置をタイム スライス 4、終了位置をタイム スライス 7 に指定します。 また、合計 6 つの予測を要求することもできますが、最初の 3 つのタイム スライスは追加した新しいデータと重複します。  
  
 クエリの例と詳細を使用する構文については`REPLACE_MODEL_CASES`と`EXTEND_MODEL_CASES`を参照してください[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)します。  
  
###  <a name="bkmk_EXTEND"></a> EXTEND_MODEL_CASES を使用した予測の作成  
 予測動作は、モデル ケースを拡張するか置換するかによって異なります。 モデルを拡張するときは、新しいデータは系列の末尾に追加され、トレーニング セットのサイズは増加します。 ただし、予測クエリに使用されるタイム スライスは常に元の系列の末尾から開始されます。 このため、3 つの新しいデータ ポイントを追加し、6 つの予測を要求した場合、返される最初の 3 つの予測は新しいデータと重複します。 この場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はすべての新しいデータ ポイントをすべて使用するまで予測を作成せずに実際の新しいデータ ポイントを返します。 その後、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は複合系列に基づいて予測を作成します。  
  
 この動作により新しいデータを追加して、予測を表示せずに予測チャート内に実際の販売成績を表示できます。  
  
 たとえば、3 つの新しいデータ ポイントを追加し 3 つの新しい予測を作成するには、次の操作を行います。  
  
-   時系列モデルに `PREDICTION JOIN` を作成し、3 か月の新しいデータのソースを指定します。  
  
-   6 つのタイム スライスの予測を要求します。 予測を要求するには、6 つのタイム スライスを指定します。このとき、開始位置がタイム スライス 1、終了位置がタイム スライス 7 です。 これは EXTEND_MODEL_CASES にのみ該当します。  
  
-   新しい予測のみを取得するには、開始位置に 4、終了位置に 7 を指定します。  
  
-   `EXTEND_MODEL_CASES` 引数を使用する必要があります。  
  
     最初の 3 つのタイム スライスについては実際の販売成績が返され、次の 3 つのタイム スライスについては拡張されたモデルに基づく予測が返されます。  
  
###  <a name="bkmk_REPLACE"></a> REPLACE_MODEL_CASES を使用した予測の作成  
 モデルのケースを置換するときは、モデルのサイズは同じですが、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってモデルの個々のケースが置換されます。 これは、トレーニング データ セットを一定のサイズに保持することが重要なクロス予測およびシナリオに便利です。  
  
 たとえば、ストアの 1 つの販売データが不十分であるとします。 特定の地域のすべてのストアの販売を平均し、モデルをトレーニングして、汎用モデルを作成できます。 次に、十分な販売データを使用しないでストアの予測を作成するには、そのストアだけの新しい販売データに対して `PREDICTION JOIN` を作成します。 このようにするとき、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では地域モデルから派生するパターンは保持されますが、既存のトレーニング ケースは個々のストアのデータで置換されます。 その結果、予測値は個々のストアの傾向を示す線に近づきます。  
  
 `REPLACE_MODEL_CASES` 引数を使用すると、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって継続して新しいケースがケース セットの末尾に追加され、対応する数がケース セットの先頭から削除されます。 新しいデータを元のトレーニング セットよりも多く追加する場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって最も古いデータが破棄されます。 新しい値が十分に提供された場合は、完全に新しいデータに基づいて予測を行うことができます。  
  
 たとえば、1000 行が含まれているケース データ セットにモデルをトレーニングするとします。 新しいデータ 100 行を追加します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ではトレーニング セットから最初の 100 行を削除し、合計 1000 行になるようにセットの末尾に新しいデータ 100 行を追加します。 新しいデータ 1100 行を追加した場合は、最新の 1000 行のみが使用されます。  
  
 別の例を示します。 新しい 3 か月分のデータを追加し、3 つの予測を新しく作成するには、次の操作を行います。  
  
-   時系列モデルに `PREDICTION JOIN` を作成し、`REPLACE_MODEL_CASE` 引数を使用します。  
  
-   3 か月の新しいデータのソースを指定します。 このデータは、元のトレーニング データとはまったく別のソースのものである場合があります。  
  
-   6 つのタイム スライスの予測を要求します。 予測を要求するには、6 つのタイム スライスを指定するか、開始位置をタイム スライス 1 に、終了位置をタイム スライス 7 に指定します。  
  
    > [!NOTE]  
    >  `EXTEND_MODEL_CASES` とは異なり、入力データとして追加したものと同じ値が返されることはありません。 返された 6 つの値はすべて、更新されたモデルに基づく予測です。これには古いデータと新しいデータが含まれます。  
  
    > [!NOTE]  
    >  REPLACE_MODEL_CASES では、タイムスタンプ 1 から開始すると、古いトレーニング データを置換する新しいデータに基づく新しい予測が取得されます。  
  
 クエリの例と詳細を使用する構文については`REPLACE_MODEL_CASES`と`EXTEND_MODEL_CASES`を参照してください[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)します。  
  
###  <a name="bkmk_MissingValues"></a> 時系列モデルで不足値を置換する  
 `PREDICTION JOIN` ステートメントを使用して時系列モデルに新しいデータを追加するとき、新しいデータセットに不足値があってはいけません。 系列が不完全である場合、モデルでは NULL、数値平均、特定の数値平均、予測値のいずれかを使用して不足値を指定する必要があります。 `EXTEND_MODEL_CASES` を指定する場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって不足値が元のモデルに基づく予測で置換されます。 使用する場合`REPLACE_MODEL_CASES`、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]欠損値で指定した値に置換、 *MISSING_VALUE_SUBSTITUTION*パラメーター。  
  
## <a name="list-of-prediction-functions"></a>予測関数の一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムでは、次の表のような追加の関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)|現在のケースの日付とトレーニング セットの最後の日付の間のタイム スライス数を返します。<br /><br /> この関数の一般的な使用方法は、最近のトレーニング ケースに関する詳細なデータを取得できるように、そのようなケースを判別することです。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|指定した予測可能列のノードの ID を返します。<br /><br /> この関数の一般的な使用目的は、特定の予測値を生成したノードを識別して、そのノードに関連付けられているケースの表示や、式などの詳細の取得ができるようにすることです。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|指定した予測可能列の予測の標準偏差を返します。<br /><br /> この関数を、時系列モデルでサポートされない INCLUDE_STATISTICS 引数の代わりに使用できます。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|指定した予測可能列の予測の分散を返します。<br /><br /> この関数を、時系列モデルでサポートされない INCLUDE_STATISTICS 引数の代わりに使用できます。|  
|[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)|時系列の予測される履歴値または将来の予測値を返します。<br /><br /> 汎用の予測関数である [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx) を使用して、時系列モデルに対するクエリを実行することもできます。|  
  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムに共通の関数の一覧については、「[一般的な予測関数 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)」を参照してください。 特定の関数の構文については、「[データ マイニング拡張機能 &#40;DMX&#41; 関数リファレンス](/sql/dmx/data-mining-extensions-dmx-function-reference)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ](data-mining-queries.md)   
 [Microsoft タイム シリーズ アルゴリズム](microsoft-time-series-algorithm.md)   
 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](microsoft-time-series-algorithm-technical-reference.md)   
 [タイム シリーズ モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
