---
title: Python + T-SQL:データの探索
description: SQL Server ストアド プロシージャおよび T-SQL 関数に Python を埋め込む方法について説明するチュートリアルです
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ba5f48b7788b6ebec63149175568777e6659017f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725066"
---
# <a name="explore-and-visualize-the-data"></a>データの探索および視覚化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、[SQL 開発者向けのデータベース内の Python 分析](sqldev-in-database-python-for-sql-developers.md)チュートリアルの一部です。 

この手順では、サンプル データを探索し、いくつかのプロットを生成します。 後で、Python でグラフィックス オブジェクトをシリアル化し、それらのオブジェクトを逆シリアル化してプロットする方法を学習します。

## <a name="review-the-data"></a>データを確認する

まず、NYC タクシー データを簡単に使用できるように変更を加えたため、データ スキーマを時間を取って概観してください

+ タクシーの識別情報と乗車記録には、個別のファイルが使用されていました。 _medallion_、_hack_license_、_pickup_datetime_ 列の 2 つの元のデータセットを結合しました。  
+ 元のデータセットは多くのファイルにまたがっており、非常に大きくなっていました。 レコードをダウンサンプリングし、元のレコード数の 1% のみを取得しています。 現在のデータ テーブルには、1,703,957 行と 23 列が含まれています。

**タクシーの識別子**

_medallion_ 列は、タクシーの一意の ID を表します。

_hack_license_ 列には、タクシー運転手のライセンス番号が含まれます (匿名にしてあります)。

**乗車と料金の記録**

各乗車記録には、乗車場所、降車場所、走行距離が含まれています。

各料金記録には、支払の種類、支払の合計額、チップ額など、支払情報が含まれています。

最後の 3 つの列はさまざまな機械学習タスクに利用できます。  _tip_amount_ 列には連続する数値が含まれ、回帰分析用の **label** 列として利用できます。 _tipped_ 列には yes/no 値のみが含まれ、二項分類に利用されます。 _tip_class_ 列には複数の **クラス ラベル** が含まれ、複数クラスの分類タスク用のラベルとして利用できます。

ラベル列に使用される値はすべて `tip_amount` 列に基づき、次のようなビジネス ルールが適用されます。

+ ラベル列 `tipped` には、0 と 1 の値が可能です

    `tip_amount` > 0 の場合は `tipped` = 1。それ以外の場合は `tipped` = 0

+ ラベル列 `tip_class` には、0-4 のクラス値が可能です

    クラス 0: `tip_amount` = $0

    クラス 1: `tip_amount` > $0 および `tip_amount` <= $5
    
    クラス 2: `tip_amount` > $5 および `tip_amount` <= $10
    
    クラス 3: `tip_amount` > $10 および `tip_amount` <= $20
    
    クラス 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>T-SQL で Python を使用してプロットを作成する

データ科学ソリューションの開発には、通常、集中的なデータの探索とデータの視覚化が伴います。 データの分布や外れ値を理解する上で視覚化は強力なツールとなります。Python はデータを視覚化するためのさまざまなパッケージを提供します。 **matplotlib** モジュールは、視覚化用のより一般的なライブラリの 1 つであり、ヒストグラム、散布図、ボックス プロット、およびその他のデータ探索グラフを作成するための多くの機能が含まれています。

このセクションでは、ストアド プロシージャを利用し、プロットを使用する方法について学習します。 サーバーでイメージを開くのではなく、**varbinary** データとして Python オブジェクト `plot` を格納してから、他の場所で共有または表示できるファイルに書き込みます。

### <a name="create-a-plot-as-varbinary-data"></a>varbinary データとしてプロットを作成する

このストアド プロシージャは、シリアル化された Python `figure` オブジェクトを **varbinary** データのストリームとして返します。 バイナリ データを直接表示することはできませんが、クライアントで Python コードを使用して、図を逆シリアル化して表示し、イメージ ファイルをクライアント コンピューターに保存することができます。

1. PowerShell スクリプトによってまだ作成されていない場合は、ストアド プロシージャ **PyPlotMatplotlib** を作成します。

    - 変数 `@query` によりクエリ テキスト `SELECT tipped FROM nyctaxi_sample` が定義され、スクリプト入力変数 `@input_data_1`の引数として Python コード ブロックに渡されます。
    - Python スクリプトは非常に単純です。**matplotlib** `figure` オブジェクトを使用してヒストグラムと散布図を作成し、これらのオブジェクトを `pickle` ライブラリを使用してシリアル化します。
    - Python グラフィックス オブジェクトは、出力のために **pandas** DataFrame にシリアル化されます。
  
    ```sql
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
    AS
    BEGIN
        SET NOCOUNT ON;
        DECLARE @query nvarchar(max) =
        N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
        EXECUTE sp_execute_external_script
        @language = N'Python',
        @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. 次に、引数を指定せずにストアド プロシージャを実行し、入力クエリとしてハードコーディングされたデータからプロットを生成します。

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 結果は次のようになります。
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. [Python クライアント](../python/setup-python-client-tools-sql.md)から、バイナリ プロット オブジェクトを生成した SQL Server インスタンスに接続し、プロットを表示できるようになりました。 

    これを行うには、次の Python コードを実行します。必要に応じて、サーバー名、データベース名、および資格情報を置き換えます。 クライアントとサーバーで Python のバージョンが同じであることを確認してください。 また、クライアント上の Python ライブラリ (matplotlib など) が、サーバーにインストールされているライブラリのバージョンと同じかそれ以降のバージョンであることを確認します。
  
    **SQL Server 認証を使用する:**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Windows 認証を使用する:**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  接続に成功すると、次のようなメッセージが表示されます。
  
    *プロットは、次のディレクトリに保存されます: xxxx*
  
6.  出力ファイルは、Python 作業ディレクトリに作成されます。 プロットを表示するには、Python 作業ディレクトリに移動し、ファイルを開きます。 次の図は、クライアント コンピューターに保存されているプロットを示しています。
  
    ![チップ額と料金の比較](media/sqldev-python-sample-plot.png "チップ額と料金の比較") 

## <a name="next-step"></a>次の手順

[T-SQL を使用してデータ機能を作成する](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>前の手順

[NYC タクシー データ セットをダウンロードする](demo-data-nyctaxi-in-sql.md)

