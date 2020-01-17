---
title: R + T-SQL チュートリアル:モデルのトレーニング
description: SQL Server ストアド プロシージャと T-SQL 関数を使用して R モデルをトレーニング、シリアル化、および保存する方法を示すチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724458"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>レッスン 3:T-SQL を使用したモデルのトレーニングと保存
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、SQL Server で R を使用する方法に関する SQL 開発者向けのチュートリアルの一部です。

このレッスンでは、R を使用して機械学習モデルをトレーニングする方法について説明します。前のレッスンで作成したデータ機能を使用してモデルをトレーニングし、トレーニング済みのモデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存します。 この場合、R パッケージは [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]と共に既にインストールされているため、SQL からすべてを実行できます。

## <a name="create-the-stored-procedure"></a>ストアド プロシージャを作成する

T-SQL から R を呼び出すときは、システムストアドプロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用します。 ただし、モデルの再トレーニングなど、頻繁に繰り返すプロセスでは、別のストアド プロシージャに sp_execute_exernal_script の呼び出しをカプセル化する方が簡単です。

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で、新しい **[クエリ]** ウィンドウを開きます。

2. 次のステートメントを実行して、ストアド プロシージャ **RxTrainLogitModel** を作成します。 このストアド プロシージャは、入力データを定義し、RevoScaleR の **rxLogit** を使用してロジスティック回帰モデルを作成します。

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
    
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model 
    trained_model <- as.raw(serialize(logitObj, NULL));
    ',
      @input_data_1 = @inquery,
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT; 
    END
    GO
    ```

    - モデルをテストするために一部のデータが残っていることを確認するために、トレーニング目的で、データの70% がタクシー データ テーブルからランダムに選択されます。

    - SELECT クエリによって、カスタムのスカラー関数 *fnCalculateDistance* が使用され、乗車位置と降車位置直線距離が計算されます。 クエリの結果は R の既定の入力変数 `InputDataset` に格納されます。
  
    - R スクリプトは、ロジスティック回帰モデルを作成するために、[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] に含まれる拡張 R 関数の 1 つである **rxLogit** 関数を呼び出します。
  
        二項変数 _tipped_ が *ラベル* または結果列として使用され、モデルは、  _passenger_count_、 _trip_distance_、 _trip_time_in_secs_、および _direct_distance_の機能列を使用して調整されます。
  
    - R 変数 `logitObj` に保存されたトレーニング済みのモデルはシリアル化され、出力パラメーターとして返されます。

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>ストアド プロシージャを使用した R モデルのトレーニングとデプロイ

ストアド プロシージャには、既に入力データの定義が含まれているため、入力クエリを提供する必要はありません。

1. R モデルをトレーニングしてデプロイするには、ストアド プロシージャを呼び出してデータベース テーブル _nyc_taxi_models_ に挿入します。これにより、将来の予測に使用できるようになります。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[メッセージ]** ウィンドウに、次のように R の **stdout** ストリームにパイプ処理されるメッセージが表示されていないか注意してください。 

    "外部スクリプトからの STDOUT メッセージ:読み取られる行:1193025、処理された行数の合計:1193025、合計チャンク時間:0.093 秒"

    また、個別の関数 `rxLogit` に固有のメッセージが表示される場合、モデル作成の一環として生成された変数とテスト メトリックを表示します。

3.  ステートメントが完了したら、テーブル *nyc_taxi_models* を開きます。 データの処理とモデルの調整には、しばらく時間がかかる場合があります。

    _[モデル]_ 列にシリアル化されたモデル、および _[名前]_ 列にモデル名 **RxTrainLogit_model** を含む、1 つの新しい行が追加されていることがわかります。

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

次の手順では、トレーニング済みのモデルを使用して予測を作成します。

## <a name="next-lesson"></a>次のレッスン

[レッスン 4:ストアド プロシージャで R モデルを使用して潜在的な結果を予測する](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>前のレッスン

[レッスン 2:R と T-SQL 関数を使用したデータ機能の作成](..//tutorials/sqldev-create-data-features-using-t-sql.md)

