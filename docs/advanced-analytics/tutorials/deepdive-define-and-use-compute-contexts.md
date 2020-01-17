---
title: RevoScaleR コンピューティング コンテキストを使用する
description: SQL Server 上で R 言語を使用してコンピューティング コンテキストを定義する方法に関するチュートリアルです。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0ae3f3ac7747410730cb91cf56733130ab9f0abb
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727200"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>コンピューティング コンテキストの定義と使用 (SQL Server と RevoScaleR のチュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

前のレッスンでは、**RevoScaleR** 関数を使用してデータ オブジェクトを検査しました。 このレッスンでは、リモート SQL Server のコンピューティング コンテキストを定義できる、[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 関数について説明します。 リモートのコンピューティング コンテキストを使用すると、ローカル セッションからサーバー上のリモート セッションに R の実行をシフトできます。 

> [!div class="checklist"]
> * リモート SQL Server のコンピューティング コンテキストの要素について学ぶ
> * コンピューティング コンテキスト オブジェクトでトレースを有効にする

**RevoScaleR** では、複数のコンピューティング コンテキストがサポートされています。Hadoop、HDFS 上の Spark、およびデータベース内の SQL Server。 SQL Server の場合、**RxInSqlServer** 関数がサーバー接続に使用され、ローカル コンピューターとリモート実行コンテキストの間でオブジェクトを渡します。

## <a name="create-and-set-a-compute-context"></a>コンピューティング コンテキストを作成および設定する

SQL Server コンピューティング コンテキストを作成する **RxInSqlServer** 関数は、次の情報を使用します。

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの接続文字列
+ 出力の処理方法の指定
+ 共有データ ディレクトリの指定 (省略可能)
+ トレースを有効にするかトレース レベルを指定する、省略可能な引数

このセクションでは、それぞれの手順について説明します。

1. 計算を実行するインスタンスの接続文字列を指定します。 前に作成した接続文字列を再利用できます。

    **SQL ログインを使用する**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Windows 認証を使用する**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 出力の処理方法を指定します。 次の操作を処理する前に、サーバー上で R ジョブの結果を待つようにローカル R セッションに指示するスクリプトを次に示します。 また、リモートの計算からの出力が、ローカル セッションに表示されないようにします。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* に渡す **wait** 引数は、次のオプションをサポートします。
  
    -   **TRUE**。 ジョブはブロック中として構成され、制御は完了するか失敗するまで戻りません。  詳細については、「[Machine Learning Server での分散コンピューティングと並列コンピューティング](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)」に関するページを参照してください。
  
    -   **FALSE**。 ジョブは非ブロックとして構成され、制御は直ちに戻ります。これにより、引き続き他の R コードを実行することができます。 ただし、非ブロック モードであっても、ジョブの実行中は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とのクライアント接続を維持する必要があります。

3. 必要に応じて、ローカルの R セッション、およびリモートの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューターとそのアカウントによって共有される、ローカル ディレクトリの場所を指定します。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   共有のために特定のディレクトリを手動で作成する場合は、次のような行を追加します。

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. **RxInSqlServer** コンストラクターに引数を渡して、*コンピューティング コンテキスト オブジェクト*を作成します。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    **RxInSqlServer** の構文は、前にデータソースを定義するために使用した **RxSqlServerData** 関数とほぼ同じです。 しかし、次に示すいくつかの重要な相違点があります。
      
    - [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)関数を使用して定義するデータ ソース オブジェクトは、データの保存場所を指定します。
    
    - これに対し、関数 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) を使用して定義されたコンピューティング コンテキストは、集計やその他の計算を実行する場所を指定します。
    
    計算コンテキストを定義しても、ワークステーションで実行されるその他の一般的な R 計算に影響なく、データのソースは変わりません。 たとえば、データ ソースとしてローカル テキスト ファイルを定義できますが、計算コンテキストを SQL Server に変更し、すべての読み取りと集計を SQL Server コンピューター上のデータに対して行うことができます。

5. リモート コンピューティング コンテキストをアクティブ化します。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. プロパティを含む、コンピューティング コンテキストに関する情報を返します。

    ```R
    rxGetComputeContext()
    ```

7. "local" キーワードを指定して、コンピューティング コンテキストをローカル コンピューターに戻します (次のレッスンでは、リモート コンピューティング コンテキストの使用方法を示します)。

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> この関数でサポートされているその他のキーワードの一覧が必要な場合、R コマンド ラインに「 `help("rxSetComputeContext")` 」と入力してください。

## <a name="enable-tracing"></a>トレースを有効にする

リモート計算コンテキストで実行すると、ローカル コンテキストで動作する操作で問題が発生することがあります。 問題を分析したりパフォーマンスを監視したりする場合は、実行時のトラブルシューティングを支援するために、コンピューティング コンテキストでトレースを有効にすることができます。

1. 同じ接続文字列を使用する新しいコンピューティング コンテキストを作成しますが、引数 *traceEnabled* と *traceLevel* を、**RxInSqlServer** コンストラクターに追加します。

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
   この例では、*traceLevel* プロパティを 7 に設定してあります。これは、"すべてのトレース情報を表示する" ことを意味します。

2. トレースが有効なコンピューティング コンテキストを名前で指定するには、[rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 関数を使用します。

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>次の手順

サーバーまたはローカルで R コードを実行するように、コンピューティング コンテキストを切り替える方法について説明します。

> [!div class="nextstepaction"]
> [ローカルとリモートのコンピューティング コンテキストで概要統計情報を計算する](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)