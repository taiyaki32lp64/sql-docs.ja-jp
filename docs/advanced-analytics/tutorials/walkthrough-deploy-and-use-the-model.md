---
title: R チュートリアル:モデルの配置
description: データベース内分析のために SQL Server に R モデルを配置する方法を示すチュートリアル。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d553d991bd07785a6a6a7592cee38a1e66badf29
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73723710"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>R モデルを配置して SQL Server で使用する (チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンでは、ストアド プロシージャからトレーニング済みのモデルを呼び出すことによって、運用環境に R モデルを配置する方法について説明します。 R または [!INCLUDE[tsql](../../includes/tsql-md.md)] をサポートするアプリケーション プログラミング言語 (C#、Java、Python など) からストアド プロシージャを呼び出し、モデルを使用して新しい観察結果を予測することができます。

この記事では、スコアリングでモデルを使用する最も一般的な 2 つの方法について説明します。

> [!div class="checklist"]
> * 複数の予測を生成する**バッチ スコアリング モード**
> * 一度に 1 つの予測を生成する**個別スコアリング モード**

## <a name="batch-scoring"></a>バッチ スコアリング

複数の予測を生成し、SQL クエリまたはテーブルを入力として渡す、*PredictTipBatchMode* というストアド プロシージャを作成します。 結果のテーブルが返されます。これにテーブルに直接挿入したり、ファイルに書き込んだりすることができます。

- SQL クエリとして一連の入力データを取得する
- 前のレッスンで保存したトレーニング済みのロジスティック回帰モデルを呼び出す
- 運転手がチップを受け取ることができる確率を予測する

1. Management Studio で、新しいクエリ ウィンドウを開き、次の T-SQL スクリプトを実行して、PredictTipBatchMode ストアド プロシージャを作成します。
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + SELECT ステートメントを使用して、SQL テーブルから格納されているモデルを呼び出します。 このモデルは **varbinary (max)** データとしてテーブルから取得され、SQL 変数 _\@lmodel2_ に格納された後、パラメーター *mod* としてシステム ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に渡されます。

    + スコアリングの入力として使用されるデータは、SQL クエリとして定義され、SQL 変数 _\@input_ に文字列として格納されます。 データベースからデータが取得されると、*InputDataSet* と呼ばれるデータ フレームに格納されます。これは、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) プロシージャに対する入力データの既定の名前にすぎません。必要に応じて、 *_\@input_data_1_name_* パラメーターを使用して別の変数名を定義できます。

    + スコアを生成するために、ストアド プロシージャで **RevoScaleR** ライブラリの rxPredict 関数が呼び出されます。

    + 戻り値 (*Score*) は、特定のモデルで、そのドライバーがチップをもらう確率です。 (省略可能) 戻り値に特定の種類のフィルターを適用して、戻り値を "チップあり" グループと "チップなし" グループに容易に分類できます。  たとえば、確率が 0.5 よりも小さい場合、チップをもらえない可能性が高いと考えられます。
  
2.  バッチ モードでストアド プロシージャを呼び出すには、ストアド プロシージャへの入力として必要なクエリを定義します。 次の SQL クエリは、SSMS で実行して動作することを確認できます。

    ```sql
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. 次の R コードを使用して、SQL クエリから入力文字列を作成します。

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @input = ", input, sep="");
    ```

4. R からストアド プロシージャを実行するには、**RODBC** パッケージの **sqlQuery** メソッドを呼び出し、先ほど定義した SQL 接続 `conn` を使用します。

    ```R
    sqlQuery (conn, q);
    ```

    ODBC エラーが発生した場合は、構文エラーを確認し、適切な数の引用符があるかどうかを確認します。 
    
    権限エラーが発生した場合は、ログインにストアド プロシージャを実行する権限があることを確認します。

## <a name="single-row-scoring"></a>単一行のスコアリング

個別スコアリング モードでは、一度に 1 つの予測が生成され、個別の値のセットが入力としてストアド プロシージャに渡されます。 値は、モデル内の特徴に対応しています。モデルではこの特徴を使用して、予測の作成や、確率値などの別の結果の生成が行われます。 その後、その値をアプリケーションまたはユーザーに返すことができます。

予測のために行単位でモデルを呼び出す場合は、個々のケースの特徴を表す値のセットを渡します。 その後、ストアド プロシージャによって 1 つの予測または確率が返されます。 

ストアド プロシージャ *PredictTipSingleMode* で、このアプローチを確認できます。 これは、特徴の値 (乗客数や走行距離など) を表す複数のパラメーターを入力として受け取り、格納されている R モデルを使用してこれらの特徴をスコア付けし、チップの確率を出力します。

1. ストアド プロシージャを作成するには、次の Transact-SQL ステートメントを実行します。

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. SQL Server Management Studio で、[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** プロシージャ (または **EXECUTE**) を使用して、ストアド プロシージャを呼び出し、必要な入力に渡すことができます。 たとえば、Management Studio で次のステートメントを実行してみます。

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    ここで渡される値は、それぞれ、変数 _passenger\_count_、_trip_distance_、_trip\_time\_in\_secs_、_pickup\_latitude_、_pickup\_longitude_、_dropoff\_latitude_、_dropoff\_longitude_ に対応します。

3. R コードからこの同じ呼び出しを実行するには、次のようにストアド プロシージャの呼び出しをすべて含む R 変数を定義するだけです。

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    ここで渡される値は、それぞれ、変数 _passenger\_count_、_trip\_distance_、_trip\_time\_in\_secs_、_pickup\_latitude_、_pickup\_longitude_、_dropoff\_latitude_、_dropoff\_longitude_ に対応します。

4. (**RODBC** パッケージから) `sqlQuery` を呼び出し、接続文字列を、ストアド プロシージャの呼び出しを含む文字列変数と共に渡します。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R Tools for Visual Studio (RTVS) により、SQL Server と R の両方の優れた統合がもたらされます。SQL Server 接続での RODBC の使用例については、こちらの記事を参照してください。[SQL Server と R の使用](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>次の手順

ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データを使用し、トレーニング済みの R モデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に保持する方法を学習したので、このデータセットに基づいて比較的容易に新しいモデルを作成できます。 たとえば、次のような追加のモデルを作成することができます。

+ チップの金額を予測する回帰モデル
+ チップが多い、普通、少ないのいずれになるかを予測するマルチクラス分類モデル

次の追加のサンプルとリソースを調べることもできます。

+ [データ サイエンスのシナリオとソリューション テンプレート](data-science-scenarios-and-solution-templates.md)
+ [高度な分析 (データベース内)](sqldev-in-database-r-for-sql-developers.md)
+ [Machine Learning Server に関するハウツー ガイド](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server のその他のリソース](https://docs.microsoft.com//machine-learning-server/resources-more)
