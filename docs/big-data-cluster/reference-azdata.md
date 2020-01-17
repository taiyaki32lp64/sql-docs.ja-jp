---
title: azdata リファレンス
titleSuffix: SQL Server big data clusters
description: azdata コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4ef2ba9c68f3586e159c326863ef76ba231f01b9
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531648"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下の記事では、`azdata` ツールの `sql` コマンドに関するリファレンスを提供します。 `azdata` の他のコマンドに関する詳細については、[azdata のリファレンス](reference-azdata.md)に関するページをご覧ください

## <a name="commands"></a>コマンド
|     |     |
| --- | --- |
|[azdata bdc](reference-azdata-bdc.md) | SQL Server ビッグ データ クラスターを選択、管理、および操作します。 |
|[azdata app](reference-azdata-app.md) | アプリケーションを作成、削除、実行、および管理します。 |
[azdata login](#azdata-login) | クラスターのコントローラー エンドポイントにログインし、その名前空間をアクティブなコンテキストとして設定します。 ログイン時にパスワードを使用するには、AZDATA_PASSWORD 環境変数を設定する必要があります。
[azdata logout](#azdata-logout) | クラスターからログアウトします。
|[azdata context](reference-azdata-context.md) | コンテキスト管理コマンド。 |
|[azdata control](reference-azdata-control.md) | コントロール プレーンを作成、削除、管理します。 |
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI により、ユーザーは T-SQL を使用して SQL Server を操作できます。 |
|[azdata notebook](reference-azdata-notebook.md) | ターミナルからノートブックを表示、実行、管理するコマンドです。 |
## <a name="azdata-login"></a>azdata login
クラスターが展開されると、展開中にコントローラー エンドポイントが一覧表示されます。これをログインに使用する必要があります。  コントローラー エンドポイントがわからない場合は、システム上の <user home>/.kube/config の既定の場所にクラスターの kube 構成を配置してログインするか、KUBECONFIG 環境変数を使用する (つまり KUBECONFIG=path/to/.kube/config をエクスポートする) ことをお勧めします。ログインすると、このクラスターの名前空間がアクティブなコンテキストに設定されます。
```bash
azdata login [--auth] 
             [--endpoint -e]  
             [--accept-eula -a]  
             [--namespace -n]  
             [--username -u]  
             [--principal -p]
```
### <a name="examples"></a>使用例
基本認証を使用してログインします。
```bash
azdata login --auth basic --username johndoe --endpoint https://<ip or domain name>:30080            
```
Active directory を使用してログインします。
```bash
azdata login --auth ad --endpoint https://<ip or domain name>:30080                
```
明示的なプリンシパルで active directory を使用してログインします。
```bash
azdata login --auth ad --principal johndoe@COSTOSO.COM --endpoint https://<ip or domain name>:30080
```
対話形式でログインします。 引数として指定されていない場合は、クラスター名の入力が常に求められます。 システムに AZDATA_USERNAME、AZDATA_PASSWORD、および ACCEPT_EULA 環境変数を設定している場合、これらの入力は求められません。 システムに kube 構成がある場合、または構成のパスを指定するために KUBECONFIG 環境変数を使用している場合は、対話型エクスペリエンスでは、まず構成の使用が試行され、構成が失敗した場合にプロンプトが表示されます。
```bash
azdata login
```
ログイン (非対話形式)。 クラスター名、コントローラーのユーザー名、コントローラー エンドポイント、および使用許諾契約の同意を引数として設定してログインします。 環境変数 AZDATA_PASSWORD を設定する必要があります。  コントローラー エンドポイントを指定しない場合は、マシン上の <user home>/.kube/config の既定の場所に kube 構成を配置するか、KUBECONFIG 環境変数を使用してください (つまり、KUBECONFIG=path/to/.kube/config をエクスポートしてください)。
```bash
azdata login --namespace ClusterName --username johndoe@contoso.com  --endpoint https://<ip or domain name>:30080 --accept-eula yes
```
マシン上で kube 構成を使用してログインし、AZDATA_USERNAME、AZDATA_PASSWORD、および ACCEPT_EULA の環境変数を設定してログインします。
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--auth`
認証方法。 基本認証または Active Directory 認証。 既定値は "basic" 認証です。
#### `--endpoint -e`
クラスター コントローラーのエンドポイント "https://host:port"。 この引数を使用しない場合は、マシンで kube 構成を使用できます。 構成を <user home>/.kube/config の既定の場所に配置するか、KUBECONFIG 環境変数を使用してください。
#### `--accept-eula -a`
Do you accept the license terms? (ライセンス条項に同意しますか?) [yes/no]. ([はい/いいえ]。) この引数を使用しない場合は、環境変数 ACCEPT_EULA を 'yes' に設定できます。 この製品のライセンス条項は https://aka.ms/eula-azdata-en で確認できます。
#### `--namespace -n`
クラスター コントロール プレーンの名前空間。
#### `--username -u`
アカウント ユーザー。 この引数を使用しない場合は、環境変数 AZDATA_USERNAME を設定できます。
#### `--principal -p`
Kerberos 領域。 ほとんどの場合、Kerberos 領域は、大文字のドメイン名です。
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
## <a name="azdata-logout"></a>azdata logout
クラスターからログアウトします。
```bash
azdata logout 
```
### <a name="examples"></a>使用例
このユーザーをログアウトします。
```bash
azdata logout
```
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
