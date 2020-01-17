---
title: R チュートリアル:グラフとプロットの作成
description: SQL Server で R 言語関数を使用してグラフやプロットを作成する方法を示すチュートリアル。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 34ec0c2814dda7d2cf4bada10e5e53c05f8e08b9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724022"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>SQL と R を使用してグラフとプロットを作成する (チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

チュートリアルのこのパートでは、R を使用して SQL Server データでプロットとマップを生成する方法について説明します。 単純なヒストグラムを作成してから、より複雑なマップ プロットを作成します。

## <a name="prerequisites"></a>Prerequisites

この手順では、進行中の R セッションは、このチュートリアルの前の手順に基づいていることを前提としています。 ここでは、これらの手順で作成した接続文字列とデータ ソース オブジェクトを使用します。 スクリプトの実行には、次のツールとパッケージが使用されます。

+ R コマンドを実行する Rgui.exe
+ T-SQL を実行する Management Studio
+ googMap
+ ggmap パッケージ
+ mapproj パッケージ

## <a name="create-a-histogram"></a>ヒストグラムの作成

1. [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) 関数を利用し、最初のプロットを生成します。  rxHistogram 関数は、オープンソース R パッケージのそれと同様の機能を提供しますが、リモート実行コンテキストで実行できます。

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. この画像はお使いの開発環境の R グラフィックス デバイスで返されたものです。  たとえば、RStudio で、 **プロット** ウィンドウをクリックします。  [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]で、別個のグラフィックス ウィンドウが開きます。

    ![rxHistogram を使用して料金をプロットする](media/rsql-e2e-rxhistogramresult.png "rxHistogram を使用して料金量をプロットする")

    > [!NOTE]
    > グラフの外観が異なっていますか?
    >  
    > それは、_inDataSource_ では上位の 1000 行のみが使用されるからです。 TOP を利用した行の順序付けは ORDER BY 句なしでは非決定性となるため、データと結果のグラフが異なる可能性があります。
    > この画像は約 10,000 行のデータを利用して生成されました。 行数を変えて、実験してみることをお勧めします。お使いの環境で結果を得るためにかかった時間をメモしてください。

## <a name="create-a-map-plot"></a>マップ プロットの作成

通常、データベース サーバーによってインターネット アクセスがブロックされます。 これは、マップやその他の画像をダウンロードしてプロットを生成する必要がある R パッケージを使用する場合に、不便な場合があります。 しかし、独自のアプリケーションを開発する場合に役立つ回避策があります。 基本的に、クライアントでマップ表現を生成してから、SQL Server テーブルに属性として格納されているポイントをマップ上でオーバーレイします。

1. R プロット オブジェクトを作成する関数を定義します。 カスタム関数 *mapPlot* は、タクシーが客を乗せた場所を利用し、それぞれの場所から開始した乗車の数をプロットする散布図を作成します。 これは **ggplot2** パッケージと **ggmap** パッケージを利用します。この 2 つのパッケージは既に[インストールされ、読み込まれている](walkthrough-data-science-end-to-end-walkthrough.md#add-packages)はずです。

    ```R
    mapPlot <- function(inDataSource, googMap){
        library(ggmap)
        library(mapproj)
        ds <- rxImport(inDataSource)
        p <- ggmap(googMap)+
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,
    color="darkred", size = 1.5)
        return(list(myplot=p))
    }
    ```

    + 関数 *mapPlot* は 2 つの引数を受け取ります。RxSqlServerData を利用して先に定義した既存のデータ オブジェクトとクライアントから渡されたマップ表示です。
    + *ds* 変数で始まる行では、以前に作成したデータ ソース *inDataSource* からメモリ データを読み込むために、rxImport が使用されます (このデータ ソースには 1000 行しか含まれていません。より多くのデータ ポイントを含むマップを作成する場合は、別のデータ ソースに置き換えることができます)。
    + オープンソース R 関数を使用するときは、データをローカル メモリのデータ フレームに読み込む必要があります。 ただし、[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 関数を呼び出すことによって、リモート計算コンテキストのメモリ内で実行できます。

2. 計算コンテキストをローカルに変更し、マップの作成に必要なライブラリを読み込みます。

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + `gc` 変数は、ニューヨークにあるタイムズ スクウェアの一組の座標を保存します。

    + `googmap` で始まる行により、指定した座標を中心に据えるマップが生成されます。

3. 次に示すように、[rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) でプロット関数をラップすることで、SQL Server 計算コンテキストに切り替え、結果を表示します。 rxExec 関数は **RevoScaleR** パッケージに含まれ、リモート計算コンテキストで任意の R 関数の実行をサポートします。

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + `googMap` のマップ データは、リモートで実行される関数 *mapPlot* に引数として渡されます。 マップはローカル環境で生成されたため、SQL Server のコンテキストでプロットを作成するためには、マップを関数に渡す必要があります。

    + `plot` で始まる行を実行すると、レンダリングされたデータがローカル R 環境にシリアル化され、R クライアントで表示できるようになります。

    > [!NOTE]
    > Azure 仮想マシンで SQL Server を使用している場合は、この時点でエラーが発生する可能性があります。 Azure の既定のファイアウォール規則によって R コードによるネットワーク アクセスがブロックされると、エラーが発生します。 このエラーを修正する方法の詳細については、[Azure VM で Machine Learning (R) Services をインストールする](../install/sql-machine-learning-azure-virtual-machine.md)に関するページを参照してください。

4. 出力プロットは次の図のようになります。 乗車場所が赤い点でマップ上に追加されます。 使用したデータ ソースに格納されている場所の数によっては、画像が異なる場合があります。

    ![カスタム R 関数を使用してタクシーの乗車をプロットする](media/rsql-e2e-mapplot.png "カスタム R 関数を使用してタクシーの乗車をプロットする")

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [R と SQL を使用してデータ機能を作成する](walkthrough-create-data-features.md)
