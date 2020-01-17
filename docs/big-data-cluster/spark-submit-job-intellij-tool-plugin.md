---
title: SQL Server ビッグ データ クラスター上の Azure Toolkit for IntelliJ で Spark ジョブを実行する
titleSuffix: SQL Server big data clusters
description: SQL Server ビッグ データ クラスター上の Azure Toolkit for IntelliJ で Spark ジョブを送信します。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 59946731dc1e76716b6202dd6f8aa93d777986b3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653716"
---
# <a name="submit-spark-jobs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-intellij"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上の IntelliJ で Spark ジョブを送信する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の主なシナリオの 1 つは、Spark ジョブを送信する機能です。 Spark ジョブの送信機能では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]への参照を含むローカル Jar ファイルまたは Py ファイルを送信できます。 また、HDFS ファイル システムに既に配置されている Jar ファイルまたは Py ファイルを実行することもできます。 

## <a name="prerequisites"></a>Prerequisites

- SQL Server ビッグ データ クラスター。
- Oracle Java Development Kit。 [Oracle Web サイト](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)からインストールできます。
- IntelliJ IDEA。 [JetBrains Web サイト](https://www.jetbrains.com/idea/download/)からインストールできます。
- Azure Toolkit for IntelliJ 拡張機能。 インストール手順については、「[Azure Toolkit for IntelliJ のインストール](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation)」を参照してください。

## <a name="link-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターのリンク
1. IntelliJ IDEA ツールを開きます。

2. 自己署名証明書を使用している場合は、 **[Tools]\(ツール\)** メニューの SSL 証明書の検証を無効にし、 **[Azure]** 、 **[Validate Spark Cluster SSL Certificate]\(Spark クラスター SSL 証明書の検証\)** 、 **[Disable]\(無効にする\)** の順に選択して SSL 証明書の検証を無効にします。

    ![SQL Server ビッグ データ クラスターのリンク - SSL を無効にする](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. **[View]\(表示\)** メニューから Azure エクスプローラーを開き、 **[Tool Windows]\(ツール ウィンドウ\)** 、 **[Azure Explorer]\(Azure エクスプローラー\)** の順に選択します。
4. **[SQL Server big data cluster]\(SQL Server ビッグ データ クラスター\)** を右クリックし、 **[Link SQL Server big data cluster]\(SQL Server ビッグ データ クラスターのリンク\)** を選択します。 **[Server]\(サーバー\)** 、 **[User Name]\(ユーザー名\)** 、および **[Password]\(パスワード\)** を入力し、 **[OK]** をクリックします。

    ![ビッグ データ クラスターのリンク - ダイアログ](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. 信頼されていないサーバーの証明書のダイアログが表示されたら、 **[Accept]\(同意する\)** をクリックします。 証明書は後で管理できます。「[Server Certificates (サーバー証明書)](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html)」を参照してください。

6. **[SQL Server big data cluster]\(SQL Server ビッグ データ クラスター\)** に、リンクされているクラスターの一覧が表示されます。 Spark ジョブを監視するには、Spark 履歴 UI と Yarn UI を開きます。また、クラスターを右クリックしてリンクを解除することもできます。

    ![ビッグ データ クラスターのリンク - コンテキスト メニュー](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-spark-template"></a>Spark テンプレートから Spark Scala アプリケーションを作成する

1. IntelliJ IDEA を開始し、プロジェクトを作成します。 **[New Project]\(新しいプロジェクト\)** ダイアログ ボックスで、次の手順を実行します。 

   A. **[Azure Spark/HDInsight]**  >  **[Project with Samples (Scala)]\(サンプル付きのプロジェクト (Scala)\)** を選択します。

   B. **[Build tool]\(ビルド ツール\)** 一覧で、必要に応じて次のいずれかを選択します。

      * **Maven** (Scala プロジェクト作成ウィザードのサポートの場合)
      * **SBT** (依存関係を管理し、Scala プロジェクトのために構築する場合)

    ![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. **[次へ]** を選択します。

3. Scala プロジェクト作成ウィザードによって、Scala プラグインがインストールされているかどうかが自動的に検出されます。 **[インストール]** を選択します。

   ![Scala プラグイン チェック](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Scala プラグインをダウンロードするには、 **[OK]** を選択します。 指示に従って IntelliJ を再起動します。 

   ![Scala プラグインのインストール ダイアログ ボックス](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. **[New Project]\(新しいプロジェクト\)** ウィンドウで、次の手順を実行します。  

    ![Spark SDK の選択](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   A. プロジェクトの名前と場所を入力します。

   B. **[Project SDK]\(プロジェクト SDK\)** ドロップダウン リストで、Spark 2.x クラスターの場合は **[Java 1.8]** を選択し、Spark 1.x クラスターの場合は **[Java 1.7]** を選択します。

   c. **[Spark version]\(Spark のバージョン\)** ドロップダウン リストで、Scala プロジェクトの作成ウィザードで、Spark SDK と Scala SDK の適切なバージョンが統合されます。 Spark クラスターのバージョンが 2.0 より前の場合は、 **[Spark 1.x]** を選択します。 それ以外の場合は、 **[Spark2.x]** を選択します。 この例では、 **[Spark 2.0.2 (Scala 2.11.8)]** を使用します。

6. **[完了]** を選択します。

7. Spark プロジェクトによって自動的に成果物が作成されます。 成果物を表示するには、次の手順を実行します。

   A. **[File]\(ファイル\)** メニューの **[Project Structure]\(プロジェクト構造\)** をクリックします。

   B. **[Project Structure]\(プロジェクト構造\)** ダイアログ ボックスで、 **[Artifacts]\(成果物\)** を選択して、作成された既定の成果物を表示します。 プラス記号 ( **+** ) を選択して、独自の成果物を作成することもできます。

      ![ダイアログ ボックスの成果物情報](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターにアプリケーションを送信する
SQL Server ビッグ データ クラスターをリンクした後は、それにアプリケーションを送信できます。

1. **[Run/Debug Configurations]\(実行/デバッグの構成\)** ウィンドウで構成を設定し、 **[Apache Spark on SQL Server]** をクリックし、 **[Remotely Run in Cluster]\(クラスターでリモート実行する\)** タブを選択し、次のようにパラメーターを設定してから、[OK] をクリックします。

    ![対話型コンソールの構成エントリの追加](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![ビッグ データ クラスターのリンク - 構成](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * **Spark クラスター (Linux のみ)** の場合は、アプリケーションを実行するクラスターを選択します。

    * IntelliJ プロジェクトから成果物を選択するか、ハード ドライブから成果物を 1 つ選択します。

    * **[Main class name]\(メイン クラス名\)** フィールド:既定値は、選択したファイルのメイン クラスです。 クラスを変更するには、省略記号 ( **...** ) をクリックし、別のクラスを選択します。   

    * **[Job Configurations]\(ジョブの構成\)** フィールド:既定値は、上の図のように設定されます。 ジョブの送信には、値を変更するか、新しいキー/値を追加します。 詳細:[Apache Livy REST API](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![[Spark Submission]\(Spark の送信\) ダイアログ ボックスのジョブ構成の意味](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **[Command line arguments]\(コマンド ライン引数\)** フィールド:必要に応じて、メイン クラスの空間で分割した引数値を入力できます。

    * **[Referenced Jars]\(参照されている Jar\)** フィールドと **[Referenced Files]\(参照されているファイル\)** フィールド:参照されている Jar およびファイルのパスを入力できます (存在する場合)。 詳細:[Apache Spark の構成](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![Spark の [Submission]\(送信\) ダイアログ ボックスの Jar ファイルの意味](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > 参照されている JAR と参照されているファイルをアップロードするには、以下を参照してください。[リソースをクラスターにアップロードする方法](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **アップロード パス**:Jar または Scala プロジェクトのリソース送信の保存場所を指定できます。 サポートされているストレージの種類はいくつかあります。 **[Use Spark interactive session to upload]\(Spark 対話型セッションを使用してアップロードする\)** と **[Use WebHDFS to upload]\(WebHDFS を使用してアップロードする\)** です。
    
2. **[SparkJobRun]** をクリックし、選択したクラスターにプロジェクトを送信します。 **[Remote Spark Job in Cluster]\(クラスターのリモート Spark ジョブ\)** タブの下部には、ジョブの実行の進行状況が表示されます。 赤いボタンをクリックすると、アプリケーションを停止できます。  

    ![ビッグ データ クラスターのリンク - 実行](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Spark コンソール
Spark Local Console(Scala) を実行するか、Spark Livy Interactive Session Console(Scala) を実行することができます。

### <a name="spark-local-consolescala"></a>Spark Local Console(Scala)
WINUTILS.EXE の前提条件を満たしていることを確認します。

1. メニュー バーから、 **[Run]\(実行\)**  >  **[Edit Configurations]\(構成の編集\)** に移動します。

2. **[Run/Debug Configurations]\(実行/デバッグの構成\)** ウィンドウの左側のウィンドウで、 **[Apache Spark on SQL Server big data cluster]\(SQL Server ビッグ データ クラスター上の Apache Spark\)**  >  **[[Spark on SQL] myApp]** に移動します。

3. メイン ウィンドウで、 **[Locally Run]\(ローカル実行\)** タブを選択します。

4. 次の値を指定し、 **[OK]** を選択します。

    |プロパティ |[値] |
    |----|----|
    |ジョブのメイン クラス|既定値は、選択したファイルのメイン クラスです。 クラスを変更するには、省略記号 ( **...** ) をクリックし、別のクラスを選択します。|
    |環境変数|HADOOP_HOME の値が正しいことを確認します。|
    |WINUTILS.exe の場所|パスが正しいことを確認します。|

    ![Local Console の構成の設定](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. [Project]\(プロジェクト\) から **myApp** > **src** > **main** > **scala** > **myApp** に移動します。  

6. メニュー バーから、 **[Tools]\(ツール\)**  >  **[Spark Console]\(Spark コンソール\)**  >  **[Run Spark Local Console(Scala)]\(Spark Local Console(Scala) の実行\)** に移動します。

7. 次に、依存関係を自動修正するかどうかを確認する 2 つのダイアログ ボックスが表示されます。 そうする場合は、 **[Auto Fix]\(自動修正\)** を選択します。

    ![Spark Auto Fix1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Spark Auto Fix2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. コンソールは次の図のようになります。 コンソール ウィンドウに「`sc.appName`」と入力し、Ctrl + Enter キーを押します。  結果が表示されます。 赤いボタンをクリックすると、ローカル コンソールを終了できます。

    ![Local Console の結果](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Spark Livy Interactive Session Console(Scala)
Spark Livy Interactive Session Console(Scala) は、IntelliJ 2018.2 および 2018.3 でのみサポートされています。

1. メニュー バーから、 **[Run]\(実行\)**  >  **[Edit Configurations]\(構成の編集\)** に移動します。

2. **[Run/Debug Configurations]\(実行/デバッグの構成\)** ウィンドウの左側のウィンドウで、 **[Apache Spark on SQL Server big data cluster]\(SQL Server ビッグ データ クラスター上の Apache Spark\)**  >  **[[Spark on SQL] myApp]** に移動します。

3. メイン ウィンドウから **[Remotely Run in Cluster]\(クラスターでリモート実行\)** タブを選択します。

4. 次の値を指定し、 **[OK]** を選択します。

    |プロパティ |[値] |
    |----|----|
    |Spark クラスター (Linux のみ)|アプリケーションを実行する SQL Server ビッグ データ クラスターを選択します。|
    |メイン クラス名|既定値は、選択したファイルのメイン クラスです。 クラスを変更するには、省略記号 ( **...** ) をクリックし、別のクラスを選択します。|

    ![対話型コンソールセットの構成](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. [Project]\(プロジェクト\) から **myApp** > **src** > **main** > **scala** > **myApp** に移動します。  

6. メニュー バーで、 **[Tools]\(ツール\)**  >  **[Spark Console]\(Spark コンソール\)**  >  **[Run Spark Livy Interactive Session Console(Scala)]\(Spark Livy Interactive Session Console(Scala) の実行\)** に移動します。

7. コンソールは次の図のようになります。 コンソール ウィンドウに「`sc.appName`」と入力し、Ctrl + Enter キーを押します。  結果が表示されます。 赤いボタンをクリックすると、ローカル コンソールを終了できます。

    ![Interactive Console の結果](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>選択内容を Spark コンソールに送信する

Local Console または Livy Interactive Session Console(Scala) に何らかのコードを送信すると、スクリプトの結果を確認できるので便利です。 Scala ファイル内の一部のコードを強調表示し、 **[Send Selection To Spark Console]\(選択内容を Spark コンソールに送信\)** を右クリックします。 選択したコードがコンソールに送信され、実行されます。 結果は、コンソールのコードの後に表示されます。 コンソールでは、エラーが存在するかどうかがチェックされます。  

   ![選択内容を Spark コンソールに送信する](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>次の手順
SQL Server ビッグ データ クラスターと関連するシナリオの詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の概要](big-data-cluster-overview.md)に関するページを参照してください。
