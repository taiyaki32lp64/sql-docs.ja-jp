---
title: R チュートリアル:データの探索
description: SQL Server でのデータベース内分析に R 関数を使用して、統計の概要を視覚化および生成する方法を示すチュートリアル。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f279be39a9edc91dd9d8cd6b72183988a607ce31
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73723747"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>R を使用した SQL Server データの表示と集計 (チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンでは、**RevoScaleR** パッケージの関数について説明し、次のタスクについて説明します。

> [!div class="checklist"]
> * SQL Server への接続
> * 必要なデータを含むクエリを定義するか、テーブルまたはビューを指定します。
> * R コードの実行時に使用する計算コンテキストを 1 つまたは複数定義します。
> * 必要に応じて、ソースからの読み込み時に、データ ソースに適用される変換を定義します。

## <a name="define-a-sql-server-compute-context"></a>SQL Server の計算コンテキストを定義する

クライアント ワークステーションの R 環境で次の R ステートメントを実行します。 このセクションでは、[データ サイエンス ワークステーションと Microsoft R Client](../r/set-up-a-data-science-client.md) を想定しています。これには、すべての RevoScaleR パッケージに加えて、基本の軽量な R ツール セットが含まれているためです。 たとえば、Rgui.exe を使用して、このセクションで R スクリプトを実行できます。

1. **RevoScaleR** パッケージがまだ読み込まれていない場合、次の R コード行を実行します。

    ```R
    library("RevoScaleR")
    ```

     引用符は省略可能ですが、この場合は推奨されます。
     
     エラーが発生した場合は、ご使用の R 開発環境で RevoScaleR パッケージを含むライブラリが使用されていることを確認します。 現在のライブラリ パスを表示するには、`.libPaths()` のようなコマンドを使用します。

2. SQL Server の接続文字列を作成し、R 変数 *connStr* に保存します。

   プレースホルダー "your_server_name" を有効な SQL Server インスタンス名に変更する必要があります。 サーバー名については、インスタンス名のみを使用できます。または、ご使用のネットワークによっては、名前を完全修飾する必要がある場合もあります。
    
   SQL Server 認証の場合、接続構文は次のようになります。

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Windows 認証の場合、構文は少し異なります。
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    通常は、R コードにパスワードが保存されないように、可能であれば、Windows 認証の使用をお勧めします。

3. 新しい*計算コンテキスト*の作成で使用する変数を定義します。 計算コンテキスト オブジェクトを作成したら、それを使用して SQL Server インスタンスで R コードを実行できます。

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - ワークステーションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューター間で双方向に R オブジェクトをシリアル化する際、R では、一時ディレクトリが使用されます。 *sqlShareDir*として使用されるローカル ディレクトリを指定するか、既定のものをそのまま利用できます。
  
    - *sqlWait* を利用し、R にサーバーからの結果を待機させるかどうかを指示します。  待機するジョブと待機しないジョブの詳細については、[Microsoft R で RevoScaleR を使用した分散コンピューティングと並列コンピューティング](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)に関するページを参照してください。
  
    - 引数 *sqlConsoleOutput* を使用し、R コンソールから出力を表示しないことを指示します。

4. [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) コンストラクターを呼び出して、既に定義されている変数と接続文字列で計算コンテキスト オブジェクトを作成し、新しいオブジェクトを R 変数 *sqlcc* に保存します。
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. 既定では、計算コンテキストはローカルです。つまり、*アクティブな計算コンテキスト*を明示的に設定する必要があります。

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) では以前のアクティブな計算コンテキストが非表示で返されるので、それを利用できます
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) ではアクティブな計算コンテキストが返されます
    
    計算コンテキストの設定は、**RevoScaleR** パッケージ内の関数を使用する操作にのみ影響します。計算コンテキストは、オープン ソース R 操作を実行する方法には影響しません。

## <a name="create-a-data-source-using-rxsqlserver"></a>RxSqlServer を使用してデータ ソースを作成する

RevoScaleR や RevoScaleR などの Microsoft R ライブラリを使用する場合、*データ ソース*は、RevoScaleR 関数を使用して作成するオブジェクトです。 データ ソース オブジェクトでは、モデルのトレーニングや特徴の抽出などのタスクに使用するデータのセットを指定します。 SQL Server を含むさまざまなソースからデータを取得できます。 現在サポートされているソースの一覧については、「[RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource)」を参照してください。

以前に、接続文字列を定義し、その情報を R 変数に保存しました。 この接続情報を再利用して、取得するデータを指定できます。

1. SQL クエリを文字列変数として保存します。 このクエリでは、モデルをトレーニングするためのデータが定義されます。

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    ここでは、実行速度を向上させるために TOP 句を使用していましたが、クエリによって返される実際の行は、順序によって異なる場合があります。 そのため、概要の結果も以下に示すものと異なる場合があります。 TOP 句は削除してもかまいません。

2. [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 関数にクエリの定義を引数として渡します。

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + 引数  *colClasses* により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と R の間でデータを移動するときに使用する列の型が指定されます。これが重要なのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が R と異なるデータ型とその他のデータ型を使用するためです。 詳しくは、[R のライブラリとデータ型](../r/r-libraries-and-data-types.md)に関する記事をご覧ください。
  
    + 引数 *rowsPerRead* はメモリ使用量を管理し効率的な計算を行うために重要な役割を果たします。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 内の拡張分析関数の大部分は、データをチャンク単位で処理し、中間結果を蓄積していきます。すべてのデータを読み取ったら、最終的な計算結果を返します。  *rowsPerRead* パラメーターを追加して、各チャンクに読み取られる処理対象のデータ行の数を制御できます。  このパラメーターの値が大きすぎる場合、そのような大規模なデータ チャンクを効率的に処理するのに十分なメモリは備えていないため、データ アクセスは遅くなる可能性があります。  一部のシステムでは、*rowsPerRead* を極端に小さい値に設定しても、パフォーマンスが低下することがあります。

3. この時点で、*inDataSource* オブジェクトが作成されましたが、これにはデータは何も含まれていません。 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) や [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) のような関数を実行するまで、データは SQL クエリからローカル環境にプルされません。

    ただし、データ オブジェクトを定義したので、それを他の関数の引数として使用することができます。

## <a name="use-the-sql-server-data-in-r-summaries"></a>R の概要で SQL Server データを使用する

このセクションでは、リモート計算コンテキストをサポートする [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] で提供されている機能のいくつかを試してみましょう。 データ ソースに R 関数を適用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データの探索、集計、グラフの作成ができます。

1. 関数 [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) を呼び出して、データ ソース内の変数とそのデータ型の一覧を取得します。

    **rxGetVarInfo** は便利な機能です。任意のデータ フレームまたはリモート データ オブジェクト内のデータ セットでこれを呼び出して、最大値や最小値、データ型、因子列内のレベル数などの情報を取得します。
    
    あらゆる種類のデータ入力、機能変換、または機能エンジニアリングの後にこの関数を実行することを検討してください。 そうすることで、モデルで使用するすべての機能が予期したデータ型を持つことを確認し、エラーを回避できます。
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **結果**
    
    ```R
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. 次に、RevoScaleR 関数 [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) を呼び出して、個々の変数に関する詳細な統計情報を取得します。

    rxSummary は R `summary` 関数に基づいていますが、いくつかの追加機能と利点があります。 rxSummary は複数の計算コンテキストで機能し、チャンキングをサポートしています。  rxSummary を使用して値を変換したり、係数レベルに基づいて集計したりすることもできます。
    
    この例では、乗客の数に基づいて料金を集計します。
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + rxSummary への最初の引数は、集計する数式または用語を指定します。 ここでは、集計する前に、`F()` 関数を使用して、_passenger\_count_ 内の値を因子に変換します。 また、_passenger\_count_ 因子変数に最小値 (1) および最大値 (6) を指定する必要があります。
    + 出力する統計情報を指定しない場合、rxSummary は平均、StDev、最小、最大、有効な結果と不足している結果の数を出力します。
    + この例には、パフォーマンスを比較できるように、関数の開始時間と終了時間を追跡するコードも含まれています。
  
    **結果**

    RxSummary 関数が正常に実行された場合は、次のような結果が表示され、その後にカテゴリ別の統計情報の一覧が表示されます。 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>ビッグ データに関するボーナス演習

すべての行を含む新しいクエリ文字列を定義してみます。 この実験用に新しいデータ ソース オブジェクトを設定することをお勧めします。 *rowsToRead* パラメーターを変更して、スループットにどのように影響するかを確認することもできます。

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> これが実行されている間、[プロセス エクスプローラー](https://technet.microsoft.com/sysinternals/processexplorer.aspx)や SQL Profiler などのツールを使用して、接続がどのように行われ、R コードが SQL Server サービスを使用して実行されているかを確認できます。
> 
> 別の方法として、これらの[カスタム レポート](../r/monitor-r-services-using-custom-reports-in-management-studio.md)を使用して SQL Server で実行されている R ジョブを監視することもできます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [R を利用してグラフやプロットを作成する](walkthrough-create-graphs-and-plots-using-r.md)