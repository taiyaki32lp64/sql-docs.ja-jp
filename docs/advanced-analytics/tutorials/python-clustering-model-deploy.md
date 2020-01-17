---
title: Python のチュートリアル:クラスター モデルのデプロイ
description: この 4 部構成チュートリアル シリーズの第 4 部では、SQL Server Machine Learning Services などのクラスター モデルを Python にデプロイします。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: df0fd7cb27977679a6ca879d7ae01045ed3fa8c8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727139"
---
# <a name="tutorial-deploy-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>チュートリアル:モデルを Python に配置し、SQL Server Machine Learning Services で顧客を分類する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この 4 部構成チュートリアルシリーズの第 4 部では、SQL Server Machine Learning Services を使用して、Python で開発されたクラスター モデルを SQL データベースにデプロイします。

新しい顧客が登録する際、クラスターを定期的に実行するには、どのアプリからでも Python スクリプトを呼び出せる必要があります。 これを行うには、データベースの SQL ストアドプロシージャ内に Python スクリプトを置き、SQL Server に Python スクリプトをデプロイします。 モデルは SQL database で実行されるため、データベースに格納されているデータに対して、容易にトレーニングできます。

このセクションでは、SQL Server に先ほど書き込んだ Python コードを移動し、SQL Server Machine Learning Services を使用して、クラスタリングをデプロイします。

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * モデルを生成するストアド プロシージャの作成
> * SQL Server でのクラスタリング
> * クラスタリング情報の使用

[第 1 部](python-clustering-model.md)では、前提条件をインストールしてサンプル データベースを復元しました。

[第 2 部](python-clustering-model-prepare-data.md)では、SQL データベースからデータを準備してクラスタリングを実行する方法を学びました。

[第 3 部](python-clustering-model-build.md)では、Python で K-Means クラスタリング モデルを作成し、トレーニングする方法を学びました。

## <a name="prerequisites"></a>Prerequisites

* このチュートリアルシリーズの第 4 部は、[**第 1 部**](python-clustering-model.md)の前提条件を満たし、[**第 2 部**](python-clustering-model-prepare-data.md)および[**第 3 部**](python-clustering-model-build.md)の手順を完了していることを前提としています。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>モデルを生成するストアド プロシージャの作成

以下の T-SQL スクリプトを実行して、ストアド プロシージャを作成します。 このプロシージャでは、本チュートリアル シリーズの第 1 部・2 部で作成した手順を再作成します。

* 購入・返却履歴に基づく顧客の分類
* K-Means アルゴリズムを使用した、4 つの顧客クラスターの生成

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
FROM
  (
    SELECT
      ss_customer_sk,
      -- return order ratio
      COUNT(distinct(ss_ticket_number)) AS orders_count,
      -- return ss_item_sk ratio
      COUNT(ss_item_sk) AS orders_items,
      -- return monetary amount ratio
      SUM( ss_net_paid ) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
  ) orders
  LEFT OUTER JOIN
  (
    SELECT
      sr_customer_sk,
      -- return order ratio
      count(distinct(sr_ticket_number)) as returns_count,
      -- return ss_item_sk ratio
      COUNT(sr_item_sk) as returns_items,
      -- return monetary amount ratio
      SUM( sr_return_amt ) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>SQL Database 上でのクラスタリング実行

ストアド プロシージャが作成されたので、以下のスクリプトを実行し、プロシージャを使ってクラスタリングを実行します。

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>クラスタリング情報の使用

クラスタリングのプロシージャはデータベースに格納されているため、同じデータベースに格納されている顧客データに対し、効率的にクラスタリングを実行できます。 顧客データが更新されるたびにプロシージャを実行し、更新されたクラスタリング情報を利用できます。

たとえば、クラスター 0 (非アクティブなグループ) の顧客にプロモーションメールを送るとします (本チュートリアルの[第 3 部](python-clustering-model-build.md#analyze-the-results)で 4 つのクラスターについて説明しています)。 以下のコードは、クラスター 0 の顧客のメール アドレスを選択します。

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

**c. cluster** 値を変更して、他のクラスターの顧客のメール アドレスを返すことができます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルの終了後は、SQL Server から tpcxbb_1gb データベースを削除してかまいません。

## <a name="next-steps"></a>次の手順

本チュートリアル シリーズの第 4 部では、以下の手順を完了しました。

* モデルを生成するストアド プロシージャの作成
* SQL Server でのクラスタリング
* クラスタリング情報の使用

SQL Server Machine Learning Services における Pythonの使用について、詳しくは以下の記事を参照してください。

* [クイックスタート: SQL Server Machine Learning Services で簡単な Python スクリプトを作成して実行する](quickstart-python-create-script.md)
* [SQL Server Machine Learning Services 用の、その他の Python チュートリアル](sql-server-python-tutorials.md)
* [sqlmlutils を使用した Python パッケージのインストール](../package-management/install-additional-python-packages-on-sql-server.md)

