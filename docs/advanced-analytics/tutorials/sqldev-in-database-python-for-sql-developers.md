---
title: Python + T-SQL:モデルの開発
description: SQL Server ストアド プロシージャおよび T-SQL 関数に Python コードを埋め込む方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b67be59da71667167594ef82e67dfef6f8118fbb
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725213"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>チュートリアル:SQL 開発者向けの Python データ分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL プログラマー向けのこのチュートリアルでは、SQL Server で [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) データベースを使用して Python ベースの機械学習ソリューションをビルドしてデプロイすることによる Python の統合について説明します。 T-SQL、SQL Server Management Studio、およびデータベース エンジン インスタンスを [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) および Python 言語サポートと共に使用します。

このチュートリアルでは、データ モデリング ワークフローで使用される Python 関数について説明します。 ステップには、データの探索、二項分類モデルの構築とトレーニング、モデル デプロイが含まれます。 ニューヨーク市タクシー・リムジン委員会からのサンプル データを使用します。構築するモデルは、時間帯、走行距離、および乗車場所に基づき、タクシー乗車でチップを受け取れる可能性があるかどうかを予測します。 

このチュートリアルで使用するすべての Python コードは、Management Studio で作成して実行するストアド プロシージャにラップされています。

> [!NOTE]
> このチュートリアルは、R および Python の両方で利用可能です。 R バージョンの場合、[R 開発者向けのデータベース内分析](sqldev-in-database-r-for-sql-developers.md)に関するセクションを参照してください。

## <a name="overview"></a>概要

機械学習ソリューションを構築するプロセスは、複数のツールおよび複数の段階にわたる該当分野の専門家の連携に関連する可能性がある複雑なものです。

+ データの取得とクリーニング
+ モデリングに役立つデータと構築機能の探索
+ モデルのトレーニングと最適化
+ 運用環境に展開する

実際のコードの開発とテストは、専用の開発環境を使用して実行することをお勧めします。 ただし、スクリプトのテスト完了後は、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の使い慣れた環境で [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを使用して、それを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に容易にデプロイすることができます。 ストアド プロシージャでの外部コードのラップは、SQL Server でコードを運用する場合の主要なメカニズムとなります。

Python を初めて使用する SQL プログラマーであろうと、SQL を初めて使用する Python 開発者であろうと、このマルチパート チュートリアルでは、Python と SQL Server を使用してデータベース内分析を行うための一般的なワークフローを紹介します。 

+ [レッスン 1:Python を使用したデータの探索および視覚化](sqldev-py3-explore-and-visualize-the-data.md)

+ [レッスン 2:カスタム SQL 関数を使用してデータ機能を作成する](sqldev-py4-create-data-features-using-t-sql.md)

+ [レッスン 3:T-SQL を使用して Python モデルをトレーニングし保存する](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [レッスン 4:ストアド プロシージャで Python モデルを使用して潜在的な結果を予測する](sqldev-py6-operationalize-the-model.md)

モデルをデータベースに保存した後、ストアド プロシージャを使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] から予測モデルを呼び出すことができます。

## <a name="prerequisites"></a>Prerequisites

+ [SQL Server Machine Learning Services と Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [権限](../security/user-permission.md)

+ [NYC タクシーのデモ データベース](demo-data-nyctaxi-in-sql.md)

すべてのタスクは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを使用して実行できます。

このチュートリアルでは、データベースと表の作成、データのインポート、SQL クエリの作成などの基本的なデータベース操作について理解していることを前提としています。 Python を理解していることは前提としていません。 そのため、すべての Python コードが提供されています。 

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Python を使用したデータの探索および視覚化](sqldev-py3-explore-and-visualize-the-data.md)
