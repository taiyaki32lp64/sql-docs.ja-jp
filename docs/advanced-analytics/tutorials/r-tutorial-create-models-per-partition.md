---
title: R でパーティションベースのモデルを作成する
description: SQL Server Machine Learning のパーティション ベースのモデリング機能を使用するときに、動的に作成されるパーティション分割されたデータをモデル化、トレーニング、使用する方法について説明します。
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: tutorial
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ee5d6cbf9b1d5430e431cf04fb3b86ae7fb5743b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73726230"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>チュートリアル:SQL Server 上の R でパーティション ベースのモデルを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2019 でのパーティション ベースのモデリングは、パーティション分割されたデータでモデルを作成してトレーニングする機能です。 地理的地域、日付と時刻、年齢、性別など、特定の分類体系に自然に分割される層化データの場合、モデル化、トレーニング、スコアリングのすべてでそのまま残るパーティションにこれらの操作を行う機能を使用して、データ セット全体に対してスクリプトを実行できます。 

パーティション ベースのモデリングを有効にするには、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) で次の 2 つの新しいパラメーターを使用します。

+ **input_data_1_partition_by_columns** では、パーティション分割に使用する列を指定します。
+ **input_data_1_order_by_columns** では、並べ替えに使用する列を指定します。 

このチュートリアルでは、従来の NYC タクシー サンプル データと R スクリプトを使用して、パーティション ベースのモデリングについて説明します。 パーティション列は支払い方法です。

> [!div class="checklist"]
> * パーティションは支払いの種類 (5) に基づいています。
> * 各パーティションでモデルを作成およびトレーニングし、データベースにオブジェクトを格納します。
> * 各パーティション モデルについてチップの結果の確率を予測します。それには、その目的のために用意されているサンプル データを使用します。

## <a name="prerequisites"></a>Prerequisites
 
このチュートリアルを完了するには次の準備が必要です。

+ 十分なシステム リソース。 データ セットは大きく、トレーニング操作ではリソースが大量に消費されます。 可能であれば、少なくとも 8 GB の RAM を搭載したシステムを使用します。 または、使用するデータ セットを小さくして、リソースの制約を回避することもできます。 データ セットを減らす手順は文中で説明されています。 

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)など、T-SQL クエリを実行するためのツール。

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)。ローカル環境のデータベース エンジン インスタンスに[ダウンロードして復元](demo-data-nyctaxi-in-sql.md)することができます。 ファイル サイズは約 90 MB です。

+ Machine Learning Services と R の統合を使用した、 SQL Server 2019 のデータベース エンジン インスタンス。

クエリ ツールで T-SQL クエリとして **`SELECT @@Version`** を実行し、バージョンを確認します。

お使いのデータベース エンジン インスタンスで現在インストールされているすべての R パッケージの適切な形式の一覧を取得することにより、R パッケージを利用できるかどうかを確認します。

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>データベースに接続する

Management Studio を開始し、データベース エンジン インスタンスに接続します。 オブジェクト エクスプローラーで、[NYCTaxi_Sample データベース](demo-data-nyctaxi-in-sql.md)が存在することを確認します。 

## <a name="create-calculatedistance"></a>CalculateDistance を作成する

デモ データベースには距離を計算するためのスカラー関数が用意されていますが、ここで使用するストアド プロシージャの動作にはテーブル値関数の方が適しています。 次のスクリプトを実行して、後の[トレーニング ステップ](#training-step)で使用する **CalculateDistance** 関数を作成します。

関数が作成されたことを確認するには、オブジェクト エクスプローラーで **NYCTaxi_Sample** データベースの下の [プログラミング] > [関数] > [テーブル値関数] を調べます。

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>パーティションごとのモデルを作成してトレーニングするためのプロシージャを定義する

このチュートリアルでは、R スクリプトをストアド プロシージャにラップします。 このステップでは、R を使用して入力データセットを作成し、チップの結果を予測するための分類モデルを構築して、データベースにモデルを格納する、ストアド プロシージャを作成します。

このスクリプトで使用されるパラメーター入力の中から、**input_data_1_partition_by_columns** と **input_data_1_order_by_columns** を調べます。 これらのパラメーターは、パーティション分割されたモデリングを実行するメカニズムであることを思い出してください。 パラメーターは、すべてのパーティションに対して 1 回実行される外部スクリプトでパーティションを処理するために、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) に入力として渡されます。 

このストアド プロシージャでは、完了までの時間を短縮するため[並列処理を使用](#parallel)します。

このスクリプトを実行した後、オブジェクト エクスプローラーで **NYCTaxi_Sample** データベースの下の [プログラミング] > [プストアド プロシージャ] に **train_rxLogIt_per_partition** が表示されます。 また、モデルの格納に使用される新しいテーブル **dbo.nyctaxi_models** も表示されます。

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>並列実行

[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) の入力に、並列処理を有効にするために使用される `@parallel=1` が含まれていることに注意してください。 以前のリリースとは異なり、SQL Server 2019 では、`@parallel=1` を設定すると、クエリ オプティマイザーに対してより強力なヒントが提供されるため、並列実行の結果がいっそうよくなります。

既定では、クエリ オプティマイザーは、256 行を超えるテーブルでは `@parallel=1` で動作する傾向がありますが、このスクリプトで示されているように、`@parallel=1` を設定することによって明示的に処理できます。

> [!Tip]
> トレーニング ワークロードの場合、Microsoft-rx 以外のアルゴリズムを使用している場合でも、任意のトレーニング スクリプトで `@parallel` を使用できます。 通常、SQL Server のトレーニング シナリオで並列処理が提供されるのは、RevoScaleR アルゴリズム (rx プレフィックスが付いたもの) だけです。 ただし、新しいパラメーターを使用すると、その機能対応に特に設計されていない関数 (オープンソースの R 関数を含む) を呼び出すスクリプトを並列化できます。 このように動作するのは、パーティションには特定のスレッドに対するアフィニティがあり、スクリプト内で呼び出されたすべての操作は、特定の `thread.`<a name="training-step"></a> でパーティションごとに実行されるためです

## <a name="run-the-procedure-and-train-the-model"></a>プロシージャを実行してモデルをトレーニングする

このセクションでは、前のステップで作成して保存したモデルを、スクリプトでトレーニングします。 次の例では、モデルをトレーニングするための 2 つの方法 (データ セット全体を使用するものと部分的なデータを使用するもの) を示します。 

このステップには時間がかかることが予想されます。 トレーニングは計算量が多く、完了までに何分もかかります。 システム リソース (特にメモリ) が負荷に対して十分でない場合は、データのサブセットを使用します。 2 番目の例では、その構文を示します。

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> 他のワークロードを実行している場合、クエリ処理を 2 コアのみに制限するには、SELECT ステートメントに `OPTION(MAXDOP 2)` を追加します。

## <a name="check-results"></a>結果をチェックする

モデルのテーブルの結果は、5 つの支払いの種類でセグメント化された 5 つのパーティションに基づいて、5 つの異なるモデルになるはずです。 モデルは、**ml_models** データ ソース内にあります。

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>結果を予測するためのプロシージャを定義する

同じパラメーターをスコアリングに使用できます。 次のサンプルに含まれる R スクリプトでは、現在処理中のパーティションに対する正しいモデルを使用して、スコアリングが行われます。

前と同様に、R コードをラップするストアド プロシージャを作成します。

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>予測を格納するテーブルを作成する

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>プロシージャを実行して予測を保存する

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>予測を表示する

予測は保存されるので、簡単なクエリを実行して結果セットを返すことができます。

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>次の手順

このチュートリアルでは、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) を使用して、パーティション分割されたデータに対する操作を繰り返しました。 ストアド プロシージャでの外部スクリプトの呼び出しと RevoScaleR 関数の使用の詳細については、次のチュートリアルを参照してください。

> [!div class="nextstepaction"]
> [R と SQL Server のチュートリアル](walkthrough-data-science-end-to-end-walkthrough.md)

