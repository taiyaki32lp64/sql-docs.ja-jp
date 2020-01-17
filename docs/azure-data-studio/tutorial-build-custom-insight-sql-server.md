---
title: チュートリアル:カスタムの分析情報ウィジェットを構築する
titleSuffix: Azure Data Studio
description: このチュートリアルでは、カスタムの分析情報ウィジェットを構築し、Azure Data Studio のデータベースとサーバー ダッシュボードに追加する方法について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 34ee9c23569897247f05d6b9b5f9f2610f5d68fc
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959097"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>チュートリアル:カスタムの分析情報ウィジェットを構築する

このチュートリアルでは、独自の分析情報クエリを使用してカスタムの分析情報ウィジェットを構築する方法について説明します。

このチュートリアルでは、次の方法を学習します。
> [!div class="checklist"]
> * 独自のクエリを実行し、それをグラフで表示する
> * グラフからカスタムの分析情報ウィジェットを構築する
> * サーバーまたはデータベース ダッシュボードにグラフを追加する
> * カスタムの分析情報ウィジェットに詳細を追加する

## <a name="prerequisites"></a>Prerequisites

このチュートリアルには、SQL Server か Azure SQL Database *TutorialDB* が必要です。 *TutorialDB* データベースを作成するには、次のクイックスタートのいずれかを実行します。

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して SQL Server に接続し、クエリを実行する](quickstart-sql-server.md)
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して Azure SQL Database に接続し、クエリを実行する](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>独自のクエリを実行し、グラフ ビューに結果を表示する
この手順では、SQL スクリプトを実行し、現在アクティブになっているセッションにクエリを実行します。

1. 新しいエディターを開くには、**Ctrl + N** を押します。 

2. 接続コンテキストを **TutorialDB** に変更します。

3. 次のクエリをクエリ エディターに貼り付けます。

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. エディターのクエリを \*.sql ファイルに保存します。 このチュートリアルでは、スクリプトを *activeSession.sql* を保存します。

5. クエリを実行するには、**F5** を押します。

6. 結果が表示されたら、 **[View as Chart]\(グラフとして表示\)** をクリックし、 **[Chart Viewer]\(グラフ ビューアー\)** タブをクリックします。

7. **[グラフの種類]** を **[カウント]** に変更します。 以上の設定によりカウント グラフがレンダリングされます。

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>カスタムの分析情報をデータベース ダッシュボードに追加する

1. 分析情報ウィジェット構成を開き、 *[Chart Viewer]\(グラフ ビューアー\)* で **[Create Insight]\(分析情報の作成\)** をクリックします。

   ![構成](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 分析情報構成 (JSON データ) をコピーします。 

3. **Ctrl** を押しながらコンマ キーを押し、 *[ユーザー設定]* を開きます。

4. *[検索の設定]* に「*dashboard*」と入力します。

5. *dashboard.database.widgets* の **[編集]** をクリックします。

   ![ダッシュボード設定](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 分析情報構成 JSON を *dashboard.database.widgets* に貼り付けます。 データベース ダッシュボードの設定は次のようになります。

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. *[ユーザー設定]* ファイルを保存し、*TutorialDB* データベース ダッシュボードを開き、アクティブになっているセッション ウィジェットを表示します。

   ![activesession 分析情報](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>詳細をカスタムの分析情報に追加する

1. 新しいエディターを開くには、**Ctrl + N** を押します。

2. 接続コンテキストを **TutorialDB** に変更します。

3. 次のクエリをクエリ エディターに貼り付けます。

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. エディターのクエリを \*.sql ファイルに保存します。 このチュートリアルでは、スクリプトを *activeSessionDetail.sql* として保存します。

5. **Ctrl** を押しながらコンマ キーを押し、 *[ユーザー設定]* を開きます。

6. 設定ファイルの既存の *dashboard.database.widgets* ノードを編集します。

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. *[ユーザー設定]* ファイルを保存し、*TutorialDB* データベース ダッシュボードを開きます。 *[My-Widget]\(マイ ウィジェット\)* の隣にある省略記号 (...) をクリックすると、詳細が表示されます。

    ![activesession 分析情報](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>次の手順
このチュートリアルでは、次の方法を学習しました。
> [!div class="checklist"]
> * 独自のクエリを実行し、それをグラフで表示する
> * グラフからカスタムの分析情報ウィジェットを構築する
> * サーバーまたはデータベース ダッシュボードにグラフを追加する
> * カスタムの分析情報ウィジェットに詳細を追加する

データベースをバックアップし、復元する方法については、次のチュートリアルを完了してください。

> [!div class="nextstepaction"]
> [データベースのバックアップと復元](tutorial-backup-restore-sql-server.md)。
