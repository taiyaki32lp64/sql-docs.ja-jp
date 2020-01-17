---
title: sp_rxPredict |Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 38eeb94dad960af3dc0f15921dbba717e819c828
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252029"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server データベースにバイナリ形式で格納されている機械学習モデルで構成される、指定された入力の予測値を生成します。

R と Python の機械学習モデルのスコア付けをほぼリアルタイムで提供します。 `sp_rxPredict` は、 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)および[microsoft Ml](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)の `rxPredict` R 関数のラッパーとして提供されているストアドプロシージャ、および[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)と[microsoft ml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)の[rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 関数のラッパーとして提供されています。 これは、でC++記述され、スコアリング操作専用に最適化されています。

モデルは R または Python を使用して作成する必要がありますが、シリアル化され、ターゲットデータベースエンジンインスタンスでバイナリ形式で格納されると、R または Python の統合がインストールされていない場合でも、そのデータベースエンジンのインスタンスから使用できます。 詳細については、「 [sp_rxPredict を使用したリアルタイムのスコアリング](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)」を参照してください。

## <a name="syntax"></a>構文

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>引数

**model**

サポートされている形式の事前トレーニング済みモデル。 

**input**

有効な SQL クエリ

### <a name="return-values"></a>戻り値

スコア列、および入力データソースのすべてのパススルー列が返されます。
アルゴリズムがそのような値の生成をサポートしている場合は、信頼区間などの追加のスコア列を返すことができます。

## <a name="remarks"></a>Remarks

ストアドプロシージャを使用できるようにするには、インスタンスで SQLCLR が有効になっている必要があります。

> [!NOTE]
> このオプションの enabing には、セキュリティ上の影響があります。 サーバーで SQLCLR が有効になっていない場合は、 [TRANSACT-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017)関数などの代替の実装を使用します。

ユーザーは、データベースに対する `EXECUTE` 権限を持っている必要があります。

### <a name="supported-algorithms"></a>サポートされているアルゴリズム

モデルを作成してトレーニングするには、R または Python に対してサポートされているアルゴリズムのいずれかを使用します。 [SQL Server 2016 r Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017)、 [SQL Server 2016 r Server (スタンドアロン)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016)、 [SQL Server 2017 Machine Learning Services (r または python)](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017)、または[SQL Server 2017 Server (スタンドアロン) (r または python)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017)を使用します。

#### <a name="r-revoscaler-models"></a>R: RevoScaleR モデル

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: Microsoft Ml モデル

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: Microsoft Ml によって提供される変換

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: revoscalepy モデル

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: microsoft ml モデル

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: microsoft ml によって提供される変換

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>サポートされていないモデルの種類

次の種類のモデルはサポートされていません。

+ RevoScaleR の `rxGlm` アルゴリズムまたは `rxNaiveBayes` アルゴリズムを使用するモデル
+ R の PMML モデル
+ 他のサードパーティライブラリを使用して作成されたモデル 

## <a name="examples"></a>使用例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

*\@inputData*の入力データには、有効な SQL クエリに加えて、格納されているモデルの列と互換性のある列が含まれている必要があります。

`sp_rxPredict` でサポートされる .NET 列の型は、double、float、short、ushort、long、ulong、および string のみです。 リアルタイムスコアリングに使用する前に、入力データでサポートされていない型を除外することが必要になる場合があります。 

  対応する SQL 型の詳細については、「[SQL と CLR 型のマッピング](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)」または「[CLR パラメーター データのマッピング](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)」を参照してください。

