---
title: Python + T-SQL:モデルのトレーニング
description: SQL Server で Transact-SQL を使用して、モデルをトレーニングし、保存する方法を示す Python チュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8bec553502b2e5c8d69436e539437be9a5989aa
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724876"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>T-SQL を使用して Python モデルをトレーニングし保存する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、[SQL 開発者向けのデータベース内の Python 分析](sqldev-in-database-python-for-sql-developers.md)チュートリアルの一部です。 

この手順では、Python パッケージの **scikit-learn** と **revoscalepy** を使用して、機械学習モデルをトレーニングする方法について説明します。 これらの Python ライブラリは、SQL Server Machine Learning Services と共に、既にインストールされています。

SQL Server ストアド プロシージャを使用してモデルを作成およびトレーニングするには、モジュールを読み込んでから、必要な関数を呼び出します。 このモデルには、過去のレッスンで作成したデータ機能が必要です。 最後に、トレーニング済みのモデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存します。
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>トレーニング セットとテスト セットへのデータの分割

1. **PyTrainTestSplit** という名のストアドプロシージャを作成し、nyctaxi_sample テーブルのデータを 2 つに分割します。nyctaxi_sample_training と nyctaxi_sample_testing です。 

    このストアド プロシージャは既に作成されているはずですが、以下のコードを実行して作成することもできます。

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. カスタム分割を使用してデータを分割するには、ストアド プロシージャを実行し、トレーニング セットに割り当てられたデータの比率を表す整数を入力します。 たとえば、次のステートメントでは、60% のデータがトレーニング セットに割り当てられます。

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>ロジスティック回帰モデルの作成

データの準備完了後、それを使用してモデルをトレーニングできます。 これを行うには、トレーニング データ テーブルの入力として、Python コードを実行するストアド プロシージャを呼び出します。 このチュートリアルでは、2 つのモデル (二項分類モデル) を作成します。

+ ストアドプロシージャ **PyTrainScikit** は、**scikit-learn** パッケージを使用して、チップ予測モデルを作成します。
+ ストアドプロシージャ **TrainTipPredictionModelRxPy** は、**revoscalepy** パッケージを使用して、チップ予測モデルを作成します。

それぞれのストアド プロシージャは、入力したデータを使用して、ロジスティック回帰モデルを作成およびトレーニングします。 すべての Python コードは、システムストアドプロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)にラップされます。

新しいデータでモデルを再トレーニングしやすくするために、別のストアド プロシージャに sp_execute_external_script の呼び出しをラップし、新しいトレーニング データをパラメーターとして渡します。 このセクションでは、このプロセスを、順を追って説明します。

### <a name="pytrainscikit"></a>PyTrainScikit

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で新しい**クエリ** ウィンドウを開き、次のステートメントを実行して、ストアド プロシージャ **PyTrainScikit** を作成します。  ストアド プロシージャには入力データの定義が含まれているため、入力クエリを提供する必要はありません。

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from sklearn.linear_model import LogisticRegression
    
    ##Create SciKit-Learn logistic regression model
    X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
    y = numpy.ravel(InputDataSet[["tipped"]])
    
    SKLalgo = LogisticRegression()
    logitObj = SKLalgo.fit(X, y)
    
    ##Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

2. 次の SQL ステートメントを実行して、トレーニング済みのモデルをテーブル nyc\_taxi_models に挿入します。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    データ処理とモデルの調整には、数分かかることがあります。 Python の **stdout** ストリームにパイプ出力されるメッセージが、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[メッセージ]** ウィンドウに表示されます。 例:

    *外部スクリプトからの STDOUT メッセージ:* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. テーブル *nyc\_taxi_models* を開きます。 _model_列にシリアル化されたモデルを含む新しい行が 1 つ追加されます。

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

このストアド プロシージャは、新しい **revoscalepy** パッケージを使用します。これは Python 用の新しいパッケージです。 これには、R 言語の **RevoScaleR** パッケージに提供されているものと同様のオブジェクト、変換、およびアルゴリズムが含まれています。 

**revoscalepy** を使用すると、リモート コンピューティング コンテキストの作成、コンピューティング コンテキスト間でのデータ移動、データ変換、および、ロジスティック、線形回帰、デシジョンツリーなどの一般的アルゴリズムを使用した、予測モデルのトレーニングを行うことができます。 詳細については、「[SQL Server の revoscalepy モジュール](../python/ref-py-revoscalepy.md)」および「[revoscalepy 関数参照](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)」を参照してください。

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で新しい**クエリ** ウィンドウを開き、次のステートメントを実行して、ストアド プロシージャ _TrainTipPredictionModelRxPy_ を作成します。  ストアド プロシージャには、既に入力データの定義が含まれているため、入力クエリを提供する必要はありません。

    ```sql
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    このストアド プロシージャは、モデル トレーニングの一環として、以下の手順を実行します。

    - SELECT クエリにより、カスタム スカラー関数 _fnCalculateDistance_ が適用され、乗車場所と降車場所間の直線距離が計算されます。 クエリの結果は、Python の既定の入力変数 `InputDataset` に格納されます。
    - 二項変数 _tipped_ が*ラベル*または結果列として使用され、モデルは、_passenger_count_、_trip_distance_、_trip_time_in_secs_、および _direct_distance_ の機能列を使用して調整されます。
    - トレーニング済みモデルはシリアル化され、Python 変数`logitObj`に格納されます。 T-SQL キーワードの OUTPUT を追加することにより、変数をストアド プロシージャの出力として追加できます。 次の手順では、この変数を使用して、モデルのバイナリコードをデータベース テーブル _nyc_taxi_models_ に挿入します。 このメカニズムにより、モデルの格納と再利用が容易になります。

2. 以下のようにストアド プロシージャを実行し、トレーニングした **revoscalepy** モデルを、テーブル *nyc_taxi_models* に挿入します。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    データ処理とモデルの調整には、しばらく時間がかかることがあります。 Python の **stdout** ストリームにパイプ出力されるメッセージが、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[メッセージ]** ウィンドウに表示されます。 例:

    *外部スクリプトからの STDOUT メッセージ:* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. テーブル *nyc_taxi_models*を開きます。 _model_列にシリアル化されたモデルを含む新しい行が 1 つ追加されます。

    *revoscalepy_model* *0x8003637265766F7363616c....*

次の手順では、トレーニングしたモデルを使用して予測を作成します。

## <a name="next-step"></a>次の手順

[ストアド プロシージャに埋め込まれた Python を使用した予測の実行](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>前の手順

[T-SQL を使用してデータ機能を作成する](sqldev-py5-train-and-save-a-model-using-t-sql.md)
