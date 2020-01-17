---
title: はじめに
titleSuffix: SQL Server Big Data Clusters
description: SQL Server ビッグ データ クラスターを展開するための手順とリソースについて説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2bbb4c05a6760709fcb873cd8c39f301c37aeb2b
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706359"
---
# <a name="get-started-with-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の使用を開始する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)を展開する方法の概要を示します。

その他の展開シナリオについては、以下を参照してください。

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Docker コンテナー](../linux/sql-server-linux-configure-docker.md)

この記事では、概念を確認すると共に、このセクションにある他の展開に関する記事を理解するためのフレームワークを提供します。 特定の展開手順は、クライアントとサーバーに対するプラットフォームの選択に応じて異なります。

> [!TIP]
> Kubernetes とビッグ データ クラスターが展開された環境を迅速に取得して、その機能を向上させるには、[スクリプト セクション](#scripts)に示されているサンプル スクリプトの 1 つを使用します。 展開後、クラスターを管理するには、次のセクションの[クライアント ツール](#tools)を使用します。

## <a id="tools"></a> クライアント ツール

ビッグ データ クラスターには、特定のクライアント ツール セットが必要です。 Kubernetes にビッグ データ クラスターを展開する前に、次のツールをインストールする必要があります。

| ツール | [説明] |
|---|---|
| **azdata** | ビッグ データ クラスターを展開して管理します。 |
| **kubectl** | 基になる Kubernetes クラスターを作成して管理します。 |
| **Azure Data Studio** | ビッグ データ クラスターを使用するためのグラフィカル インターフェイス。 |
| **SQL Server 2019 の拡張機能** | ビッグ データ クラスター機能を有効にする Azure Data Studio の拡張機能。 |

別のシナリオでは、ほかのツールが必要になります。 各記事では、特定のタスクを実行するための前提条件が説明されています。 ツールとインストール リンクの完全な一覧については、「[SQL Server 2019 ビッグ データ ツールのインストール](deploy-big-data-tools.md)」を参照してください。

## <a name="kubernetes"></a>Kubernetes

ビッグ データ クラスターは、[Kubernetes ](https://kubernetes.io/docs/home) 上で管理される一連の相互に関連するコンテナーとして、展開されます。 Kubernetes は、さまざまな方法でホストできます。 既存の Kubernetes 環境が既にある場合でも、ビッグ データ クラスターに対する関連要件を確認する必要があります。

- **Azure Kubernetes Service (AKS)** :AKS を使用すると、Azure 内にマネージド Kubernetes クラスターを展開できます。 ユーザーは、エージェント ノードの管理と保守のみを行います。 AKS では、クラスター用に独自のハードウェアをプロビジョニングする必要はありません。 [Python スクリプト](quickstart-big-data-cluster-deploy.md)や[展開ノートブック](deploy-notebooks.md)を使用すると、1 つの手順で AKS クラスターを作成してビッグ データ クラスターを展開することも簡単になります。 ビッグ データ クラスターの展開のために AKS を構成する方法の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の展開のために Azure Kubernetes Service を構成する](deploy-on-aks.md)」を参照してください。

- **複数のマシン**:Kubernetes を複数の Linux マシンに展開することもできます。物理サーバーまたは仮想マシンの可能性があります。 [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) ツールは、Kubernetes クラスターを作成するために使用できます。 この種類の展開を自動化するには、[bash スクリプト](deployment-script-single-node-kubeadm.md)を使用できます。 ビッグ データ クラスターに使用する既存のインフラストラクチャが既に存在する場合には、この方法が適しています。 ビッグ データ クラスターでの **kubeadm** 展開の利用に関する詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の展開のために複数のマシン上に Kubernetes を構成する](deploy-with-kubeadm.md)」を参照してください。

## <a name="deploy-a-big-data-cluster"></a>ビッグ データ クラスターをデプロイする

Kubernetes を構成した後、`azdata bdc create` コマンドを使用してビッグ データ クラスターを展開します。 展開時には、いくつかの異なる方法を使用できます。

- 開発/テスト環境に展開する場合は、**azdata** によって提供される[既定の構成](deployment-guidance.md#deploy)の 1 つを使用することを選択できます。

- 展開をカスタマイズするには、独自の[展開構成ファイル](deployment-guidance.md#configfile)を作成して使用します。

- 完全な無人インストールの場合は、環境変数によって他のすべての設定を渡すことができます。 詳細については、[無人展開](deployment-guidance.md#unattended)に関するセクションを参照してください。


## <a id="scripts"></a> 展開スクリプト

展開スクリプトを使用すると、Kubernetes とビッグ データ クラスターの両方を 1 つの手順で展開できます。 また、通常は、ビッグ データ クラスター設定に対して既定値が指定されます。 ビッグ データ クラスターの展開を別の方法で構成する独自のバージョンを作成することで、展開スクリプトをカスタマイズできます。

現時点では、次の展開スクリプトを使用できます。

- [Python スクリプト -- Azure Kubernetes Service (AKS) 上にビッグ データ クラスターを展開する](quickstart-big-data-cluster-deploy.md)
- [Bash スクリプト--単一ノード kubeadm クラスターにビッグ データ クラスターを展開する](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>展開ノートブック

Azure Data Studio ノートブックを実行して、ビッグ データ クラスターを展開することも可能です。 ノートブックを使用して AKS 上に展開する方法の詳細については、次の記事を参照してください:

- 「[Azure Data Studio ノートブックを使用して SQL Server ビッグ データ クラスターを展開する](deploy-notebooks.md)」。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターを正常に展開した後は、[クラスターに接続](connect-to-big-data-cluster.md)して、複数のチュートリアルに使用する[サンプル データを読み込む](tutorial-load-sample-data.md)ことを検討してください。
