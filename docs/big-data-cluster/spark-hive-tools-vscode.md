---
title: SQL Server ビッグ データ クラスター上で Spark & Hive Tools for VS Code を使用して Spark ジョブを実行する
titleSuffix: SQL Server big data clusters
description: SQL Server ビッグ データ クラスター上で Spark & Hive Tools for Visual Studio Code を使用して Spark ジョブを送信します。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b09a5febe9bc67f04d70c4d5b7850ef26ebac750
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653730"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>SQL Server ビッグ データ クラスター上の Visual Studio Code で Spark ジョブを送信する

Spark & Hive Tools for Visual Studio Code を使用して Apache Spark 用の PySpark スクリプトを作成して送信する方法について説明します。まず、Spark & Hive Tools を Visual Studio Code にインストールする方法について説明し、次に Spark にジョブを送信する方法について説明します。  

Spark & Hive Tools は、Windows、Linux、macOS など、Visual Studio Code でサポートされているプラットフォームにインストールできます。 以下では、さまざまなプラットフォームの前提条件について説明します。


## <a name="prerequisites"></a>Prerequisites

この記事の手順を完了するには、次の項目が必要です。

- SQL Server ビッグ データ クラスター。 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)に関するページを参照してください。
- [Visual Studio Code](https://code.visualstudio.com/)。
- [Mono](https://www.mono-project.com/docs/getting-started/install/)。 Mono は、Linux と macOS の場合にのみ必要です。
- [Visual Studio Code 用に PySpark の対話型の環境を設定します](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment)。
- **SQLBDCexample** という名前のローカル ディレクトリ。  この記事では、**C:\SQLBDC\SQLBDCexample** を使用しています。

## <a name="install-spark--hive-tools"></a>Spark & Hive Tools をインストールする

前提条件を満たしたら、Spark & Hive Tools for Visual Studio Code をインストールできます。  Spark & Hive Tools をインストールするには、次の手順を実行します。

1. Visual Studio Code を開きます。

2. メニュー バーから **[View]\(表示\)**  >  **[Extensions]\(拡張機能\)** に移動します。

3. 検索ボックスに、「**Spark & Hive**」と入力します。

4. 検索結果から **[Spark & Hive Tools]** を選択し、 **[Install]\(インストール\)** を選択します。  

   ![拡張機能のインストール](./media/spark-hive-tools-vscode/extension.png)

5. 必要に応じてリロードします。

## <a name="open-work-folder"></a>作業フォルダーを開く

次の手順を実行して作業フォルダーを開き、Visual Studio Code でファイルを作成します。

1. メニュー バーから **[ファイル]**  >  **[フォルダーを開く]**  > **C:\SQLBDC\SQLBDCexample** に移動し、 **[フォルダーの選択]** ボタンを選択します。 左側の **[Explorer]\(エクスプローラー\)** ビューにフォルダーが表示されます。

2. **[エクスプローラー]** ビューで、**SQLBDCexample** というフォルダーを選択し、作業フォルダーの横にある **[新しいファイル]** アイコンを選択します。

   ![新しいファイル](./media/spark-hive-tools-vscode/new-file.png)

3. 新しいファイルに `.py` (Spark スクリプト) ファイル拡張子を付けます。  この例では、**HelloWorld.py** を使用します。
4. 次のコードをコピーしてスクリプト ファイルに貼り付けます。
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターをリンクする

Visual Studio Code からクラスターにスクリプトを送信するには、SQL Server ビッグ データ クラスターをリンクする必要があります。

1. メニュー バーから **[表示]\(表示\)**  >  **[Command Palette]\(コマンド パレット\)** に移動し、「**Spark / Hive:Link a Cluster**」と入力します。

   ![クラスターのリンク コマンド](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. リンクされるクラスターの種類として **[SQL Server Big Data]\(SQL Server ビッグ データ\)** を選択します。

3. SQL Server ビッグ データ エンドポイントを入力します。

4. SQL Server ビッグ データ クラスターのユーザー名を入力します。

5. ユーザー管理者のパスワードを入力します。

6. クラスターの表示名を設定します (省略可能)。

7. クラスターを一覧表示し、 **[OUTPUT]\(出力\)** ビューを確認します。

## <a name="list-clusters"></a>クラスターを一覧表示する

1. メニュー バーから **[表示]\(表示\)**  >  **[Command Palette]\(コマンド パレット\)** に移動し、「**Spark / Hive:List Cluster**」と入力します。

2. **[OUTPUT]\(出力\)** ビューを確認します。  このビューには、リンクされたクラスターが表示されます。

    ![既定のクラスター構成を設定する](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>既定のクラスターを設定する

1. [前の手順](#open-work-folder)で作成したフォルダー **SQLBDCexample** を閉じている場合は再び開きます。  

2. [以前の手順](#open-work-folder)で作成した **HelloWorld.py** ファイルを選択し、スクリプト エディターで開きます。

3. クラスターをまだリンクしていない場合は、リンクします。

4. スクリプト エディターを右クリックし、 **[Spark / Hive:Set Default Cluster]\(Spark / Hive: 既定のクラスターの設定\)** を選択します。   

5. 現在のスクリプト ファイルの既定のクラスターとしてクラスターを選択します。 ツールによって構成ファイル **.VSCode\settings.json** が自動的に更新されます。 

   ![既定のクラスター構成を設定する](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>対話型の PySpark クエリを送信する

次の手順に従って、対話型の PySpark クエリを送信できます。

1. [前の手順](#open-work-folder)で作成したフォルダー **SQLBDCexample** を閉じている場合は再び開きます。  

2. [以前の手順](#open-work-folder)で作成した **HelloWorld.py** ファイルを選択し、スクリプト エディターで開きます。

3. クラスターをまだリンクしていない場合は、リンクします。

4. すべてのコードを選択し、スクリプト エディターを右クリックして、 **[Spark:PySpark Interactive]** を選択するか、ショートカット キーの **Ctrl + Alt + I** を使用します。

   ![PySpark Interactive のコンテキスト メニュー](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. 既定のクラスターを指定していない場合は、クラスターを選択します。 しばらくすると、**Python Interactive** の結果が新しいタブに表示されます。また、このツールでは、コンテキスト メニューを使用して、スクリプト ファイル全体ではなくコード ブロックを送信することもできます。 

   ![PySpark Interactive の Python Interactive ウィンドウ](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. 「 **%%Info**」と入力し、**Shift + Enter** キーを押してジョブ情報を表示します。 (オプション)

   ![ジョブ情報の表示](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > 設定で **[Python Extension Enabled]\(Python 拡張機能が有効\)** がオフの場合 (既定の設定はオン)、送信される PySpark の対話結果には古いウィンドウが使用されます。
   >
   > ![Python Interactive の Python 拡張機能の無効](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>PySpark バッチ ジョブを送信する

1. [前の手順](#open-work-folder)で作成したフォルダー **SQLBDCexample** を閉じている場合は再び開きます。  

2. [以前の手順](#open-work-folder)で作成した **HelloWorld.py** ファイルを選択し、スクリプト エディターで開きます。

3. クラスターをまだリンクしていない場合は、リンクします。

4. スクリプト エディターを右クリックし、 **[Spark:PySpark Batch]** を選択するか、ショートカット キー **Ctrl + Alt + H** を使用します。 

5. 既定のクラスターを指定していない場合は、クラスターを選択します。 Python ジョブを送信すると、Visual Studio Code の **[OUTPUT]\(出力\)** ウィンドウに送信ログが表示されます。 **Spark UI URL** と **Yarn UI URL** も表示されます。 Web ブラウザーで URL を開いて、ジョブの状態を追跡することができます。

   ![Python ジョブ結果を送信する](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Apache Livy の構成

[Apache Livy](https://livy.incubator.apache.org/) の構成はサポートされており、ワーク スペース フォルダーの **.VSCode\settings.json** で設定できます。 現時点では、Livy の構成では Python スクリプトのみがサポートされています。 詳細については、[Livy の README](https://github.com/cloudera/livy/blob/master/README.rst ) を参照してください。

### <a id="triggerlivyconf"></a>**Livy の構成をトリガーする方法**

#### <a name="method-1"></a>方法 1

1. メニュー バーから **[File]\(ファイル\)**  >  **[Preferences]\(基本設定\)**  >  **[Settings]\(設定\)** に移動します。  
2. **[Search settings]\(検索設定\)** テキスト ボックスに「**HDInsight Job Sumission:Livy Conf**」と入力します。  
3. 関連する検索結果に対して **[Edit in settings.json]\(settings.json で編集\)** を選択します。

#### <a name="method-2"></a>方法 2

ファイルを送信すると、`.vscode` フォルダーが自動的に作業フォルダーに追加されることがわかります。 Livy の構成を確認するには、`.vscode\settings.json` をクリックします。

+ プロジェクトの設定:

    ![Livy の構成](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>設定の **driverMomory** と **executorMomry** について、値を単位付きで設定します (たとえば、1g、1024m など)。 

### <a name="supported-livy-configurations"></a>サポートされている Livy の構成

#### <a name="post-batches"></a>POST /batches

**要求本文**

| NAME | description | 型 |
| :- | :- | :- |
| file | 実行するアプリケーションを含むファイル | パス (必須) |
| proxyUser | ジョブの実行時に権限を借用するユーザー | string |
| className | アプリケーション Java/Spark のメイン クラス | string |
| args | アプリケーションのコマンド ライン引数 | 文字列の一覧 |
| jars | このセッションで使用される Jar | 文字列の一覧 |
| pyFiles | このセッションで使用される Python ファイル | 文字列の一覧 |
| files | このセッションで使用されるファイル | 文字列の一覧 |
| driverMemory | ドライバー プロセスに使用するメモリの量 | string |
| driverCores | ドライバー プロセスに使用するコアの数 | INT |
| executorMemory | 実行プログラム プロセスごとに使用するメモリの量 | string |
| executorCores | 実行プログラムごとに使用するコアの数 | INT |
| numExecutors | このセッションで起動する実行プログラムの数 | INT |
| archives | このセッションで使用するアーカイブ | 文字列の一覧 |
| queue | 送信先の YARN キューの名前 | string |
| NAME | このセッションの名前 | string |
| conf | Spark の構成プロパティ | キーのマップ = val |

#### <a name="response-body"></a>応答本文

作成されるバッチ オブジェクト。

| NAME | description | 型 |
| :- | :- | :- |
| id | セッション ID | INT |
| appId | このセッションのアプリケーション ID | String |
| appInfo | アプリケーションの詳細情報 | キーのマップ = val |
| log | ログの行 | 文字列の一覧 |
| state | バッチの状態 | string |

>[!NOTE]
>割り当てられた Livy の構成は、スクリプトの送信時に出力ウィンドウに表示されます。

## <a name="additional-features"></a>その他の機能

Spark & Hive for Visual Studio Code は次の機能をサポートしています。

- **IntelliSense のオートコンプリート**。 キーワード、メソッド、変数などの候補がポップアップ表示されます。 さまざまな種類のオブジェクトを表すさまざまなアイコン。

    ![Spark & Hive Tools for Visual Studio Code の IntelliSense オブジェクトの種類](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **IntelliSense エラー マーカー**。 言語サービスによって、Hive スクリプトの編集エラーに下線が引かれます。     
- **構文の強調表示**。 言語サービスでは、変数、キーワード、データ型、関数などを区別するためにさまざまな色が使用されます。 

    ![Spark & Hive Tools for Visual Studio Code の構文の強調表示](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>クラスターのリンク解除

1. メニュー バーから **[表示]\(表示\)**  >  **[Command Palette]\(コマンド パレット\)** に移動し、「**Spark / Hive:Unlink a Cluster**」と入力します。  

2. リンクを解除するクラスターを選択します。  

3. **[OUTPUT]\(出力\)** ビューを確認します。  

## <a name="next-steps"></a>次の手順
SQL Server ビッグ データ クラスターと関連するシナリオの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)」を参照してください。
