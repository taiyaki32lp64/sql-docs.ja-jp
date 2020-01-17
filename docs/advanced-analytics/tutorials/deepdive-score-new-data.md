---
title: RevoScaleR を使用してデータをスコア付けする
description: このチュートリアルでは、SQL Server で R 言語を使用してデータを表示する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf4198e4f8baa0c572f5da3d2b4cf457e695a4b7
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727177"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>新しいデータのスコア付け (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

この手順では、前のレッスンで作成したロジスティック回帰モデルを使用して、同じ独立変数を入力として使用する別のデータセットをスコア付けします。

> [!div class="checklist"]
> * 新しいデータのスコア付け
> * スコアのヒストグラムを作成する

> [!NOTE]
> 手順の一部には、DDL 管理者特権が必要です。

## <a name="generate-and-save-scores"></a>スコアの生成と保存
  
1. 前のレッスンで作成した列情報を使用するには、sqlScoreDS データソース ([レッスン 2](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)で作成) を更新します。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 結果が失われないようにするには、新しいデータソースオブジェクトを作成します。 次に、新しいデータ ソース オブジェクトを使用して、RevoDeepDive データベースに新しいテーブルを作成します。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    この時点では、テーブルは作成されていません。 これはデータのコンテナーを定義するためだけのステートメントです。
     
3. 現在のコンピューティング コンテキストを **rxGetComputeContext()** 使用して確認し、必要に応じてコンピューティング コンテキストをサーバーに設定します。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 念のため、出力テーブルが存在するかどうかを確認してください。 同じ名前のものが既に存在する場合は、新しいテーブルを書き込もうとしたときにエラーが表示されます。
  
    この処理を実行するには、入力としてテーブル名を渡して、関数 [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) と [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)を呼び出します。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** は ODBC ドライバーに対してクエリを行い、テーブルが存在する場合は TRUE、それ以外の場合は FALSE を返します。
    + **rxSqlServerDropTable** は DDL を実行し、テーブルが正常にドロップされた場合は TRUE、それ以外の場合は FALSE を返します。

5. [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) を実行してスコアを作成し、データ ソース sqlScoreDS で定義されている新しいテーブルに保存します。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    **rxPredict** 関数も、リモート計算コンテキストでの実行をサポートする関数です。 **rxPredict** 関数を使用すると、[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)、[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)、または [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) に基づくモデルからスコアを作成できます。
  
    - ここで *writeModelVars* パラメーターは **TRUE** に設定されます。 これは見積もりに使用された変数が新しいテーブルに追加されることを意味します。
  
    - *predVarNames* パラメーターにより、結果が保存される変数が指定されます。 ここで、新しい変数の `ccFraudLogitScore` を渡します。
  
    - *rxPredict* の **type** パラメーターで、予測の計算方法を定義します。 応答変数のスケールに基づいてスコアを生成するには、キーワード **応答** を指定します。 または、キーワード **リンク**を使用して、基になるリンク関数に基づいてスコアを生成します。この場合、予測はロジスティック スケールを使用して作成されます。

6. 少し時間をおいて Management Studio でテーブルの一覧を更新すると、新しいテーブルとそのデータを確認することができます。

7. 出力予測に変数を追加するには、*extraVarsToWrite* 引数を使用します。  たとえば、次のコードの変数 *custID* は、スコアリング データ テーブルから予測の出力テーブルに追加されています。
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>ヒストグラムでスコアを表示する

新しいテーブルが作成されたら、10,000 件の予測スコアのヒストグラムを計算し、表示します。 下限値と上限値を指定すると、計算が高速になります。そのため、これらの値をデータベースから取得し、作業中のデータに追加します。

1. 新しいデータソース sqlMinMax を作成します。このデータ ソースに対してクエリを行い、上限値と下限値を取得します。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     この例を見ると、 **RxSqlServerData** データ ソース オブジェクトを使用して SQL クエリ、関数、またはストアド プロシージャに基づいて任意のデータセットを定義し、それを R コードで使用するのが簡単だということがわかります。 この変数には実際の値は格納されず、データ ソースの定義のみが格納されます。 **rxImport**など関数で使用する場合にのみ、このクエリを実行して値を生成します。
      
2. [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 関数を呼び出して、コンピューティング コンテキスト全体で共有できるデータ フレームに値を配置します。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **結果**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 最大値と最小値を使用できるようになったので、値を使用して、生成されたスコアに対して別のデータ ソースを作成します。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. データ ソース オブジェクト sqlOutScoreDS を使用してスコアを取得し、ヒストグラムを計算して表示します。 必要に応じて、計算コンテキストを設定するコードを追加してください。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **結果**
  
    ![R によって作成された複雑なヒストグラム](media/rsql-sue-complex-histogram.png "R によって作成された複雑なヒストグラム")
  
## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [R を使用したデータの変換](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)