---
title: azdata bdc リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc コマンドのリファレンス記事です。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a4b619396c2dcdad589deff3f9fc6a03fe37c1d5
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531691"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下の記事では、`azdata` ツールの `sql` コマンドに関するリファレンスを提供します。 `azdata` の他のコマンドに関する詳細については、[azdata のリファレンス](reference-azdata.md)に関するページをご覧ください

## <a name="commands"></a>コマンド
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | ビッグ データ クラスターを作成します。
[azdata bdc delete](#azdata-bdc-delete) | ビッグ データ クラスターを削除します。
[azdata bdc upgrade](#azdata-bdc-upgrade) | SQL Server ビッグ データ クラスターの各コンテナーにデプロイされているイメージを更新します。
[azdata bdc config](reference-azdata-bdc-config.md) | 構成コマンド。
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | エンドポイント コマンド。
[azdata bdc debug](reference-azdata-bdc-debug.md) | デバッグ コマンド。
[azdata bdc status](reference-azdata-bdc-status.md) | BDC の状態コマンド。
[azdata bdc control](reference-azdata-bdc-control.md) | 制御サービス コマンド。
[azdata bdc sql](reference-azdata-bdc-sql.md) | SQL サービス コマンド。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS サービス コマンド。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark サービス コマンド。
[azdata bdc gateway](reference-azdata-bdc-gateway.md) | ゲートウェイ サービス コマンド。
[azdata bdc app](reference-azdata-bdc-app.md) | アプリ サービス コマンド。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark コマンドを使用してセッション、ステートメント、およびバッチを作成および管理することで、ユーザーは Spark システムと対話できます。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS モジュールには、HDFS ファイル システムにアクセスするコマンドが用意されています。
## <a name="azdata-bdc-create"></a>azdata bdc create
SQL Server ビッグ データ クラスターを作成します。Kubernetes の構成と環境変数 ['AZDATA_USERNAME', 'AZDATA_PASSWORD'] がシステムに必要です。
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>使用例
ガイド付きの BDC 展開のエクスペリエンス。必要な値の入力を求めるプロンプトが表示されます。
```bash
azdata bdc create
```
引数を使用した BDC 展開。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
既定の名前ではなくプロファイルに名前を指定した BDC 展開。
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```
引数を使用した BDC 展開。--force フラグが使用されるため、プロンプトは表示されません。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--name -n`
ビッグ データ クラスターの名前。kubernetes 名前空間に使用されます。
#### `--config-profile -c`
ビッグ データ クラスター構成プロファイル。クラスターの展開に使用されます: ['kubeadm-dev-test', 'kubeadm-prod', 'aks-dev-test', 'aks-dev-test-ha']
#### `--accept-eula -a`
Do you accept the license terms? (ライセンス条項に同意しますか?) [yes/no]. ([はい/いいえ]。) この引数を使用しない場合は、環境変数 ACCEPT_EULA を 'yes' に設定できます。 Azdata のライセンス条項は https://aka.ms/eula-azdata-en で確認できます。ビッグ データ クラスターのライセンス条項は、次の場所で確認できます: Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292 、Standard: https://go.microsoft.com/fwlink/?linkid=2104294 、Developer: https://go.microsoft.com/fwlink/?linkid=2104079 。
#### `--node-label -l`
ビッグ データ クラスター ノードのラベル。展開先のノードを指定するために使用されます。
#### `--force -f`
強制的に作成すると、ユーザーは値の入力を求められず、すべての問題が stderr の一部として出力されます。
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
## <a name="azdata-bdc-delete"></a>azdata bdc delete
SQL Server ビッグ データ クラスターを削除します。Kubernetes の構成がシステムに必要です。
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>使用例
BDC の削除。
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--name -n`
ビッグ データ クラスターの名前。kubernetes 名前空間に使用されます。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--force -f`
ビッグ データ クラスターを強制的に削除します。
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
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
SQL Server ビッグ データ クラスターの各コンテナーにデプロイされているイメージを更新します。 更新されるイメージは、渡した Docker イメージに基づきます。 更新されるイメージが、現在展開されているイメージとは別の Docker イメージ リポジトリからのものである場合は、"repository" パラメーターも必要です。
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   [--repository -r]
```
### <a name="examples"></a>使用例
同じリポジトリからの新しいイメージ タグ "cu2" への BDC のアップグレード。
```bash
azdata bdc upgrade -t cu2
```
新しいリポジトリ "foo/bar/baz" からのタグ "cu2" を持つ新しいイメージへの BDC のアップグレード。
```bash
azdata bdc upgrade -t cu2 -r foo/bar/baz
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--name -n`
ビッグ データ クラスターの名前。kubernetes 名前空間に使用されます。
#### `--tag -t`
クラスター内のすべてのコンテナーをアップグレードするターゲットの Docker イメージ タグ。
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--repository -r`
クラスター内のすべてのコンテナーでイメージをプルする Docker リポジトリ。
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
