---
title: 拡張性によるさらなる機能の追加
titleSuffix: Azure Data Studio
description: Azure Data Studio の機能を拡張するための拡張性モデルと主要な拡張性の領域について説明します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 20158894567c1452a8d605f5cec84354654c5e96
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959596"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] の拡張性の概要

[!INCLUDE[name-sos](../includes/name-sos.md)] には、ユーザー エクスペリエンスをカスタマイズし、それらのカスタマイズ結果をユーザー コミュニティ全体で利用できるようにするいくつかの拡張性メカニズムがあります。 [!INCLUDE[name-sos](../includes/name-sos.md)] のコア プラットフォームは Visual Studio Code 上に構築されているため、Visual Studio Code の拡張 API のほとんどが利用できます。 さらに、データ管理に固有のアクティビティに対して追加の拡張性ポイントを提供しました。

主要な拡張性のポイントを次に示します。

- Visual Studio Code の拡張 API
- Azure Data Studio 拡張機能作成ツール
- [ダッシュボード] タブ パネルのコントリビューションを管理する
- アクション エクスペリエンスでの分析情報
- Azure Data Studio 拡張 API
- カスタム データ プロバイダー API

## <a name="visual-studio-code-extensibility-apis"></a>Visual Studio Code の拡張 API

[!INCLUDE[name-sos](../includes/name-sos.md)] のコア プラットフォームは Visual Studio Code に基づいて構築されているため、Visual Studio Code 拡張 API の詳細については、Visual Studio Code の Web サイトにある[拡張機能の作成](https://code.visualstudio.com/docs/extensions/overview)と[拡張 API](https://code.visualstudio.com/docs/extensionAPI/overview) に関するドキュメントを参照してください。

## <a name="manage-dashboard-tab-panel-contributions"></a>[ダッシュボード] タブ パネルのコントリビューションを管理する

詳細については、「[貢献ポイント](#contribution-points)」と「[コンテキスト変数](#context-variables)」を参照してください。

## <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 拡張 API

詳細については、[拡張 API](extensibility-apis.md) に関するページを参照してください。


## <a name="contribution-points"></a>コントリビューション ポイント

このセクションでは、package.json 拡張機能マニフェストで定義されているさまざまなコントリビューション ポイントについて説明します。

IntelliSense は、azuredatastudio 内でサポートされています。

## <a name="contributes-dashboard"></a>ダッシュボードへの提供

タブ、コンテナー、分析情報ウィジェットをダッシュボードに提供します。

![ダッシュボード](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs では、ダッシュボード ページ内にタブ セクションが作成されます。 これには、オブジェクトまたはオブジェクトの配列が必要です。  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

ダッシュボード コンテナーをインラインで (dashboard.tab 内に) 指定するのではなく、 dashboard.containers を使用して、コンテナーを登録することができます。 これは、オブジェクトまたはオブジェクトの配列を受け入れます。

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

登録済みコンテナーを参照するには、コンテナーの ID を指定します。

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

dashboard.insights を使用すれば、分析情報を登録できます。 これは、[チュートリアル: カスタム分析情報ウィジェットのビルド](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)によく似ています

```json
"dashboard.insights": {
"id": "my-widget"
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
```


### <a name="dashboard-container-types"></a>ダッシュボード コンテナーの種類

現在、次の 4 種類のコンテナーがサポートされています。

1. `widgets-container`

    ![ウィジェット コンテナー](media/extensibility/widgets-container.png)

    コンテナーに表示されるウィジェットの一覧。 これはフロー レイアウトです。 これはウィジェットの一覧を受け入れます。

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![Web ビュー コンテナー](media/extensibility/webview-container.png)

    Web ビューがコンテナー全体に表示されます。 Web ビュー ID がタブ ID と同じである必要があります

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![グリッド コンテナー](media/extensibility/grid-container.png)

   グリッド レイアウトに表示されるウィジェットまたは Web ビューの一覧

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![nav セクション](media/extensibility/nav-section.png)

    コンテナーにはナビゲーション セクションが表示されます

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>コンテキスト変数

Visual Studio Code およびその後の Azure Data Studio のコンテキスト変数に関する一般的な情報については、[拡張性](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example)に関するページを参照してください。

Azure Data Studio には、拡張機能で使用できるデータベース接続に関する特定のコンテキストがあります。

### <a name="dashboard"></a>ダッシュボード

ダッシュボードでは、次のコンテキスト変数が用意されています。

|コンテキスト変数| description|
|:---|:---|
|`connectionProvider` | 現在の接続のプロバイダーの識別子の文字列。 例: `connectionProvider == 'MSSQL'`|
|`serverName`|現在の接続のサーバー名の文字列。 例: `serverName == 'localhost'`|
|`databaseName` | 現在の接続のデータベース名の文字列。 例: `databaseName == 'master'`|
|`connection` | 現在の接続の完全な接続プロファイル オブジェクト (IConnectionProfile)|
|`dashboardContext` | 現在オンになっているダッシュボードのページのコンテキストの文字列。 'database' または 'server' のいずれかです。 例: `dashboardContext == 'database'`|
