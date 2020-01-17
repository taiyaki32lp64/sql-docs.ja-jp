---
title: Azure Kubernetes Service の構成
titleSuffix: SQL Server big data clusters
description: '[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] のデプロイ用に Azure Kubernetes Service (AKS) を構成する方法について説明します。'
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9a3b52a87927eb85d638ed97c1e145efd50602bf
ms.sourcegitcommit: 6413b7495313830ad1ae5aefe0c09e8e7a284b07
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016889"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>SQL Server ビッグ データ クラスターの展開のために Azure Kubernetes Service を構成する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] のデプロイ用に Azure Kubernetes Service (AKS) を構成する方法について説明します。

AKS を使用すると、コンテナー化されたアプリケーションを実行するために、Kubernetes クラスターを利用して事前に構成された仮想マシンのクラスターを簡単に作成、構成、管理できます。 これにより、既存のスキルを使用したり、規模が拡大している専門知識コミュニティを利用したりして、コンテナー ベースのアプリケーションを Microsoft Azure 上に展開して管理することができます。

この記事では、Azure CLI を使用して AKS 上に Kubernetes を展開する手順について説明します。 Azure サブスクリプションをお持ちでない場合は、開始する前に無料アカウントを作成してください。

> [!TIP]
> また、1 つの手順で AKS とビッグ データ クラスターの展開をスクリプト化することもできます。 詳細については、[Python スクリプト](quickstart-big-data-cluster-deploy.md)または Azure Data Studio の[ノートブック](deploy-notebooks.md)において、この操作を行う方法を確認してください。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 ビッグ データ ツールを展開する](deploy-big-data-tools.md):
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
   - **Azure CLI**

- Kubernetes サーバーでの最小の 1.13 バージョン。 AKS の場合、`--kubernetes-version` パラメータ―を使用して、既定値とは異なるバージョンを指定する必要があります。

- AKS の基本的なシナリオを検証しながら、正常なデプロイと最適なエクスペリエンスを確保するために、次のリソースを使用可能な単一ノードまたはマルチノードの AKS クラスターを使用できます。
   - すべてのノード全体で 8個の vCPU
   - VM ごとに 64 GB のメモリ
   - すべてのノード全体で 24 個以上の接続されたディスク

   > [!TIP]
   > Azure インフラストラクチャでは、VM に対して複数のサイズ オプションを提供しています。展開を計画しているリージョンでの選択については、[こちら](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)を参照してください。

## <a name="create-a-resource-group"></a>リソース グループを作成する

Azure リソース グループは、Azure リソースが展開され管理される論理グループです。 次の手順では、Azure にサインインし、AKS クラスターに対するリソース グループを作成します。

1. コマンド プロンプトで次のコマンドを実行し、画面の指示に従って Azure サブスクリプションにログインします。

    ```azurecli
    az login
    ```

1. 複数のサブスクリプションがある場合は、次のコマンドを実行すると、すべてのサブスクリプションを表示できます。

   ```azurecli
   az account list
   ```

1. 別のサブスクリプションに変更する場合は、このコマンドを実行できます。

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. **az group create** コマンドを使用して、リソース グループを作成します。 次の例では、`westus2` の場所に `sqlbdcgroup` という名前のリソース グループを作成します。

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>利用可能な Kubernetes バージョンを確認する

利用可能な最新バージョンの Kubernetes を使用します。 利用可能な最新バージョンは、クラスターを展開する場所に応じて異なります。 次のコマンドは、特定の場所で利用できる Kubernetes バージョンを返します。

コマンドを実行する前に、スクリプトを更新します。 `<Azure data center>` をクラスターの場所に置き換えます。

   **bash**

   ```bash
   az aks get-versions \
   --location <Azure data center> \
   --query orchestrators \
   --o table
   ```

   **PowerShell**

   ```powershell
   az aks get-versions `
   --location <Azure data center> `
   --query orchestrators `
   --o table
   ```

お使いのクラスターで利用可能な最新のバージョンを選択します。 バージョン番号を記録します。 次の手順で使用します。

## <a name="create-a-kubernetes-cluster"></a>Kubernetes クラスターを作成する

1. [az aks create](https://docs.microsoft.com/cli/azure/aks) コマンドを利用して、AKS に Kubernetes クラスターを作成します。 次の例では、サイズが **Standard_L8s** の Linux エージェント ノードを 1 つ備えた *kubcluster* という名前の Kubernetes クラスターを作成します。

   スクリプトを実行する前に、`<version number>` を前の手順で特定したバージョン番号に置き換えます。

   AKS クラスターは必ず、前のセクションで使用したときと同じリソース グループ内に作成してください。

   **bash:**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version <version number>
   ```

   **PowerShell:**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version <version number>
   ```

   Kubernetes エージェント ノードの数を増減するには、`--node-count <n>` を変更します。`<n>` は、使用するエージェント ノードの数です。 これには、AKS によってバックグラウンドで管理されるマスター Kubernetes ノードは含まれません。 上記の例では、評価目的のために 1 つのノードのみを使用しています。

   数分後、コマンドが完了すると、クラスターに関する JSON 形式の情報が返されます。

   > [!TIP]
   > AKS にクラスターを作成する際にエラーを受け取った場合は、この記事の[「トラブルシューティング」のセクション](#troubleshoot)を参照してください。

1. 後から使用するために、前のコマンドからの JSON 出力を保存します。

## <a name="connect-to-the-cluster"></a>クラスターに接続する

1. kubectl を構成して Kubernetes クラスターに接続するには、[az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) コマンドを実行します。 この手順では、資格情報をダウンロードし、それらを使用するために kubectl CLI を構成します。

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. クラスターへの接続を確認するには、クラスター ノードの一覧を返す [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) コマンドを使用します。  以下の例は、1 つのマスター ノードと 3 つのエージェント ノードがある場合の出力を示しています。

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> トラブルシューティング

上記のコマンドを利用して Azure Kubernetes サービスを作成する際に問題が発生した場合は、次の解決策を試してください。

- [最新の Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) がインストールされていることを確認してください。
- 別のリソース グループとクラスター名を使用して、同じ手順を試してください。

## <a name="next-steps"></a>次の手順

この記事の手順では、AKS に Kubernetes クラスターを構成しました。 次のステップとして、AKS Kubernetes クラスター上に SQL Server 2019 ビッグ データ クラスターを展開します。 ビッグ データ クラスターを展開する方法の詳細については、次の記事を参照してください。

[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する方法](deployment-guidance.md)
