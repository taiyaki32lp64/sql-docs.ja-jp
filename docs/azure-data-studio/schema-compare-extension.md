---
title: スキーマ比較の拡張機能
titleSuffix: Azure Data Studio
description: Azure Data Studio 用のスキーマ比較の拡張機能をインストールして使用します
ms.custom: seodec18
ms.date: 11/04/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: f93711983eb32a979e47941883e968b52e03459c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532541"
---
# <a name="schema-compare-extension"></a>スキーマ比較の拡張機能
スキーマ比較の拡張機能では、2 つのデータベース定義を比較して、ソースとターゲットの相違を適用するための使いやすいエクスペリエンスが提供されます。


## <a name="features"></a>[機能]

* 2 つの dacpac ファイルまたはデータベースのスキーマを比較する
* ソースと一致させるためにターゲットに対して実行する必要がある一連のアクションとして結果を表示する
* 結果に一覧表示されるアクションを選択的に除外する
* 比較のスコープを制御するオプションを設定する
* ターゲットに変更を適用するか、同じ効果でスクリプトを生成する
* 比較を保存する

![スキーマ比較:比較例](media/extensions/schema-compare-extension/schema-compare.png)


## <a name="why-would-i-use-the-schema-compare-extension"></a>スキーマ比較の拡張機能を使用する理由

異なるデータベース バージョンを手動で管理し、同期するのは面倒な場合があります。 スキーマ比較の拡張機能を使用すると、データベースを比較するプロセスが簡略化され、同期時に完全に制御できます。変更を適用する前に、特定の相違点とカテゴリを選択的にフィルター処理できます。 スキーマ比較の拡張機能は、時間とコードを節約する信頼性の高いツールです。

![スキーマ比較:[オプション] ダイアログ](media/extensions/schema-compare-extension/schema-compare-options.png)


## <a name="install-the-extension"></a>拡張機能をインストールする

1. 拡張機能アイコンを選択すると、使用可能な拡張機能が表示されます。

    ![拡張機能マネージャーのアイコン](media/extensions/extension-manager-icon.png)

2. **スキーマ比較**の拡張機能を検索し、それを選択して詳細を表示します。 **[インストール]** をクリックして、拡張機能を追加します。

3. インストール後、 **[再度読み込む]** をクリックすると、Azure Data Studio で拡張機能が有効になります (初めて拡張機能をインストールするときにのみ必須)。


## <a name="launch-a-schema-compare"></a>スキーマ比較を開始する

1. [スキーマ比較] ダイアログを開くには、オブジェクト エクスプローラーでデータベースを**右クリック**して、 **[スキーマ比較]** をクリックします。 選択したデータベースは、比較でソース データベースとして設定されます。

    ![スキーマ比較の起動メニュー](media/extensions/schema-compare-extension/schema-compare-launch.png)


2. 省略記号 (...) のいずれかを選択して、スキーマ比較のソースとターゲットを変更し、[OK] をクリックします。

    ![スキーマ比較のソース/ターゲットの選択](media/extensions/schema-compare-extension/schema-compare-select-source-target.png)

3. 比較をカスタマイズするには、ツールバーの **[オプション]** ボタンをクリックします。

4. 比較の結果を表示するには、 **[比較]** をクリックします。


## <a name="next-steps"></a>次の手順

スキーマ比較の詳細については、[Microsoft のドキュメントを参照してください。](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions)
問題の報告や機能の要求を行うには、[ここ](https://github.com/microsoft/azuredatastudio/issues)にアクセスしてください。