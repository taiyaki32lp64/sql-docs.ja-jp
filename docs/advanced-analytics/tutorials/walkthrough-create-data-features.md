---
title: R チュートリアル:機能エンジニアリング
description: データベース内分析に SQL Server 関数を使用してデータ機能を作成する方法を示すチュートリアル。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 67d2c0bf73e24bc3f70e94cd6cf7ce94d13e5297
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73723859"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>R と SQL Server を使用したデータ機能の作成 (チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

データ エンジニアリングは、機械学習の重要な部分です。 データを予測モデリングに使用するには、多くの場合、事前に変換する必要があります。 必要な機能がデータにない場合、既存の値からデータをエンジニアリングできます。

このモデリング タスクでは、乗車位置と降車位置の未加工の緯度値と経度値を使用するのではなく、2 つの位置間の距離 (マイル単位) が必要です。 この機能を作成するには、[ヘイバーサイン式](https://en.wikipedia.org/wiki/Haversine_formula)を使用して 2 点間の直線距離を計算します。

この手順では、データから機能を作成するため、次の 2 つの方法について説明します。

> [!div class="checklist"]
> * カスタム R 関数を使用する
> * [!INCLUDE[tsql](../../includes/tsql-md.md)] でカスタム T-SQL 関数を使用する

目標は、元の列と新しい数値機能 *direct_distance* を含む新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ セットを作成することです。

## <a name="prerequisites"></a>Prerequisites

この手順では、進行中の R セッションは、このチュートリアルの前の手順に基づいていることを前提としています。 ここでは、これらの手順で作成した接続文字列とデータ ソース オブジェクトを使用します。 スクリプトの実行には、次のツールとパッケージが使用されます。

+ R コマンドを実行する Rgui.exe
+ T-SQL を実行する Management Studio

## <a name="featurization-using-r"></a>R を使用した特性付け

R 言語は統計ライブラリが豊富なことで知られていますが、カスタム データの変換の作成も必要になることがあります。

まず、R ユーザーが使い慣れた方法を使用して行いましょう。つまり、ご使用のノート PC にデータを取得してから、カスタム R 関数 *ComputeDist* を実行します。これにより、緯度値と経度値によって指定された 2 点間の直線距離が計算されます。

1. 前に作成したデータ ソース オブジェクトでは、上位 1000 行しか取得されないことを思い出してください。 そのため、すべてのデータを取得するクエリを定義してみましょう。

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. クエリを使用して、新しいデータ ソース オブジェクトを作成します。

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) では、_sqlQuery_ パラメーターの引数として指定された、有効な SELECT クエリで構成されるクエリ、または _table_ パラメーターとして指定されたテーブル オブジェクトの名前のいずれかを指定できます。
    
    - テーブルからデータをサンプリングする場合は、_sqlQuery_ パラメーターを使用して、T-SQL TABLESAMPLE 句を使用してサンプリング パラメーターを定義し、_rowBuffering_ 引数を FALSE に設定する必要があります。

3. 次のコードを実行して、カスタム R 関数を作成します。 ComputeDist は、緯度値と経度値の 2 組を引数に使用して、2 点間の直線距離を計算します。距離はマイル単位で返されます。

    ```R
    env <- new.env();
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){
      R <- 6371/1.609344 #radius in mile
      delta_lat <- dropoff_lat - pickup_lat
      delta_long <- dropoff_long - pickup_long
      degrees_to_radians = pi/180.0
      a1 <- sin(delta_lat/2*degrees_to_radians)
      a2 <- as.numeric(a1)^2
      a3 <- cos(pickup_lat*degrees_to_radians)
      a4 <- cos(dropoff_lat*degrees_to_radians)
      a5 <- sin(delta_long/2*degrees_to_radians)
      a6 <- as.numeric(a5)^2
      a <- a2+a3*a4*a6
      c <- 2*atan2(sqrt(a),sqrt(1-a))
      d <- R*c
      return (d)
    }
    ```
  
    + 1 行目で新しい環境を定義します。 R では、環境を使用して、パッケージなどの名前空間をカプセル化できます。 `search()` 関数を使用すると、ワークスペース内の環境を確認できます。 特定の環境内にあるオブジェクトを確認するには、「 `ls(<envname>)`」と入力します。
    + `$env.ComputeDist` から始まる行には、ヘイバーサイン式を定義するコードが含まれています。この式で、球面上にある 2 点間の *大圏距離* を計算します。

4. 関数を定義したら、それをデータに適用して *direct_distance* という新しい機能列を作成します。 ただし、変換を実行する前に、コンピューティング コンテキストをローカルに変更します。

    ```R
    rxSetComputeContext("local");
    ```

5. [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) 関数を呼び出して機能エンジニアリング データを取得し、`env$ComputeDist` 関数をメモリ内のデータに適用します。

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + RxDataStep 関数では、データをインプレースで変更するためのさまざまなメソッドをサポートしています。 詳細については、次の記事を参照してください。[Microsoft R でデータを変換およびサブセット化する方法](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    ただし、rxDataStep について注目すべき点がいくつかあります。 
    
    他のデータ ソースでは、*varsToKeep* と *varsToDrop* の引数が使用できますが、これらは SQL Server データ ソースではサポートされていません。 したがって、この例では、_transforms_ 引数を使用して、パススルー列と変換された列の両方を指定しています。 また、SQL Server のコンピューティング コンテキストで実行している場合、_inData_ 引数で受け取れるのは、SQL Server データ ソースだけです。

    上記のコードでは、より大きなデータ セットに対して実行すると警告メッセージが生成される場合もあります。 行数を作成される列数に掛けた値が設定値 (既定値は 300 万) を超えると、rxDataStep によって警告が返され、返されたデータ フレーム内の行数が切り捨てられます。 警告を削除するには、rxDataStep 関数の _maxRowsByCols_ 引数を変更します。 ただし、_maxRowsByCols_ が大きすぎる場合は、データ フレームをメモリに読み込むときに問題が発生する可能性があります。

7. 必要に応じて [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) を呼び出して、変換されたデータ ソースのスキーマを検査できます。

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Transact-SQL を使用した特性付け

この演習では、カスタム R 関数の代わりに、SQL 関数を使用して同じタスクを実行する方法について学習します。 

[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) または別のクエリ エディターに切り替えて、T-SQL スクリプトを実行します。

1. *fnCalculateDistance* という名前の SQL 関数を使用します。 この関数は、NYCTaxi_Sample データベースに既に含まれているはずです。 オブジェクト エクスプローラーで、次のパスに移動して関数が存在することを確認します。データベース > NYCTaxi_Sample > プログラミング > 関数 > スカラー値関数 > dbo.fnCalculateDistance。

    関数が存在しない場合は、SQL Server Management Studio を使用して、NYCTaxi_Sample データベースに関数を生成します。

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS decimal(28, 10)
    AS
    BEGIN
      DECLARE @distance decimal(28, 10)
      -- Convert to radians
      SET @Lat1 = @Lat1 / 57.2958
      SET @Long1 = @Long1 / 57.2958
      SET @Lat2 = @Lat2 / 57.2958
      SET @Long2 = @Long2 / 57.2958
      -- Calculate distance
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
      --Convert to miles
      IF @distance <> 0
      BEGIN
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
      END
      RETURN @distance
    END
    ```

2. Management Studio の新しいクエリ ウィンドウで、[!INCLUDE[tsql](../../includes/tsql-md.md)] をサポートする任意のアプリケーションから次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行して、関数の動作を確認します。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. 新しいテーブル (最初に作成する必要があります) に値を直接挿入するには、テーブル名を指定する **INTO** 句を追加します。

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. R コードから SQL 関数を呼び出すこともできます。 Rgui に戻り、SQL 特性付けクエリを R 変数に保存します。

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > このチュートリアルを短時間で終わらせるために、このクエリはサンプルのデータを少なく取得するように変更されています。 すべてのデータを取得する場合は、TABLESAMPLE 句を削除できます。ただし、ご使用の環境によっては、完全なデータセットを R に読み込むことができず、エラーが発生する可能性があります。
  
5. 次のコード行を使用して R 環境から [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を呼び出し、*featureEngineeringQuery* に定義されているデータに適用します。
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  これで新しい機能が作成されました。**rxGetVarsInfo** を呼び出し、機能テーブル内のデータの概要を作成します。
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    **結果**

    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > 場合によっては、次のようなエラーが表示されることがあります。*EXECUTE 権限がオブジェクト ' fnCalculateDistance ' で拒否されました。* その場合は、使用しているログインに、スクリプトの実行と、インスタンスだけでなく、データベースでオブジェクトを作成する権限があることを確認してください。
    > オブジェクトのスキーマ (fnCalculateDistance) を確認します。 オブジェクトがデータベース所有者によって作成されており、ログインがロール db_datareader に属している場合は、スクリプトを実行するための明示的な権限をログインに付与する必要があります。

## <a name="comparing-r-functions-and-sql-functions"></a>R 関数と SQL 関数の比較

R コードのときにも使われていたこのコードを覚えていますか。

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

SQL 関数を呼び出すときにデータ変換にかかる時間を確認するために、これを SQL カスタム関数の例で使用してみることができます。 また、rxSetComputeContext を使用してコンピューティング コンテキストを切り替えて、タイミングを比較してみてください。

ネットワークの速度やハードウェアの構成によっては、時間が大幅に異なる場合があります。 テストした構成では、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数のアプローチの方が、カスタム R 関数を使用するよりも高速でした。 そのため、以降の手順ではこれらの計算に [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を使用しています。

> [!TIP]
> 非常に多くの場合、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用する機能エンジニアリングの方が R よりも高速になります。たとえば、T-SQL には、移動平均や *n* タイルのロールなど、一般的なデータ サイエンス計算に適用できる高速ウィンドウ関数と順位付け関数が含まれています。 データとタスクに基づいて、最も効率的な方法を選択してください。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [R モデルを構築して SQL に保存する](walkthrough-build-and-save-the-model.md)

