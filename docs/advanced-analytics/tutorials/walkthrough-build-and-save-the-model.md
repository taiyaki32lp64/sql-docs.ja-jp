---
title: R チュートリアル:モデルの構築と保存
description: SQL Server のデータベース内分析に使用される R 言語モデルを構築する方法を示すチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cb806c0a6286ec8a6608b346d12e666a8e9a09f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724531"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>R モデルを構築して SQL Server に保存する (チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このステップでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で機械学習モデルを構築し、モデルを保存する方法について説明します。 モデルを保存することにより、システム ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) または [PREDICT (T-SQL) 関数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)を使用して、[!INCLUDE[tsql](../../includes/tsql-md.md)] コードから直接呼び出すことができます。

## <a name="prerequisites"></a>Prerequisites

この手順では、進行中の R セッションは、このチュートリアルの前の手順に基づいていることを前提としています。 ここでは、これらの手順で作成した接続文字列とデータ ソース オブジェクトを使用します。 スクリプトの実行には、次のツールとパッケージが使用されます。

+ R コマンドを実行する Rgui.exe
+ T-SQL を実行する Management Studio
+ ROCR パッケージ
+ RODBC パッケージ

### <a name="create-a-stored-procedure-to-save-models"></a>モデルを保存するストアド プロシージャを作成する

この手順では、ストアド プロシージャを使用して、トレーニング済みのモデルを SQL Server に保存します。 この操作を実行するストアド プロシージャを作成すると、タスクが簡単になります。

Management Studio のクエリ ウィンドウで次の T-SQL コードを実行して、ストアド プロシージャを作成します。

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> エラーが発生した場合は、ログインにオブジェクトを作成する権限があることを確認してください。 オブジェクトを作成するための明示的な権限を付与するには、次のような T-SQL ステートメントを実行します。`exec sp_addrolemember 'db_owner', '<user_name>'`

## <a name="create-a-classification-model-using-rxlogit"></a>rxLogit を使用して分類モデルを作成する

このモデルは、タクシー運転手が特定の乗車でチップを受け取る可能性が高いかどうかを予測する二項分類子です。 前のレッスンで作成したデータ ソースを使用し、ロジスティック回帰を使用してチップ分類子をトレーニングします。

1. [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) パッケージに含まれる **rxLogit** 関数を呼び出し、ロジスティック回帰モデルを作成します。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    モデルを構築する呼び出しは、system.time 関数で囲まれます。 これにより、モデルの構築に必要な時間を取得できます。

2. モデルの構築後に、`summary` 関数を使用して検査し、係数を表示します。

    ```R
    summary(logitObj);
    ```

    **結果**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
     *Data: featureDataSource (RxSqlServerData Data Source)*
     *Dependent variable(s): tipped*
     *Total independent variables: 5*
     *Number of valid observations: 17068*
     *Number of missing observations: 0*
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     *Coefficients:*
     *Estimate Std. Error z value Pr(>|z|)*
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     *---*
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     *Condition number of final variance-covariance matrix: 48.3933*
     *Number of iterations: 4*
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>スコアリングにロジスティック回帰モデルを使用する

モデルが構築されたので、そのモデルを使用して運転手が特定のドライブでチップを受け取る可能性が高いかどうかを予測できます。

1. 最初に、[RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 関数を使用して、スコアリング結果を格納するためのデータ ソース オブジェクトを定義します。

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + この例を単純にするために、ロジスティック回帰モデルへの入力は、モデルのトレーニングに使用したものと同じ特徴を持つデータ ソース (`sql_feature_ds`) とします。  多くの場合、スコアリングには新しいデータを使用したり、テスト用とトレーニング用のデータを別に確保したりします。
  
    + 予測結果は _taxiscoreOutput_ というテーブルに保存されます。 rxSqlServerData を使用して作成した場合、このテーブルのスキーマは定義されていないことに注意してください。 スキーマは、rxPredict 出力から取得されます。
  
    + 予測値を格納するテーブルを作成するには、rxSqlServer データ関数を実行する SQL ログインが、データベースの DDL 権限を持っている必要があります。 ログインでテーブルを作成できない場合、ステートメントは失敗します。

2. [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 関数を呼び出して結果を生成します。

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    ステートメントが成功した場合は、実行に時間がかかることがあります。 完了したら、SQL Server Management Studio を開いて、テーブルが作成されたこと、およびそのテーブルにスコア列およびその他の予想される出力が含まれていることを確認できます。

## <a name="plot-model-accuracy"></a>モデル精度のプロット

モデルの精度を把握するには、[rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) 関数を使用して受信者側の動作曲線をプロットします。 rxRoc は、リモート コンピューティング コンテキストをサポートする RevoScaleR パッケージが提供する新しい関数の 1 つなので、2 つのオプションがあります。

+ rxRoc 関数を使用してリモート コンピューティング コンテキストでプロットを実行し、プロットをローカル クライアントに返すことができます。

+ また、R クライアント コンピューターにデータをインポートして、他の R プロット関数を使用してパフォーマンス グラフを作成することもできます。

このセクションでは、両方を実験します。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>リモート (SQL Server) コンピューティング コンテキストでプロットを実行する

1. rxRoc 関数を呼び出して、入力として以前に定義したデータを指定します。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    この呼び出しは、ROC チャートの計算に使用される値を返します。 ラベル列は、予測しようとしている実際の結果が含まれている _tipped_ になります。一方、 _[スコア]_ 列には予測が表示されます。

2. グラフを実際にプロットするには、ROC オブジェクトを保存し、プロット関数を使用して描画します。 このグラフは、リモート コンピューティング コンテキストで作成され、R 環境に返されます。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    表示するには、R グラフィック デバイスを開くか、RStudio の **[プロット]** ウィンドウをクリックします。

    ![モデルの ROC プロット](media/rsql-e2e-rocplot.png "モデルの ROC プロット")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>SQL Server のデータを使用して、ローカル コンピューティング コンテキストでプロットを作成する

コマンド プロンプトで `rxGetComputeContext()` を実行することで、コンピューティング コンテキストがローカルであることを確認できます。 戻り値は "RxLocalSeq コンピューティング コンテキスト" にする必要があります。

1. ローカル コンピューティング コンテキストでは、プロセスはほぼ同じです。 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 関数を使用して、指定したデータをローカルの R 環境に読み込みます。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. ローカル メモリ内のデータを使用して、**ROCR** パッケージを読み込み、そのパッケージの予測関数を使用して新しい予測を作成します。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 出力変数 `pred` に格納されている値に基づいて、ローカル プロットを生成します。

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![R を使用したモデル パフォーマンスのプロット](media/rsql-e2e-performanceplot.png "R を使用したモデル パフォーマンスのプロッ=ト")

> [!NOTE]
> 使用するデータ ポイントの数によっては、グラフの外観が異なる場合があります。

## <a name="deploy-the-model"></a>モデルの配置

モデルを構築した後、それが正常に実行されていることを確かめたら、おそらく、組織内のユーザーまたはユーザーがモデルを利用できるサイトにデプロイしたり、定期的にモデルを再トレーニングしたり再調整したりすることができます。 このプロセスは、モデルの*運用*と呼ばれることがあります。 SQL Server では、ストアド プロシージャに R コードを埋め込むことによって運用が実現されます。 コードはプロシージャ内に存在するので、SQL Server に接続できる任意のアプリケーションから呼び出すことができます。

外部アプリケーションからモデルを呼び出すには、実稼働に使用されるデータベースにモデルを保存する必要があります。 トレーニングしたモデルは、**varbinary(max)** 型の 1 列にバイナリ形式で保存されます。

一般的なデプロイ ワークフローは、次の手順で構成されています。

1. モデルを 16 進数文字列にシリアル化する
2. シリアル化されたオブジェクトをデータベースに転送する
3. varbinary(max) 列にモデルを保存する

このセクションでは、ストアド プロシージャを使用してモデルを保持し、予測に使用できるようにする方法について説明します。 このセクションで使用するストアド プロシージャは PersistModel です。 PersistModel の定義は[前提条件](#prerequisites)にあります。

1. まだ使用していない場合は、ローカルの R 環境に戻り、モデルをシリアル化して、変数に保存します。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. **RODBC**を使用して ODBC 接続を開きます。 パッケージが既に読み込まれている場合は、RODBC への呼び出しを省略できます。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. SQL Server に対して PersistModel ストアド プロシージャを呼び出して、シリアル化されたオブジェクトをデータベースに送信し、モデルのバイナリ表現を列に格納します。 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Management Studio を使用して、モデルが存在することを確認します。 オブジェクト エクスプローラーで、**nyc_taxi_models** テーブルを右クリックし、 **[上位 1000 行を選択]** をクリックします。 結果として、 **[モデル]** 列にバイナリ表現が表示されます。

モデルをテーブルへの保存に必要なステートメントは、INSERT のみです。 ただし、多くの場合、*PersistModel* などのストアド プロシージャにラップすると、より簡単になります。

## <a name="next-steps"></a>次の手順

次の最後のレッスンでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、保存したモデルに対してスコアリングを実行する方法について説明します。

> [!div class="nextstepaction"]
> [R モデルを展開して SQL で使用する](walkthrough-deploy-and-use-the-model.md)
