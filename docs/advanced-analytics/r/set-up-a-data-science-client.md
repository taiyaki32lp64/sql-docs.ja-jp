---
title: R データ サイエンス クライアントをセットアップする
description: SQL Server にリモート接続するために、開発ワークステーションにローカルの R ライブラリとツールをインストールします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 643de4d56692687b7c88b88c712fb1cc478eb0a1
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727381"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>SQL Server で R 開発用のデータ サイエンス クライアントをセットアップする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) または [SQL Server Machine Learning Services (データベース内)](../install/sql-machine-learning-services-windows-install.md) のインストール時に R 言語オプションを含めた場合、SQL Server 2016 以降で R 統合を使用できます。 

SQL Server 用の R ソリューションを開発してデプロイするには、[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) を開発ワークステーションにインストールし、[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) やその他の R ライブラリを入手します。 リモート SQL Server インスタンスでも必要な RevoScaleR ライブラリは、両方のシステム間での計算要求を調整します。 

この記事では、R クライアント開発ワークステーションを構成して、機械学習と R 統合のために有効になっているリモート SQL Server と対話できるようにする方法について説明します。 この記事の手順を完了すると、SQL Server にあるものと同じ R ライブラリが得られます。 また、ローカル R セッションから SQL Server 上のリモート R セッションに計算をプッシュする方法についても説明します。

![クライアント/サーバー コンポーネント](media/sqlmls-r-client-revo.png "ローカルおよびリモートの R セッションとライブラリ")

インストールを検証するには、この記事で説明されているように組み込みの **RGUI** ツールを使用するか、または RStudio もしくは通常使用する他の IDE に[ライブラリをリンクする](#install-ide)ことができます。

> [!Note]
> クライアント ライブラリのインストールの代替手段は、[スタンドアロン サーバー](../install/sql-machine-learning-standalone-windows-install.md)をリッチ クライアントとして使用することです。これは、より高度なシナリオの作業の場合に、一部のお客様に好まれます。 スタンドアロン サーバーは SQL Server から完全に切り離されていますが、同じ R ライブラリがあるため、SQL Server データベース内分析のクライアントとして使用できます。 また、他のデータ プラットフォームからデータをインポートおよびモデル化する機能など、SQL に関連しない作業にも使用できます。 スタンドアロン サーバーをインストールする場合、R 実行可能ファイルはこの場所 (`C:\Program Files\Microsoft SQL Server\140\R_SERVER`) にあります。 インストールを検証するには、[R コンソール アプリを開き](#R-tools)、その場所で R.exe を使用してコマンドを実行します。

## <a name="commonly-used-tools"></a>一般的に使用されるツール

SQL を初めて使用する R 開発者、または R とデータベース内分析を初めて使用する SQL 開発者である場合、データベース内分析のすべての機能を実行するには、R 開発ツールと [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) などの T-SQL クエリ エディターの両方が必要になります。

単純な R 開発シナリオでは、RGUI 実行可能ファイルを使用できます。これは、MRO および SQL Server の R 基本ディストリビューションにバンドルされています。 この記事では、ローカルとリモートの R セッションの両方で RGUI を使用する方法について説明します。 生産性を向上させるには、[RStudio や Visual Studio](#install-ide) などの完全な機能を備えた IDE を使用する必要があります。

SSMS は個別にダウンロードします。これは、R コードが含まれているものを含め、SQL Server でストアド プロシージャを作成および実行する場合に便利です。 開発環境で記述する R コードは、ほとんどすべてストアド プロシージャに埋め込むことができます。 他のチュートリアルでは、[SSMS と埋め込み R](../tutorials/sqldev-in-database-r-for-sql-developers.md) について学習できます。

## <a name="1---install-r-packages"></a>1 - R パッケージをインストールする

Microsoft の R パッケージは、複数の製品およびサービスで利用できます。 ローカル ワークステーションでは、Microsoft R Client をインストールすることをお勧めします。 R Client には、[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)、[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)、[SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)、およびその他の R パッケージが用意されています。

1. [Microsoft R Client をダウンロードします](https://aka.ms/rclient/download)。

2. インストール ウィザードで、既定のインストール パスに同意するかまたは変更し、コンポーネントの一覧に同意するかまたは変更し、Microsoft R Client ライセンス条項に同意します。

  インストールが完了すると、ようこそ画面に製品とドキュメントが紹介されます。

3. Intel Math Kernel Library (MKL) 計算での一貫性のある出力を保証するために、MKL_CBWR システム環境変数を作成します。

  + コントロール パネルで、 **[システムとセキュリティ]**  >  **[システム]**  >  **[システムの詳細設定]**  >  **[環境変数]** の順にクリックします。
  + **MKL_CBWR** という名前の新しいシステム変数を作成し、値を **AUTO** に設定します。

## <a name="2---locate-executables"></a>2 - 実行可能ファイルの検索

インストール フォルダーの内容を見つけ出して一覧表示し、R.exe、RGUI、およびその他のパッケージがインストールされていることを確認します。 

1. エクスプローラーで C:\Program Files\Microsoft\R Client\R_SERVER\bin フォルダーを開き、R.exe の場所を確認します。

2. x64 サブフォルダーを開き、**RGUI** を確認します。 このツールは次の手順で使用します。

3. C:\Program Files\Microsoft\R Client\R_SERVER\library を開き、RevoScaleR、MicrosoftML その他を含む、R Client と共にインストールされたパッケージの一覧を確認します。


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - RGUI を開始する

SQL Server と共に R をインストールすると、RGui、Rterm などの、すべての R の基本インストールで標準となる R ツールと同じものが得られます。 これらのツールは軽量で、パッケージとライブラリの情報をチェックしたり、アドホック コマンドやスクリプトを実行したり、チュートリアルを実行したりするのに便利です。 これらのツールを使用して R バージョン情報を取得し、接続性を確認することができます。

1. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 を開き、 **[RGui]** をダブルクリックして、R コマンド プロンプトで R セッションを開始します。

  Microsoft プログラム フォルダーから R セッションを開始すると、RevoScaleR を含むいくつかのパッケージが自動的に読み込まれます。 

2. RevoScaleR パッケージのバージョン情報を返すには、コマンド プロンプトで「`print(Revo.version)`」と入力します。 RevoScaleR のバージョン 9.2.1 または 9.3.0 が必要です。

3. インストールされているパッケージの一覧については、R プロンプトで「**search ()** 」と入力してください。

   ![R の読み込み時のバージョン情報](../install/media/rclient-rgui-r-prompt.png "R プロンプトを開く")


## <a name="4---get-sql-permissions"></a>4 - SQL のアクセス許可を取得する

R クライアントでは、R の処理は 2 つのスレッドとメモリ内データで制限されています。 複数のコアと大規模なデータセットを使用するスケーラブルな処理の場合は、リモート SQL Server インスタンスのデータセットと計算能力に実行をシフト (*コンピューティング コンテキスト*と呼ばれます) できます。 これは、実稼働 SQL Server インスタンスとクライアントの統合のために推奨される方法です。この方法を使用するには、アクセス許可と接続情報が必要です。

スクリプトを実行してデータをアップロードするために SQL Server のインスタンスに接続するには、データベース サーバーでの有効なログインが必要です。 SQL ログインまたは統合 Windows 認証を使用できます。 一般的には Windows 統合認証を使用することをお勧めしますが、一部のシナリオでは、特にスクリプトに外部データへの接続文字列が含まれている場合は、SQL ログインを使用する方が簡単です。

少なくとも、コードの実行に使用するアカウントには、操作するデータベースから読み取るためのアクセス許可に加え、特別なアクセス許可である EXECUTE ANY EXTERNAL SCRIPT が必要です。 ほとんどの開発者には、ストアド プロシージャを作成し、トレーニング データまたはスコア付きデータを含むテーブルにデータを書き込むためのアクセス許可も必要です。 

R を使用するデータベースで[アカウントに次のアクセス許可を構成する](../security/user-permission.md)ように、データベース管理者に依頼してください。

+ **EXECUTE ANY EXTERNAL SCRIPT** - サーバー上で R スクリプトを実行します。
+ **db_datareader** 特権 - モデルのトレーニングに使用するクエリを実行します。
+ **db_datawriter** - トレーニング データまたはスコア付きデータを書き込みます。
+ **db_owner** - ストアド プロシージャ、テーブル、関数などのオブジェクトを作成します。 
  サンプルを作成し、データベースをテストする場合は、**db_owner** も必要です。 

SQL Server と共に既定でインストールされないパッケージをコードが必要とする場合は、データベース管理者に連絡して、インスタンスと共にパッケージがインストールされるようにしてください。 SQL Server はセキュリティで保護された環境であり、パッケージをインストールできる場所に制限があります。 詳細については、「[SQL Server に新しい R パッケージをインストールする](install-additional-r-packages-on-sql-server.md)」に関するページを参照してください。

## <a name="5---test-connections"></a>5 - 接続のテスト

 検証手順として、**RGUI** と RevoScaleR を使用して、リモート サーバーへの接続性を確認します。 SQL Server が[リモート接続](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server)に対して有効になっている必要があります。また、接続先のユーザー ログインやデータベースなどのアクセス許可が必要です。 

次の手順では、[NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md) のデモ データベース、および Windows 認証を想定しています。

1. クライアント ワークステーションで **RGUI** を開きます。 たとえば、`~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` にアクセスし、**RGui.exe** をダブルクリックして起動します。

2. RevoScaleR は自動的に読み込まれます。 コマンド「`print(Revo.version)`」を実行して、RevoScaleR が動作可能であることを確認します。

3. リモート サーバーで実行するデモ スクリプトを入力します。 次のサンプル スクリプトを変更して、リモート SQL Server インスタンスの有効な名前を含める必要があります。 このセッションはローカル セッションとして開始されますが、**rxSummary** 関数はリモート SQL Server インスタンスで実行されます。

  ```R
  # Define a connection. Replace server with a valid server name.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
  # Specify the input data in a SQL query.
  sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
  # Define a remote compute context based on the remote server.
  cc <-RxInSqlServer(connectionString=connStr)

  # Execute the function using the remote compute context.
  rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
  ```

  **結果:**

  このスクリプトは、リモート サーバー上のデータベースに接続し、クエリを提供し、リモート コードの実行のためにコンピューティング コンテキスト `cc` 命令を作成します。次に、RevoScaleR 関数 **rxSummary** を提供して、クエリ結果の統計サマリーを返します。

  ```R
    Call:
  rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
      connectionString = connStr), computeContext = cc)

  Summary Statistics Results for: ~.
  Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
  Number of valid observations: 100 
  
  Name       Mean   StdDev   Min Max ValidObs MissingObs
  tip_amount 63.245 31.61087 36  180 100      0     
  ```

4. コンピューティング コンテキストを取得して設定します。 コンピューティング コンテキストを設定すると、セッションの間は有効なままになります。 計算がローカルとリモートのどちらなのかわからない場合は、次のコマンドを実行して確認します。接続文字列が明示される結果は、リモートのコンピューティング コンテキストであることを示します。

  ```R
  # Return the current compute context.
  rxGetComputeContext()

  # Revert to a local compute context.
  rxSetComputeContext("local")
  rxGetComputeContext()

  # Switch back to remote.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  cc <-RxInSqlServer(connectionString=connStr)
  rxSetComputeContext(cc)
  rxGetComputeContext()
  ```  

5. 名前と型を含む、データ ソース内の変数に関する情報を返します。

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  結果には 23 個の変数が含まれます。


6. 散布図を生成して、2 つの変数の間に依存関係があるかどうかを調べます。 

  ```R
  # Set the connection string. Substitute a valid server name for the placeholder.
  connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

  # Specify a query on the nyctaxi_sample table.
  # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
  sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
  cc <-RxInSqlServer(connectionString=connStr)

  # Generate a scatter plot.
  rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
  ```

  次のスクリーンショットでは、入力と散布図の出力が示されています。

   ![RGUI の散布図](media/rclient-setup-scatterplot.png "NYC タクシーのデモ データでの散布図")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - R.exe にリンクするツール

継続的かつ本格的な開発プロジェクトの場合は、統合開発環境 (IDE) をインストールする必要があります。 SQL Server ツールと組み込みの R ツールは、大型の R 開発を行うための機能を備えていません。 動作するコードを作成したら、それを SQL Server で実行するためのストアド プロシージャとして配置できます。

IDE から ベース R、RevoScaleR などのローカル R ライブラリを参照します。 リモート SQL Server でのワークロードの実行は、スクリプトの実行中にスクリプトが SQL Server でリモートのコンピューティング コンテキストを呼び出し、そのサーバー上でデータと処理にアクセスするときに発生します。

### <a name="rstudio"></a>RStudio

[RStudio](https://www.rstudio.com/) を使用する場合は、リモート SQL Server 上の R ライブラリと実行可能ファイルに対応するそれらを使用するように、環境を構成できます。

1. SQL Server でインストールされている R パッケージのバージョンを確認します。 詳細については、「[R パッケージ情報の取得](../package-management/r-package-information.md)」を参照してください。

1. Microsoft R Client またはスタンドアロン サーバー オプションの 1 つをインストールして、RevoScaleR、および SQL Server インスタンスで使用されている R 基本ディストリビューションを含む、その他の R パッケージを追加します。 同じ、もしくはより低いバージョンを選択してください (パッケージは下位互換性があります)。それはサーバーと同じバージョンのパッケージを提供します。 バージョン情報については、次の記事のバージョン マップを参照してください。[R および Python コンポーネントのアップグレード](../install/upgrade-r-and-python.md)。

1. RStudio で [R パスを更新して](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)、RevoScaleR、Microsoft R Open、およびその他の Microsoft パッケージを提供する R 環境を参照するようにします。 

  + R Client のインストールの場合は、C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 を探します
  + スタンドアロン サーバーの場合は、C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library または C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library を探します

2. RStudio を閉じ、その後すぐに開きます。

RStudio を再度開くと、R クライアント (またはスタンドアロン サーバー) の R 実行可能ファイルが既定の R エンジンになります。


### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools for Visual Studio (RTVS)

希望する R 用の IDE がまだない場合は、**R Tools for Visual Studio** をお勧めします。

+ [R Tools for Visual Studio (RTVS) をダウンロードする](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [インストール手順](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) - RTVS は、いくつかのバージョンの Visual Studio で使用できます。
+ [R Tools for Visual Studio を使用して作業を開始する](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>RTVS から SQL Server への接続

この例では、データ サイエンス ワークロードがインストールされた Visual Studio 2017 Community Edition を使用します。

1. **[ファイル]** メニューの **[新規作成]** を選択し、 **[プロジェクト]** を選択します。

2. 左側のウィンドウには、プレインストールされたテンプレートの一覧が表示されます。 **[R]** をクリックし、 **[R プロジェクト]** を選択します。 **[名前]** ボックスに「`dbtest`」と入力し、 **[OK]** をクリックします。 

  Visual Studio によって、新しいプロジェクト フォルダーと既定のスクリプト ファイル `Script.R` が作成されます。 

3. スクリプト ファイルの最初の行に「`.libPaths()`」を入力し、CTRL + ENTER キーを押します。

  現在の R ライブラリのパスは、 **[R インタラクティブ]** ウィンドウに表示されます。 

4. **[R Tools]** メニューをクリックし、 **[ウィンドウ]** を選択して、ワークスペースに表示できる他の R 固有のウィンドウの一覧を表示します。
 
  + CTRL + 3 キーを押すと、現在のライブラリのパッケージに関するヘルプを表示します。
  + CTRL + 8 キーを押すと、**変数エクスプローラー**の R 変数を確認します。

## <a name="next-steps"></a>次の手順

2 つの異なるチュートリアルでは、コンピューティング コンテキストをローカルからリモート SQL Server インスタンスに切り替える練習を行うことができます。

+ [チュートリアル: SQL Server データでの RevoScaleR R 関数の使用](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [データ サイエンスのエンド ツー エンド チュートリアル](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)