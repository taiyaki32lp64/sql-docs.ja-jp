---
title: T-SQL PREDICT を使用するネイティブ スコアリング
description: PREDICT T-SQL 関数を使用して予測を生成します。SQL Server 上で、R または Python で記述された事前にトレーニング済みのモデルに対するデータ入力をスコアリングします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 766adecbc91f88ed0796e4214b7e4074fc564f01
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727286"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>PREDICT T-SQL 関数を使用したネイティブ スコアリング
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

ネイティブ スコアリングでは、[PREDICT T-SQL 関数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)と SQL Server 2017 のネイティブ C++ 拡張機能を使用して、ほぼリアルタイムで新しいデータ入力の予測値または*スコア*を生成します。 この方法では、予測と予測のワークロードの可能な処理速度が最速になりますが、次のプラットフォームとライブラリの要件があります。RevoScaleR と revoscalepy からの関数のみが C++ を実装していることです。

ネイティブ スコアリングには、既にトレーニング済みのモデルが必要です。 SQL Server 2017 の Windows または Linux、または Azure SQL Database では、Transact-SQL で PREDICT 関数を呼び出して、入力パラメーターとして指定した新しいデータに対してネイティブ スコアリングを呼び出すことができます。 PREDICT 関数は、指定されたデータ入力に対してスコアを返します。

## <a name="how-native-scoring-works"></a>ネイティブ スコアリングのしくみ

ネイティブ スコアリングでは、事前に特別なバイナリ形式で保存されたか、RAW 型バイト ストリームとしてディスクに保存された、既にトレーニング済みのモデルを読み取ることができる Microsoft のネイティブ C++ ライブラリを使用し、指定した新しいデータ入力に対してスコアを生成します。 モデルはトレーニング、発行、および保存されるため、R または Python インタープリターを呼び出す必要なくスコアリングに使用できます。 そのため、複数のプロセス相互作用のオーバーヘッドが軽減されるため、エンタープライズの実稼働シナリオでは、予測パフォーマンスが格段に速くなります。

ネイティブ スコアリングを使用するには、予測 PREDICT T-SQL 関数を呼び出し、次の必須の入力を渡します。

+ サポートされているアルゴリズムに基づく互換性のあるモデル。
+ 入力データ (通常は SQL クエリとして定義される)。

この関数は、入力データの予測を、パス スルーしたいソース データの任意の列と一緒に返します。

## <a name="prerequisites"></a>Prerequisites

PREDICT は、SQL Server 2017 データベース エンジンのすべてのエディションで使用でき、既定で有効になっています。これには、Windows の SQL Server Machine Learning Services、SQL Server 2017 (Windows)、SQL Server 2017 (Linux)、または Azure SQL Database が含まれます。 R や Python をインストールしたり、追加機能を有効にしたりする必要はありません。

+ このモデルは、下記に一覧表示されているサポートされる **rx** アルゴリズムのいずれかを使用して、事前にトレーニングされる必要があります。

+ R の場合は [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)、Python の場合は [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) を使用して、モデルをシリアル化します。 これらのシリアル化関数は、高速スコアリングをサポートするように最適化されています。

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>サポートされているアルゴリズム

+ revoscalepy モデル

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR モデル

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

MicrosoftML または microsoftml からのモデルを使用する必要がある場合は、[sp_rxPredict でリアルタイムのスコアリング](real-time-scoring.md)を使用します。

サポートされていないモデル タイプには、次のタイプが含まれます。

+ 他の変換を含むモデル
+ RevoScaleR または revoscalepy の同等の `rxGlm` または `rxNaiveBayes` アルゴリズムを使用するモデル
+ PMML モデル
+ 他のオープンソース ライブラリまたはサードパーティ ライブラリを使用して作成されたモデル

## <a name="example-predict-t-sql"></a>例:PREDICT (T-SQL)

この例では、モデルを作成してから、T-SQL からリアルタイムの予測関数を呼び出します。

### <a name="step-1-prepare-and-save-the-model"></a>手順 1. モデルを構築して保存する

次のコードを実行して、サンプル データベースと必要なテーブルを作成します。

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

次のステートメントを使用して、データ テーブルに**アヤメ** データセットのデータを設定します。

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

ここで、モデルを格納するテーブルを作成します。

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

次のコードでは、**アヤメ** データセットに基づいてモデルを作成し、それを **models** という名前のテーブルに保存します。

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> RevoScaleR からの [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 関数を使用して、モデルを保存してください。 標準の R `serialize` 関数では、必要な形式を生成できません。

次のようなステートメントを実行すると、格納されているモデルをバイナリ形式で表示できます。

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>手順 2. モデルで PREDICT を実行する

次の単純な PREDICT ステートメントでは、**ネイティブ スコアリング**関数を使用して、デシジョン ツリー モデルから分類を取得します。 指定した属性に基づいてアヤメの種類、花弁の長さと幅が予測されます。

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

"PREDICT 関数の実行中にエラーが発生しました。 モデルが破損しているか無効です" というエラーを受け取った場合、通常は、クエリがモデルを返さなかったことを意味します。 モデル名を正しく入力したかどうか、またはモデル テーブルが空であるかどうかを確認します。

> [!NOTE]
> **PREDICT** によって返される列と値は、モデルの種類によって異なる場合があるため、**WITH** 句を使用して、返されるデータのスキーマを定義する必要があります。

## <a name="next-steps"></a>次の手順

ネイティブ スコアリングを含む完全なソリューションについては、SQL Server 開発チームのこれらのサンプルを参照してください。

+ ML スクリプトをデプロイします。[Python モデルの使用](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ ML スクリプトをデプロイします。[R モデルの作成](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)