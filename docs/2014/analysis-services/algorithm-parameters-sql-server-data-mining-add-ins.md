---
title: アルゴリズム パラメーター (SQL Server データ マイニング アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e902272c58f1e841a3108199e53d51ac12f8ae4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062596"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>アルゴリズム パラメーター (SQL Server データ マイニング アドイン)
  Excel 用のテーブル分析ツールを使用してデータ マイニングを実行する場合は、データ マイニングのアルゴリズムまたはパラメーターを構成する必要はありません。各ツールによってデータが分析され、最適なパラメーターが自動的に選択されます。 ただし、モデルを修正する場合や、マイニング モデルを最初から作成する場合に備えて、Excel 用のデータ マイニング クライアントにはカスタマイズのためのオプションがいくつか用意されています。  
  
-   クリックして、データ マイニング モデルを手動で作成**詳細設定**  をクリックし、**構造にモデルの追加**します。  
  
-   モデリング ウィザードのいずれかをデータ マイニング クライアントで使用し、をクリックして**パラメーター**の動作を制御する、[!INCLUDE[msCoName](../includes/msconame-md.md)]データ マイニング アルゴリズム。  
  
-   をクリックして**クエリ**クエリ モデル ウィザードを開き、クリックして **[詳細設定]** を開く、**データ マイニング詳細クエリ エディター**します。 このエディターでは、DMX テンプレートを使用してモデルを作成できます。  
  
 作成済みのマイニング モデルの動作を変更することや、マイニング モデル ビューアーでパラメーターを設定して結果をフィルター処理することもできます。  
  
## <a name="list-of-algorithm-parameters"></a>アルゴリズム パラメーターの一覧  
 すべての [!INCLUDE[msCoName](../includes/msconame-md.md)] アルゴリズムは、パラメーターを設定することでカスタマイズできます。 最適なパラメーター設定はデータの構成によって異なるため、パラメーターを変更した場合の影響についてはここでは詳しく説明しません。  
  
 次の表では、パラメーターの一覧を示して個々の機能について説明し、詳細な技術情報へのリンクを示します。  
  
|[パラメーター名]|使用される場所|説明|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Microsoft Time Series アルゴリズム|周期性を検出するために使用する 0 から 1 までの数値を指定します。 1 に近い値を設定するには、多くのほぼ周期的なパターンの検出と周期性のヒントの自動生成が優先されます。 周期性のヒントを多数処理すると、モデルのトレーニングに非常に長い時間がかかりますが、精度の高いモデルになる可能性があります。 より 0 に近い値を設定すると、周期性の高いデータのみを対象にして周期性が検出されます。<br /><br /> 既定値は 0.6 です。|  
|CLUSTER_COUNT|Microsoft クラスタリング アルゴリズム<br /><br /> 「Microsoft シーケンス クラスター アルゴリズム」|アルゴリズムによって作成されるクラスターの概数を指定します。 その数のクラスターをデータから作成できない場合は、可能な限り多数のクラスターが作成されます。 CLUSTER_COUNT を 0 に設定すると、アルゴリズムではヒューリスティックを使用して、作成するクラスターの数が最適に決定されます。<br /><br /> 既定値は 10 です。|  
|CLUSTER_SEED|Microsoft クラスタリング アルゴリズム|モデル作成の初期段階にクラスターをランダムに生成するために使用するシード数を指定します。<br /><br /> 既定値は 0 です。|  
|CLUSTERING_METHOD|Microsoft クラスタリング アルゴリズム|アルゴリズムで使用するクラスタリング手法を指定します。 使用可能なクラスタリング手法は、スケーラブル EM (1)、非スケーラブル EM (2)、スケーラブル K-Means (3)、および非スケーラブル K-Means (4) です。<br /><br /> 既定値は 1 です。|  
|COMPLEXITY_PENALTY|Microsoft デシジョン ツリー アルゴリズム<br /><br /> Microsoft Time Series アルゴリズム|デシジョン ツリーの拡大を制御します。 値を小さくすると分割数が増加し、値を大きくすると分割数が減少します。 次に示すように、既定値は特定のモデルの属性数に基づいて決定されます。<br /><br /> 属性数が 1 ～ 9 の場合、既定値は 0.5 です。<br /><br /> 属性数が 10 ～ 99 の場合、既定値は 0.9 です。<br /><br /> 属性数が 100 以上の場合、既定値は 0.99 です。<br /><br /> 注:タイム シリーズ モデルでは、このパラメーターは、または混合モデルを ARTxp アルゴリズムを使用して作成されたモデルにのみ適用されます。|  
|FORCED_REGRESSOR|Microsoft デシジョン ツリー アルゴリズム<br /><br /> Microsoft 線形回帰アルゴリズム|アルゴリズムによって計算された列の重要度に関係なく、指定した列をアルゴリズムでリグレッサーとして使用するように設定します。<br /><br /> 注:このパラメーターは、連続属性を予測するデシジョン ツリーでのみ使用します。 定義上、線形回帰モデルは、連続属性を予測する特殊なデシジョン ツリーです。 ただし、どのデシジョン ツリー モデルにも、線形回帰式を表すノードが含まれている可能性があります。|  
|FORECAST_METHOD|Microsoft Time Series アルゴリズム|予測の作成に、ARTxp アルゴリズム、ARIMA アルゴリズム、または両者の組み合わせのどれを使用するかを指定します。<br /><br /> 既定値は MIXED です。|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|入力ニューロンおよび出力ニューロンに対する非表示ニューロンの比率を指定します。 次の式で、非表示層のニューロンの最初の数を求めます。<br /><br /> HIDDEN_NODE_RATIO * SQRT (入力ニューロンの総数 \* 出力ニューロンの総数)<br /><br /> 既定値は、4.0 です。|  
|HISTORIC_MODEL_COUNT|Microsoft Time Series アルゴリズム|作成する履歴モデルの数を指定します。<br /><br /> 既定値は 1 です。|  
|HISTORICAL_MODEL_GAP|Microsoft Time Series アルゴリズム|2 つの連続した履歴モデル間のタイム ラグを指定します。 たとえば、この値を g に設定すると、g、2*g、3\*g などの間隔でタイム スライスによって切り捨てられるデータに対して履歴モデルが作成されます。<br /><br /> 既定値は 10 です。|  
|HOLDOUT_PERCENTAGE|Microsoft ロジスティック回帰アルゴリズム<br /><br /> Microsoft Neural Network Algorithm|提示されたエラーの計算に使用するトレーニング データ内のケースの割合を指定します。この割合は、マイニング モデルのトレーニング中に停止条件の一部として使用されます。<br /><br /> 既定値は、30 です。<br /><br /> 注:このパラメーターは、マイニング構造に適用される提示データ割合値と異なります。|  
|HOLDOUT_SEED|Microsoft ロジスティック回帰アルゴリズム<br /><br /> Microsoft Neural Network Algorithm|アルゴリズムが予約データをランダムに調べるときに使用する擬似乱数ジェネレーターのシード値を指定します。 このパラメーターを 0 に設定すると、アルゴリズムによってマイニング モデルの名前に基づいたシードが生成され、再処理中にモデルのコンテンツが変更されることはありません。<br /><br /> 既定値は 0 です。<br /><br /> 注:このパラメーターは、マイニング構造に適用される提示データのシード値と異なります。|  
|INSTABILITY_SENSITIVITY|Microsoft Time Series アルゴリズム|予測の分散が一定のしきい値を超え、ARTxp アルゴリズムで予測が非表示化されるポイントを制御します。 既定値は 1 です。<br /><br /> 注:このパラメーターは、混合モデルまたは ARTxp アルゴリズムを使用するモデルにのみ適用されます。|  
|MAXIMUM_INPUT_ATTRIBUTES|Microsoft クラスタリング アルゴリズム<br /><br /> Microsoft デシジョン ツリー アルゴリズム<br /><br /> Microsoft 線形回帰アルゴリズム<br /><br /> Microsoft Na&#239;</ph>ve Bayes アルゴリズム<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft ロジスティック回帰アルゴリズム|選択した機能を呼び出す前にアルゴリズムが処理できる入力属性の数を定義します。 この値を 0 に設定すると、機能の選択がオフになります。<br /><br /> 既定値は 255 です。|  
|MAXIMUM_ITEMSET_COUNT|Microsoft アソシエーション アルゴリズム|生成されるアイテムセットの最大数を指定します。 数が指定されていない場合、アルゴリズムは生成可能なアイテムセットをすべて生成します。<br /><br /> 既定値は 200000 です。|  
|MAXIMUM_ITEMSET_SIZE|Microsoft アソシエーション アルゴリズム|アイテムセットで使用できるアイテムの最大数を指定します。 この値を 0 に設定すると、アイテムセットのサイズに制限がなくなります。<br /><br /> 既定値は 3 です。|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Microsoft デシジョン ツリー アルゴリズム<br /><br /> Microsoft 線形回帰アルゴリズム<br /><br /> Microsoft ロジスティック回帰アルゴリズム<br /><br /> Microsoft Na&#239;</ph>ve Bayes アルゴリズム<br /><br /> Microsoft Neural Network Algorithm|選択した機能を呼び出す前にアルゴリズムが処理できる出力属性の数を定義します。 この値を 0 に設定すると、機能の選択がオフになります。<br /><br /> 既定値は 255 です。|  
|MAXIMUM_SEQUENCE_STATES|「Microsoft シーケンス クラスター アルゴリズム」|シーケンスの状態の最大数を指定します。 この値を 100 より大きい数値に設定すると、アルゴリズムは意味のある情報を提供するモデルを作成できなくなります。<br /><br /> 既定値は、64 です。|  
|MAXIMUM_SERIES_VALUE|Microsoft Time Series アルゴリズム|予測に使用する最大値を指定します。 このパラメーターを MINIMUM_SERIES_VALUE と共に使用すると、予測が所定の範囲内に制約されます。 たとえば、日次の予測販売数量が製品の在庫数を超えないように指定することができます。|  
|MAXIMUM_STATES|Microsoft クラスタリング アルゴリズム<br /><br /> Microsoft Neural Network Algorithm<br /><br /> 「Microsoft シーケンス クラスター アルゴリズム」|アルゴリズムによってサポートされる属性状態の最大数を指定します。 属性の状態の数が状態の最大数よりも大きい場合は、アルゴリズムは、属性の最も一般的な状態を使用し、残りの状態を無視します。<br /><br /> 既定値は、100 です。|  
|MAXIMUM_SUPPORT|Microsoft アソシエーション アルゴリズム|アイテムセットがサポートされるケースの最大数を指定します。 この値が 1 より小さい場合、値はケースの総数の割合を表します。 この値が 1 より大きい場合、アイテムセットを含めることができるケースの絶対数を表します。<br /><br /> 既定値は 1 です。|  
|MINIMUM_IMPORTANCE|Microsoft アソシエーション アルゴリズム|アソシエーション ルールの重要度のしきい値を指定します。 重要度がこの値より低いルールは除外されます。|  
|MINIMUM_ITEMSET_SIZE|Microsoft アソシエーション アルゴリズム|アイテムセットで使用できるアイテムの最小数を指定します。<br /><br /> 既定値は 1 です。|  
|MINIMUM_DEPENDENCY_PROBABILITY|Microsoft Na&#239;</ph>ve Bayes アルゴリズム|入力属性と出力属性間の依存関係の最小確率を指定します。 この値は、アルゴリズムによって生成されるコンテンツのサイズを制限するために使用されます。 このプロパティは 0 ～ 1 の範囲で設定できます。 値を大きくすると、モデルのコンテンツの属性数が減ります。<br /><br /> 既定値は 0.5 です。|  
|MINIMUM_PROBABILITY|Microsoft アソシエーション アルゴリズム|ルールが true である最小確率を指定します。 たとえば、この値を 0.5 に設定するには、確率が 50% より低いルールを生成しないことを指定します。<br /><br /> 既定値は 0.4 です。|  
|MINIMUM_SERIES_VALUE|Microsoft Time Series アルゴリズム|時系列予測に対する下限の制約を指定します。 予測値がこの制約を下回ることはありません。|  
|MINIMUM_SUPPORT|Microsoft アソシエーション アルゴリズム|アルゴリズムによってルールが生成される前に、アイテムセットを含む必要があるケースの最小数を指定します。 この値を 1 より小さい値に設定すると、ケースの最小数がケースの総数の割合として指定されます。 この値を 1 より大きい整数に設定すると、ケースの最小数がアイテムセットを含む必要のあるケースの絶対数として指定されます。 メモリに制限がある場合は、アルゴリズムによってこのパラメーターが大きな値に設定されることがあります。<br /><br /> 既定値は 0.03 です。|  
|MINIMUM_SUPPORT|Microsoft クラスタリング アルゴリズム|各クラスターのケースの最小数を指定します。<br /><br /> 既定値は 1 です。|  
|MINIMUM_SUPPORT|Microsoft デシジョン ツリー アルゴリズム|デシジョン ツリー内で分割を生成するために必要なリーフ ケースの最小数を決定します。<br /><br /> 既定値は 10 です。|  
|MINIMUM_SUPPORT|「Microsoft シーケンス クラスター アルゴリズム」|各クラスターのケースの最小数を指定します。<br /><br /> 既定値は 10 です。|  
|MINIMUM_SUPPORT|Microsoft Time Series アルゴリズム|各タイム シリーズ ツリーで分割を生成するために必要なタイム スライスの最小数を指定します。<br /><br /> 既定値は 10 です。|  
|MISSING_VALUE_SUBSTITUTION|Microsoft Time Series アルゴリズム|履歴データのギャップを埋めるために使用する方法を指定します。 既定では、データに不規則なギャップや不揃いな境界があることは許されません。 不規則なギャップや境界を埋めるには、以前の値、平均値、または特定の数値定数を使用します。|  
|MODELLING_CARDINALITY|Microsoft クラスタリング アルゴリズム|クラスタリング処理中に作成されるサンプル モデルの数を指定します。<br /><br /> 既定値は 10 です。|  
|PERIODICITY_HINT|Microsoft Time Series アルゴリズム|データの周期性に関して、アルゴリズムにヒントを提供します。 たとえば、売上が年ごとに異なり、シリーズの単位が月である場合、周期性は 12 です。 このパラメーターの形式は {n [, n]} です。ここで、n には正の値を指定します。 角かっこ ([]) 内の n は省略可能で、必要なだけ繰り返すことができます。<br /><br /> 既定値は {1} です。|  
|PREDICTION_SMOOTHING|Microsoft Time Series アルゴリズム|ARTxp および ARIMA タイム シリーズ アルゴリズムの組み合わせを制御します。 指定した値は、FORECAST_METHOD パラメーターが MIXED に設定されている場合にのみ有効となります。 値は 0 から 1 までの範囲で指定する必要があります。 値が 0 の場合は、ARTxp のみがモデルで使用されます。 値が 1 の場合は、ARIMA のみがモデルで使用されます。 値が 0 に近づくほど、ARTxp が使用される割合が高くなります。 値が 1 に近づくほど、ARIMA が使用される割合が高くなります。|  
|SAMPLE_SIZE|Microsoft クラスタリング アルゴリズム|CLUSTERING_METHOD パラメーターをスケーラブルなクラスタリング手法のいずれかに設定する場合に、アルゴリズムにより各パスで使用されるケースの数を指定します。 SAMPLE_SIZE パラメーターを 0 に設定すると、データセット全体が単一のパスでクラスター化されます。 この場合、メモリとパフォーマンスに関する問題が生じる可能性があります。<br /><br /> 既定値は 50000 です。|  
|SAMPLE_SIZE|Microsoft ロジスティック回帰アルゴリズム<br /><br /> Microsoft Neural Network Algorithm|モデルのトレーニングに使用するケースの数を指定します。 アルゴリズム プロバイダーでは、この数と、HOLDOUT_PERCENTAGE パラメーターで指定された割合に含まれないケースの総数の割合のうち、いずれか小さい方が使用されます。<br /><br /> たとえば、HOLDOUT_PERCENTAGE が 30 に設定されている場合、アルゴリズムでは、このパラメーターの値と、ケースの総数の 70% に相当する値のうち、いずれか小さい方が使用されます。<br /><br /> 既定値は 10000 です。|  
|SCORE_METHOD|Microsoft デシジョン ツリー アルゴリズム|分割スコアを計算するために使用する方法を決定します。 使用できるオプションは以下のとおりです。(1) エントロピ、(2) K2 事前、または前の (3) ベイズ ディリクレ相当 (BDE) したベイズ定理します。<br /><br /> 既定値は 3 です。|  
|SPLIT_METHOD|Microsoft デシジョン ツリー アルゴリズム|ノードを分割するために使用する方法を決定します。 使用できるオプションは以下のとおりです。バイナリ (1)、完全な (2)、または両方 (3)。<br /><br /> 既定値は 3 です。|  
|STOPPING_TOLERANCE|Microsoft クラスタリング アルゴリズム テクニカル リファレンス|収束に到達し、アルゴリズムによるモデルの作成が完了する時点を決定するための値を指定します。 収束に到達するのは、クラスターの確率の全体的な変化が、モデルのサイズで除算された STOPPING_TOLERANCE パラメーターの比率に満たないときです。<br /><br /> 既定値は 10 です。|  
  
### <a name="comments"></a>コメント  
 アルゴリズムの詳細については、SQL Server オンライン ブックを参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム&#40;SQL Server データ マイニング アドイン&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
