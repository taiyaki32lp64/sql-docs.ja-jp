---
title: CREATE TABLE AS SELECT (Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2016
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 22f296db7717e81068ac52d6c3df547a0ba0d085
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660790"
---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>CREATE TABLE AS SELECT (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

CREATE TABLE AS SELECT (CTAS) は、使用可能な最も重要な T-SQL 機能の 1 つです。 SELECT ステートメントの出力に基づいて新しいテーブルを作成する完全に並列化された操作です。 CTAS は、テーブルのコピーを作成する最も簡単で速い方法です。   
 
 たとえば、次のような場合に CTAS を使用します。  
  
-   異なるハッシュ ディストリビューション列を持つテーブルを再作成する。
-   レプリケート済みとしてテーブルを再作成する。   
-   テーブル内の一部の列でのみ、列ストア インデックスを作成する。  
-   外部データをクエリまたはインポートする。  

> [!NOTE]  
> CTAS はテーブルの作成機能に加えられたものであるため、このトピックでは CREATE TABLE トピックの内容は繰り返しません。 代わりに、CTAS と CREATE TABLE のステートメントの違いについて説明します。 CREATE TABLE の詳細については、[CREATE TABLE (Azure SQL Data Warehouse)](https://msdn.microsoft.com/library/mt203953/) ステートメントを参照してください。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>構文   

```  
CREATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>  
    OPTION <query_hint> 
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | CLUSTERED COLUMNSTORE INDEX ORDER (column[,...n])
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
      | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

<query_hint> ::=
    {
        MAXDOP 
    }
```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>引数  
詳細については、CREATE TABLE の「[引数](https://msdn.microsoft.com/library/mt203953/#Arguments)」セクションを参照してください。  

<a name="column-options-bk"></a>

### <a name="column-options"></a>列のオプション
`column_name` [ ,...`n` ]   
 列名では、CREATE TABLE に示されている[列のオプション](https://msdn.microsoft.com/library/mt203953/#ColumnOptions)は使用できません。  代わりに、新しいテーブルには 1 つ以上の列名のオプション リストを指定できます。 新しいテーブルの列では、指定した名前を使用します。 列名を指定する場合、列リスト内の列の数は、SELECT の結果内の列の数と一致する必要があります。 列名を指定しない場合、新しいターゲット テーブルでは、SELECT ステートメントの結果の列名を使用します。 
  
 データ型、照合順序、NULL 値の許容など、その他の列オプションを指定することはできません。 これらの各属性は、`SELECT` ステートメントの結果から派生されます。 ただし、SELECT ステートメントを使用して、属性を変更することができます。 例については、「[CTAS を使用して列属性を変更する](#ctas-change-column-attributes-bk)」を参照してください。   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>テーブル分散オプション

`DISTRIBUTION` = `HASH` ( *distribution_column_name* ) | ROUND_ROBIN | REPLICATE      
CTAS ステートメントには分散オプションが必要であり、既定値はありません。 これは、既定値を持つ CREATE TABLE とは異なります。 

最適な分散オプションの選択方法などの詳細については、CREATE TABLE の「[Table distribution options](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions)」 (テーブル分散オプション) セクションを参照してください。 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>テーブル パーティションのオプション
CTAS ステートメントは、ソース テーブルがパーティション分割されている場合でも、既定では、非パーティション テーブルを作成します。 CTAS ステートメントを使用して、パーティション テーブルを作成するには、パーティション オプションを指定する必要があります。 

詳細については、CREATE TABLE の「[Table partition options](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions)」 (テーブル パーティションのオプション) セクションを参照してください。

<a name="select-options-bk"></a>

### <a name="select-statement"></a>Select ステートメント
SELECT ステートメントは、CTAS と CREATE TABLE の基本的な違いです。  

 `WITH` *common_table_expression*  
 共通テーブル式 (CTE) と呼ばれる一時的な名前付き結果セットを指定します。 詳細については、「[WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)」を参照してください。  
  
 `SELECT` *select_criteria*  
 SELECT ステートメントの結果を新しいテーブルに追加します。 *select_criteria* は、新しいテーブルにコピーするデータを決定する SELECT ステートメントの本文です。 SELECT ステートメントについては、「[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)」を参照してください。  
 
### <a name="query-hint"></a>クエリ ヒント
ユーザーは MAXDOP を整数値に設定し、並列処理の最大値を制御できます。  MAXDOP が 1 に設定されていると、クエリは 1 つのスレッドによって実行されます。

 
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>アクセス許可  
CTAS には、*select_criteria* で参照されるすべてのオブジェクトに対する `SELECT` 権限が必要です。

テーブルを作成する権限については、CREATE TABLE の「[権限](https://msdn.microsoft.com/library/mt203953/#Permissions)」を参照してください。 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>全般的な解説
詳細については、CREATE TABLE の「[全般的な解説](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks)」を参照してください。

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
Azure SQL Data Warehouse では、統計の自動作成や自動更新はまだサポートされていません。  クエリから最高のパフォーマンスを得るには、CTAS を実行した後と、データで大幅な変更が発生した後に、すべてのテーブルのすべての列の統計を作成することが重要です。 詳細については、「 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)」をご覧ください。

順序付けされたクラスター化列ストア インデックスは、文字列型の列を除く Azure SQL Data Warehouse でサポートされている任意のデータ型の列に作成できます。  

CTAS では [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) の効果はありません。 同様の動作を実現するには、[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) を使用します。  
 
詳細については、CREATE TABLE の「[制限事項と制約](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions)」を参照してください。

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>ロック動作  
 詳細については、CREATE TABLE の「[ロック動作](https://msdn.microsoft.com/library/mt203953/#LockingBehavior)」を参照してください。
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>パフォーマンス 

ハッシュ分散テーブルの場合、CTAS を使用して、結合と集計のパフォーマンスを高めるために異なる分散列を選択できます。 異なる分散列を選択することが目的ではない場合、同じ分散列を指定すると、行の再分散が避けられるため、CTAS の最高のパフォーマンスが得られます。 

CTAS を使用してテーブルを作成するときに、パフォーマンスが重要でない場合は、分散列を決定しなくてすむように `ROUND_ROBIN` を指定できます。

後続のクエリでのデータ移動を避けるため、`REPLICATE` を指定できますが、各計算ノードにテーブルの完全なコピーを読み込むための記憶域は増加します。  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>テーブルのコピー例

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. CTAS を使用してテーブルをコピーする 
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse

`CTAS` の最も一般的な使用方法の 1 つとして、DDL を変更できるようにテーブルのコピーを作成することが考えられます。 たとえば、最初に `ROUND_ROBIN` としてテーブルを作成し、それを列で分散されるテーブルに変更する必要がある場合、`CTAS` を使用して分散列を変更します。 また、`CTAS` を使用して、パーティション、インデックス、列の型を変更することができます。

たとえば、分散列が `CREATE TABLE` で指定されていないため、既定の分散種類である `ROUND_ROBIN` 分散を使用して、このテーブルを作成したとします。

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

ここで、クラスター化列ストア テーブルのパフォーマンスを利用できるように、クラスター化列ストア インデックスを持つこのテーブルの新しいコピーを作成する必要があります。 また、この列の結合を予測しており、ProductKey の結合時にデータが移動されないようにしたいため、ProductKey にこのテーブルを分散する必要があります。 最後に、古いパーティションを削除して古いデータをすばやく削除できるように、OrderDateKey にパーティションを追加する必要もあります。 新しいテーブルに古いテーブルをコピーする CTAS ステートメントを以下に示します。

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

最終的に、新しいテーブルの名前を変更して、新しいテーブルを置き換えてから古いテーブルを削除できます。

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>列のオプション例

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. CTAS を使用して列属性を変更する 
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse

この例では CTAS を使用して、DimCustomer2 テーブルのデータ型、NULL 値の許容、いくつかの列の照合順序を変更します。  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
最後の手順として、[RENAME &#40;Transact-SQL&#41;](../../t-sql/statements/rename-transact-sql.md) を使用して、テーブル名を切り替えることができます。 これにより、DimCustomer2 が新しいテーブルになります。

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>テーブルの分散例

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. CTAS を使用してテーブルの分散方法を変更する
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse

この簡単な例では、テーブルの分散方法を変更する方法を示します。 これを行う方法のしくみを表示するには、ハッシュ分散テーブルをラウンドロビンに変更してから、ラウンドロビン テーブルをハッシュ分散に戻します。 最終的なテーブルは元のテーブルと一致します。 

ほとんどの場合、ハッシュ分散テーブルをラウンドロビン テーブルに変更する必要はありません。 多くの場合、ラウンドロビン テーブルをハッシュ分散テーブルに変更する必要がある場合があります。 たとえば、最初にラウンド ロビンとして新しいテーブルを読み込み、後で、結合パフォーマンスを向上させるためにハッシュ分散テーブルに移行する場合があります。

この例では AdventureWorksDW サンプル データベースを使用します。 SQL Data Warehouse バージョンを読み込む場合は、[SQL Data Warehouse へのサンプル データの読み込み](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)に関するページを参照してください。
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
次に、ハッシュ分散テーブルに戻します。

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. CTAS を使用してテーブルをレプリケートされたテーブルに変換する  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse 

この例は、ラウンドロビン テーブルまたはハッシュ分散テーブルをレプリケートされたテーブルに変換する場合に適用されます。 この特定の例では、分散の種類を変更する前の方法を 1 歩進めた方法を使用します。  DimSalesTerritory はディメンションであり、より小さいテーブルである可能性があるため、テーブル間の結合時にデータが移動されないようにテーブルをレプリケート済みとして再作成することを選択できます。 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. CTAS を使用して列が少ないテーブルを作成する
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse 

次の例では、`myTable (c, ln)` という名前のラウンドロビン分散テーブル テーブルを作成します。 新しいテーブルには 2 つの列のみがあります。 列名には、SELECT ステートメントの列の別名を使用します。  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>クエリ ヒントの例

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. CREATE TABLE AS SELECT (CTAS) でクエリ ヒントを使用する  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse
  
このクエリは、CTAS ステートメントでクエリの結合ヒントを使用するための基本構文を示しています。 クエリが送信されると、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] では、分散ごとにクエリ プランを生成する際にハッシュ結合方法が適用されます。 ハッシュ結合のクエリ ヒントの詳細については、「[OPTION 句 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)」を参照してください。  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>外部テーブルの例

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. CTAS を使用して Azure BLOB ストレージからデータをインポートする  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse  

外部テーブルからデータをインポートするには、CREATE TABLE AS SELECT を使用して外部テーブルから選択するだけです。 外部テーブルからデータを選択して [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] に格納する構文は、通常のテーブルからデータを選択する構文と同じです。  
  
 次の例では、Azure BLOB ストレージ アカウントのデータに対して外部テーブルを定義します。 次に CREATE TABLE AS SELECT を使用して、外部テーブルから選択します。 これで、Azure BLOB ストレージのテキスト区切りファイルからデータがインポートされ、新しい [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] テーブルにデータが格納されます。  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. CTAS を使用して外部テーブルから Hadoop データをインポートする  
適用対象: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
外部テーブルからデータをインポートするには、CREATE TABLE AS SELECT を使用して外部テーブルから選択するだけです。 外部テーブルからデータを選択して [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] に格納する構文は、通常のテーブルからデータを選択する構文と同じです。  
  
 次の例では、Hadoop クラスターに外部テーブルを定義します。 次に CREATE TABLE AS SELECT を使用して、外部テーブルから選択します。 これで、Hadoop のテキスト区切りファイルからデータがインポートされ、新しい [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] テーブルにデータが格納されます。  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>CTAS を使用して SQL Server コードを置き換える例

CTAS を使用して、サポートされていない一部の機能に対処します。 データ ウェアハウスでコードを実行できるだけでなく、既存のコードを書き直して CTAS を使用することで、通常はパフォーマンスが向上します。 これは、完全に並列化された設計の結果です。 

> [!NOTE]
> "CTAS を第一" に考えてみてください。 `CTAS` を使用して問題を解決できると思われる場合、結果としてより多くのデータを書き込むことになる場合でも、一般的にはこれが最良の方法です。
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. SELECT..INTO の代わりに CTAS を使用する  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse

SQL Server コードでは通常、SELECT..INTO を使用して、テーブルに SELECT ステートメントの結果を設定します。 これは、SQL Server の SELECT..INTO ステートメントの例です。

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

この構文は SQL Data Warehouse と Parallel Data Warehouse ではサポートされていません。 この例では、以前の SELECT..INTO ステートメントを CTAS ステートメントとして書き直す方法を示します。 CTAS 構文に記述されている DISTRIBUTION オプションのいずれかを選択できます。 この例では、ROUND_ROBIN 分散方法を使用します。

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. CTAS と暗黙の結合を使用して、`UPDATE` ステートメントの `FROM` 句で ANSI 結合を置き換える  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse  

UPDATE または DELETE を実行するために ANSI 結合構文を使用して、3 つ以上のテーブルをまとめて結合する更新は複雑になることがあります。

たとえば、次のテーブルを更新する必要があるとします。

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

元のクエリは次のようになっている可能性があります。

```sql
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

SQL Data Warehouse では `UPDATE` ステートメントの `FROM` 句での ANSI 結合がサポートされていないため、この SQL Server コードを少し変更しないと使用できません。

`CTAS` と暗黙の結合を組み合わせて使用して、このコードを置き換えることができます。

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. CTAS を使用して、DELETE ステートメントの FROM 句で ANSI 結合を使用する代わりに保持するデータを指定する  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse  

データを削除するときに `CTAS` を使用するのが最良の方法である場合があります。 データを削除するのではなく、保持する必要があるデータを選択するだけです。 SQL Data Warehouse では `DELETE` ステートメントの `FROM` 句での ANSI 結合がサポートされていないため、これは特に、ansi 結合構文を使用する `DELETE` ステートメントの場合に当てはまります。

以下の変換された DELETE ステートメントの例を使用できます。

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. CTAS を使用して MERGE ステートメントを簡略化する  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse  

MERGE ステートメントの少なくとも一部は、`CTAS` を使用して置き換えることができます。 `INSERT` と `UPDATE` を単一のステートメントにまとめることができます。 削除されたレコードは、2 番目のステートメントで閉じる必要があります。

以下の `UPSERT` の例を使用できます。

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>M. 出力のデータ型と NULL 値の許容を明示的に指定する  
適用対象:Azure SQL Data Warehouse と Parallel Data Warehouse  

SQL Server コードを SQL Data Warehouse に移行したときに、次のようなコーディング パターンが発生する場合があります。

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

直感的に、このコードを CTAS に移行する必要があり、それが正しいと思うかもしれません。 ただし、ここには隠れた問題があります。

次のコードでは同じ結果が生成されません。

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

"結果" 列に、式のデータ型と NULL 値の許容値が引き継がれることに注目してください。 注意しないと、これで値が微妙に変化する可能性があります。

例として、以下を試してみてください。

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

結果の格納される値が異なります。 結果列に永続化された値が他の式で使用されているため、エラーがさらに重大になります。

![CREATE TABLE AS SELECT の結果](../../t-sql/statements/media/create-table-as-select-results.png)

これは、データの移行では特に重要です。 ほぼ間違いなく、2 番目のクエリがより正確であっても、問題があります。 ソース システムと比較して、データが異なり、このことが移行での整合性の問題につながります。 これは、"間違った" 答えが実際は正しいものである場合のまれなケースの 1 つです。

2 つの結果の間でこのような違いが見られる理由は、暗黙的な型キャストへの依存です。 最初の例では、テーブルで列定義が定義されます。 行が挿入されたときに、暗黙的な型変換が発生します。 2 番目の例では、式で列のデータ型が定義されるため、暗黙的な型変換は発生しません。 また、2 番目の例の列が NULL 許容列として定義されているのに対して、最初の例では定義されていないことに注目してください。 最初の例でテーブルが作成されたときに、列の NULL 値の許容は明示的に定義されました。 2 番目の例では、式にただ任せ、その結果、既定で NULL 定義となります。  

これらの問題を解決するには、`CTAS` ステートメントの `SELECT` 部分で型変換と NULL 値の許容を明示的に設定する必要があります。 CREATE TABLE 部分でこれらのプロパティを設定することはできません。

次の例ではコードを修正する方法を示します。

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

次のことを考慮してください。
- CAST または CONVERT を使用できた
- COALESCE ではなく NULL 値の許容を強制するために ISNULL が使用されている
- ISNULL は最も外側の関数である
- ISNULL の 2 番目の部分は定数 (つまり、0) である

> [!NOTE]
> NULL 値の許容を正しく設定するには、`COALESCE` ではなく、`ISNULL` を使用することが重要です。 `COALESCE` は決定的関数ではないため、式の結果は常に NULL 許容になります。 `ISNULL` は異なります。 これは決定的です。 そのため、`ISNULL` 関数の 2 番目の部分が定数またはリテラルである場合、結果の値は NOT NULL になります。

このヒントは、計算の整合性を確保するために役立つだけではありません。 テーブルのパーティション切り替えにも重要になります。 以下のテーブルがファクトとして定義されているとします。

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

ただし、値フィールドは、ソース データの一部ではない、計算された式です。

パーティション分割されたデータセットを作成するには、次のようにします。

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

クエリは適切に実行されます。 パーティション切り替えを実行しようとすると問題が発生します。 テーブルの定義は一致しません。 テーブルの定義を一致させるには、CTAS の変更が必要です。

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

したがって、型の一貫性と、CTAS で NULL 値の許容プロパティを維持することが適切なエンジニアリングのベスト プラクティスであることがわかります。 計算の整合性を維持するのに役立ち、また、確実にパーティションを切り替えることができます。

### <a name="n-create-an-ordered-clustered-columnstore-index-with-maxdop-1"></a>N. MAXDOP 1 で順序指定クラスター化列ストア インデックスを作成する  
```sql
CREATE TABLE Table1 WITH (DISTRIBUTION = HASH(c1), CLUSTERED COLUMNSTORE INDEX ORDER(c1) )
AS SELECT * FROM ExampleTable
OPTION (MAXDOP 1);
```

 
## <a name="see-also"></a>参照  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  


