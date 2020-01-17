---
title: Python のチュートリアル:モデルのトレーニング
description: このチュートリアルでは、SQL Server Machine Learning Services で Python と線形回帰を使用して、スキーのレンタル数を予測します。 Python で線形回帰モデルをトレーニングします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5f83fe37890c997865c44198cbe30bc13cdea4e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727049"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python のチュートリアル:SQL Server Machine Learning Services で線形回帰モデルをトレーニングします。
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この 4 部構成のチュートリアル シリーズの第 3 部では、Python で線形回帰モデルをトレーニングします。 このシリーズの次の部では、Machine Learning Services を使用して、このモデルを SQL Server データベースにデプロイします。

この記事では以下の方法について学習します。

> [!div class="checklist"]
> * 線形回帰モデルをトレーニングする
> * 線形回帰モデルを使用して予測を作成する

[第 1 部](python-ski-rental-linear-regression.md)では、サンプル データベースを復元する方法を学習しました。

[第 2 部](python-ski-rental-linear-regression-prepare-data.md)では、SQL Server から Python データ フレームにデータを読み込み、Python でデータを準備する方法を学習しました。

[第 4 部](python-ski-rental-linear-regression-deploy-model.md)では、モデルを SQL Server に格納し、そして第 2 部と第 3 部で開発した Python スクリプトからストアド プロシージャを作成する方法について学習します。 ストアド プロシージャは、新しいデータに基づいて予測を行うために SQL Server で実行されます。

## <a name="prerequisites"></a>Prerequisites

* このチュートリアルの第 3 部は、[第 1 部](python-ski-rental-linear-regression.md)とその前提条件を完了していることを前提としています。

## <a name="train-the-model"></a>モデルをトレーニングする

予測するには、データセット内の変数間の依存関係を最も適切に説明する関数 (モデル) を見つける必要があります。 これは、モデルのトレーニングと呼ばれます。 トレーニング データセットは、このシリーズの第 2 部で作成した、pandas データ フレーム **df** のデータセット全体のサブセットになります。

線形回帰アルゴリズムを使用して、モデル **lin_model** をトレーニングします。

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

次のような結果が表示されます。

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>予測を作成します

モデル **lin_model** を使用してレンタル カウントを予測するには、predict 関数を使用します。

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>次の手順

このチュートリアル シリーズの第 3 部では、次の手順を完了しました。

* 線形回帰モデルをトレーニングする
* 線形回帰モデルを使用して予測を作成する

作成した機械学習モデルをデプロイするには、このチュートリアル シリーズの第 4 部の手順に従います。

> [!div class="nextstepaction"]
> [Python のチュートリアル:機械学習モデルのデプロイ](python-ski-rental-linear-regression-deploy-model.md)