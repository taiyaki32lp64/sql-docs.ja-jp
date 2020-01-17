---
title: インメモリ OLTP を使用した JSON の処理の最適化
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a2b02d5b987958abc8dd97e48f86e7b44636efad
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096078"
---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>インメモリ OLTP を使用した JSON の処理の最適化
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SQL Server と Azure SQL Database では、JSON 形式のテキストを使用できます。 JSON データを処理するクエリのパフォーマンスを上げるには、標準の文字列型の列 (NVARCHAR 型) を使用してメモリ最適化テーブルに JSON ドキュメントを格納します。 JSON データをメモリ最適化テーブルに格納すると、ロックはされることがなく、データはインメモリでアクセスされるので、クエリのパフォーマンスが向上します。

## <a name="store-json-in-memory-optimized-tables"></a>メモリ最適化テーブルへの JSON の格納
次に、`Tags` と `Data` という 2 つの JSON 列があるメモリ最適化 `Product` テーブルの例を示します。

```sql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```

## <a name="optimize-json-processing-with-additional-in-memory-features"></a>その他のインメモリ機能での JSON 処理の最適化
SQL Server と Azure SQL Database の機能を使用すると、既存のインメモリ OLTP のテクノロジに JSON の機能を完全に統合できます。 たとえば、次を実行できます。
 - ネイティブ コンパイルの CHECK 制約を使用して、メモリ最適化テーブルに格納された [JSON ドキュメントの構造を検証](#validate)できます。
 - 計算列を使用して JSON ドキュメントに格納された[値を公開し、型を厳密に指定](#computedcol)できます。
 - メモリ最適化インデックスを使用して JSON ドキュメントの[値にインデックスを作成](#index)できます。
 - JSON ドキュメントの値を使用する [SQL クエリをネイティブでコンパイル](#compile)したり、結果を JSON テキストとして書式設定したりできます。

## <a name="validate"></a> JSON の列の検証
SQL Server と Azure SQL Database では、文字列の列に格納された JSON ドキュメントの内容を検証するネイティブ コンパイルの CHECK 制約を追加できます。 ネイティブ コンパイルされた JSON の CHECK 制約では、メモリ最適化テーブルに格納されている JSON テキストの書式が正しいことを保証します。

次の例では、JSON 列 `Tags` を含む `Product` テーブルを作成します。 `Tags` 列には、`ISJSON` 関数を使用して列の JSON テキストを検証する、CHECK 制約が設定されています。

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

ネイティブ コンパイルの CHECK 制約は、JSON の列がある既存のテーブルに追加することもできます。

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

## <a name="computedcol"></a> 計算列を使用した JSON 値の公開
計算列では、JSON テキストの値が公開されます。JSON テキストから値を再度取得したり、JSON の構造を再度解析したりすることなくそれらの値にアクセスできます。 このようにして公開される値の型は厳密に指定され、計算列に物理的に保存されます。 保存される計算列を使用した JSON 値へのアクセスは、JSON ドキュメント内の値に直接アクセスするよりも高速です。

次の例では、JSON の `Data` 列から次の 2 つの値を公開する方法を示します。
-   製品の製造国。
-   製品の製造コスト。

この例では、計算列の `MadeIn` と `Cost` は、`Data` 列に格納された JSON ドキュメントが変更されるたびに更新されます。

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

## <a name="index"></a> JSON の列のインデックス値
SQL Server と Azure SQL Database では、メモリ最適化インデックスを使用して JSON の列の値にインデックスを作成できます。 インデックスが作成されている JSON 値は、次の例のように、計算列を使用して公開され、型が厳密に指定されている必要があります。

JSON の列の値には、標準の非クラスター化インデックスとハッシュ インデックスの両方を使用してインデックスを作成できます。
-   非クラスター化インデックスは、いくつかの JSON 値による行範囲の選択または JSON 値による結果の並べ替えを行うクエリを最適化します。
-   ハッシュ インデックスは、検索対象の正確な値を指定することによって、1 行または少数の行を選択するクエリを最適化します。

次の例では、2 つの計算列を使用して JSON 値を公開するテーブルを構築します。 例では、1 つの JSON 値に非クラスター化インデックスを作成し、もう 1 つの値にハッシュ インデックスを作成します。

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```

## <a name="compile"></a> JSON クエリのネイティブ コンパイル
プロシージャ、関数、およびトリガーに組み込み JSON 関数を使用するクエリが含まれている場合は、ネイティブ コンパイルによって、それらのクエリのパフォーマンスが向上し、クエリの実行に必要な CPU サイクルが減少します。

次に、いくつかの JSON 関数 (**JSON_VALUE**、**OPENJSON**、**JSON_MODIFY**) を使用するネイティブ コンパイル プロシージャの例を示します。

```sql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
