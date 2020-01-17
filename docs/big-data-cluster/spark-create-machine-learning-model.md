---
title: MLeap での Spark の機械学習モデルの作成とエクスポート
titleSuffix: SQL Server big data clusters
description: PySpark を使用して、SQL Server ビッグ データ クラスターで Spark を使用して機械学習モデルをトレーニングし、作成します。 MLeap でエクスポートし、SQL Server で Java でモデルをスコア付けします。
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bc9191ad90b05e9f48facab0cc4003bbf5adce11
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844231"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] で Spark の機械学習モデルを作成、エクスポート、およびスコア付けする

次のサンプルでは、[Spark の ML](https://spark.apache.org/docs/latest/ml-guide.html) でモデルを作成し、そのモデルを [MLeap](http://mleap-docs.combust.ml/) にエクスポートし、SQL Server で [Java 言語拡張機能](../language-extensions/language-extensions-overview.md) を使用してそのモデルをスコア付けする方法を示します。 これは、SQL Server 2019 ビッグ データ クラスターのコンテキストで行われます。

次の図は、このサンプルで実行される作業を示しています。

![Spark を使用してスコアのエクスポートをトレーニングする](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Prerequisites

このサンプルのすべてのファイルは、[https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml) にあります。

サンプルを実行するには、以下のコンポーネントが必要になります。

- [SQL Server ビッグ データ クラスター](deploy-get-started.md)

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Spark の ML を使用したモデル トレーニング

このサンプルでは、国勢調査データ (**AdultCensusIncome.csv**) を使用して Spark の ML パイプライン モデルを作成します。

1. [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/setup.sh) ファイルを使用して、データ セットをインターネットからダウンロードし、SQL Server ビッグ データ クラスターの HDFS に配置します。 これにより、Spark からアクセスできるようになります。

1. 次に、サンプルのノートブック [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb) をダウンロードします。 PowerShell または Bash コマンド ラインから、次のコマンドを実行してノートブックをダウンロードします。

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   このノートブックには、サンプルのこのセクションに必要なコマンドを含むセルが含まれています。

1. Azure Data Studio でノートブックを開き、各コード ブロックを実行します。 ノードブックの操作に関する詳細については、「[SQL Server でノートブックを使用する方法](notebooks-guidance.md)」を参照してください。

データはまず Spark に読み取られ、トレーニング データ セットとテスト データ セットに分割されます。 次に、トレーニング データを使用してパイプライン モデルをトレーニングします。 最後に、モデルを MLeap バンドルにエクスポートします。

> [!TIP]
> [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_pyspark.py) ファイルのノートブックの外部で、これらの手順に関連付けられている Python コードを確認または実行することも可能です。

## <a name="model-scoring-with-sql-server"></a>SQL Server を使用したモデルのスコアリング

Spark の ML パイプライン モデルが共通のシリアル化 [MLeap バンドル](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html)形式になったため、Spark がなくても Java でモデルをスコア付けすることができます。 

このサンプルでは、SQL Server の [Java 言語拡張機能](../language-extensions/language-extensions-overview.md)を使用します。 SQL Server でモデルをスコア付けするために、まず、Java にモデルを読み込んでスコアを付けることができる Java アプリケーションをビルドする必要があります。 この Java アプリケーションのサンプル コードは、[mssql-mleap-app フォルダー](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mssql-mleap-app)にあります。

サンプルをビルドした後、Transact-SQL を使用して Java アプリケーションを呼び出し、データベース テーブルを使用してモデルをスコア付けすることができます。 これは、[mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_sql_tests.py) ソース ファイルで確認できます。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する方法](deployment-guidance.md)に関するページを参照してください
