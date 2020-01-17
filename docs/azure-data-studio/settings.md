---
title: ユーザーとワークスペースの設定
titleSuffix: Azure Data Studio
description: ユーザーとワークスペースの設定を変更して Azure Data Studio をカスタマイズする方法。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a874aaf9ec136ff9ea27cbeaa92011a07f3718c7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959277"
---
# <a name="modify-user-and-workspace-settings"></a>ユーザーとワークスペースの設定を変更する

設定を使用すると、[!INCLUDE[name-sos](../includes/name-sos-short.md)] を好みに合わせて簡単に構成できます。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] のエディター、ユーザー インターフェイス、機能的な動作のほとんどすべての部分に、変更可能なオプションがあります。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、次の 2 つの異なる設定のスコープがあります。

* **ユーザー**: これらの設定は、開かれた [!INCLUDE[name-sos](../includes/name-sos-short.md)] のすべてのインスタンスにグローバルに適用されます。
* **ワークスペース**: ワークスペースの設定は、コンピューター上のフォルダー固有の設定であり、Explorer のサイドバーでフォルダーが開かれている場合のみ使用できます。 このスコープで定義された設定は、ユーザー スコープよりも優先されます。

## <a name="creating-user-and-workspace-settings"></a>ユーザーとワークスペースの設定を作成する

メニュー コマンド **[ファイル]** 、 **[基本設定]** 、 **[設定]** (Mac の場合は、 **[コード]** 、 **[基本設定]** 、 **[設定]** ) の順にクリックすると、ユーザーおよびワークスペースの設定の構成を開始できます。 既定の設定の一覧が表示されます。 変更する任意の設定を適切な `settings.json` ファイルにコピーします。 右側のタブでは、ユーザーとワークスペースの設定ファイル間をすばやく切り替えることができます。

また、**コマンド パレット** (**Ctrl + Shift + P**) からユーザーとワークスペースの設定を開くこともできます。ここで、 **[基本設定]: [ユーザー設定を開く]** および **[基本設定]: [ワークスペース設定を開く]** を使用します。またはキーボード ショートカット (**Ctrl +** ) を使用することもできます。

次の例は、エディターで行番号を無効にし、コード行が自動的にインデントされるように構成します。

![設定例](media/settings/sample-settings.png)

変更した `settings.json` ファイルを保存した後、設定の変更が [!INCLUDE[name-sos](../includes/name-sos-short.md)] によって再度読み込まれます。

>**注:** ワークスペースの設定は、チーム全体でプロジェクト固有の設定を共有する場合に便利です。

## <a name="settings-file-locations"></a>設定ファイルの場所

ユーザー設定ファイルは、プラットフォームに応じて次の場所に格納されます。

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

ワークスペース設定ファイルは、プロジェクトの `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` フォルダーの下に格納されます。

## <a name="hot-exit"></a>Hot Exit

既定で、終了時に保存されていないファイルの変更は Azure Data Studio によって記憶されます。 これは、Visual Studio Code の Hot Exit 機能と同じです。

既定では、Hot Exit は無効になっています。 Hot Exit を有効にするには、`files.hotExit` 設定を編集します。 詳細については、「[Hot Exit (Visual Studio Code のドキュメント)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)」を参照してください。


## <a name="tab-color"></a>タブの色

使用している接続を簡単に識別できるように、エディターで開かれたタブの色を、接続が属しているサーバー グループの色と一致する色に設定できます。 既定では、タブの色は無効になっています。 タブの色を有効にするには、`sql.tabColorMode` 設定を編集します。

## <a name="additional-resources"></a>その他のリソース

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、ユーザーとワークスペースの設定機能が Visual Studio Code から継承されているため、設定の詳細については、[Visual Studio Code の設定](https://code.visualstudio.com/docs/getstarted/settings)に関する記事を参照してください。
