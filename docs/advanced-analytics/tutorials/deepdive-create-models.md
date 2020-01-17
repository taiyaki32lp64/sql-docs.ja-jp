---
title: RevoScaleR を使用して R モデルを作成する
description: このチュートリアルは、SQL Server で R 言語を使用してモデルを構築する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9a23691e8ed4b5ec5290ae666455f789954fa95d
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727265"
---
# <a name="create-r-models-sql-server-and-revoscaler-tutorial"></a>R モデルを作成する (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

トレーニング データを強化しました。 ここで、回帰モデリングを使用してデータを分析してみましょう。 線形モデルは、予測分析の世界における重要なツールです。 **RevoScaleR** パッケージには、ワークロードを分割して、それを並列で実行できる回帰アルゴリズムが含まれています。

> [!div class="checklist"]
> * 線形回帰モデルを作成する
> * ロジスティック回帰モデルを作成する

## <a name="create-a-linear-regression-model"></a>線形回帰モデルを作成する

この手順では、独立変数として *gender* 列と *creditLine* 列の値を使用して、顧客のクレジット カード残高を推定する単純な線形モデルを作成します。
  
そのためには、リモートの計算コンテキストをサポートする [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) 関数を使用します。
  
1. 完成したモデルを格納する R 変数を作成し、**rxLinMod** を呼び出して適切な数式を渡します。
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 結果の概要を確認するには、モデル オブジェクトに対して標準の R 関数 **summary** を呼び出します。
  
     ```R
     summary(linModObj)
     ```

前の手順では、サーバーに対して計算コンテキストを設定したので、この手順で **summary** のような単純な R 関数を利用できることが奇妙に感じられるかもしれませんが、 **rxLinMod** 関数でリモート計算コンテキストを使用してモデルを作成する場合でも、そのモデルを含むオブジェクトがローカル ワークステーションに返され、共有ディレクトリに格納されます。

そのため、"ローカル" コンテキストを使用して作成した場合と同様に、モデルに対して標準の R コマンドを実行することができます。

**結果**

```R
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>ロジスティック回帰モデルを作成する

次に、特定の顧客に不正使用の危険があるかどうかを示すロジスティック回帰モデルを作成します。 ロジスティック回帰をリモートの計算コンテキストに収めることができる **RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) 関数を使用します。

計算コンテキストはそのまま保持します。 データ ソースも引き続き同じものを使用します。

1. **rxLogit** 関数を呼び出して、モデルの定義に必要な数式を渡します。

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    60 個の独立変数 (破棄される 3 つのダミー変数を含む) を使用する大規模なモデルなので、計算コンテキストからオブジェクトが返されるまでにしばらく時間がかかる場合があります。
    
    このモデルがこのように大きくなるのは、R と **RevoScaleR** パッケージでは、カテゴリ要因変数のすべてのレベルがそれぞれ個別のダミー変数として自動的に処理されるためです。
  
2. 返されるモデルの概要を確認するには、R の **summary** 関数を呼び出します。
  
    ```R
    summary(logitObj)
    ```
  
**結果の一部**

```R
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [新しいデータのスコア付け](../../advanced-analytics/tutorials/deepdive-score-new-data.md)