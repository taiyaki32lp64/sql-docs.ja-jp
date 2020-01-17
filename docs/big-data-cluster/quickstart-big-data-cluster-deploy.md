---
title: Python スクリプトを使用した展開
titleSuffix: SQL Server Big Data Clusters
description: 展開スクリプトを使用して SQL Server ビッグ データ クラスターを Azure Kubernetes Service (AKS) に展開する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1b2a838f8ad386b8a236304401308d5be0f63ff1
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706348"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Python スクリプトを使用して SQL Server ビッグ データ クラスターを Azure Kubernetes Service (AKS) に展開する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このチュートリアルでは、サンプルの python 展開スクリプトを使用して、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]を Azure Kubernetes Service (AKS) に展開します。

> [!TIP]
> AKS は、ビッグ データ クラスター用の Kubernetes をホストするための選択肢の 1 つにすぎません。 その他の展開オプションと、展開オプションをカスタマイズする方法の詳細については、「[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する方法](deployment-guidance.md)」を参照してください。

ここで使用される既定のビッグ データ クラスターの展開は、1 つの SQL マスター インスタンス、1 つのコンピューティング プール インスタンス、2 つのデータ プール インスタンス、2 つの記憶域プール インスタンスで構成されています。 データは、AKS の既定の記憶域クラスを使用する Kubernetes 永続ボリュームを使用して永続化されます。 このチュートリアルで使用する既定の構成は、開発/テスト環境に適しています。

## <a name="prerequisites"></a>Prerequisites

- Azure サブスクリプション。
- [ビッグ データ ツール](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>Azure アカウントにログインする

このスクリプトでは、AKS クラスターの作成を自動化するために Azure CLI を使用します。 スクリプトを実行する前に、少なくとも 1 回は Azure CLI を使用して Azure アカウントにログインする必要があります。 コマンド プロンプトで次のコマンドを実行します。

```
az login
```

## <a name="download-the-deployment-script"></a>展開スクリプトをダウンロードする

このチュートリアルでは、python スクリプト **deploy-sql-big-data-aks.py** を使用して AKS 上のビッグ データ クラスターの作成を自動化します。 **azdata** 用に python を既にインストールしている場合は、このチュートリアルのスクリプトを正常に実行できます。 

Windows PowerShell または Linux bash プロンプトで、次のコマンドを実行して、GitHub から展開スクリプトをダウンロードします。

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>展開スクリプトを実行する

展開スクリプトを実行するには、次の手順を実行します。 このスクリプトによって、Azure に AKS サービスを作成され、AKS に SQL Server 2019 ビッグ データ クラスターが展開されます。 他の[環境変数](deployment-guidance.md#configfile)を使用してスクリプトを変更して、カスタムの展開を作成することもできます。

1. 次のコマンドを使用してこのスクリプトを実行します。

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > クライアント マシンとパスに python3 と python2 の両方がある場合は、python3 を使用してコマンド `python3 deploy-sql-big-data-aks.py` を実行する必要があります。

1. プロンプトが表示されたら、次の情報を入力します。

   | [値] | [説明] |
   |---|---|
   | **[Azure subscription ID]\(Azure サブスクリプション ID\)** | AKS に使用する Azure サブスクリプション ID。 別のコマンド ラインから `az account list` を実行して、すべてのサブスクリプションとその ID を一覧表示できます。 |
   | **[Azure resource group]\(Azure リソース グループ\)** | AKS クラスター用に作成する Azure リソース グループの名前。 |
   | **[Azure region]\(Azure リージョン\)** | 新しい AKS クラスター用の Azure リージョン (既定値は **westus**)。 |
   | **[Machine size]\(マシン サイズ\)** | AKS クラスター内のノードに使用する[マシン サイズ](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) (既定値は **Standard_L8s**)。 |
   | **[Worker nodes]\(ワーカー ノード\)** | AKS クラスター内のワーカー ノードの数 (既定値は **1**)。 |
   | **[Cluster name]\(クラスター名\)** | AKS クラスターとビッグ データ クラスターの両方の名前。 ビッグ データ クラスターの名前は、小文字の英数字のみを使用し、スペースを含めない必要があります (既定値は **sqlbigdata**)。 |
   | **パスワード** | コントローラー、HDFS/Spark ゲートウェイ、およびマスター インスタンスのパスワード (既定値は **MySQLBigData2019**)。 |
   | **ユーザー名** | コントローラー ユーザーのユーザー名 (既定値: **admin**)。 |

   > [!IMPORTANT]
   > 既定の **Standard_L8s** マシン サイズは、すべての Azure リージョンで使用できるとは限りません。 別のマシン サイズを選択する場合は、クラスター内のノード間で接続できるディスクの合計数が 24 以上であることを確認します。 クラスター内の各永続ボリューム要求には、接続されたディスクが必要です。 現在、ビッグ データ クラスターには 24 個の永続的なボリューム要求が必要です。 たとえば、[Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) マシン サイズでは、32 個の接続ディスクがサポートされているため、このマシン サイズの 1 つのノードでビッグ データ クラスターを評価することができます。

   > [!NOTE]
   > SQL Server の `sa` アカウントは、ビッグ データ クラスターの展開の間に無効になります。 SQL Server のマスター インスタンスに、 **[ユーザー名]** 入力で指定したものと同じ名前と **[パスワード]** 入力に対応するパスワードで、新しい sysadmin ログインがプロビジョニングされます。 コントローラー管理者ユーザーのプロビジョニングにも、同じ**ユーザー名**と**パスワード**の値が使用されます。 ゲートウェイ (Knox) に対してサポートされているユーザーのみが**ルート**であり、パスワードは上記と同じです。

1. スクリプトを開始するには、指定したパラメーターを使用して AKS クラスターを作成します。 この手順には数分かかります。

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>状態を監視する

スクリプトによって AKS クラスターが作成されると、前に指定した設定で必要な環境変数の設定に進みます。 次に、**azdata** が呼び出され、AKS にビッグ データ クラスターが展開されます。

クライアント コマンド ウィンドウに、展開の状態が出力されます。 展開プロセス中に、コントローラー ポッドを待機している一連のメッセージが表示されます。

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10 から 20 分後に、コントローラー ポッドが実行中になっていることが通知されるはずです。

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> ビッグ データ クラスターのコンポーネントに対応するコンテナー イメージのダウンロードに必要な時間によって、展開全体に時間がかかる場合があります。 ただし、数時間もかかることはありません。 展開時に問題が発生した場合は、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の監視とトラブルシューティング](cluster-troubleshooting-commands.md)」を参照してください。

## <a name="inspect-the-cluster"></a>クラスターを検査する

展開中はいつでも、**kubectl** または **azdata** を使用して、実行中のビッグ データ クラスターの状態と詳細を調べることができます。

### <a name="use-kubectl"></a>kubectl を使用する

新しいコマンド ウィンドウを開いて、展開プロセス中に **kubectl** を使用します。

1. 次のコマンドを実行して、クラスター全体の状態の概要を取得します。

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > ビッグ データ クラスター名を変更しなかった場合、スクリプトにより、既定で **sqlbigdata** に設定されます。

1. 次の **kubectl** コマンドを使用して、kubernetes サービスとその内部および外部エンドポイントを調べます。

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 次のコマンドを使用して、kubernetes ポッドの状態を調べることもできます。

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 次のコマンドを使用して、特定のポッドに関する詳細情報を確認します。

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 展開の監視とトラブルシューティングの方法の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の監視とトラブルシューティング](cluster-troubleshooting-commands.md)」を参照してください。

## <a name="connect-to-the-cluster"></a>クラスターに接続する

展開スクリプトが完了すると、出力に成功したことが通知されます。

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

SQL Server ビッグ データ クラスターが AKS に展開されるようになりました。 これで、Azure Data Studio を使用してクラスターに接続できるようになりました。 詳細については、「[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)」を参照してください。

## <a name="clean-up"></a>クリーンアップ

Azure で [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]をテストしている場合は、予期しない料金が発生しないように、完了時に AKS クラスターを削除するようにします。 クラスターを引き続き使用する場合は、削除しないでください。

> [!WARNING]
> 次の手順では、AKS クラスターを破棄します。これにより、SQL Server ビッグ データ クラスターも削除されます。 保持するデータベースまたは HDFS データがある場合は、そのデータをバックアップしてからクラスターを削除してください。

次の Azure CLI コマンドを実行して、Azure のビッグ データ クラスターと AKS サービスを削除します (`<resource group name>` は、展開スクリプトで指定した **Azure リソース グループ**に置き換えます)。

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>次の手順

展開スクリプトで Azure Kubernetes サービスを構成し、SQL Server 2019 ビッグ データ クラスターも展開しました。 また、手動インストールを使用して、今後の展開をカスタマイズすることもできます。 ビッグ データ クラスターの展開方法と展開をカスタマイズする方法の詳細については、「[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する方法](deployment-guidance.md)」を参照してください。

SQL Server ビッグ データ クラスターが展開されたので、サンプル データを読み込んでチュートリアルを調べることができます。

> [!div class="nextstepaction"]
> [チュートリアル: SQL Server 2019 ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)
