---
title: 記憶域プール内の HDFS データにクエリを実行する
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]内の HDFS データにクエリを実行する方法について説明します。 記憶域プール内のデータに対して外部テーブルを作成し、クエリを実行します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ba5721ef461fe327a3309431cc994a5ed377be7
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652442"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>チュートリアル:SQL Server ビッグ データ クラスター内の HDFS にクエリを実行する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このチュートリアルでは、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の HDFS データにクエリを実行する方法について説明します。

このチュートリアルでは、次の方法を学習します。

> [!div class="checklist"]
> * ビッグ データ クラスター内の HDFS データを指す外部テーブルを作成する。
> * このデータを、マスター インスタンスの価値の高いデータと結合する。

> [!TIP]
> 必要に応じて、このチュートリアルのコマンド用のスクリプトをダウンロードして実行できます。 手順については、GitHub の[データ仮想化のサンプル](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)を参照してください。

## <a id="prereqs"></a> 前提条件

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
- [ビッグ データ クラスターへのサンプル データの読み込み](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>HDFS に対する外部テーブルを作成する

記憶域プールには、HDFS に格納されている CSV ファイル内の Web クリックストリーム データが含まれます。 次の手順を使用して、そのファイル内のデータにアクセスできる外部テーブルを定義します。

1. Azure Data Studio で、ビッグ データ クラスターの SQL Server マスター インスタンスに接続します。 詳細については、「[SQL Server マスター インスタンスに接続する](connect-to-big-data-cluster.md#master)」を参照してください。

1. **[サーバー]** ウィンドウで接続をダブルクリックして、SQL Server マスター インスタンスのサーバー ダッシュボードを表示します。 **[新しいクエリ]** を選択します。

   ![SQL Server マスター インスタンス クエリ](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. 次の Transact-SQL コマンドを実行し、マスター インスタンスの **Sales** データベースにコンテキストを変更します。

   ```sql
   USE Sales
   GO
   ```

1. HDFS から読み取る CSV ファイルの形式を定義します。 F5 キーを押して、ステートメントを実行します。

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

1. まだ存在しない場合は、記憶域プールに対する外部データ ソースを作成します。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   END
   ```

1. 記憶域プールから `/clickstream_data` を読み取ることができる外部テーブルを作成します。 **SqlStoragePool** には、ビッグ データ クラスターのマスター インスタンスからアクセスできます。

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>データにクエリを実行する

次のクエリを実行し、`web_clickstream_hdfs` 外部テーブルの HDFS データを、ローカルの `Sales` データベースのリレーショナル データと結合します。

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>クリーンアップ

このチュートリアルで使用される外部テーブルを削除するには、次のコマンドを使用します。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>次の手順

次の記事に進み、ビッグ データ クラスターから Oracle にクエリを実行する方法を学習します。
> [!div class="nextstepaction"]
> [Oracle の外部データにクエリを実行する](tutorial-query-oracle.md)
