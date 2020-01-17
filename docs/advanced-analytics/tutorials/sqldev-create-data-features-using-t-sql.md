---
title: R + T-SQL チュートリアル:データ機能
description: R 機械学習モデルで使用するために計算をストアド プロシージャに追加する方法を示すチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6970fd92fc1b655e0df66cdb548a044e3bdc746e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725761"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>レッスン 2:R と T-SQL を使用してデータ機能を作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、SQL Server で R を使用する方法に関する SQL 開発者向けのチュートリアルの一部です。

この手順では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を利用し、生データから機能を作成する方法について説明します。 その後、その関数をストアド プロシージャから呼び出し、機能の値を含むテーブルを作成します。

## <a name="about-feature-engineering"></a>機能エンジニアリングについて

データ探索を何度か行うと、データからインサイトが収集されているので、 *機能エンジニアリング*に移ることができます。 生データから意味のある特徴を作成するこのプロセスは、分析モデルを作成するための重要な手順です。

このデータセットでは、距離の値は報告されたメーター距離に基づいており、必ずしも地理的距離や実際の走行距離を示す距離を表しているとは限りません。 そのため、ソースである NYC タクシー データセットの座標を利用し、乗車地点と降車地点の間の直接距離を計算する必要があります。 カスタム [関数で](https://en.wikipedia.org/wiki/Haversine_formula) Haversine 式 [!INCLUDE[tsql](../../includes/tsql-md.md)] を利用し、この計算を実行できます。

1 つ目のカスタム T-SQL 関数、 _fnCalculateDistance_を利用し、Haversine 式で距離を計算し、2 つ目のカスタム T-SQL 関数、 _fnEngineerFeatures_を利用し、すべての機能を含むテーブルを作成します。

全体的なプロセスは次のとおりです。

- 計算を実行する T-SQL 関数を作成する

- 関数を呼び出して機能データを生成します

- 機能データをテーブルに保存する

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>fnCalculateDistance を利用して乗車距離を計算する

このチュートリアルの準備の一環として、関数 _fnCalculateDistance_ をダウンロードし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録する必要があります。 少し時間をかけてコードを確認してください。
  
1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、 **[プログラミング]** 、 **[関数]** 、 **[スカラー値関数]** の順に展開します。   

2. _fnCalculateDistance_を右クリックし、 **[変更]** を選択し、新しいクエリ ウィンドウで [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを開きます。
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
    RETURNS float  
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
    GO
    ```
  
    - この関数はスカラー値関数であり、事前定義されている種類の単一データ値を返します。
  
    - 乗車場所と降車場所から取得した緯度値と経度値を入力値として受け取ります。 Haversine 式は場所をラジアンに変換し、その値を利用して 2 場所間の直接距離をマイルで計算します。

## <a name="generate-the-features-using-_fnengineerfeatures_"></a>_fnEngineerFeatures を使用して機能を生成する_

モデルのトレーニングに使用できるテーブルに計算値を追加するには、別の関数 _fnEngineerFeatures_を使用します。 この新しい関数は、以前に作成した T-SQL 関数 _fnCalculateDistance_を呼び出して、乗車場所と降車場所の距離を直接取得します。 

1. カスタム T-SQL 関数、 _fnEngineerFeatures_のコードを再確認します。この関数は、このチュートリアルの一環として自動的に作成されているはずです。
  
    ```sql
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + このテーブル値関数は、複数の列を入力値として受け取り、複数の機能列を含むテーブルを出力します。

    + この関数の目的は、モデルの構築に利用する新しい機能を作成することです。

2.  この関数が動作することを確認するために、それを利用し、メーター距離が 0 であったが、乗車場所と降車場所が異なっていた乗車の地理的距離を計算できます。
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    ご覧のとおり、メーターによって報告された距離と地理的距離は常に一致しているわけではありません。 そのため、機能エンジニアリングが重要となります。 これらの改善されたデータ機能を使用して、R を使用して機械学習モデルをトレーニングすることができます。

## <a name="next-lesson"></a>次のレッスン

[レッスン 3:T-SQL を使用してモデルをトレーニングし保存する](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>前のレッスン

[レッスン 1:R と保存済み手続きを使用したデータの探索と視覚化](sqldev-explore-and-visualize-the-data.md)
