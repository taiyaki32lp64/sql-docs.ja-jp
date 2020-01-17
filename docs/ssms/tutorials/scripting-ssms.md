---
title: チュートリアル:SQL Server Management Studio でオブジェクトのスクリプトを作成する
description: SSMS でのオブジェクトのスクリプトの作成に関するチュートリアル
keywords: SQL Server, SSMS, SQL Server Management Studio, スクリプト, スクリプト作成
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: 36d3b90a9ac1e49af564323c86421216216522a9
ms.sourcegitcommit: d65cef35cdf992297496095d3ad76e3c18c9794a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72988414"
---
# <a name="script-objects-in-sql-server-management-studio"></a>SQL Server Management Studio でオブジェクトのスクリプトを作成する

このチュートリアルでは、SQL Server Management Studio (SSMS) で見つかるさまざまなオブジェクトの Transact-SQL (T-SQL) スクリプトを生成する方法を説明します。 次のオブジェクトのスクリプトを作成する方法の例を示します。

> [!div class="checklist"]
> * クエリ、GUI 内でアクションを実行する場合
> * データベース、2 種類の方法 (スクリプト化とスクリプトの生成)
> * テーブル
> * ストアド プロシージャ
> * 拡張イベント

**オブジェクト エクスプローラー**内のオブジェクトをスクリプトするには、そのオブジェクトを右クリックし、 **[Script Object As]\(オブジェクトをスクリプト化\)** オプションを選択します。 このチュートリアルでは、そのプロセスについて説明します。

## <a name="prerequisites"></a>Prerequisites

このチュートリアルを実行するには、SQL Server Management Studio、SQL Server を実行しているサーバーへのアクセス、および AdventureWorks データベースが必要です。

* [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールする。
* [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。
* [AdventureWorks2016 サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases)をダウンロードする。

SSMS でデータベースを復元する手順については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)に関するページをご覧ください。 

## <a name="script-queries-from-the-gui"></a>GUI からクエリのスクリプトを作成する

SSMS の GUI を使用してタスクを完了するたびに、タスクに対して関連する T-SQL コードを生成することができます。 次の例では、データベースのバックアップを作成するときと、トランザクション ログを圧縮するときについて、その方法を示します。 GUI を使って行うすべてのアクションに、同じ手順を適用できます。

### <a name="script-t-sql-when-you-back-up-a-database"></a>データベースをバックアップするときの T-SQL をスクリプト化する

1. SQL Server を実行しているサーバーに接続します。

2. **[データベース]** ノードを展開します。

3. **Adventureworks2016** データベースを右クリックし、 >  **[タスク]**  >  **[バックアップ]** の順に選択します。

    ![データベースをバックアップする](media/scripting-ssms/backupdb.png)

4. 好みの方法でバックアップを構成します。 このチュートリアルでは、すべてを既定値のままにしています。 ただし、ウィンドウで行った変更もすべて、スクリプトに反映されます。 

5. **[スクリプト]**  >  **[スクリプト操作を新規クエリ ウィンドウに保存]** を選択します。

    ![スクリプト データベースのバックアップ--スクリプト アクション](media/scripting-ssms/scriptdbbackup.PNG)
6. クエリ ウィンドウに生成された T-SQL を確認します。

    ![スクリプト データベースのバックアップ--T-SQL の確認](media/scripting-ssms/dbbackupscript.PNG)
7. **[実行]** を選択して、T-SQL を使用してデータベースをバックアップするクエリを実行します。 

### <a name="script-t-sql-when-you-shrink-the-transaction-log"></a>トランザクション ログを圧縮するときの T-SQL をスクリプト化する

1. **AdventureWorks2016** データベースを右クリックし、 >  **[タスク]**  >  **[圧縮]**  >  **[ファイル]** の順に選択します。

     ![ファイルを圧縮する](media/scripting-ssms/shrinkfiles.png)

2. **[ファイルの種類]** ドロップダウン リスト ボックスから **[ログ]** を選択します。

    ![トランザクション ログを圧縮する](media/scripting-ssms/shrinktlog.png)

3. **[スクリプト]** 、 **[スクリプト操作をクリップボードに保存]** の順に選択します。

    ![[スクリプトをクリップボードに保存]](media/scripting-ssms/scriptactiontoclipboard.png)

4. **[新しいクエリ]** ウィンドウを開いて貼り付けます (ウィンドウで右クリックし、 **[貼り付け]** を選択します)。

    ![スクリプトを貼り付ける](media/scripting-ssms/paste.png)

5. **[実行]** を選択してクエリを実行し、トランザクション ログを圧縮します。

## <a name="script-databases"></a>データベースをスクリプト化する

次のセクションでは、 **[スクリプト化]** オプションと **[スクリプトの生成]** オプションを使って、データベースのスクリプトを作成する方法を説明します。 **[スクリプト化]** オプションを使うと、データベースとその構成オプションが再作成されます。 **[スクリプトの生成]** オプションを使用して、スキーマとデータの両方のスクリプトを作成することができます。 このセクションでは、新しいデータベースを作成します。 **[スクリプト化]** オプションを使用して *AdventureWorks2016a* を作成します。 **[スクリプトの生成]** オプションを使用して *AdventureWorks2016b* を作成します。

### <a name="script-a-database-by-using-the-script-option"></a>[スクリプト] オプションを使用してデータベースのスクリプトを作成する

1. SQL Server を実行しているサーバーに接続します。

2. **[データベース]** ノードを展開します。

3. **AdventureWorks2016** データベースを右クリックし、 >  **[Script Database As]\(データベースをスクリプト化\)**  >  **[新規作成]**  >  **[新しいクエリ エディター ウィンドウ]** の順に選択します。

    ![データベースのスクリプトを作成する](media/scripting-ssms/scriptdb.png)

4. ウィンドウでデータベース作成クエリを確認します。

    ![スクリプト化されたデータベース](media/scripting-ssms/scriptedoutdb.png) このオプションを選択すると、データベース構成オプションのみがスクリプト化されます。

5. キーボードで Ctrl キーを押しながら F キーを押して **[検索]** ダイアログ ボックスを開きます。 ↓キーを押して **[置換]** オプションを開きます。 上部の **[検索]** 行に「AdventureWorks2016」と入力し、下部の **[置換]** 行に「AdventureWorks2016a」と入力します。

6. *AdventureWorks2016* のインスタンスをすべて *AdventureWorks2016a* に置き換えるには、 **[すべて置換]** を選択します。 

    ![検索と置換](media/scripting-ssms/findandreplace.png)

7. **[実行]** を選択してクエリを実行し、AdventureWorks2016a データベースを新しく作成します。 

### <a name="script-a-database-by-using-the-generate-scripts-option"></a>[スクリプトの生成] オプションを使用してデータベースのスクリプトを作成する

1. SQL Server を実行しているサーバーに接続します。

2. **[データベース]** ノードを展開します。

3. **AdventureWorks2016** を右クリックし、 >  **[タスク]**  >  **[スクリプトの生成]** の順に選択します。

    ![データベースのスクリプトを生成する](media/scripting-ssms/generatescriptsfordb.png)

4. **[説明]** ページが開きます。 **[次へ]** を選択し、 **[オブジェクトの選択]** ページを開きます。 データベース全体、またはデータベース内の特定のオブジェクトを選択することができます。 **[データベース全体とすべてのデータベース オブジェクトのスクリプトを作成]** を選択します。

    ![オブジェクトのスクリプトを生成する](media/scripting-ssms/scriptobjects.png)

5. **[次へ]** を選択し、 **[スクリプト作成オプションの設定]** ページを開きます。 ここでは、スクリプトの保存場所とその他の詳細オプションを構成できます。 

    A. **[新しいクエリ ウィンドウに保存]** を選択します。

    B. **[詳細設定]** を選択し、次のオプションを設定します。

      * **[統計のスクリプトを作成]** を *[統計のスクリプトを作成]* に設定します。
      * **[スクリプトを作成するデータの種類]** を *[スキーマのみ]* に設定します。
      * **[インデックスのスクリプトを作成]** を *[True]* に設定します

   ![オブジェクトをスクリプト化する](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > **[スクリプトを作成するデータの種類]** オプションに *[スキーマとデータ]* を選択すると、データベースのデータをスクリプト化することができます。 ただし、この設定は大規模なデータベースには適していません。 SSMS で割り当て可能なメモリよりも多くのメモリが割り当てられる可能性があります。 小さなデータベースの場合、この制限は問題ありません。 大規模なデータベースのデータを移動する場合は、[インポートとエクスポート ウィザード](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)を使用します。

6. **[OK]** を選択し、 **[次へ]** を選択します。

7. **[概要]** ページで **[次へ]** を選択します。 もう一度 **[次へ]** を選択して、スクリプトを **[新しいクエリ]** ウィンドウに生成します。

8. キーボードで **[検索]** ダイアログ ボックスを開きます (Ctrl + F キー)。 ↓キーを押して **[置換]** オプションを開きます。 上の **[検索]** 行に「*AdventureWorks2016*」と入力します。 下の **[置換]** 行に「*AdventureWorks2016b*」と入力します。

9. *AdventureWorks2016* のインスタンスをすべて *AdventureWorks2016b* に置き換えるには、 **[すべて置換]** を選択します。

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)

10. **[実行]** を選択してクエリを実行し、AdventureWorks2016b データベースを新しく作成します。

## <a name="script-tables"></a>テーブルをスクリプト化する

このセクションでは、データベースからテーブルをスクリプト化する方法について説明します。 このオプションを使用すると、テーブルの作成またはテーブルの削除と作成ができます。 このオプションを使用して、テーブルの変更に関連する T-SQL をスクリプト化することもできます。 たとえば、テーブルへの挿入、テーブルの更新などの変更です。 このセクションでは、テーブルを削除して、再作成します。 

1. SQL Server を実行しているサーバーに接続します。

2. **[データベース]** ノードを展開します。

3. **AdventureWorks2016** データベースのノードを展開します。 

4. **[テーブル]** ノードを展開します。

5. **dbo.ErrorLog** を右クリックし、 >  **[テーブルをスクリプト化]**  >  **[削除および作成]**  >  **[新しいクエリ エディター ウィンドウ]** の順に選択します。

    ![テーブルのスクリプトを作成する](media/scripting-ssms/scripttable.png)

6. **[実行]** を選択してクエリを実行します。 この操作で *Errorlog* テーブルが削除され、再作成されます。 

    >[!NOTE]
    > AdventureWorks2016 データベースの *Errorlog* テーブルは、既定では空です。 そのため、テーブルを削除してもデータは失われません。 ただし、データが含まれるテーブルで次の手順を実行すると、データが失われます。

## <a name="script-stored-procedures"></a>ストアド プロシージャのスクリプトを作成する

このセクションでは、ストアド プロシージャを削除して作成する方法について説明します。  

1. SQL Server を実行しているサーバーに接続します。

2. **[データベース]** ノードを展開します。

3. **[プログラミング]** ノードを展開します。 

4. **[ストアド プロシージャ]** ノードを展開します。

5. ストアド プロシージャ **dbo.uspGetBillOfMaterials** を右クリックし、 >  **[ストアド プロシージャをスクリプト化]**  >  **[削除および作成]**  >  **[新しいクエリ エディター ウィンドウ]** の順に選択します。

    ![ストアド プロシージャのスクリプトを作成する](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>拡張イベントのスクリプトを作成する

このセクションでは、[拡張イベント](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)のスクリプトを作成する方法について説明します。

1. SQL Server を実行しているサーバーに接続します。

2. **[管理]** ノードを展開します。

3. **[拡張イベント]** ノードを展開します。

4. **[セッション]** ノードを展開します。

5. 対象の拡張セッションを右クリックして、 **[セッションをスクリプト化]**  >  **[新規作成]**  >  **[新しいクエリ エディター ウィンドウ]** を選択します。

    ![[新しいクエリ エディター ウィンドウ] セッションを展開します。](media/scripting-ssms/scriptxevents.png)

6. **[新しいクエリ エディター ウィンドウ]** でセッションの新しい名前を *system_health* から *system_health2* に変更します。 **[実行]** を選択してクエリを実行します。

7. **オブジェクト エクスプローラー**で **[セッション]** を右クリックします。 **[更新]** を選択すると、新しい拡張イベント セッションが表示されます。 セッションの横にある緑色のアイコンは、セッションが実行中であることを示します。 赤色のアイコンは、セッションが停止していることを示します。

    ![新しい拡張イベント セッション](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > セッションを右クリックして **[開始]** を選択すると、セッションを開始できます。 ただし、これは既に実行されている **system_health** セッションのコピーなので、この手順はスキップすることができます。 拡張したイベント セッションのコピーを削除するには、右クリックして **[削除]** を選択します。

## <a name="next-steps"></a>次の手順

SSMS に慣れ親しむには、実践的な経験を積むのが最も効果的です。 以下の "*チュートリアル*" と "*操作方法*" に関する記事は、SSMS 内で使用できるさまざまな機能を使用するのに役立ちます。 以下の記事では、SSMS のコンポーネントを管理する方法と、頻繁に使用する機能にアクセスする方法が説明されています。

* [インスタンスに接続してクエリを実行する](connect-query-sql-server.md)
* [SSMS でテンプレートを使用する](../template/templates-ssms.md)
* [SSMS を構成する](ssms-configuration.md)
* [SSMS を使用するための追加のヒントとテクニック](ssms-tricks.md)
