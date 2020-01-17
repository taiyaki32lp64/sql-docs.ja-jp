---
title: アプリケーション展開とは
titleSuffix: Big Data Clusters for SQL Server 2019
description: この記事では、SQL Server 2019 ビッグ データ クラスターへのアプリケーションの展開について説明します。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: da497f8d7c435a807ba530ae619ff91a6f2dff71
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653004"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>SQL Server 2019 ビッグ データ クラスターのアプリケーション展開とは

アプリケーション展開は、アプリケーションを作成、管理、および実行するためのインターフェイスを提供することにより、ビッグ データ クラスターでアプリケーションの展開を可能にします。 ビッグ データ クラスターに展開されたアプリケーションは、クラスターの計算機能を利用し、クラスターで使用可能なデータにアクセスできます。 これにより、データが存在するアプリケーションを管理しながら、アプリケーションのスケーラビリティとパフォーマンスが向上します。
以降のセクションでは、アプリケーション展開のアーキテクチャと機能について説明します。

## <a name="application-deployment-architecture"></a>アプリケーション展開アーキテクチャ

アプリケーション展開は、コントローラーとアプリのランタイム ハンドラーで構成されます。 アプリケーションを作成するときに、仕様ファイル (`spec.yaml`) が提供されます。 この `spec.yaml` ファイルには、アプリケーションを正常に展開するためにコントローラーが認識する必要があるすべてのものが含まれています。 `spec.yaml` の内容例を次に示します。

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

コントローラーは、`spec.yaml` ファイル内で指定された `runtime` を検査し、対応するランタイム ハンドラーを呼び出します。 ランタイム ハンドラーによってアプリケーションが作成されます。 まず、Kubernetes ReplicaSet が作成されます。これには、それぞれに展開するアプリケーションが含まれた 1 つ以上のポッドが含まれます。 ポッドの数は、アプリケーションの `spec.yaml` ファイルで設定された `replicas` パラメーターによって定義されます。 各ポッドには、1 つ以上のプールを含めることができます。 プールの数は、`spec.yaml` ファイルの `poolsize` パラメーター セットによって定義されます。

これらの設定は、展開が並列で処理できる要求の量に影響します。 指定された時間内の要求の最大数は、`replicas` に `poolsize` を掛けた数と等しくなります。 5 つのレプリカがあり、レプリカあたり 2 つのプールがある場合、展開では 10 個の要求を並行して処理できます。 次の図は、`replicas` と `poolsize` をグラフィカルに表現したものです。

![Poolsize と replicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

ReplicaSet が作成され、ポッドが開始されると、`spec.yaml` ファイルで `schedule` が設定されている場合は、cron ジョブが作成されます。 最後に、アプリケーションの管理と実行に使用できる Kubernetes サービスが作成されます (以下を参照)。

アプリケーションが実行されると、アプリケーションの Kubernetes サービスによって、レプリカに対する要求がプロキシされ、結果が返されます。

## <a name="how-to-work-with-application-deployment"></a>アプリケーション展開を使用する方法

アプリケーション展開には、次の 2 つの主要なインターフェイスがあります。 
- [コマンド ライン インターフェイス `azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code と Azure Data Studio 拡張機能](app-deployment-extension.md)

RESTful Web サービスを使用してアプリケーションを実行することもできます。 詳細については、[ビッグ データ クラスターでのアプリケーションの使用](big-data-cluster-consume-apps.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]でアプリケーションを作成して実行する方法の詳細については、次を参照してください。

- [azdata を使用してアプリケーションを展開する](big-data-cluster-create-apps.md)
- [アプリケーション展開の拡張機能を使用してアプリケーションを展開する](app-deployment-extension.md)
- [ビッグ データ クラスターでアプリケーションを使用する](big-data-cluster-consume-apps.md)

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、次の概要を参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
