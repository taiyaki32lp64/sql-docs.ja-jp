---
title: Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- HOLDOUT_PERCENTAGE parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- regression algorithms [Analysis Services]
- HOLDOUT_SEED parameter
ms.assetid: cf32f1f3-153e-476f-91a4-bb834ec7c88d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9d3dd4e9da0445f966e9e46013f0b7cd4998190
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083936"
---
# <a name="microsoft-logistic-regression-algorithm-technical-reference"></a>Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ロジスティック回帰アルゴリズムは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ニューラル ネットワーク アルゴリズムを変形したものです。このアルゴリズムでは、 *HIDDEN_NODE_RATIO* パラメーターは 0 に設定されています。 この設定により、非表示の層を含んでいない、ロジスティック回帰に相当するニューラル ネットワーク モデルが作成されます。  
  
## <a name="implementation-of-the-microsoft-logistic-regression-algorithm"></a>Microsoft ロジスティック回帰アルゴリズムの実装  
 予測可能列に状態が 2 つしか含まれていない場合に、予測可能列に特定の状態が含められる確率と入力列を関連付けて、回帰分析を実行する必要があるとします。 次の図は、予測可能列の状態に 1 と 0 を割り当て、この列に特定の状態が含められる確率を計算し、入力変数に対する線形回帰を実行した場合に得られる結果を示しています。  
  
 ![線形回帰を使用してデータをモデル化が不十分な](../media/logistic-linear-regression.gif "が不十分な線形回帰を使用してデータをモデル化")  
  
 x 軸には入力列の値が表示されます。 y 軸には、予測可能列が特定の状態またはもう一方の状態になる確率が表示されます。 この場合の問題は、列の最大値と最小値が 0 と 1 であっても、線形回帰によって列が 0 と 1 の間に制限されないことです。 この問題を解決するには、ロジスティック回帰を実行します。 ロジスティック回帰分析では、直線を作成するのではなく、制約の最大値と最小値を含んでいる "S" 字型曲線が作成されます。 たとえば、次の図は、前の例で使用したのと同じデータに対してロジスティック回帰を実行した場合に得られる結果を示しています。  
  
 ![ロジスティック回帰を使用してデータがモデル化](../media/logistic-regression.gif "ロジスティック回帰を使用してデータがモデル化")  
  
 曲線が 0 ～ 1 の範囲を超えていないことに注目してください。 ロジスティック回帰を使用して、予測可能列の状態の決定に重要な役割を果たす入力列を特定できます。  
  
### <a name="feature-selection"></a>機能の選択  
 機能の選択は、分析の向上と処理負荷の削減のためにすべての Analysis Services データ マイニング アルゴリズムで自動的に使用されます。 ロジスティック回帰モデルの機能の選択に使用される方法は、属性のデータ型によって異なります。 ロジスティック回帰は、Microsoft ニューラル ネットワーク アルゴリズムに基づいているため、ニューラル ネットワークに適用される機能の選択方法のサブセットを使用します。 詳細については、「[機能の選択 &#40;データ マイニング&#41;](feature-selection-data-mining.md)」を参照してください。  
  
### <a name="scoring-inputs"></a>入力のスコアリング  
 ニューラル ネットワーク モデルまたはロジスティック回帰モデルのコンテキストにおける "*スコアリング* " とは、データに存在する値を同じ尺度を使用する値のセットに変換して相互に比較できるようにするプロセスを意味します。 たとえば、Income に対する入力の範囲が 0 ～ 100,000 であるのに対し、[Number of Children] に対する入力の範囲は 0 ～ 5 であるとします。 この変換プロセスを使用する*スコア*、または値の違いに関係なく、各入力の重要性を比較します。  
  
 トレーニング セットに表示されている状態ごとに、モデルは 1 つの入力を生成します。 不連続な入力または分離された入力の場合、Missing 状態がトレーニング セットに 1 回以上表示されると、Missing 状態を表す追加の入力が作成されます。 連続する入力では、最大 2 つの入力ノードが作成されます。1 つはトレーニング データに存在する場合の Missing 値用の入力ノードで、もう 1 つはすべての既存の値 (Null 以外の値) 用の入力ノードです。 各入力は (μ) x、z スコア正規化法を使用して数値の書式にスケーリング/StdDev します。  
  
 z スコア正規化中に、トレーニング セット全体の平均 (μ) と標準偏差が取得されます。  
  
 **連続値**  
  
 値が存在します。 (X-μ)/σ//X はエンコードされている実際の値)  
  
 値が存在しません - μ/σ//負のミューをシグマで除算)。  
  
 **不連続値**  
  
 Μ = p - (状態の前の確率)  
  
 StdDev  = sqrt(p(1-p))  
  
 値が存在します。   (1-μ)/σ//(からミューを引いたもの) をシグマで除算)  
  
 値が存在しない (-μ)/σ/負のミューをシグマで除算)。  
  
### <a name="understanding-logistic-regression-coefficients"></a>ロジスティック回帰係数について  
 統計学の文献にはロジスティック回帰を実行するためのさまざまな方法が記されていますが、どの方法でも重要なのはモデルの適合性を評価する部分です。 適合度統計の中でも、オッズ比と共変量パターンを扱うものについて、さまざまな提案がなされています。 モデルの適合性を測定する方法についてはこのトピックでは扱いませんが、モデルの係数の値を取得し、それらの係数を使用して独自に適合性の測定方法を設計できます。  
  
> [!NOTE]  
>  ロジスティック回帰モデルの一部として作成される係数はオッズ比を表しているわけではなく、またそのように解釈すべきではありません。  
  
 モデル グラフ内の各ノードの係数は、そのノードへの入力の加重和を表します。 ロジスティック回帰モデルでは、非表示層が空であるため、出力ノードに 1 セットの係数だけが格納されます。 次のクエリを使用すると、係数の値を取得できます。  
  
```  
SELECT FLATTENED [NODE_UNIQUE NAME],  
(SELECT ATTRIBUTE_NAME< ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) AS t  
FROM <model name>.CONTENT  
WHERE NODE_TYPE = 23  
```  
  
 このクエリは、出力値ごとに、係数と、関連の入力ノードを指す ID を返します。 また、出力と切片の値を含む行も返します。 各入力 X が独自の係数 (Ci) が、入れ子になったテーブルには、次の式に従って計算された「空き」係数 (Co) も含まれています。  
  
 F (x) = X1 * C1 + X2\*C2 + + Xn\*Cn + X0  
  
 アクティブ化: exp(F(X)) / (1 + exp(F(X)) )  
  
 詳細については、「 [ロジスティック回帰モデルのクエリ例](logistic-regression-model-query-examples.md)」を参照してください。  
  
## <a name="customizing-the-logistic-regression-algorithm"></a>ロジスティック回帰アルゴリズムのカスタマイズ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ロジスティック回帰アルゴリズムでは、結果として得られるマイニング モデルの動作、パフォーマンス、および精度に影響を与えるいくつかのパラメーターがサポートされています。 また、入力として使用する列にモデリング フラグを設定して、モデルの動作を変更することもできます。  
  
### <a name="setting-algorithm-parameters"></a>アルゴリズム パラメーターの設定  
 次の表は、Microsoft ロジスティック回帰アルゴリズムで使用できるパラメーターを示しています。  
  
 HOLDOUT_PERCENTAGE  
 提示されたエラーの計算に使用するトレーニング データ内のケースの割合を指定します。 HOLDOUT_PERCENTAGE は、マイニング モデルのトレーニング中に停止条件の一部として使用されます。  
  
 既定値は 30 です。  
  
 HOLDOUT_SEED  
 予約データをランダムに調べるときに使用する擬似乱数ジェネレーターのシード値を指定します。 HOLDOUT_SEED を 0 に設定すると、アルゴリズムによってマイニング モデルの名前に基づいたシードが生成され、再処理中にモデルのコンテンツが変更されることはありません。  
  
 既定値は 0 です。  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 選択した機能を呼び出す前にアルゴリズムが処理できる入力属性の数を定義します。 この値を 0 に設定すると、機能の選択がオフになります。  
  
 既定値は 255 です。  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 選択した機能を呼び出す前にアルゴリズムが処理できる出力属性の数を定義します。 この値を 0 に設定すると、機能の選択がオフになります。  
  
 既定値は 255 です。  
  
 MAXIMUM_STATES  
 アルゴリズムによってサポートされる属性状態の最大数を指定します。 属性の状態の数が状態の最大数よりも大きい場合、アルゴリズムでは属性の最も一般的な状態が使用され、残りの状態は無視されます。  
  
 既定値は、100 です。  
  
 SAMPLE_SIZE  
 モデルのトレーニングに使用するケースの数を指定します。 アルゴリズム プロバイダーでは、この数と、HOLDOUT_PERCENTAGE パラメーターで指定された割合に含まれないケースの総数の割合のうち、いずれか小さい方が使用されます。  
  
 たとえば、HOLDOUT_PERCENTAGE が 30 に設定されている場合、アルゴリズムでは、このパラメーターの値と、ケースの総数の 70% に相当する値のうち、いずれか小さい方が使用されます。  
  
 既定値は 10000 です。  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ロジスティック回帰アルゴリズムでは、次のモデリング フラグを使用できます。  
  
 NOT NULL  
 列に NULL を含めることはできないことを示します。 モデルのトレーニング中に NULL が検出された場合はエラーが発生します。  
  
 マイニング構造列に適用されます。  
  
 MODEL_EXISTENCE_ONLY  
 列が、`Missing` および `Existing` の 2 つの可能な状態を持つ列として扱われることを示します。 NULL は Missing 値になります。  
  
 マイニング モデル列に適用されます。  
  
## <a name="requirements"></a>必要条件  
 ロジスティック回帰モデルには、キー列、入力列、および少なくとも 1 つの予測可能列が必要です。  
  
### <a name="input-and-predictable-columns"></a>入力列と予測可能列  
 次の表のように、[!INCLUDE[msCoName](../../includes/msconame-md.md)] ロジスティック回帰アルゴリズムでは、特定の入力列のコンテンツの種類、予測可能列のコンテンツの種類、およびモデリング フラグがサポートされています。 マイニング モデルにおけるコンテンツの種類の意味については、「[コンテンツの種類 &#40;データ マイニング&#41;](content-types-data-mining.md)」を参照してください。  
  
|[列]|コンテンツの種類|  
|------------|-------------------|  
|入力属性|Continuous、Discrete、Discretized、Key、Table|  
|予測可能な属性|Continuous、Discrete、Discretized|  
  
## <a name="see-also"></a>参照  
 [Microsoft ロジスティック回帰アルゴリズム](microsoft-logistic-regression-algorithm.md)   
 [線形回帰モデルのクエリ例](linear-regression-model-query-examples.md)   
 [ロジスティック回帰モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-for-logistic-regression-models.md)   
 [Microsoft ニューラル ネットワーク アルゴリズム](microsoft-neural-network-algorithm.md)  
  
  
