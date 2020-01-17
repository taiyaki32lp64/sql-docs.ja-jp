---
title: Spark を SQL Server に接続する
titleSuffix: SQL Server big data clusters
description: Spark で MSSQL Spark コネクタを使用して、SQL Server に対する読み取りと書き込みを行う方法について学習します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7720db661d90c3ff2ebec593b22a5aa638038132
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844215"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>MSSQL Spark コネクタを使用して Spark から SQL Server に対する読み取りと書き込みを行う方法

主なビッグ データの使用パターンでは、Spark で大量のデータ処理を行った後、基幹業務アプリケーションにアクセスするために SQL Server にデータを書き込みます。 これらの使用パターンでは、主な SQL の最適化を利用し、効率的な書き込みメカニズムを提供するコネクタの恩恵を受けます。

この記事では、MSSQL Spark コネクタを使用して、ビッグ データ クラスター内の次の場所に対する読み取りと書き込みを行う方法の例を示します。

1. SQL Server マスター インスタンス
1. SQL Server データ プール

   ![MSSQL Spark コネクタ ダイアグラム](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

このサンプルでは、次のタスクが実行されます。

- HDFS からファイルを読み取り、いくつかの基本的な処理を行います。
- データフレームを SQL テーブルとして SQL Server マスター インスタンスに書き込んでから、テーブルをデータフレームに読み取ります。
- データフレームを SQL 外部テーブルとして SQL Server データ プールに書き込んでから、外部テーブルをデータフレームに読み取ります。

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark コネクタ インターフェイス

SQL Server 2019 では、Spark から SQL への書き込みに SQL Server 一括書き込み API を使用する、ビッグ データ クラスター用の **MSSQL Spark コネクタ**を提供します。 MSSQL Spark コネクタは Spark データ ソース API に基づいており、使い慣れた Spark JDBC コネクタ インターフェイスを備えています。 インターフェイス パラメーターについては、[Apache Spark のドキュメント](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)を参照してください。 MSSQL Spark コネクタは、**com.microsoft.sqlserver.jdbc.spark** という名前で参照されます。

次の表では、変更された、または新しくなったインターフェイス パラメーターについて説明します。

| プロパティ名 | 省略可 | [説明] |
|---|---|---|
| **isolationLevel** | はい | これにより、接続の分離レベルが記述されます。 MSSQL Spark コネクタの既定値は、**READ_COMMITTED** です。 |

このコネクタでは、SQL Server 一括書き込み API を使用します。 任意の一括書き込みパラメーターは、任意のパラメーターとして渡される場合があり、コネクタによって基になる API にそのまま渡されます。 一括書き込み操作の詳細については、「[SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server ビッグ データ クラスター](deploy-get-started.md)

- [Azure Data Studio](https://aka.ms/getazuredatastudio)

## <a name="create-the-target-database"></a>ターゲット データベースを作成する

1. Azure Data Studio を開いて、[ご利用のビッグ データ クラスターの SQL Server マスター インスタンスに接続します](connect-to-big-data-cluster.md)。

1. 新しいクエリを作成して、次のコマンドを実行し、**MyTestDatabase** という名前のサンプル データを作成します。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>サンプル データを HDFS に読み込む

1. [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) を自分のローカル コンピューターにダウンロードします。

1. Azure Data Studio を起動して、[ビッグ データ クラスターに接続します](connect-to-big-data-cluster.md)。

1. 自分のビッグ データ クラスターの HDFS フォルダーを右クリックして、 **[新しいディレクトリ]** を選択します。 ディレクトリに **spark_data** という名前を付けます。

1. **spark_data** ディレクトリを右クリックして、 **[ファイルのアップロード]** を選択します。 **AdultCensusIncome.csv** ファイルをアップロードします。

   ![AdultCensusIncome CSV ファイル](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>サンプル ノートブックを実行する

このデータを使って MSSQL Spark コネクタの使用法を示すには、サンプル ノートブックをダウロードして、Azure Data Studio で開き、各コード ブロックを実行します。 ノードブックの操作に関する詳細については、「[SQL Server でノートブックを使用する方法](notebooks-guidance.md)」を参照してください。

1. PowerShell または Bash コマンド ラインから、次のコマンドを実行して **mssql_spark_connector.ipynb** サンプル ノートブックをダウンロードします。

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. Azure Data Studio で、サンプル ノードブック ファイルを開きます。 自分のビッグ データ クラスター用の HDFS/Spark ゲートウェイに接続されていることを確認します。

1. サンプルで各コード セルを実行して、MSSQL Spark コネクタの使用法を参照してください。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する方法](deployment-guidance.md)に関するページを参照してください