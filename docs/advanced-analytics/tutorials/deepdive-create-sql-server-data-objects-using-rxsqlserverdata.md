---
title: RxSqlServerData オブジェクトを作成する
description: このチュートリアルは、SQL Server で R 言語を使用してデータ オブジェクトを作成する方法について詳しく説明しています。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb6c88c5ce53a072d8cd9611d80cbe621c0fa485
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727261"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>RxSqlServerData を使用した SQL Server のデータ オブジェクトを作成する (SQL Server および RevoScaleR チュートリアル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このレッスンは、SQL Server で [RevoScaleR 関数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)を使用する方法についての [RevoScaleR チュートリアル](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)の一部です。

レッスン 2 は、データベースの作成の続きで、テーブルの追加とデータの読み込みについてです。 [レッスン 1](deepdive-work-with-sql-server-data-using-r.md) で、DBA がデータベースを作成しログインした場合、RStudio などの R IDE または **Rgui** などの組み込みツールを使用してテーブルを追加できます。

R から、SQL Server に接続し、**RevoScaleR** 関数を使用して次のタスクを実行します。

> [!div class="checklist"]
> * トレーニング データと予測用のテーブルを作成する
> * ローカルの .csv ファイルからのデータを使用してテーブルを読み込む

サンプル データは、クレジット カード不正データ (ccFraud データセット) をシミュレートしたもので、トレーニング データ セットとスコアリング データセットにパーティション分割されています。 データ ファイルは **RevoScaleR** に含まれています。

これらのタスクを完了するには、R IDE または **Rgui** を使用します。 必ず次の場所にある R 実行可能ファイルを使用してください。C:\Program Files\Microsoft\R Client \ R_SERVER \bin\x64 (そのツールを使用している場合は Rgui、または R IDE で C:\Program Files\Microsoft\R Client\R_SERVER を指定)。 [R クライアント ワークステーション](../r/set-up-a-data-science-client.md)にこれらの実行可能ファイルがあることを、このチュートリアルの前提条件としています。

## <a name="create-the-training-data-table"></a>トレーニング データ テーブルを作成する

1. データベース接続文字列を R 変数に格納します。 SQL Server に対する有効な ODBC 接続文字列の例を下記に 2 つ示します。1 つは SQL ログインを使用するもので、もう 1 つは Windows 統合認証を使用するものです。 

   サーバー名、ユーザー名、およびパスワードは必ず適切なものに変更してください。

    **SQL ログイン**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Windows 認証**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. 作成するテーブルの名前を指定し、R 変数に保存します。
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    サーバー インスタンスとデータベースの名前は接続文字列の一部として既に指定されているので、2 つの変数を組み合わせると、新しいテーブルの*完全修飾*名は、*instance.database.schema.ccFraudSmall* となります。
  
3.  必要に応じて、*rowsPerRead* を指定して、各バッチで読み込まれるデータ行の数を制御します。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    このパラメーターは省略可能ですが、これを設定すると、より効率的に計算できます。 **RevoScaleR** および **MicrosoftML** のほどんどの各著された分析関数は、チャンクでデータを処理します。 *rowsPerRead* パラメーターは、各チャンクで行数を決定します。
  
    適切なバランスを見つけるために、この設定を試してみることが必要な場合があります。 値が大きすぎる場合、そのサイズのチャンクでデータを処理するのに十分なメモリがないと、データ アクセスの速度が低下する可能性があります。 逆に、一部のシステムでは、*rowsPerRead* の値が小さすぎると、パフォーマンスが低下する可能性もあります。
  
    初期値として、データベース エンジン インスタンスによって定義された既定のバッチ処理サイズを使用して、各チャンク内の行の数を制御します (5000 行)。 この値を変数 *sqlRowsPerRead* に保存します。
  
4.  新しいデータ ソース オブジェクトの変数を定義し、前に **RxSqlServerData** コンストラクターに対して定義した引数を渡します。 ここではデータ ソース オブジェクトが作成されるだけで、設定は行われないことに注意してください。 データの読み込みは別の手順です。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>スコアリング データ テーブルを作成する

同じ手順を使用し、スコアリング データを保持するテーブルを同じプロセスを使用して作成します。

1. スコア付けで使用するテーブルの名前を格納するための新しい R 変数 *sqlScoreTable*を作成します。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. その変数を引数として **RxSqlServerData** 関数に渡して、2 つ目のデータ ソース オブジェクト *sqlScoreDS*を定義します。
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

接続文字列およびその他のパラメーターは変数として R ワークスペースに定義済みであるため、異なるテーブル、ビュー、クエリを表す新しいデータ ソース用にそれを再利用することができます。

> [!NOTE]
> この関数では、クエリに基づくデータ ソースよりも、テーブル全体に基づいたデータ ソースの定義に異なる引数を使用します。 これは、SQL Server データベース エンジンがクエリを別に準備する必要があるためです。 このチュートリアルの後の方で、SQL クエリを使用してデータ ソース オブジェクトを作成する方法について説明します。

## <a name="load-data-into-sql-tables-using-r"></a>R を使用して SQL テーブルにデータを読み込む

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルが作成されましたので、それらのテーブルには、適切な **Rx** 関数を使用してデータを読み込むことができます。

**RevoScaleR** パッケージには、データソースの種類に固有の関数が含まれています。 テキスト データの場合は、[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) を使用して、データ ソース オブジェクトを生成します。 その他に、Hadoop データや ODBC データなどからデータ ソース オブジェクトを作成するための関数もあります。

> [!NOTE]
> このセクションでは、データベースに対する **Execute DDL** アクセス許可が必要です。

### <a name="load-data-into-the-training-table"></a>トレーニング用のテーブルにデータを読み込む

1. R 変数 *ccFraudCsv* を作成し、サンプル データを含む CSV ファイルへのパスをこの変数に割り当てます。 このデータ セットは、**RevoScaleR** で提供されています。 "sampleDataDir" は、**rxGetOption** 関数のキーワードです。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    **rxGetOption** の呼び出しに注意してください。これは、**RevoScaleR** の [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) に関連付けられている GET メソッドです。 このユーティリティを使用して、既定の共有ディレクトリや計算で使用するプロセッサ (コア) の数などの、ローカルおよびリモートのコンピューティング コンテキストに関連するオプションを設定し一覧表示します。
    
    この特定の呼び出しによって、コードを実行している場所に関係なく、正しいライブラリからサンプルを取得します。 たとえば、SQL Server で関数を実行し、開発用コンピューターでパスがどのように違うかを確認してください。
  
2. 新しいデータを格納する変数を定義し、 **RxTextData** 関数を使用してテキスト データ ソースを指定します。
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    引数 *colClasses* は重要です。 この引数は、テキスト ファイルから読み込まれたデータの各列に割り当てるデータ型を指定するために使用します。 この例では、すべての列がテキストとして扱われます。例外として、名前付きの列は整数として扱われます。
  
3. この時点で、少し間を置いてから、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でデータベースを表示できます。 データベース内のテーブルの一覧を更新します。
  
    ローカル ワークスペースには R データ オブジェクトが作成されているが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにはテーブルが作成されていないのがわかります。 また、テキスト ファイルから R 変数に読み込まれたデータもありません。
  
4. [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 関数を呼び出して、データを挿入します。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    接続文字列に問題がなければ、しばらくすると、次のような結果が表示されます。
  
    *合計書き込み行数:10000、合計時間:0.466* *読み取られる行:10000、処理された行数の合計:10000、合計チャンク時間:0.577 秒*
  
5. テーブルの一覧を更新します。 各変数に適切なデータ型が格納されていること、また各変数が正常にインポートされたことを確認するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でテーブルを右クリックして、 **[上位 1000 行の選択]** を選択してもかまいません。

### <a name="load-data-into-the-scoring-table"></a>スコアリング用テーブルにデータを読み込む

1. この手順を繰り返して、スコアリングに使用されるデータ セットをデータベースに読み込みます。
  
    まず、ソース ファイルへのパスを指定します。
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. **RxTextData** 関数を使用してデータを取得し、それを変数 *inTextData*に保存します。
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  **rxDataStep** 関数を呼び出して、現在のテーブルを新しいスキーマとデータで上書きします。
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - *inData* 引数では、使用するデータ ソースを定義します。
  
    - *OutFile* 引数では、データを保存する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内のテーブルを指定します。
  
    - テーブルが既に存在しているために*上書き*オプションを使用しない場合は、切り捨てなしで結果が挿入されます。
  
ここでも、接続に成功した場合は、完了を示すメッセージと、テーブルへのデータ書き込みに要した時間が表示されます。

*合計書き込み行数:10000、合計時間:0.384*
*読み取られる行:10000、処理された行数の合計:10000、合計チャンク時間:0.456 秒*

## <a name="more-about-rxdatastep"></a>rxDataStep に関する詳細情報

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) は、R データ フレームに対して複数の変換を実行できる強力な関数です。 rxDataStep を使用して、変換先に必要な表現 (この場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) にデータを変換することもできます。

必要に応じて、**rxDataStep** への引数で R 関数を使用して、データの変換を指定できます。 これらの操作の例については、このチュートリアルで後述します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [SQL Server データに対するクエリおよび変更](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)