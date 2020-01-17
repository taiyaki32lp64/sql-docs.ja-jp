---
title: Oracle の外部データにクエリを実行する
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の Oracle データにクエリを実行する方法について説明します。 Oracle のデータに対する外部テーブルを作成し、クエリを実行します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b880e3758481e5b061221bd2753b5a26f01ed856
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708367"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>チュートリアル:SQL Server ビッグ データ クラスターから Oracle にクエリを実行する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このチュートリアルでは、SQL Server 2019 ビッグ データ クラスターから Oracle データにクエリを実行する方法について説明します。 このチュートリアルを実行するには、Oracle サーバーにアクセスできる必要があります。 アクセスできない場合は、このチュートリアルで、SQL Server ビッグ データ クラスター内の外部データ ソースに対してデータ仮想化がどのように機能するかを理解できます。

このチュートリアルでは、次の方法を学習します。

> [!div class="checklist"]
> * 外部 Oracle データベースのデータ用の外部テーブルを作成する。
> * このデータを、マスター インスタンスの価値の高いデータと結合する。

> [!TIP]
> 必要に応じて、このチュートリアルのコマンド用のスクリプトをダウンロードして実行できます。 手順については、GitHub の[データ仮想化のサンプル](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)を参照してください。

## <a id="prereqs"></a> 前提条件

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
- [ビッグ データ クラスターへのサンプル データの読み込み](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Oracle テーブルを作成する

次の手順では、Oracle で `INVENTORY` という名前のサンプル テーブルを作成します。

1. このチュートリアルで使用する Oracle インスタンスとデータベースに接続します。

1. `INVENTORY` テーブルを作成するには、次のステートメントを実行します。

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. このテーブルに、**inventory.csv** ファイルの内容をインポートします。 このファイルは、「[前提条件](#prereqs) 」セクションのサンプル作成スクリプトによって作成されたものです。

## <a name="create-an-external-data-source"></a>外部データ ソースを作成する

最初の手順では、Oracle サーバーにアクセスできる外部データ ソースを作成します。

1. Azure Data Studio で、ビッグ データ クラスターの SQL Server マスター インスタンスに接続します。 詳細については、「[SQL Server マスター インスタンスに接続する](connect-to-big-data-cluster.md#master)」を参照してください。

1. **[サーバー]** ウィンドウで接続をダブルクリックして、SQL Server マスター インスタンスのサーバー ダッシュボードを表示します。 **[新しいクエリ]** を選択します。

   ![SQL Server マスター インスタンス クエリ](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 次の Transact-SQL コマンドを実行し、マスター インスタンスの **Sales** データベースにコンテキストを変更します。

   ```sql
   USE Sales
   GO
   ```

1. Oracle サーバーに接続するためのデータベース スコープ資格情報を作成します。 次のステートメントで、Oracle サーバーに適切な資格情報を指定します。

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Oracle サーバーを指す外部データ ソースを作成します。

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

## <a name="create-an-external-table"></a>外部テーブルを作成する

次に、Oracle サーバー上の `INVENTORY` テーブルに対して **iventory_ora** という名前の外部テーブルを作成します。

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> Oracle に対するクエリの実行中に、テーブル名と列名では ANSI SQL 引用符で囲まれた識別子が使用されます。 その結果、名前では大文字と小文字が区別されます。 Oracle メタデータ内のテーブル名と列名の大文字と小文字が正確に一致する、外部テーブル定義で名前を指定することが重要です。

## <a name="query-the-data"></a>データにクエリを実行する

次のクエリを実行し、`iventory_ora` 外部テーブルのデータを、ローカルの `Sales` データベース内のテーブルと結合します。

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>クリーンアップ

このチュートリアルで作成されたデータベース オブジェクトを削除するには、次のコマンドを使用します。

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>次の手順

データ プールにデータを取り込む方法を学習します:
> [!div class="nextstepaction"]
> [データをデータ プールに読み込む](tutorial-data-pool-ingest-sql.md)
