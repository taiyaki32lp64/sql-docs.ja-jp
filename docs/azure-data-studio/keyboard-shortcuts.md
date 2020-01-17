---
title: キーボード ショートカットの作成とカスタマイズ
titleSuffix: Azure Data Studio
description: Azure Data Studio でキーボード ショートカットを作成し、カスタマイズする方法について説明します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8e577f50152eb5f86b81caa23cc493b92bbab270
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959479"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>[!INCLUDE[name-sos](../includes/name-sos.md)] でのキーボード ショートカット

この記事では、[!INCLUDE[name-sos](../includes/name-sos-short.md)] でキーボード ショートカットをすばやく表示、編集、および作成する手順について説明します。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] のキー バインド機能は Visual Studio Code から継承されているため、高度なカスタマイズや、さまざまなキーボード レイアウトの使用などの詳細については、「[Visual Studio Code のキー バインド](https://code.visualstudio.com/docs/getstarted/keybindings)」を参照してください。 一部のキー バインド機能については使用できない場合があります (たとえば、キーマップ拡張機能は、[!INCLUDE[name-sos](../includes/name-sos-short.md)] ではサポートされていません)。


## <a name="open-the-keyboard-shortcuts-editor"></a>キーボード ショートカット エディターを開く

現在定義されているキーボード ショートカットをすべて表示するには:

**[ファイル]** メニューから、**キーボード ショートカット** エディターを開きます。 **[ファイル]**  >  **[基本設定]**  >  **[キーボード ショートカット]** (Mac の場合は **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**  >  **[基本設定]**  >  **[キーボード ショートカット]** )。

**キーボード ショートカット** エディターでは、現在のキー バインドを表示することに加えて、キーボード ショートカットが定義されていない使用可能なコマンドの一覧を表示できます。 **キーボード ショートカット** エディターを使用すると、キー バインドの変更、削除、リセット、および新しいキー バインドの定義を簡単に行うことができます。  


## <a name="edit-existing-keyboard-shortcuts"></a>既存のキーボード ショートカットを編集する

既存のキーボード ショートカットのキー バインドを変更するには:

1. 検索ボックスを使用するか、または一覧をスクロールして、変更するキーボード ショートカットを見つけます。
   > [!TIP]
   > キー、コマンド、ソースなどで検索して、関連するすべてのキーボード ショートカットを表示します。

1. 目的のエントリを右クリックし、 **[Change Key binding]\(キー バインドの変更\)** を選択します

   ![キーボード ショートカットを編集する](media/keyboard-shortcuts/change-keybinding.png)

1. 目的のキーの組み合わせを押し、**Enter** キーを押してそれを保存します。 

   ![キーボード ショートカットを保存する](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>新しいキーボード ショートカットを作成する

新しいショートカットキーを作成するには:

1. キー バインドが設定されていないコマンドを右クリックし、 **[Add Key binding]\(キー バインドの追加\)** を選択します。

   ![キーボード ショートカットを作成する](media/keyboard-shortcuts/add-keybinding.png)

1. 目的のキーの組み合わせを押し、**Enter** キーを押してそれを保存します。


