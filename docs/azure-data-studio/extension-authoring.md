---
title: 拡張機能の作成
titleSuffix: Azure Data Studio
description: 拡張機能を作成して Azure Data Studio に追加する方法について学習します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d0c43df8b24a33f3763dc5ff3a80e989b9b85038
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959605"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Azure Data Studio 拡張機能を作成することで機能を拡張する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 内の拡張機能では、[!INCLUDE[name-sos](../includes/name-sos-short.md)] の基本インストールにさらに機能を追加する簡単な方法を提供します。

拡張機能は、Azure Data Studio チーム (Microsoft) と、サード パーティのコミュニティ (お客様) によって提供されます。


## <a name="author-an-extension"></a>拡張機能を作成する

Azure Data Studio の拡張に関心がある場合は、独自の拡張機能を作成し、拡張機能ギャラリーに公開することができます。

**拡張機能を作成する**

***前提条件***

拡張機能を開発するには、Node.js をインストールし、自分の $PATH で利用できるようにする必要があります。 Node.js には、拡張機能ジェネレーターのインストールに使用される npm (Node.js パッケージ マネージャー) が含まれています。

新しい拡張機能を開始するには、Azure Data Studio 拡張機能ジェネレーターを使用できます。 この Yeoman [拡張機能ジェネレーター](https://www.npmjs.com/package/generator-azuredatastudio)を使用すると、シンプルな拡張機能プロジェクトをとても簡単に作成できます。 ジェネレーターを起動するには、コマンド プロンプトで次のように入力します。

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**機能拡張の参照**

Azure Data Studio 機能拡張の詳細については、[拡張機能の概要](extensibility.md)に関するページを参照してください。 また、既存の[サンプル](https://github.com/Microsoft/azuredatastudio/tree/master/samples)で API を使用する方法の例もご覧いただけます。


## <a name="debug-an-extension"></a>拡張機能をデバッグする

Visual Studio Code 拡張機能の [Azure Data Studio Debug](https://github.com/kevcunnane/sqlops-debug) を使用して、新しい拡張機能をデバッグできます。

手順
- [Visual Studio Code](https://code.visualstudio.com/) で拡張機能を開きます。
- Azure Data Studio Debug 拡張機能をインストールします。
- **F5** キーを押すか、デバッグ アイコンをクリックして **[開始]** をクリックします。
- Azure Data Studio の新しいインスタンスが特別なモード (拡張機能開発ホスト) で起動し、この新しいインスタンスによってご利用の拡張機能が認識されています。


## <a name="create-an-extension-package"></a>拡張機能パッケージを作成する

拡張機能を作成した後は、VSIX パッケージを作成して、Azure Data Studio にインストールできるようにする必要があります。 [vsce](https://github.com/Microsoft/vscode-vsce) を使用して、VSIX パッケージを作成できます。

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>拡張機能を公開する

Azure Data Studio に新しい拡張機能を公開するには、次の操作を行います。

1. 拡張機能を https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json に追加する
2. 現在、サード パーティの拡張機能をホストすることはサポートされていないため、拡張機能をダウンロードする代わりに、Azure Data Studio にはダウンロード ページを参照するオプションがあります。 拡張機能のダウンロード ページを設定するには、アセット "Microsoft.AzureDataStudio.DownloadPage" の値を設定します。
3. リリース/拡張機能ブランチに対して PR を作成します。
4. 校閲リクエストをチームに送信します。

拡張機能が確認され、拡張機能ギャラリーに追加されます。

**拡張機能の更新プログラムを公開する** 更新プログラムを公開するプロセスは、拡張機能の公開と同様です。 バージョンが package.json で更新されていることを確認してください。
