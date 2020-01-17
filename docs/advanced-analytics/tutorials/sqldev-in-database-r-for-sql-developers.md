---
title: R + T-SQL チュートリアル:モデルの開発
description: SQL Server ストアド プロシージャおよび T-SQL 関数に R プログラミング言語コードを埋め込む方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f0734203a5b5e49ad344b2c0440208c6b652c080
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725468"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>チュートリアル:SQL 開発者向けの R data analytics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL プログラマー向けのこのチュートリアルでは、SQL Server で [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) データベースを使用して R ベースの機械学習ソリューションを構築してデプロイすることによる R の統合について説明します。 T-SQL、SQL Server Management Studio、およびデータベース エンジン インスタンスを [[Machine Learning Services]](../install/sql-machine-learning-services-windows-install.md) および R 言語サポートと共に使用します

このチュートリアルでは、データ モデリング ワークフローで使用される R 関数について説明します。 手順には、データの探索、二項分類モデルの構築とトレーニング、モデル デプロイが含まれます。 構築するモデルは、旅行が、時間、移動距離、乗車位置に 基づいたヒントを生成する可能性があるかどうかを予測します。 

このチュートリアルで使用するすべての R コードは、Management Studio で作成して実行するストアド プロシージャにラップされています。

## <a name="background-for-sql-developers"></a>SQL 開発者向けの履歴

機械学習ソリューションを構築するプロセスは、複数のツールおよび複数の段階にわたる該当分野の専門家の連携に関連する可能性がある複雑なものです。

+ データの取得とクリーニング
+ モデリングに役立つデータと構築機能の探索
+ モデルのトレーニングと最適化
+ 実稼働へのデプロイ

実際のコードの開発とテストは、専用の R 開発環境を使用して実行することをお勧めします。 ただし、スクリプトのテスト完了後は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使い慣れた環境で [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアドプロシージャを使用して、それを [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に容易にデプロイすることができます。

このマルチパートチュートリアルの目的は、"完成した R コード" を SQL Server に移行するための一般的なワークフローの概要です。 

- [レッスン 1:ストアド プロシージャ中の R 関数を呼び出して、データの形状と分布を調べ、視覚化する](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [レッスン 2:T-SQL 関数で R を使用してデータ機能を作成する](sqldev-create-data-features-using-t-sql.md)
  
- [レッスン 3:関数とストアド プロシージャを使用した R モデルのトレーニングと保存](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [レッスン 4:ストアド プロシージャで R モデルを使用して潜在的な結果を予測する](../tutorials/sqldev-operationalize-the-model.md)

データベースにモデルが保存されたら、ストアド プロシージャを使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] から予測モデルを呼び出します。

## <a name="prerequisites"></a>Prerequisites

すべてのタスクは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを使用して実行できます。

このチュートリアルでは、データベースと表の作成、データのインポート、SQL クエリの作成などの基本的なデータベース操作について理解していることを前提としています。 R がわかっていることを前提としていません。そのため、すべての R コードが提供されます。 

+ R が有効になっている [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) または [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R ライブラリ](../package-management/r-package-information.md)

+ [権限](../security/user-permission.md)

+ [NYC タクシーのデモ データベース](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [ストアド プロシージャで R 関数を使用してデータの探索と視覚化を行う](../tutorials/sqldev-explore-and-visualize-the-data.md)
