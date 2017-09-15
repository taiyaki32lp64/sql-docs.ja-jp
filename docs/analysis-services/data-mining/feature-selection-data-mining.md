---
title: "機能の選択 (データ マイニング) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], feature selections
- attributes [data mining]
- feature selection algorithms [Analysis Services]
- data mining [Analysis Services], feature selections
- neural network algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
- decision tree algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
- coding [Data Mining]
ms.assetid: b044e785-4875-45ab-8ae4-cd3b4e3033bb
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ae50c18dab1894b42e209d2a37762e0fa9e0d57
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="feature-selection-data-mining"></a>機能の選択 (データ マイニング)
  "*機能の選択* " は、機械学習の重要な部分です。 機能の選択とは、処理や分析のための入力を減らしたり、最も意味のある入力を探したりするプロセスのことです。 関連用語である " *機能エンジニアリング* " (" *機能抽出*" ともいいます) とは、既存のデータから有益な情報や機能を抽出するプロセスのことです。  
  
## <a name="why-do-feature-selection"></a>機能の選択を行う理由  
 機能の選択は優れたモデル作りに不可欠ですが、それにはいくつか理由があります。 その 1 つは、機能の選択によってある程度 " *基数を削減*" し、モデルの作成時に考慮すべき属性の数を制限できる点にあります。 ほとんどすべての場合において、データには、モデルの作成に必要とされるよりも多くの情報、または間違った種類の情報が含まれています。 たとえば、顧客データを格納した 500 列のデータセットがあるとします。ここで、データ数の少ない列をモデルに追加してもほとんどメリットは得られません。また、データが重複した列を使用するとモデルに影響することがあります。  
  
 機能の選択によって、モデルの品質が向上するだけでなく、モデルの作成プロセスが効率化されます。 不要な列を保持したままモデルを作成すると、トレーニング処理時により多くの CPU リソースとメモリが必要となり、完成したモデルに必要な記憶領域も増大します。 リソースに問題がない場合でも、機能の選択を行って最適な列を特定することにはメリットがあります。なぜなら、不要な列によって、次のようにさまざまな形でモデルの品質低下が起こり得るからです。  
  
-   不要なデータや重複したデータが含まれていると、データから意味のあるパターンを見つけるのが困難になります。  
  
-   高次元のデータセットでは、ほとんどのデータ マイニング アルゴリズムではるかに大きなトレーニング データセットが必要になります。  
  
 選択機能の処理中は、分析での有用性に基づいて、アナリストまたはモデリング ツール (アルゴリズム) のいずれかが能動的に属性を選択または除外します。  アナリストは機能エンジニアリングを実施して、機能を追加したり既存のデータを削除したり変更したりします。一方、機械学習アルゴリズムは、通常は列にスコアを付けてモデルでの実用性を検証します。  
  
 ![機能の選択とエンジニア リング プロセス](../../analysis-services/data-mining/media/ssdm-featureselectionprocess.png "の特徴の選択とエンジニア リング プロセス")  
  
 つまり、機能の選択は、価値の低いデータが多すぎること、または価値の高いデータが少なすぎることという、2 つの問題を解決するために役立ちます。 機能の選択の目的は、モデルの作成に最低限必要なデータ ソースの列を特定することです。  
  
## <a name="how-feature-selection-works-in-sql-server-data-mining"></a>SQL Server データ マイニングでの機能の選択のしくみ  
 機能の選択は、モデルをトレーニングする前に実行されます。 一部のアルゴリズムでは、関係のない列を除外して最も優れた機能を自動的に残すことができるよう、機能の選択の手法が "組み込まれて" います。 各アルゴリズム独自の既定の手法により、機能の削減が適切に適用されます。  ただし、機能の選択の動作に影響を与えるようにパラメーターを手動で設定することもできます。  
  
 機能の選択が自動で行われるときに、属性ごとにスコアが計算され、最適なスコアを持つ属性のみがモデル用に選択されます。 トップ スコアのしきい値を調整することもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ マイニングでは、これらのスコアを計算するための複数のメソッドを提供しており、モデルに適したメソッドは、次の要因によって異なります。  
  
-   モデルで使用されるアルゴリズム  
  
-   属性のデータ型  
  
-   モデルに設定したパラメーター  
  
 機能の選択は、列の入力、予測可能な属性、または状態に適用されます。 機能の選択のためのスコアリングが完了すると、モデル作成プロセスに含まれ、予測作成に使用できるのは、アルゴリズムが選択した属性と状態のみです。 機能の選択のしきい値に合わない予測属性を選択した場合、その属性は予想作成に使用されますが、予測はモデル内に存在する全体統計のみを基礎とします。  
  
> [!NOTE]  
>  機能の選択が影響するのはモデルで使用される列だけであり、保存されているマイニング構造には影響しません。 マイニング モデルから除外された列も、マイニング構造では引き続き使用できます。また、マイニング構造列のデータはキャッシュされます。  
  
### <a name="feature-selection-scores"></a>機能の選択のスコア  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ マイニングでは、属性のスコアリングのためによく使用される一般的な方法がサポートされています。 特定のアルゴリズムまたはデータセットで使用される方法は、データ型および列の使用法によって異なります。  
  
-   " *興味深さ* " のスコアは、非バイナリの連続する数値データを含む列の属性を順位付けして並べ替えるために使用されます。  
  
-   "*Shannon のエントロピ* " のスコア、および 2 つの " *ベイズ* " のスコアは、不連続データおよび分離されたデータを含む列で使用できます。 ただし、連続した列がモデルに含まれる場合、一貫性を保つために、すべての入力列の評価に興味深さのスコアが使用されます。  
  
#### <a name="interestingness-score"></a>興味深さのスコア  
 機能が興味深いのは、有用な情報を提供する場合です。 ただし、" *興味深さ* " はさまざまな方法で測定することができます。  たとえば、外れ値を検出する際には "*新奇性* " が、分類の際には密接に関連するアイテムの識別 (" *識別の加重*") が、興味深さの対象になると考えられます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ マイニングで使用される興味深さの尺度は " *エントロピに基づいています*"。したがって、ランダムに分布する属性はエントロピが高く、情報利得が低いため、このような属性の興味深さは低くなります。 次のようにして、特定の属性のエントロピが他のすべての属性のエントロピと比較されます。  
  
 Interestingness(Attribute) = - (m - Entropy(Attribute)) * (m - Entropy(Attribute))  
  
 中心エントロピ (m) は、機能セット全体のエントロピを表します。 対象となる属性のエントロピを中心エントロピから差し引くことにより、その属性が提供する情報の量を評価できます。  
  
 列に非バイナリの連続する数値データが含まれている場合は、常にこのスコアが既定で使用されます。  
  
#### <a name="shannons-entropy"></a>Shannon のエントロピ  
 Shannon のエントロピは、特定の結果に対する確率変数の不確かさを測定します。 たとえばコイン投げのエントロピは、コインが表になる確率の関数として表すことができます。  
  
 Analysis Services では、次の数式を使用して Shannon のエントロピを計算します。  
  
 H(X) = -  P(xi) log(P(xi))  
  
 このスコアリング方法は、不連続属性と分離された属性で使用できます。  
  
#### <a name="bayesian-with-k2-prior"></a>K2 事前分布を指定したベイズ定理  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ マイニングには、ベイジアン ネットワークに基づく 2 つの機能選択スコアが用意されています。 ベイジアン ネットワークとは、状態および状態間の遷移の " *有向* " または " *非循環* " のグラフ (常に現在の状態より前にある状態と後にある状態がある、繰り返し (ループ) を含まないグラフ) です。 定義上、ベイジアン ネットワークでは事前知識を使用できます。 ただし、前の状態のうちのどれを使用して後の状態の確率を計算するかという問題が、アルゴリズムのデザイン、パフォーマンス、および精度にとって重要になります。  
  
 ベイジアン ネットワークの学習のための K2 アルゴリズムは、Cooper と Herskovits によって開発されたもので、データ マイニングでよく使用されます。 K2 アルゴリズムは拡張可能で、複数の変数を分析できますが、入力として使用する変数の順序付けが必要とされます。 詳細については、「 [ベイジアン ネットワークの学習: 知識と統計データの組み合わせ](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf) 」(Chickering、Geiger、および Heckerman) を参照してください。  
  
 このスコアリング方法は、不連続属性と分離された属性で使用できます。  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>均一な事前分布を指定したベイズ ディリクレ等式  
 ベイズ ディリクレ等式 (BDE) スコアも、与えられたデータセットについて、ベイズ解析を使用してネットワークを評価します。 BDE のスコアリング方法は Heckerman によって開発されたもので、Cooper と Herskovits によって開発された BD メトリックに基づいています。 ディリクレ分布は、ネットワークの各変数の条件付き確率を表す多項分布で、学習に役立つ数多くの特性があります。  
  
 均一な事前分布を指定したベイズ ディリクレ等式 (BDEU) の方法では、数学定数を使用して事前状態の固定分布 (均一な分布) が作成されるディリクレ分布の特殊なケースが想定されています。 また尤度等価も想定されているため、データで等価な構造が区別されることを期待できません。 つまり、If A Then B のスコアが If B Then A のスコアと同じ場合、そのデータに基づいて構造を区別することはできず、因果関係を推論できません。  
  
 ベイジアン ネットワークの詳細およびこれらのスコアリング方法の実装の詳細については、「 [ベイジアン ネットワークの学習 : 知識と統計データの組み合わせ](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf)」を参照してください。  
  
### <a name="feature-selection-methods-per-algorithm"></a>アルゴリズム別の機能の選択の方法  
 次の表は、機能の選択をサポートするアルゴリズム、そのアルゴリズムによって使用される機能の選択の方法、および機能の選択の動作を制御するために設定するパラメーターの一覧です。  
  
|アルゴリズム|分析の方法|コメント|  
|---------------|------------------------|--------------|  
|Naive Bayes|Shannon のエントロピ<br /><br /> K2 事前分布を指定したベイズ定理<br /><br /> 均一な事前分布を指定したベイズ ディリクレ等式 (既定値)|Microsoft Naïve Bayes アルゴリズムで使用できる属性は、不連続属性と分離された属性だけです。したがって、興味深さのスコアは使用できません。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft Naive Bayes アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)」を参照してください。|  
|デシジョン ツリー|興味深さのスコア<br /><br /> Shannon のエントロピー<br /><br /> K2 事前分布を指定したベイズ定理<br /><br /> 均一な事前分布を指定したベイズ ディリクレ等式 (既定値)|非バイナリの連続する値を含む列がある場合は、一貫性を保つため、すべての列に対して興味深さのスコアが使用されます。 それ以外の場合は、既定の機能の選択の方法か、モデルを作成したときに指定した方法が使用されます。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft デシジョン ツリー アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)」を参照してください。|  
|ニューラル ネットワーク|興味深さのスコア<br /><br /> Shannon のエントロピー<br /><br /> K2 事前分布を指定したベイズ定理<br /><br /> 均一な事前分布を指定したベイズ ディリクレ等式 (既定値)|Microsoft ニューラル ネットワーク アルゴリズムでは、データに連続列が含まれている限り、ベイズおよびエントロピに基づく方法の両方を使用できます。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft ニューラル ネットワーク アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)」を参照してください。|  
|ロジスティック回帰|興味深さのスコア<br /><br /> Shannon のエントロピー<br /><br /> K2 事前分布を指定したベイズ定理<br /><br /> 均一な事前分布を指定したベイズ ディリクレ等式 (既定値)|Microsoft ロジスティック回帰アルゴリズムは Microsoft ニューラル ネットワーク アルゴリズムに基づいていますが、ロジスティック回帰モデルをカスタマイズして機能の選択動作を制御することはできません。したがって、機能の選択では、常に属性に最も適した方法が既定で使用されます。<br /><br /> すべての属性が不連続属性または分離された属性の場合は、既定値は BDEU です。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft ロジスティック回帰アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)」を参照してください。|  
|クラスター|興味深さのスコア|Microsoft クラスタリング アルゴリズムでは、不連続なデータまたは分離されたデータを使用できます。 ただし、各属性のスコアは距離として計算され、連続する数値として表現されるため、興味深さのスコアを使用する必要があります。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft クラスタリング アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)」を参照してください。|  
|線形回帰|興味深さのスコア|Microsoft 線形回帰アルゴリズムでは、連続列のみをサポートするため、使用できるのは興味深さのスコアだけです。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft 線形回帰アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)」を参照してください。|  
|アソシエーション ルール<br /><br /> シーケンス クラスター|使用しない|これらのアルゴリズムでは、機能の選択は実行されません。<br /><br /> ただし、必要に応じてパラメーター MINIMUM_SUPPORT および MINIMUM_PROBABILIITY の値を設定することによって、アルゴリズムの動作を制御し、入力データのサイズを小さくすることができます。<br /><br /> 詳細については、「 [Microsoft アソシエーション アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md) 」および「 [Microsoft シーケンス クラスタリング アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)」を参照してください。|  
|タイム シリーズ。|使用しない|機能の選択は、時系列モデルには適用されません。<br /><br /> このアルゴリズムの詳細については、「 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)」を参照してください。|  
  
## <a name="feature-selection-parameters"></a>機能の選択のパラメーター  
 機能の選択をサポートするアルゴリズムでは、以下のパラメーターを使用して、機能の選択をいつオンにするかを制御できます。 各アルゴリズムには、許可される入力数の既定値がありますが、その既定値をオーバーライドして属性の数を指定できます。 このセクションは、機能の選択を管理するために提供されるパラメーターを示します。  
  
#### <a name="maximuminputattributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 *MAXIMUM_INPUT_ATTRIBUTES* パラメーターで指定した数より多い列がモデルにある場合、アルゴリズムでは、計算により無意味であると判断されたすべての列が無視されます。  
  
#### <a name="maximumoutputattributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 同様に、 *MAXIMUM_OUTPUT_ATTRIBUTES* パラメーターで指定した数より多い予測可能列がモデルにある場合、アルゴリズムでは、計算により無意味であると判断されたすべての列が無視されます。  
  
#### <a name="maximumstates"></a>MAXIMUM_STATES  
 モデルに *MAXIMUM_STATES* パラメーターで指定された数より多いケースがある場合、最も一般的でない状態はグループ化され、無視されます。 これらのパラメーターのいずれかが 0 に設定されている場合、機能の選択はオフになり、処理時間とパフォーマンスに影響を及ぼします。  
  
 機能の選択のこれらのメソッドに加え、モデルの "*モデリング フラグ*"、または構造の "*ディストリビューション フラグ*" を設定すると、アルゴリズム機能を改善して重要な属性を識別したり昇格させたりすることができます。 これらの概念の詳細については、「[モデリング フラグ &#40;データ マイニング&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)」および「[列の分布 &#40;データ マイニング&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マイニング モデルとマイニング構造のカスタマイズ](../../analysis-services/data-mining/customize-mining-models-and-structure.md)  
  
  
