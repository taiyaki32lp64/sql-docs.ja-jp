---
title: 5 つの最低速クエリのサンプル ウィジェットを有効にする
titleSuffix: Azure Data Studio
description: このチュートリアルでは、データベース ダッシュボードで 5 つの最低速クエリ サンプル ウィジェットを有効にする方法について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 08/02/2019
ms.openlocfilehash: 3f940f0f18df676eae2ca101a2eccaa2be7169e2
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957046"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>チュートリアル:データベース ダッシュボードに *5 つの最低速クエリ* サンプル ウィジェットを追加する

このチュートリアルでは、[!INCLUDE[name-sos](../includes/name-sos-short.md)] に組み込まれているサンプル ウィジェットの 1 つを*データベース ダッシュボード*に追加することでデータベースの 5 つの最低速クエリを表示するプロセスについて説明します。 低速クエリの詳細を表示する方法と [!INCLUDE[name-sos](../includes/name-sos-short.md)] の機能を利用してプランにクエリを実行する方法についても説明します。 このチュートリアルでは、次の方法を学習します。

> [!div class="checklist"]
> * データベースでクエリ ストアを有効にする
> * 事前に構築された分析情報ウィジェットをデータベース ダッシュボードに追加する
> * データベースの最低速クエリに関する詳細を表示する
> * 低速クエリのクエリ実行プランを表示する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、面倒な設定なしですぐに使える分析情報ウィジェットがいくつか含まれています。 このチュートリアルでは、*query-data-store-db-insight* ウィジェットを追加する方法を紹介しますが、手順は基本的にどのウィジェットを追加する場合でも同じです。

## <a name="prerequisites"></a>前提条件

このチュートリアルには、SQL Server か Azure SQL Database *TutorialDB* が必要です。 *TutorialDB* データベースを作成するには、次のクイックスタートのいずれかを実行します。

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して SQL Server に接続し、クエリを実行する](quickstart-sql-server.md)

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して Azure SQL Database に接続し、クエリを実行する](quickstart-sql-database.md)

## <a name="turn-on-query-store-for-your-database"></a>データベースのクエリ ストアをオンにする

この例のウィジェットでは、*クエリ ストア*を有効にする必要があります。

1. ( **[サーバー]** サイドバーで) **TutorialDB** データベースを右クリックし、 **[新しいクエリ]** を選択します。

2. クエリ エディターに次の Transact-SQL (T-SQL) ステートメントを貼り付けて、 **[実行]** をクリックします。

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>低速クエリ ウィジェットをデータベース ダッシュボードに追加する

*低速クエリ ウィジェット*をダッシュボードに追加するには、 *[ユーザー設定]* ファイルの *dashboard.database.widgets* 設定を編集します。

1. **Ctrl + Shift + P** を押して *[ユーザー設定]* を開き、 *[コマンド パレット]* を開きます。

2. 検索ボックスに「*settings*」と入力し、 **[ユーザー設定:ユーザー設定を開く]** を選択します。

   ![[ユーザー設定を開く] コマンド](./media/tutorial-qds-sql-server/open-user-settings.png)

3. [設定の検索] ボックスに「*dashboard*」と入力し、**dashboard.database.widgets** を見つけ、 *[edit in settings.json]\(settings.json で編集\)* をクリックします。

   ![検索設定](./media/tutorial-qds-sql-server/search-settings.png)

4. settings.json に、次のコードを追加します。

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

5. **Ctrl + S** を押し、変更後の **[ユーザー設定]** を保存します。

6. **[サーバー]** サイドバーの **[TutorialDB]** に移動して *[データベース ダッシュボード]* を開き、右クリックして **[管理]** を選択します。

   ![ダッシュボードを開く](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 分析情報ウィジェットがダッシュボードに表示されます。

   ![QDS ウィジェット](./media/tutorial-qds-sql-server/insight-qds-result.png)

## <a name="view-insight-details-for-more-information"></a>詳細は、分析情報詳細を参照してください。

1. 分析情報ウィジェットの追加情報を表示するには、右上にある省略記号 ( **...** ) をクリックし、 **[詳細の表示]** を選択します。

2. 項目の詳細を表示するには、 **[グラフ データ]** 一覧で任意の項目を選択します。

   ![分析情報詳細ダイアログ](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. **[項目の詳細]** で **query_sql_txt** の右にあるセルを右クリックし、 **[セルのコピー]** をクリックします。

4. **[分析情報]** ウィンドウを閉じます。

## <a name="view-the-query-plan"></a>クエリ プランを表示する

1. **TutorialDB**データベースを右クリックし、 *[管理]* を選択します

2. *[slow query widget]\(低速クエリ ウィジェット\)* で分析情報ウィジェットの追加情報を表示するには、右上にある省略記号 ( **...** ) をクリックし、 **[クエリの実行]** を選択します。

    ![クエリを実行する](media/tutorial-qds-sql-server/run-query.png)

3. これで、新しいクエリ ウィンドウに結果が表示されるはずです。

    ![クエリの実行結果](media/tutorial-qds-sql-server/run-query-results.png)

4. **[説明]** をクリックします。

   ![分析情報 QDS 説明](./media/tutorial-qds-sql-server/insight-qds-explain.png)

5. クエリの実行プランを表示します。

   ![プラン表示 (showplan)](./media/tutorial-qds-sql-server/showplan.png)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> * データベースでクエリ ストアを有効にする
> * 分析情報ウィジェットをデータベース ダッシュボードに追加する
> * データベースの最低速クエリに関する詳細を表示する
> * 低速クエリのクエリ実行プランを表示する

**テーブル領域使用**のサンプル分析情報を有効にする方法については、次のチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [テーブル領域のサンプル分析情報ウィジェットを有効にする](tutorial-table-space-sql-server.md)