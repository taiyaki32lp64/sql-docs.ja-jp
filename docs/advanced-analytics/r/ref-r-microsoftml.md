---
title: MicrosoftML R 関数ライブラリ
description: SQL Server 2016 R Services での MicrosoftML 関数ライブラリと、R を使用した SQL Server Machine Learning Services の概要について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 450091bba39cf10e551b8da5e62993ca676c64af
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73707921"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (SQL Server の R ライブラリ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**MicrosoftML** は、高パフォーマンスの機械学習アルゴリズムを提供する Microsoft の R 関数ライブラリです。 トレーニング、変換、スコアリング、テキストと画像の分析、および既存のデータから値を派生させるための特徴抽出を行うための関数が含まれています。

機械学習 API は、内部機械学習アプリケーション用に Microsoft によって開発されたものです。マルチコア処理と高速データ ストリーミングを使用してビッグ データに対する高パフォーマンスをサポートするために、長年にわたって改善され続けています。 また、MicrosoftML には、テキストと画像処理のための変換も多数含まれています。

## <a name="full-reference-documentation"></a>完全なリファレンス ドキュメント

**MicrosoftML** ライブラリは複数の Microsoft 製品で配布されていますが、SQL Server または別の製品のどちらでライブラリを取得した場合でも、使用方法は同じです。 これらの関数は同じであるため、[個々の RevoScaleR 関数のドキュメント](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)は Microsoft Machine Learning Server の [R リファレンス](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)の下でのみ公開されています。 製品固有の動作が存在する場合、関数のヘルプ ページにその相違点が示されます。

## <a name="versions-and-platforms"></a>バージョンとプラットフォーム

**MicrosoftML** ライブラリは R 3.4.3 に基づいており、次のいずれかの Microsoft 製品またはダウンロードをインストールした場合にのみ利用できます。

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 以降](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> 完全な製品リリース バージョンは、SQL Server 2017 では Windows のみです。 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) の **MicrosoftML** では、Windows と Linux の両方がサポートされています。

## <a name="package-dependencies"></a>パッケージの依存関係

**MicrosoftML** のアルゴリズムは、次に関して [RevoScaleR](ref-r-revoscaler.md) に依存します。

+ データ ソース オブジェクト。 **MicrosoftML** 関数によって使用されるデータは、**RevoScaleR** 関数を使用して作成されます。
+ リモート コンピューティング (関数の実行をリモート SQL Server インスタンスにシフトする)。 **RevoScaleR** ライブラリには、SQL Server のリモート計算コンテキストを作成およびアクティブ化するための関数が用意されています。

ほとんどの場合、**MicrosoftML** を使用しているときは常に、パッケージをまとめて読み込みます。

## <a name="functions-by-category"></a>カテゴリ別の関数

このセクションでは、関数をカテゴリ別に一覧表示し、それぞれの使用方法について説明します。 [目次](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)を使用して関数をアルファベット順に検索することもできます。

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1 - 機械学習アルゴリズム

| 関数名 | [説明] |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | MART 勾配ブースティング アルゴリズムの効率的な実装である、FastRank の実装。  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) を使用した、ランダム フォレストと分位点回帰フォレストの実装。  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | L-BFGS を使用したロジスティック回帰。  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 1 クラス サポート ベクター マシン。  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | バイナリ、多クラス、回帰ニューラル ネットワーク。  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 線形二項分類および回帰用の確率的双対座標上昇法最適化。 |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 1 つのモデルから得られるよりもさらに良い予測パフォーマンスを得るために、さまざまな種類のモデルをトレーニングします。|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2 - 変換の関数

| 関数名 | [説明] |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 複数の列から 1 つのベクトル値列を作成する変換。  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 辞書によるカテゴリ変換の使用によりインジケーター ベクトルを作成します。  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | ハッシュにより、カテゴリ値をインジケーター配列に変換します。 |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 指定したテキストのコーパスから、n-gram と呼ばれる連続した単語のシーケンスの数のバッグを生成します。 言語検出、トークン化、ストップワードの削除、テキストの正規化、特徴生成が提供されます。  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 自然言語のテキストをスコアリングし、テキストのセンチメントが正である確率を含む列を作成します。|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | カウントベースとハッシュベースの特徴抽出の引数の定義を可能とします。|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 再トレーニングする列のセットを選択し、他のすべてを削除します。 |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 指定したモードを使用して、指定した変数から特徴を選択します。|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 画像データを読み込みます。|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 指定したサイズ変更方法を使用して、画像のサイズを指定したディメンションに変更します。|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 画像からピクセル値を抽出します。|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 事前トレーニング済みのディープ ニューラル ネットワークモデルを使用して、画像を特徴化します。|


## <a name="3-scoring-and-training-functions"></a>3 - スコアリングおよびトレーニングの関数

| 関数名 | [説明] |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | より高速な予測パフォーマンスを実現するために、ストアド プロシージャを使用して SQL Server から、または R コードからスコアリング ライブラリを実行し、リアルタイムのスコアリングを可能にします。|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 入力データ セットのデータを出力データ セットに変換します。|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Microsoft R Machine Learning モデルの概要を提供します。|


## <a name="4-loss-functions-for-classification-and-regression"></a>4 - 分類および回帰の損失関数

| 関数名 | [説明] |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 指数分類損失関数の仕様。 | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | ログ分類損失関数の仕様。  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | ヒンジ分類損失関数の仕様。 | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | スムーズ ヒンジ分類損失関数の仕様。  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | ポワソン回帰分類損失関数の仕様。 | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 二乗回帰分類損失関数の仕様。   |   

## <a name="5-feature-selection-functions"></a>5 - 特徴選択の関数

| 関数名 | [説明] |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | カウント モードの特徴選択の仕様。 |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 相互情報量モードの特徴選択の仕様。 |

## <a name="6-ensemble-modeling-functions"></a>6 - アンサンブル モデリングの関数

| 関数名 | [説明] |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) で高速ツリー モデルをトレーニングするための関数名と引数を含むリストを作成します。|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) で高速フォレスト モデルをトレーニングするための関数名と引数を含むリストを作成します。|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) で高速線形モデルをトレーニングするための関数名と引数を含むリストを作成します。|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) でロジスティック回帰モデルをトレーニングするための関数名と引数を含むリストを作成します。|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) で OneClassSvm モデルをトレーニングするための関数名と引数を含むリストを作成します。|

## <a name="7-neural-networking-functions"></a>7 - ニューラル ネットワークの関数

| 関数名 | [説明] |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) 機械学習アルゴリズムの最適化アルゴリズムを指定します。|


## <a name="8-package-state-functions"></a>8 - パッケージ状態の関数

| 関数名 | [説明] |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | パッケージ全体の状態を格納するために使用される環境オブジェクト。 |


## <a name="how-to-use-microsoftml"></a>MicrosoftML の使用方法

**MicrosoftML** 内の関数は、ストアド プロシージャにカプセル化された R コードで呼び出すことができます。 ほとんどの開発者は、**MicrosoftML** ソリューションをローカルでビルドし、完成した R コードを展開の練習としてストアド プロシージャに移行します。

R 用の **MicrosoftML** パッケージは、SQL Server 2017 にすぐに使用できる状態でインストールされています。 また、インスタンスの R コンポーネントをアップグレードすると、SQL Server 2016 でも使用できます: [バインドを使用した SQL Server インスタンスのアップグレード](../install/upgrade-r-and-python.md)

既定では、パッケージは読み込まれません。 最初の手順として、**MicrosoftML** パッケージを読み込み、リモート計算コンテキスト、関連する接続またはデータ ソース オブジェクトを使用する必要がある場合は、次に **RevoScaleR** を読み込みます。 その後、必要な個々の関数を参照します。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>参照

+ [R のチュートリアル](../tutorials/sql-server-r-tutorials.md)
+ [計算コンテキストの使用方法](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 開発者向け R: モデルのトレーニングと運用化](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上の Microsoft 製品サンプル](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R リファレンス (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 