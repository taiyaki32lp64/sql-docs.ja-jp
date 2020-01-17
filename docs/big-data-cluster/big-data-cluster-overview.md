---
title: ビッグ データ クラスターとは
titleSuffix: SQL Server Big Data Clusters
description: Kubernetes 上で動作し、リレーショナル データと HDFS データの両方にスケールアウト オプションを提供する SQL Server ビッグ データ クラスターについて説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6bbb185936b2a388014a16ae0a6ecc6c52c5d29a
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706663"
---
# <a name="what-are-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]とは

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 以降、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を使用すると、Kubernetes 上で動作する SQL Server、Spark、および HDFS コンテナーのスケーラブルなクラスターを展開できます。 これらのコンポーネントを並行して実行し、Transact-SQL または Spark からのビッグ データの読み取り、書き込み、処理を行うことができるので、高価値のリレーショナル データと大量のビッグ データを簡単に組み合わせて分析できます。

最新リリースの新機能と既知の問題の詳細については、[リリース ノート](release-notes-big-data-cluster.md)を参照してください。

## <a name="scenarios"></a>シナリオ

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を使用すると、ビッグ データの操作が柔軟になります。 外部データ ソースに対してクエリを実行する、SQL Server が管理する HDFS にビッグ データを格納する、またはクラスターを介して複数の外部データ ソースのデータに対してクエリを実行することができます。 このデータは、AI、機械学習、その他の分析タスクに使用できます。 以下に、これらのシナリオについて詳しく説明します。

### <a name="data-virtualization"></a>データの仮想化

[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md) を利用することで、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]では、データを移動またはコピーすることなく、外部データ ソースに対してクエリを実行できます。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] では、データ ソースに新しいコネクタが導入されています。

![データの仮想化](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>データ レイク

SQL Server ビッグ データ クラスターには、スケーラブルな HDFS *記憶域プール*が含まれています。 これは、複数の外部ソースから取り込まれた可能性があるビッグ データを格納するために使用できます。 ビッグ データ クラスターの HDFS にビッグ データが格納されたら、そのデータを分析してクエリを実行し、リレーショナル データと組み合わせることができます。

![データ レイク](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>スケールアウト データ マート

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]には、任意のデータの分析パフォーマンスを向上させるスケールアウト コンピューティングとストレージが用意されています。 さまざまなソースのデータを取り込み、さらに分析するためにキャッシュとして*データ プール* ノード全体に分散することができます。

![データ マート](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>AI と機械学習の統合

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を使用すると、HDFS 記憶域プールとデータ プールに格納されているデータに対して AI と機械学習タスクを実行できます。 R、Python、Scala、または Java を使用し、Spark だけでなく SQL Server の組み込みの AI ツールを使用できます。

![AI と ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>管理と監視

管理と監視は、コマンド ライン ツール、API、ポータル、および動的管理ビューを組み合わせて実行できます。

Azure Data Studio を使用すると、ビッグ データ クラスターに対してさまざまなタスクを実行できます。 これは、新しい **SQL Server 2019 拡張機能**によって実現します。 この拡張機能には、次の機能があります。

- 一般的な管理タスク用の組み込みスニペット。
- HDFS の参照、ファイルのアップロード、ファイルのプレビュー、およびディレクトリの作成を行う機能。
- Jupyter 互換ノートブックを作成、開く、および実行する機能。
- 外部データ ソースの作成を簡易化するデータ仮想化ウィザード。

## <a id="architecture"></a> アーキテクチャ

SQL Server ビッグ データ クラスターは、[Kubernetes](https://kubernetes.io/docs/concepts/) によって調整された Linux コンテナーのクラスターです。

### <a name="kubernetes-concepts"></a>Kubernetes の概念

Kubernetes はオープン ソースのコンテナー オーケストレーターであり、必要に応じてコンテナーの展開を拡張できます。 次の表では、重要な Kubernetes 用語をいくつか定義します。

|||
|:--|:--|
| **Cluster** | Kubernetes クラスターは、ノードと呼ばれる一連のマシンです。 1 つのノードがクラスターを制御し、マスター ノードに指定されます。残りのノードはワーカー ノードです。 Kubernetes マスターは、ワーカー間で作業を分散し、クラスターの正常性を監視する役割を担います。 |
| **[Node]** | ノードによって、コンテナー化されたアプリケーションが実行されます。 物理マシンまたは仮想マシンのいずれかです。 Kubernetes クラスターには、物理マシンと仮想マシンの両方のノードを含めることができます。 |
| **ポッド** | ポッドは、Kubernetes のアトミック展開単位です。 ポッドは、アプリケーションの実行に必要な 1 つ以上のコンテナーと関連するリソースの論理グループです。 各ポッドはノード上で実行されます。ノードでは、1 つ以上のポッドを実行できます。 Kubernetes マスターによって、クラスター内のノードにポッドが自動的に割り当てられます。 |
| &nbsp; ||

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]では、Kubernetes は [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の状態の責任を負います。Kubernetes では、クラスター ノードの構築と構成が行われ、ポッドがノードに割り当てられ、クラスターの正常性が監視されます。

### <a name="big-data-clusters-architecture"></a>ビッグ データ クラスターのアーキテクチャ

次の図は、SQL Server 用のビッグ データ クラスターのコンポーネントを示しています。

![アーキテクチャの概要](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> コントローラー

コントローラーには、クラスターの管理とセキュリティ機能があります。 これには、制御サービス、構成ストア、および Kibana、Grafana、Elasticsearch などのその他のクラスターレベルサービスが含まれています。

### <a id="computeplane"></a> コンピューティング プール

コンピューティング プールは、クラスターにコンピューティング リソースを提供します。 これには SQL Server on Linux ポッドを実行するノードが含まれます。 コンピューティング プール内のポッドは、特定の処理タスクのために *SQL コンピューティング インスタンス*に分割されます。 

### <a id="dataplane"></a> データ プール

データ プールは、データの永続化とキャッシュに使用されます。 データ プールは、SQL Server on Linux を実行している 1 つ以上のポッドで構成されます。 これは、SQL クエリまたは Spark ジョブからデータを取り込むために使用されます。 SQL Server ビッグ データ クラスターのデータ マートは、データ プールに保持されます。 

### <a name="storage-pool"></a>記憶域プール

記憶域プールは、SQL Server on Linux、Spark、および HDFS で構成される記憶域プール ポッドで構成されます。 SQL Server ビッグ データ クラスター内のすべての記憶域ノードは、HDFS クラスターのメンバーです。

> [!TIP]
> ビッグ データ クラスターのアーキテクチャとインストールの詳細については、「[ワークショップ:Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] アーキテクチャ](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)」を参照してください。

## <a name="next-steps"></a>次の手順

SQL Server ビッグ データ クラスターの展開の詳細については、「[SQL Server ビッグ データ クラスターの使用を開始する](deploy-get-started.md)」を参照してください。
