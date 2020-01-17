---
title: Spark ジョブを使用してデータを取り込む
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、Azure Data Studio で Spark ジョブを使用して、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] のデータ プールにデータを取り込む方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6f66b42fe280ef6612a5e9974ddcf4f1f7ccfcb
ms.sourcegitcommit: add39e028e919df7d801e8b6bb4f8ac877e60e17
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119198"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>チュートリアル:Spark ジョブを使用して SQL Server のデータ プールにデータを取り込む

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このチュートリアルでは、Spark ジョブを使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] の[データ プール](concept-data-pool.md)にデータを取り込む方法について説明します。 

このチュートリアルでは、次の方法を学習します。

> [!div class="checklist"]
> * データ プールに外部テーブルを作成する
> * Spark ジョブを作成して HDFS からデータを読み込む
> * 外部テーブルの結果に対してクエリを実行する

> [!TIP]
> 必要に応じて、このチュートリアルのコマンド用のスクリプトをダウンロードして実行できます。 手順については、GitHub の[データ プールのサンプル](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)を参照してください。

## <a id="prereqs"></a> 前提条件

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
- [ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>データ プールに外部テーブルを作成する

次の手順では、**web_clickstreams_spark_results** という名前のデータ プールに外部テーブルを作成します。 このテーブルは、ビッグ データ クラスターにデータを取り込むための場所として使用できます。

1. Azure Data Studio で、ビッグ データ クラスターの SQL Server マスター インスタンスに接続します。 詳細については、「[SQL Server マスター インスタンスに接続する](connect-to-big-data-cluster.md#master)」を参照してください。

1. **[サーバー]** ウィンドウで接続をダブルクリックして、SQL Server マスター インスタンスのサーバー ダッシュボードを表示します。 **[新しいクエリ]** を選択します。

   ![SQL Server マスター インスタンス クエリ](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. まだ存在しない場合は、データ プールへの外部データ ソースを作成します。

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. データ プールで、**web_clickstreams_spark_results** という名前の外部テーブルを作成します。

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. CTP 3.1 では、データ プールの作成は非同期ですが、まだ完了しているかどうかを判断する方法がありません。 データ プールが作成されたことを確認できるまで 2 分待ってから続行してください。

## <a name="start-a-spark-streaming-job"></a>Spark ストリーミング ジョブを開始する

次の手順では、ストレージ プール (HDFS) から Web クリックストリーム データを、データ プールに作成した外部テーブルに読み込む Spark ストリーミング ジョブを作成します。 このデータは「[ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)」で /clickstream_data に追加されました。

1. Azure Data Studio で、ビッグ データ クラスターのマスター インスタンスに接続します。 詳細については、[ビッグ データ クラスターへの接続](connect-to-big-data-cluster.md)に関するページを参照してください。

2. 新しいノートブックを作成し、カーネルとして Spark | Scala を選択します。

3. Spark インジェスト ジョブを実行する
   1. Spark-SQL コネクタ パラメーターを構成する
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",LongType,true), StructField("wcs_click_time_sk",LongType,true), 
      StructField("wcs_sales_sk",LongType,true), StructField("wcs_item_sk",LongType,true),
      StructField("wcs_web_page_sk",LongType,true), StructField("wcs_user_sk",LongType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. Spark ジョブを定義して実行する
      * 各ジョブは、readStream と writeStream という 2 部構成になっています。 以下では、上で定義したスキーマでデータ フレームを作成し、データ プールの外部テーブルに書き込みます。
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.processAllAvailable()
      query.awaitTermination(40000)
      ```
## <a name="query-the-data"></a>データにクエリを実行する

次の手順は、HDFS からデータをデータ プールに読み込む Spark ストリーミング ジョブを示しています。

1. 取り込んだデータについて問い合わせる前に、Yarn アプリ ID、Spark UI、ドライバー ログなど、Spark の実行状態を確認します。

   ![Spark 実行の詳細](./media/tutorial-data-pool-ingest-spark/Spark-Joblog-sparkui-yarn.png)

1. このチュートリアルで最初に開いた SQL Server マスター インスタンス クエリ ウィンドウに戻ります。

1. 次のクエリを実行して、取り込まれたデータを検査します。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```
1. データは Spark でも照会できます。 たとえば、下のコードでは、テーブルのレコード数が印刷されます。
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
   ```
## <a name="clean-up"></a>クリーンアップ

このチュートリアルで作成されたデータベース オブジェクトを削除するには、次のコマンドを使用します。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>次の手順

Azure Data Studio でサンプル ノートブックを実行する方法について説明します。
> [!div class="nextstepaction"]
> [サンプル ノートブックの実行](tutorial-notebook-spark.md)
