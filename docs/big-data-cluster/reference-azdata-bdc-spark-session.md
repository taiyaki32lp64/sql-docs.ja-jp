---
title: azdata bdc spark session リファレンス
titleSuffix: SQL Server big data clusters
description: azdata bdc spark session コマンドの参照記事。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f1da72349e7594d267ae0d965ddad03cee93017b
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531738"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark session

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下の記事では、`azdata` ツールの `sql` コマンドに関するリファレンスを提供します。 `azdata` の他のコマンドに関する詳細については、[azdata のリファレンス](reference-azdata.md)に関するページをご覧ください

## <a name="commands"></a>コマンド
|     |     |
| --- | --- |
[azdata bdc spark session create](#azdata-bdc-spark-session-create) | 新しい Spark セッションを作成します。
[azdata bdc spark session list](#azdata-bdc-spark-session-list) | Spark 内のすべてのアクティブなセッションを一覧表示します。
[azdata bdc spark session info](#azdata-bdc-spark-session-info) | アクティブな Spark セッションに関する情報を取得します。
[azdata bdc spark session log](#azdata-bdc-spark-session-log) | アクティブな Spark セッションの実行ログを取得します。
[azdata bdc spark session state](#azdata-bdc-spark-session-state) | アクティブな Spark セッションの実行状態を取得します。
[azdata bdc spark session delete](#azdata-bdc-spark-session-delete) | Spark セッションを削除します。
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark session create
これにより、新しい対話型の Spark セッションが作成されます。 呼び出し元は、Spark セッションの種類を指定する必要があります。 このセッションは azdata の実行の有効期間を超えて存続するため、'spark session delete' で削除する必要があります。
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                [--py-files -p]  
                                [--files -f]  
                                [--driver-memory]  
                                [--driver-cores]  
                                [--executor-memory]  
                                [--executor-cores]  
                                [--executor-count]  
                                [--archives -a]  
                                [--queue -q]  
                                [--name -n]  
                                [--config -c]  
                                [--timeout-seconds -t]
```
### <a name="examples"></a>使用例
セッションを作成します。
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>省略可能なパラメーター
#### `--session-kind -k`
作成するセッションの種類の名前。  spark、pyspark、sparkr、sql のいずれか。
#### `--jar-files -j`
jar ファイル パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--py-files -p`
python ファイル パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--files -f`
ファイル パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--driver-memory`
ドライバーに割り当てるメモリの量。  値の一部として単位を指定します。  例: 512M または 2G。
#### `--driver-cores`
ドライバーに割り当てる CPU コアの量。
#### `--executor-memory`
実行プログラムに割り当てるメモリの量。  値の一部として単位を指定します。  例: 512M または 2G。
#### `--executor-cores`
実行プログラムに割り当てる CPU コアの量。
#### `--executor-count`
実行する実行プログラムのインスタンスの数。
#### `--archives -a`
アーカイブ パスのリスト。  リストを渡すには、値を JSON エンコードします。  例: '["entry1", "entry2"]'。
#### `--queue -q`
セッションを実行する Spark キューの名前。
#### `--name -n`
Spark セッションの名前。
#### `--config -c`
Spark 構成値を含む名前と値のペアのリスト。  JSON ディクショナリとしてエンコードされます。  例: '{"name":"value", "name2":"value2"}'。
#### `--timeout-seconds -t`
セッションのアイドル タイムアウト (秒単位)。
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
ログの詳細レベルを上げます。 完全なデバッグ ログには --debug を使用します。
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark session list
Spark 内のすべてのアクティブなセッションを一覧表示します。
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>使用例
すべてのアクティブなセッションを一覧表示します。
```bash
azdata spark session list
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
ログの詳細レベルを上げます。 完全なデバッグ ログには --debug を使用します。
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark session info
これにより、指定された ID を持つアクティブな Spark セッションのセッション情報が取得されます。  このセッション ID は、'spark session create' から返されます。
```bash
azdata bdc spark session info --session-id -i 
            ```
### Examples
Get session info for session with ID of 0.
```bash
azdata spark session info --session-id 0
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
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
ログの詳細レベルを上げます。 完全なデバッグ ログには --debug を使用します。
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark session log
これにより、指定された ID を持つアクティブな Spark セッションのセッション ログ エントリが取得されます。  このセッション ID は、'spark session create' から返されます。
```bash
azdata bdc spark session log --session-id -i 
           ```
### Examples
Get session log for session with ID of 0.
```bash
azdata spark session log --session-id 0
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
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
ログの詳細レベルを上げます。 完全なデバッグ ログには --debug を使用します。
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark session state
これにより、指定された ID を持つアクティブな Spark セッションのセッション状態が取得されます。  このセッション ID は、'spark session create' から返されます。
```bash
azdata bdc spark session state --session-id -i 
             ```
### Examples
Get session state for session with ID of 0.
```bash
azdata spark session state --session-id 0
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
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
ログの詳細レベルを上げます。 完全なデバッグ ログには --debug を使用します。
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark session delete
これにより、対話型の Spark セッションが削除されます。 このセッション ID は、'spark session create' から返されます。
```bash
azdata bdc spark session delete --session-id -i 
              ```
### Examples
Delete a session.
```bash
azdata spark session delete --session-id 0
```
### <a name="required-parameters"></a>必要なパラメーター
#### `--session-id -i`
Spark セッションの ID 番号。
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
