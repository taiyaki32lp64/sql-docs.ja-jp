---
title: 統合ターミナル
titleSuffix: Azure Data Studio
description: Azure Data Studio 内の統合ターミナルについて説明します。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 13a0e3c17f45e0ba136d83f832d3531bc8059884
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959535"
---
# <a name="integrated-terminal"></a>統合ターミナル

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、統合ターミナルを開くことができ、最初はご利用のワークスペースのルートから開始します。 簡単なコマンドライン タスクを実行するのにウィンドウを切り替えたり、既存のターミナルの状態を変更したりする必要がないので、これは便利な場合があります。

ターミナルを開くには: 

* **Ctrl + '** キーボード ショートカットとバッククォート文字を使用します。
* **[表示** | **Integrated Terminal]\(統合端末\)** メニュー コマンドを使用します。
* **コマンド パレット** (**Ctrl + Shift + P**) から、**[View:Toggle Integrated Terminal]\(表示:統合ターミナルの切り替え\)** コマンドを使用します。

![ターミナル](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> [!INCLUDE[name-sos](../includes/name-sos-short.md)] の外部で作業したい場合は、引き続き、エクスプローラーの **[コマンド プロンプトで開く]** コマンド (Mac または Linux の場合は **[Open in Terminal]\(ターミナルで開く\)**) を使用して外部シェルを開くことができます。

## <a name="managing-multiple-terminals"></a>複数のターミナルを管理する

さまざまな場所で開かれる複数のターミナルを作成し、それらのターミナル間を簡単に移動することができます。 ターミナル インスタンスは追加することができます。そのためには、**[ターミナル]** パネルの右上にあるプラス アイコンを押すか、または **Ctrl + Shift + `** コマンドをトリガーします。 これにより、ドロップ ダウンリストに別のエントリが作成され、ターミナルを切り替えるときに使用できます。

![複数のターミナル](media/integrated-terminal/terminal-multiple-instances.png)

ターミナル インスタンスを削除するには、ごみ箱ボタンを押します。

> [!TIP]
> 多数のターミナルを使用する場合は、キーボードのみを使用してターミナル間を移動できるように、[ターミナル キーのバインド](#key-bindings)のセクションに概説する `focusNext`、`focusPrevious`、および `kill` コマンドのキー バインドを追加することができます。

## <a name="configuration"></a>構成

既定で使用されるシェルは、Linux および macOS の場合は `$SHELL`、Windows 10 の場合は PowerShell、それ以前のバージョンの Windows の場合は cmd.exe です。 [設定](settings.md)で `terminal.integrated.shell.*` を設定することで、それらを手動で上書きすることができます。 Linux および macOS の場合は、`terminal.integrated.shellArgs.*` 設定を使用してターミナル シェルに引数を渡すことができます。

### <a name="windows"></a>Windows

Windows 上でシェルを正しく構成することは、適切な実行可能ファイルを見つけて、その設定を更新することです。 以下は、一般的なシェル実行可能ファイルとその既定の場所の一覧です。

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> 統合ターミナルとして使用するには、`stdin/stdout/stderr` をリダイレクトできるように、シェル実行可能ファイルをコンソール アプリケーションにする必要があります。

> [!TIP]
> 統合ターミナル シェルは、[!INCLUDE[name-sos](../includes/name-sos-short.md)] のアクセス許可を使用して実行されています。 昇格された (管理者) 権限または異なる権限を使用してシェル コマンドを実行する必要がある場合は、プラットフォーム ユーティリティ (ターミナル内の `runas.exe` など) を使用することができます。

### <a name="shell-arguments"></a>シェルの引数

シェルを起動するときに、そのシェルに引数を渡すことができます。

たとえば、bash をログイン シェルとして実行できるようにする (`.bash_profile` を実行する) には、引数 `-l` を渡します (二重引用符で囲んで)。

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>ターミナル表示の設定

次の設定を使用すると、統合ターミナルのフォントおよび行の高さをカスタマイズできます。

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>ターミナル キーのバインド

**[ビュー]:[Toggle Integrated Terminal]\(統合ターミナルの切り替え\)** コマンドは **Ctrl + `** キーにバインドされており、統合ターミナル パネルの表示と非表示をすばやく切り替えます。

統合ターミナル内をすばやく移動するためのキーボード ショートカットを次に示します。

|Key|コマンド|  
|---|---|  
|**Ctrl + \`**|統合ターミナルを表示します|  
|**Ctrl + Shift + \`**|新しいターミナルを作成します|  
|**Ctrl + Up**|上にスクロール|  
|**Ctrl + Down**|下にスクロール|  
|**Ctrl + PageUp**|ページを上にスクロールします|  
|**Ctrl + PageDown**|ページを下にスクロールします|  
|**Ctrl + Home**|一番上にスクロールします|  
|**Ctrl + End**|一番下にスクロールします|  
|**Ctrl + K**|ターミナルをクリアします|  

その他のターミナル コマンドも使用でき、好みのキーボード ショートカットにバインドできます。

これらは次のとおりです。

* `workbench.action.terminal.focus`:ターミナルにフォーカスを移動します。 これはトグルに似ていますが、ターミナルが表示されている場合、それを非表示にするのではなく、それにフォーカスを当てます。
* `workbench.action.terminal.focusNext`:次のターミナル インスタンスにフォーカスを移動します。
* `workbench.action.terminal.focusPrevious`:前のターミナル インスタンスにフォーカスを移動します。
* `workbench.action.terminal.kill`:現在のターミナル インスタンスを削除します。
* `workbench.action.terminal.runSelectedText`:ターミナル インスタンス内の選択したテキストを実行します。
* `workbench.action.terminal.runActiveFile`:ターミナル インスタンス内のアクティブ ファイルを実行します。

### <a name="run-selected-text"></a>選択したテキストを実行する

`runSelectedText` コマンドを使用するには、エディターでテキストを選択して、**[ターミナル]:[Run Selected Text in Active Terminal]\(アクティブなターミナルで選択したテキストを実行\)** コマンドを**コマンド パレット** (**Ctrl + Shift +P**) を介して実行します。 ターミナルでは、選択したテキストの実行が試みられます。

![選択したテキストを実行する](media/integrated-terminal/terminal_run_selected.png)

アクティブなエディターでテキストが選択されていない場合は、カーソルが置かれている行がターミナルで実行されます。

### <a name="copy--paste"></a>コピーして貼り付ける

コピーおよび貼り付け用のキーバインドは、次のプラットフォーム標準に従います。

* Linux: **Ctrl + Shift + C** および **Ctrl + Shift + V**
* MAC: **Cmd + C** および **Cmd + V**
* Windows: **Ctrl + C** および **Ctrl + V**

### <a name="find"></a>[検索]

統合ターミナルには、**Ctrl + F** キーを使用してトリガーできる基本的な検索機能があります。

Linux および Windows 上で [検索] ウィジェットを起動するのでなく、**Ctrl + F** キーを使用してシェルに切り替える場合は、次のようにキーバインドを削除する必要があります。

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>ターミナル セッションの名前を変更する

統合ターミナル セッションの名前は、**[ターミナル]:[名前の変更]** (`workbench.action.terminal.rename`) コマンドを使用して変更できるようになりました。 新しい名前がターミナルの選択ドロップダウンに表示されます。

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>キー バインドを強制的にターミナルをパススルーさせる

統合ターミナルにフォーカスがある間、キー ストロークはターミナル自体に渡され、そこで使われるため、キー バインドの多くは機能しません。 `terminal.integrated.commandsToSkipShell` 設定を使用すれば、これを回避することができます。 これにはコマンド名の配列が含められ、それらのコマンドのキー バインドはシェルによる処理をスキップし、代わりに [!INCLUDE[name-sos](../includes/name-sos-short.md)] キー バインド システムによって処理されます。 既定では、これには、いくつかの一般的に使用されるキー割り当てに加えて、すべてのターミナル キー バインドが含まれます。

