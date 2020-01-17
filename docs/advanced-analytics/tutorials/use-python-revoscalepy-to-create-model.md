---
title: Python モデルの作成 - revoscalepy
description: SQL Server でリモートで実行されるデータ サイエンス モデルを作成するには、revoscalepy 関数を使用して Python スクリプトを書き込みます。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5faa8688f3036f80b947ccc5d99c09c4612f26fb
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724449"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Python と revoscalepy を使用して、SQL Server でリモートで実行されるモデルを作成します
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft の [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python ライブラリでは、データの探索、視覚化、変換、解析のためのデータ サイエンス アルゴリズムを提供しています。 このライブラリは、SQL Server での Python による統合シナリオにおいて戦略的に重要です。 マルチコア サーバーでは、**revoscalepy** 関数を並列で実行できます。 中央サーバーとクライアント ワークステーションを使用した分散アーキテクチャ (それぞれの物理コンピューターが同じ **revoscalepy** ライブラリを保持) では、ローカルで Python コードを記述できますが、実行はデータが存在するリモートの SQL Server インスタンスに移って行います。

**revoscalepy** については、次の Microsoft 製品およびディストリビューションを参照してください。

+ [SQL Server Machine Learning Services (データベース内)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (非 SQL、スタンドアロン サーバー)](https://docs.microsoft.com/machine-learning-server/index)
+ [クライアント側の Python ライブラリ (開発ワークステーション用)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

この演習では、[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) で線形回帰モデルを作成する方法を学びます。これは、コンピューティング コンテキストを入力として受け入れる **revoscalepy** のアルゴリズムの1つです。 この演習で実行するコードは、リモート コンピューティング コンテキストを有効にする **revoscalepy** 関数によって、コードの実行をローカルからリモート コンピューティング環境にシフトします。

このチュートリアルを完了すると、次のことを行うことができます。

> [!div class="checklist"]
> * **revoscalepy** を使用して線形モデルを作成する
> * ローカルからリモート コンピューティング コンテキストへ操作をシフトする

## <a name="prerequisites"></a>Prerequisites

この演習で使用されるサンプル データは、[**フライトデータ**](demo-data-airlinedemo-in-sql.md) データベースです。

この記事のサンプルコードを実行するには IDE が必要です。また、IDE は Python 実行可能ファイルにリンクされている必要があります。

コンピューティング コンテキスト シフトを実践するには、[ローカル ワークステーション](../python/setup-python-client-tools-sql.md)と、[Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) と Python が有効になっている SQL Server データベース エンジン インスタンスが必要です。 

> [!Tip]
> コンピューターが 2 台ない場合は、関連するアプリケーションをインストールすることによって、1 台の物理コンピューター上でリモート コンピューティング コンテキストをシミュレートできます。 まず、[SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) のインストールを "リモート" インスタンスとして操作します。 次に、[の Python クライアント ライブラリのインストールをクライアント](../python/setup-python-client-tools-sql.md)として操作します。 同じマシン上に同じ Python ディストリビューションと Microsoft Python ライブラリのコピーを2つ作成します。 この演習を正常に完了するには、ファイル パスと使用している Python.exe のコピーを記録しておく必要があります。

## <a name="remote-compute-contexts-and-revoscalepy"></a>リモート コンピューティング コンテキストと revoscalepy

このサンプルでは、リモート コンピューティング コンテキストで Python モデルを作成するプロセスを示します。これにより、クライアントから作業を行うことができますが、SQL Server、Spark、Machine Learning Server など、操作が実際に実行されるリモート環境を選択できます。 リモート コンピューティング コンテキストの目的は、データが存在する場所で計算させることです。

SQL Server で Python コードを実行するには、**revoscalepy** パッケージが必要です。 これは、Microsoft が提供する特殊な Python パッケージで、R 言語用の **RevoScaleR** パッケージと似ています。 **revoscalepy** パッケージは、コンピューティング コンテキストの作成をサポートし、ローカル ワークステーションとリモート サーバーの間でデータとモデルを渡すためのインフラストラクチャを提供します。 データベース内コードの実行をサポートする **revoscalepy** 関数は、[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) です。

このレッスンでは、SQL Server のデータを使用して、非常に大規模なデータセットに対する回帰をサポートする **revoscalepy** の関数である [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) で線形モデルをトレーニングします。 

このレッスンでは、設定方法の基本を説明し、その後 Python での **SQL Server コンピューティング コンテキスト**の使用についても説明します。 コンピューティング コンテキストが他のプラットフォームとどのように機能し、どのコンピューティング コンテキストがサポートされるかについては、「[Machine Learning Server でのスクリプト実行のコンピューティング コンテキスト](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)」を参照してください。


## <a name="run-the-sample-code"></a>サンプル コードを実行します。

データベースを準備し、トレーニング用のデータをテーブルに格納したら、Python 開発環境を開き、サンプル コードを実行します。

このコードでは、次の手順を実行します。

1. 必要なライブラリと関数をインポートします。
2. SQL Server への接続を作成します。 データを操作するための**データソース** オブジェクトを作成します。
3. ロジスティック回帰アルゴリズムで使用できるように**変換**を使用してデータを変更します。
4. `rx_lin_mod` を呼び出し、モデルに適合する数式を定義します。
5. 元のデータに基づいて一連の予測を生成します。
6. 予測値に基づいて概要を作成します。

すべての操作は、コンピューティング コンテキストとして SQL Server のインスタンスを使用して実行されます。

> [!NOTE]
> このサンプルをコマンド ラインから実行する方法については、次のビデオを参照してください。[Python を使用した SQL Server 2017 Advanced Analytics](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>サンプル コード

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>データ ソースの定義とコンピューティング コンテキストの定義

データ ソースは、コンピューティング コンテキストとは異なります。 *データ ソース*は、コードで使用されるデータを定義します。 コンピューティング コンテキストは、コードが実行される場所を定義します。 ただし、同じ情報の一部を使用します。

+ `sql_query` や `sql_connection_string` などの Python 変数は、データのソースと定義します。 

    これらの変数を [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) コンストラクターに渡して、`data_source`という名前の**データソース オブジェクト**を実装します。

+ [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) コンストラクターを使用して**コンピューティング コンテキスト オブジェクト**を作成します。 結果として得られる**コンピューティング コンテキスト　オブジェクト**には、`sql_cc`という名前が付けられます。

    この例では、データ ソースで使用した同じ接続文字列を再利用します。これは、コンピューティング コンテキストとして使用するのと同じ SQL Server インスタンスにデータがあることを前提としています。 
    
    ただし、データ ソースとコンピューティング コンテキストは、異なるサーバー上に存在している可能性があります。
 
### <a name="changing-compute-contexts"></a>コンピューティング コンテキストの変更

コンピューティング コンテキストを定義したら、**アクティブなコンピューティング コンテキスト**を設定する必要があります。 

既定では、ほとんどの操作はローカルで実行されます。つまり、別のコンピューティング コンテキストを指定しない場合、データはデータ ソースからフェッチされ、コードは現在の Python 環境で実行されます。

アクティブなコンピューティング コンテキストを設定するには、次の 2 つの方法があります。
+ メソッドまたは関数の引数として
+ `rx_set_computecontext`を呼び出す

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>コンピューティング コンテキストをメソッドまたは関数の引数として設定する

この例では、個々の **rx** 関数の引数を使用して、コンピューティング コンテキストを設定します。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

このコンピューティング コンテキストは [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) の呼び出しで再利用されます。

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rx_set_compute_context"></a>Rx_set_compute_context を使用してコンピューティング コンテキストを明示的に設定する

関数 [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) を使用すると、既に定義されているコンピューティング コンテキスト間で切り替えることができます。

アクティブなコンピューティング コンテキストを設定した後は、変更するまでアクティブ状態のままになります。

### <a name="using-parallel-processing-and-streaming"></a>並列処理とストリーミングの使用

コンピューティング コンテキストを定義する場合、コンピューティング コンテキストによるデータの処理方法を制御するパラメーターを設定することもできます。 これらのパラメーターは、データ ソースの種類によって異なります。

SQL Server のコンピューティング コンテキストでは、バッチ サイズを設定したり、実行中のタスクで使用する並列処理の次数に関するヒントを指定したりすることができます。

+ このサンプルは 4 つのプロセッサを搭載したコンピューター上で実行されているため、`num_tasks` パラメーターを 4 に設定して、リソースを最大限に活用できるようにします。 
+ この値を0に設定した場合、SQL Server は既定値を使用します。これは、サーバーの現在の MAXDOP 設定により、できるだけ多くのタスクを並列処理します。 ただし、割り当てられる可能性のあるタスクの正確な数は、サーバーの設定や実行されている他のジョブなど、様々な要因によって異なります。

## <a name="next-steps"></a>次の手順

これらの追加の Python サンプルとチュートリアルでは、より複雑なデータ ソースを使用したエンドツーエンドのシナリオだけでなく、リモート コンピューティング コンテキストの使用についても紹介します。

+ [SQL 開発者向け In-Database Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python と SQL Server を使用した予測モデルの作成](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
