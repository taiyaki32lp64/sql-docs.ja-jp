---
title: 拡張機能の追加
titleSuffix: Azure Data Studio
description: 拡張機能マーケットプレースから Azure Data Studio に拡張機能を追加する
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 10/03/2019
ms.openlocfilehash: 6f0a2ab021873a2a9414bfbcdb7aed63c2d31056
ms.sourcegitcommit: cf268c4e39edf00a8552466e9440e79e6a5d0084
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2019
ms.locfileid: "72166705"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] の機能を拡張する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 内の拡張機能では、[!INCLUDE[name-sos](../includes/name-sos-short.md)] の基本インストールにさらに機能を追加する簡単な方法を提供します。 

拡張機能は、Azure Data Studio チーム (Microsoft) と、サード パーティのコミュニティ (お客様) によって提供されます。 拡張機能の作成の詳細については、[拡張機能の作成](extension-authoring.md)に関するページを参照してください。


## <a name="add-azure-data-studio-extensions"></a>Azure Data Studio の拡張機能を追加する

1. 使用可能な拡張機能にアクセスするには、[拡張機能] アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。

    ![拡張機能マネージャーのアイコン](media/extensions/extension-manager-icon.png)

    `Ctrl+Shift+X` キー (Windows/Linux) または `Command+Shift+X` キー (Mac) を押すことによって、拡張機能マネージャーに簡単アクセスすることもできます。

2. 使用可能な拡張機能を選択すると、その詳細が表示されます。
    ![拡張機能の詳細](media/extensions/extension-details.png)

3. 必要な拡張機能を選択して**インストール**します。

4. インストール後、 **[再度読み込む]** をクリックすると、Azure Data Studio で拡張機能が有効になります (初めて拡張機能をインストールするときにのみ必須)。

Azure Data Studio での拡張機能マネージャーへのアクセスに問題がある場合は、[GitHub Wiki](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions) で必要な拡張機能をダウンロードできます。


## <a name="access-installed-azure-data-studio-extensions"></a>インストールした Azure Data Studio の拡張機能にアクセスする

Azure Data Studio のエクスペリエンスの向上は拡張機能ごとに異なります。 そのため、拡張機能のエントリ ポイントはさまざまです。 インストール後、その機能にアクセスする方法については、インストールした拡張機能の個別ドキュメントを参照してください。
