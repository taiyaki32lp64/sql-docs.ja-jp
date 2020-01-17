---
title: 外部データへのアクセス:MongoDB - PolyBase
ms.date: 12/13/2019
ms.metadata: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: aed736096918d121835149f8cbc9ba32399a3e80
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255431"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>MongoDB 上の外部データにアクセスするための PolyBase の構成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server インスタンス上で PolyBase を使用して、MongoDB 上の外部データに対してクエリを実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

PolyBase をインストールしていない場合は、「[PolyBase のインストール](polybase-installation.md)」をご覧ください。

データベース スコープ資格情報より前に、[マスター キー](../../t-sql/statements/create-master-key-transact-sql.md)を作成しておく必要があります。 
    

## <a name="configure-a-mongodb-external-data-source"></a>MongoDB の外部データ ソースを構成する

MongoDB データ ソースのデータに対してクエリを実行するには、外部テーブルを作成して外部データを参照する必要があります。 このセクションでは、これらの外部テーブルを作成するサンプル コードを示します。

このセクションでは以下の Transact-SQL コマンドが使用されます。

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. MongoDB ソースにアクセスするために、データベース スコープ資格情報を作成します。

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```
1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = 'mongodb://<server>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name);
    ```

1. **省略可能:** 外部テーブルの統計を作成します。

    最適なクエリのパフォーマンスを得るために、外部テーブルの列、特に結合、フィルター、集計に使用される列に対して統計を作成することをお勧めします。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>外部データ ソースを作成すると、[CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) コマンドを使用して、そのソース上でクエリ可能なテーブルを作成することができます。 

## <a name="flattening"></a>フラット化
 フラット化は、MongoDB ドキュメント コレクションの入れ子になったデータと繰り返しデータに対して有効になります。 ユーザーは、入れ子になったデータや繰り返しデータを含む可能性のある MongoDB ドキュメント コレクションに対して `create an external table` を有効にし、リレーショナル スキーマを明示的に指定する必要があります。 その後のマイルストーンで、mongo ドキュメント コレクションに対する自動スキーマ検出を有効にします。
JSON の入れ子になったデータ型/繰り返しデータ型は次のようにフラット化されます

* オブジェクト: 中かっこで囲まれている順序付けられていないキー/値のコレクション (入れ子)

   - 各オブジェクト キーのテーブル列を作成します

     * 列名: objectname_keyname

* 配列: コンマで区切られ、角かっこで囲まれた、順序付けられた値 (繰り返し)

   - 配列項目ごとに新しいテーブル行を追加します

   - 配列ごとの列を作成して配列項目のインデックスを格納します

     * 列名: arrayname_index

     * データ型: bigint

この手法にはいくつかの潜在的な問題があります。そのうちの 2 つを次に示します。

* 空の繰り返しフィールドは、同じレコードのフラット フィールドに含まれるデータを事実上マスクする

* 複数の繰り返しフィールドが存在すると、生成される行数が急増することがある

たとえば、非リレーショナルの JSON 形式で格納されている MongoDB のサンプル データセット レストラン コレクションを評価します。 各レストランには、入れ子になった住所フィールドと、異なる日に割り当てられた採点の配列があります。 次の図は、入れ子になった住所と入れ子になった繰り返しの採点がある一般的なレストランを示しています。

![MongoDB のフラット化](../../relational-databases/polybase/media/mongo-flattening.png "MongoDB レストランのフラット化")

住所オブジェクトは次のようにフラット化されます。

* Nested field restaurant.address.building becomes restaurant.address_building
* Nested field restaurant.address.coord becomes restaurant.address_coord
* Nested field restaurant.address.street becomes restaurant.address_street
* Nested field restaurant.address.zipcode becomes restaurant.address_zipcode

採点配列は次のようにフラット化されます。

| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |A |2|
|1378857600000|A |6|
|135898560000 |A |10|
|1322006400000|A |9|
|1299715200000 |B |14|

## <a name="cosmos-db-connection"></a>Cosmos DB 接続

Cosmos DB の Mongo API および Mongo DB PolyBase コネクタを使用すると、**Cosmos DB インスタンス**の外部テーブルを作成することができます。 これは、上記と同じ手順に従って行います。 データベースのスコープ資格情報、サーバーのアドレス、ポート、場所の文字列が Cosmos DB サーバーのものを反映していることを確認してください。 

## <a name="next-steps"></a>次のステップ

PolyBase の詳細については、[SQL Server PolyBase の概要](polybase-guide.md)に関する記事をご覧ください。
