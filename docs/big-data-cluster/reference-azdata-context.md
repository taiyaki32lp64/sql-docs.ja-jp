---
title: azdata context リファレンス
titleSuffix: SQL Server big data clusters
description: azdata context コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 36b670ee8485c2e8db58847e9439dfb5fa9920ce
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531678"
---
# <a name="azdata-context"></a>azdata context

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下の記事では、`azdata` ツールの `sql` コマンドに関するリファレンスを提供します。 `azdata` の他のコマンドに関する詳細については、[azdata のリファレンス](reference-azdata.md)に関するページをご覧ください

## <a name="commands"></a>コマンド
|     |     |
| --- | --- |
[azdata context list](#azdata-context-list) | ユーザー プロファイルで使用可能なコンテキストの一覧を表示します。
[azdata context delete](#azdata-context-delete) | 指定した名前空間のコンテキストをユーザー プロファイルから削除します。
[azdata context set](#azdata-context-set) | 指定した名前空間のコンテキストを、ユーザー プロファイルでのアクティブなコンテキストとして設定します。
## <a name="azdata-context-list"></a>azdata context list
`azdata context set` または `azdata context delete` を使用して、これらのいずれかを設定または削除することができます。 新しいコンテキストにログインするには、`azdata login` を使用します。
```bash
azdata context list [--active -a] 
  ```
### <a name="examples"></a>使用例
ユーザー プロファイルで使用可能なすべてのコンテキストの一覧を表示します。
```bash
azdata context list
```
ユーザー プロファイルでアクティブなコンテキストの一覧を表示します。
```bash
azdata context list --active
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--active -a`
現在アクティブなコンテキストのみを一覧表示します。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org/) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。
## <a name="azdata-context-delete"></a>azdata context delete
アクティブなコンテキストを削除した場合、ユーザーは新しいアクティブなコンテキストを設定する必要があります。 設定または削除できるコンテキストを表示するには、`azdata context list` を使用します
```bash
azdata context delete --namespace -n 
    ```
### Examples
Deletes contextNamespace from the user profile.
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--namespace -n`
削除するコンテキストの名前空間。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org/) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。
## <a name="azdata-context-set"></a>azdata context set
設定できるコンテキストを表示するには、`azdata context list` を使用します。 コンテキストが表示されない場合は、`azdata login` を使用してログインし、ユーザー プロファイルにコンテキストを作成する必要があります。 ログインしたコンテキストが、アクティブなコンテキストになります。 複数のエンティティにログインした場合は、このコマンドを使用してアクティブなコンテキストを切り替えることができます。 現在アクティブなコンテキストを表示するには、`azdata context list --active` を使用します
```bash
azdata context set --namespace -n 
 ```
### <a name="examples"></a>使用例
contextNamespace をユーザー プロファイルでのアクティブなコンテキストとして設定します。
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--namespace -n`
設定するコンテキストの名前空間。
### <a name="global-arguments"></a>グローバル引数
#### `--debug`
すべてのデバッグ ログを表示するようにログの詳細レベルを上げます。
#### `--help -h`
このヘルプ メッセージを表示して終了します。
#### `--output -o`
出力形式。  使用できる値: json、jsonc、table、tsv。  既定値: json。
#### `--query -q`
JMESPath クエリ文字列。 詳細と例については、[http://jmespath.org/](http://jmespath.org/) を参照してください。
#### `--verbose`
ログの詳細レベルを上げます。 詳細なデバッグ ログを表示するには --debug を使います。

## <a name="next-steps"></a>次の手順

`azdata` の他のコマンドに関する詳細については、[azdata のリファレンス](reference-azdata.md)に関するページをご覧ください。 `azdata` ツールのインストール方法の詳細については、[SQL Server 2019 ビッグ データ クラスターを管理する azdata のインストール](deploy-install-azdata.md)に関するページを参照してください。
