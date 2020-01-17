---
title: azdata を使用してアプリケーションを展開する
titleSuffix: SQL Server big data clusters
description: '[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]に Python または R スクリプトをアプリケーションとして展開します。'
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1253863bcd2e1da804480a3e1d0e628024b0798b
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706694"
---
# <a name="how-to-deploy-an-app-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] にアプリを展開する方法

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、SQL Server 2019 ビッグ データ クラスター内でアプリケーションとして R および Python スクリプトを展開して管理する方法について説明します。

## <a name="whats-new-and-improved"></a>新機能と強化された機能

- クラスターとアプリを管理する 1 つのコマンドライン ユーティリティ。
- アプリの展開が簡単になり、さらに仕様ファイルを細かく制御できるようになりました。
- ホストされるアプリケーションの種類が増えました (SSIS と MLeap)。
- アプリケーションの展開を管理する [Visual Studio Code 拡張機能](app-deployment-extension.md)。

アプリケーションは、`azdata` コマンドライン ユーティリティを使用して展開および管理されます。 この記事では、コマンド ラインからアプリを展開する方法の例を示します。 Visual Studio Code でこれを使用する方法については、[Visual Studio Code 拡張機能](app-deployment-extension.md)に関する記事を参照してください。

サポートされているアプリの種類は次のとおりです。
- R および Python アプリ (関数、モデル、アプリ)
- MLeap Serving
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)
- [azdata コマンドライン ユーティリティ](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

SQL Server 2019 では、アプリケーションの作成、削除、説明、初期化、一覧の実行、更新を行うことができます。 次の表では、**azdata** で使用できるアプリケーションの展開コマンドについて説明します。

|コマンド |[説明] |
|:---|:---|
|`azdata login` | SQL Server ビッグ データ クラスターにサインインします |
|`azdata app create` | アプリケーションを作成します。 |
|`azdata app delete` | アプリケーションを削除します。 |
|`azdata app describe` | アプリケーションについて記述します。 |
|`azdata app init` | 新しいアプリケーションのスケルトンを開始します。 |
|`azdata app list` | アプリケーションを一覧表示します。 |
|`azdata app run` | アプリケーションを実行します。 |
|`azdata app update`| アプリケーションを更新します。 |

次の例のように、`--help` パラメーターを使用してヘルプを取得できます。

```bash
azdata app create --help
```

以下のセクションでは、これらのコマンドについて詳しく説明します。

## <a name="sign-in"></a>サインイン

アプリケーションを展開または操作する前に、まず、`azdata login` コマンドを使用して SQL Server ビッグ データ クラスターにサインインします。 `controller-svc-external` サービスの外部 IP アドレス (例: `https://ip-address:30080`) を、クラスターのユーザー名とパスワードと共に指定します。

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

AKS を使用している場合は、次のコマンドを実行し、bash または cmd ウィンドウで次のコマンドを実行することで `controller-svc-external` サービスの IP アドレスを取得します。


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubernetes-clusters-created-with-kubeadm"></a>Kubeadm で作成された Kubernetes クラスター

次のコマンドを実行して、クラスターにサインインするための IP アドレスを取得します

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>アプリを作成する

アプリケーションを作成するには、`azdata` コマンドと共に `app create` を使用します。 これらのファイルは、アプリを作成するマシンのローカルに展開されます。

ビッグ データ クラスターに新しいアプリを作成するには、次の構文を使用します。

```bash
azdata app create --spec <directory containing spec file>
```

次のコマンドは、このコマンドの例を示しています。

```bash
azdata app create --spec ./addpy
```

これは、アプリケーションが `addpy` フォルダーに格納されていることを前提としています。 このフォルダーには、`spec.yaml` というアプリケーションの仕様ファイルも含まれています。 `spec.yaml` ファイルの詳細については、[アプリケーションの展開](concept-application-deployment.md)に関するページを参照してください。

このアプリ サンプル アプリを展開するには、`addpy` というディレクトリに次のファイルを作成します。

- `add.py` 次の Python コードをこのファイルにコピーします。
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml` 次のコードをこのファイルにコピーします。
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

次に、次のコマンドを実行します。

```bash
azdata app create --spec ./addpy
```

list コマンドを使用してアプリが展開されているかどうかを確認できます。

```bash
azdata app list
```

展開が完了していない場合は、次の例のように `state` に `WaitingforCreate` が表示されます。

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

展開が正常に完了すると、`state` は `Ready` 状態に変わります。

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>アプリを一覧表示する

`app list` コマンドを使用して、正常に作成されたすべてのアプリを一覧表示できます。

次のコマンドで、ビッグ データ クラスターで使用できるすべてのアプリケーションが一覧表示されます。

```bash
azdata app list
```

名前とバージョンを指定すると、その特定のアプリとその状態 (Creating または Ready) が一覧表示されます。

```bash
azdata app list --name <app_name> --version <app_version>
```

このコマンドについて次の例を示します。

```bash
azdata app list --name add-app --version v1
```

次の例のような出力が表示されます。

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>アプリを実行する

アプリが `Ready` 状態の場合は、それを使用するには、指定された入力パラメーターを使用して実行します。 次の構文を使用してアプリを実行します。

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

run コマンドについて、次のコマンド例を示します。

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

実行が成功した場合は、アプリの作成時に指定した出力が表示されます。 以下に例を示します。

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>アプリのスケルトンを作成する

init コマンドには、アプリの展開に必要な関連する成果物を含むスキャフォールディングが用意されています。 次の例では、次のコマンドを実行して、これを実行できる hello を作成します。

```bash
azdata app init --name hello --version v1 --template python
```

これにより、hello という名前のフォルダーが作成されます。  `cd` を実行してディレクトリに移動し、フォルダー内に生成されたファイルを調べることができます。 spec.yaml には、名前、バージョン、ソース コードなどのアプリが定義されています。 仕様を編集して、名前、バージョン、入力、および出力を変更することができます。

フォルダーに表示される init コマンドからの出力例を次に示します。

```
hello.py
run-spec.yaml
spec.yaml
```

## <a name="describe-an-app"></a>アプリの説明

describe コマンドでは、クラスター内のエンドポイントを含め、アプリに関する詳細情報が提供されます。 通常、これは、アプリ開発者が swagger クライアントを使用してアプリを構築するときや、Web サービスを使用して RESTful 方式でアプリと対話するときに使用されます。 詳細については、「[ビッグ データ クラスターでアプリケーションを使用する](big-data-cluster-consume-apps.md)」を参照してください。

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>アプリを削除する

ビッグ データ クラスターからアプリを削除するには、次の構文を使用します。

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]に展開されているアプリを独自のアプリケーションに統合する方法の詳細については、「[ビッグ データ クラスター上でアプリケーションを使用する](big-data-cluster-consume-apps.md)」を参照してください。 その他のサンプルにはついては、[アプリの展開サンプル](https://aka.ms/sql-app-deploy)に関するページを参照してください。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
