---
title: Spark コンピューティング プールとは
titleSuffix: SQL Server big data clusters
description: この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 内のコンピューティング プールについて説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6f2813dff5e965f61f15b947725d78bf327dde7
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532395"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターのコンピューティング プールとは

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、SQL Server ビッグ データ クラスターでの "*SQL Server コンピューティング プール*" の役割について説明します。 コンピューティング プールにより、ビッグ データ クラスター用のスケールアウト コンピューティング リソースが提供されます。 以下のセクションでは、コンピューティング プールのアーキテクチャと機能について説明します。

## <a name="compute-pool-architecture"></a>コンピューティング プールのアーキテクチャ

コンピューティング プールは、Kubernetes で実行されている 1 つまたは複数のコンピューティング ポッドで構成されます。 これらのポッドの自動化された作成と管理は、[SQL Server マスター インスタンス](concept-master-instance.md)によって調整されます。 各ポッドには、一連の基本サービスと、SQL Server データベース エンジンのインスタンスが含まれています。

## <a name="scale-out-groups"></a>スケール アウト グループ

コンピューティング プールは、HDFS、Oracle、MongoDB、Teradata など、さまざまなデータ ソースに対する分散クエリの PolyBase スケールアウト グループとして機能することができます。 Kubernetes でコンピューティング ポッドを使用することにより、ビッグ データ クラスターで PolyBase スケールアウト グループ用のコンピューティング ポッドの作成と構成を自動化できます。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] の詳細については、次のリソースを参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
- [ワークショップ: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] アーキテクチャ](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
