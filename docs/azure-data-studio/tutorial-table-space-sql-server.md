---
title: テーブル領域使用のサンプル分析情報ウィジェットを有効にする
titleSuffix: Azure Data Studio
description: このチュートリアルでは、Azure Data Studio データベース ダッシュボードでテーブル領域使用のサンプル分析情報ウィジェットを有効にする方法について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/10/2019
ms.openlocfilehash: f22aba3fd2f2d006355fdd30aef6f196f2795f6c
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957016"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>チュートリアル:[!INCLUDE[name-sos](../includes/name-sos-short.md)] を利用し、テーブル領域使用のサンプル分析情報ウィジェットを有効にする

このチュートリアルでは、データベース ダッシュボードで分析情報ウィジェットを有効にする方法について説明します。データベース内のすべてのテーブルを対象に領域の使用状況がひとめでわかります。 このチュートリアルでは、次の方法を学習します。

> [!div class="checklist"]
> * 組み込みの分析情報ウィジェット サンプルを利用し、分析情報ウィジェットを簡単にオンにする
> * テーブル領域の使用状況の詳細を表示する
> * 分析情報グラフでデータにフィルターを適用し、ラベル詳細を表示する

## <a name="prerequisites"></a>前提条件

このチュートリアルには、SQL Server か Azure SQL Database *TutorialDB* が必要です。 *TutorialDB* データベースを作成するには、次のクイックスタートのいずれかを実行します。

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して SQL Server に接続し、クエリを実行する](quickstart-sql-server.md)
* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して Azure SQL Database に接続し、クエリを実行する](quickstart-sql-database.md)

## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] のデータベース ダッシュボードで管理分析情報をオンにする

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、データベース内のテーブルによって使用される領域を監視するためのサンプル ウィジェットが組み込まれています。

1. **Ctrl + Shift + P** を押して *[ユーザー設定]* を開き、 *[コマンド パレット]* を開きます。

2. 検索ボックスに「*settings*」と入力し、 **[ユーザー設定:ユーザー設定を開く]** を選択します。

3. [設定の検索] 入力ボックスに「*dashboard*」と入力し、**dashboard.database.widgets** を見つけます。

4. **dashboard.database.widgets** 設定をカスタマイズするには、 **[ユーザー設定]** セクションの **dashboard.database.widgets** を編集する必要があります。

   ![検索設定](media/tutorial-table-space-sql-server/search-settings.png)

   **[ユーザー設定]** セクションに **dashboard.database.widgets** がない場合、[デフォルト設定] 列の **dashboard.database.widgets** テキストにカーソルを合わせ、テキストの左に表示された "*歯車*" アイコンをクリックして、 **[Copy as Setting JSON]\(設定 JSON としてコピー\)** をクリックします。 ポップアップに **[設定を置換]** と表示された場合、それをクリックしないでください。 右にある **[ユーザー設定]** 列に移動し、**dashboard.database.widgets** セクションを見つけ、次の手順に進みます。

5. **dashboard.database.widgets** セクションに次の行を追加します。

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```

   **dashboard.database.widgets** セクションは、次の画像のようになります。

    ![検索設定](./media/tutorial-table-space-sql-server/insight-table-space.png)

6. **Ctrl + S** を押して設定を保存します。

7. **[TutorialDB]** を右クリックしてデータベース ダッシュボードを開き、 **[管理]** をクリックします。

8. 次の画像のように、*テーブル領域*という分析情報ウィジェットを表示します。

   ![ウィジェット](./media/tutorial-table-space-sql-server/insight-table-space-result.png)

## <a name="working-with-the-insight-chart"></a>分析情報ウィジェットを使用する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] の分析情報グラフでは、フィルターを適用したり、マウス カーソルを合わせることで詳細を表示したりできます。 次の手順でお試しいただけます。

1. グラフの *row_count* 凡例をクリックし、切り替えます。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] では、凡例のオン/オフを切り替えると、データ系列の表示/非表示が切り替わります。

2. グラフの上にマウス ポインターを置きます。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] には、次のスクリーンショットのように、データ系列ラベルとその値に関する詳細が表示されます。

   ![グラフの切り替えと凡例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> * 組み込みの分析情報ウィジェット サンプルを利用し、分析情報ウィジェットを簡単にオンにする
> * テーブル領域の使用状況の詳細を表示する
> * 分析情報グラフでデータにフィルターを適用し、ラベル詳細を表示する

カスタムの分析情報ウィジェットを構築する方法については、次のチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [カスタム分析情報ウィジェットのビルド](tutorial-build-custom-insight-sql-server.md)
