---
title: JSON データの使用
ms.date: 05/14/2019
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: quickstart
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 80f6d40fd2c548135595fd96de6de4b967460a90
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190359"
---
# <a name="json-data-in-sql-server"></a>SQL Server の JSON データ

[!INCLUDE[appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

JSON は、最新の Web アプリケーションとモバイル アプリケーションでデータを交換するために使用される、一般的なテキスト形式のデータ形式です。 また、JSON はログ ファイル内の非構造化データや Microsoft Azure Cosmos DB のような NoSQL データベースを格納するためも使用されます。 REST Web サービスの多くは結果を JSON テキスト形式で返し、データを JSON 形式で受け取ります。 たとえば、Azure Search、Azure Storage、Azure Cosmos DB などの Azure のほとんどのサービスには、JSON を返すか使用する REST エンドポイントがあります。 JSON は、AJAX 呼び出しを使用して Web ページおよび Web サーバー間でデータをやり取りするための主な形式でもあります。 

SQL Server で JSON 関数を使うと、NoSQL とリレーショナルの概念を同じデータベースに結合できます。 従来のリレーショナル列と JSON テキスト形式のドキュメントを含む列を同じテーブルに結合したり、JSON ドキュメントを解析してリレーショナル構造にインポートしたり、リレーショナル データを JSON テキストに書式設定したりできます。 SQL Server と Azure SQL Database で JSON 関数がリレーショナルの概念と NoSQL の概念を結び付けるしくみについては、次のビデオをご覧ください。

*NoSQL とリレーショナル環境間の架け橋としての JSON*
> [!VIDEO https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds/player]

JSON テキストの例を次に示します。

```json
[
  {
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
  },
  {
    "name": "Jane",
    "surname": "Doe"
  }
]
```

SQL Server の組み込みの関数と演算子を使用すると、JSON テキストで次の操作を実行できます。

- JSON テキストを解析し、値を読み取るか、変更する。  
- JSON オブジェクトの配列を表形式に変換する。  
- 変換された JSON オブジェクトに対して任意の Transact-SQL クエリを実行する。  
- Transact-SQL クエリの結果を JSON 形式で書式設定する。  
  
![組み込みの JSON サポートの概要](../../relational-databases/json/media/jsonslides1overview.png "組み込みの JSON サポートの概要")  
  
## <a name="key-json-capabilities-of-sql-server-and-sql-database"></a>SQL Server と SQL Database の主な JSON 機能

SQL Server がその組み込みの JSON サポートで提供する主な機能について以下に説明します。 JSON 関数と演算子の使い方については、次のビデオをご覧ください。

*SQL Server 2016 と JSON のサポート*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support/player?WT.mc_id=dataexposed-c9-niner]

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>JSON テキストから値を抽出し、それらをクエリで使用する

データベース テーブルに格納されている JSON テキストがある場合は、組み込み関数を使用して JSON テキスト内の値を読み取るか、変更することができます。  

- [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md) は、文字列に有効な JSON が含まれているかどうかをテストします。
- [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md) は、JSON 文字列からスカラー値を抽出します。
- [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md) は、JSON 文字列からオブジェクトまたは配列を抽出します。
- [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) は、JSON 文字列の値を変更します。

**例**

次の例のクエリでは、テーブルからリレーショナル データと (`jsonCol` という名前の列に格納された) JSON データの両方を使用しています。  
  
```sql  
SELECT Name, Surname,
  JSON_VALUE(jsonCol, '$.info.address.PostCode') AS PostCode,
  JSON_VALUE(jsonCol, '$.info.address."Address Line 1"') + ' '
  + JSON_VALUE(jsonCol, '$.info.address."Address Line 2"') AS Address,
  JSON_QUERY(jsonCol, '$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol) > 0
  AND JSON_VALUE(jsonCol, '$.info.address.Town') = 'Belgrade'
  AND Status = 'Active'
ORDER BY JSON_VALUE(jsonCol, '$.info.address.PostCode')
```  
  
アプリケーションやツールでは、スカラー テーブル列から取得した値であるか、JSON 列から取得した値であるかの見分けは付きません。 JSON テキストからの値は、Transact-SQL クエリのすべての部分で使用できます (例: WHERE 句、ORDER BY 句、または GROUP BY 句、ウィンドウの集計など)。 JSON 関数は、JavaScript のような構文を使用して JSON テキスト内の値を参照します。

詳細については、「[組み込み関数を使用した JSON データの検証、クエリ、変更 (SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)」、「[JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)」、「[JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)」を参照してください。  
  
### <a name="change-json-values"></a>JSON 値の変更

JSON テキストの一部を修正する必要がある場合は、[JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) 関数を使用して JSON 文字列のプロパティの値を更新し、更新された JSON 文字列を返します。 次の例では、JSON を格納する変数のプロパティの値を更新します。  
  
```sql
DECLARE @json NVARCHAR(MAX);
SET @json = '{"info": {"address": [{"town": "Belgrade"}, {"town": "Paris"}, {"town":"Madrid"}]}}';
SET @json = JSON_MODIFY(@json, '$.info.address[1].town', 'London');
SELECT modifiedJson = @json;
```

**結果**

|modifiedJson|  
|--------|  
|{"info":{"address":[{"town":"Belgrade"},{"town":"London"},{"town":"Madrid"}]}|  
  
### <a name="convert-json-collections-to-a-rowset"></a>JSON コレクションを行セットに変換する

SQL Server で JSON のクエリを実行するのにカスタム クエリ言語は不要です。 JSON データのクエリを実行するには、標準の T-SQL を使用することができます。 JSON データのクエリまたはレポートを作成する必要がある場合は、**OPENJSON** 行セット関数を呼び出して JSON データを簡単に行と列に変換できます。 詳細については、[OPENJSON を使用して JSON データを行と列に変換する方法 (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) に関するページを参照してください。  
  
次の例では、**OPENJSON** を呼び出し、`@json` 変数に格納されたオブジェクトの配列を、標準の SQL **SELECT** ステートメントを使用してクエリを実行できる行セットに変換します。  
  
```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = N'[
  {"id": 2, "info": {"name": "John", "surname": "Smith"}, "age": 25},
  {"id": 5, "info": {"name": "Jane", "surname": "Smith"}, "dob": "2005-11-04T12:00:00"}
]';

SELECT *
FROM OPENJSON(@json)
  WITH (
    id INT 'strict $.id',
    firstName NVARCHAR(50) '$.info.name',
    lastName NVARCHAR(50) '$.info.surname',
    age INT,
    dateOfBirth DATETIME2 '$.dob'
  );
```

**結果**

|id|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
**OPENJSON** では、JSON オブジェクトの配列がテーブルに変換され、各オブジェクトが 1 つの行として表わされ、キーと値のペアがセルとして返されます。 出力は、次の規則を監視します。

- **OPENJSON** は JSON 値を **WITH** 句で指定された型に変換します。
- **OPENJSON** は、フラットなキーと値のペアと、入れ子になった階層構造のオブジェクトの両方を処理できます。
- JSON テキストに含まれるすべてのフィールドを返す必要はありません。
- JSON 値が存在しない場合、**OPENJSON** は NULL 値を返します。
- オプションで型指定の後にパスを指定して、入れ子にされたプロパティを参照するか、異なる名前のプロパティを参照できます。
- パス内の省略可能な **strict** プレフィックスでは、指定されたプロパティの値が JSON テキストに存在していなければならないことを指定します。

詳細については、[OPENJSON を使用して JSON データを行と列に変換する方法 (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) に関するページと「[OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)」を参照してください。  

JSON ドキュメントには、サブ要素と、標準のリレーショナル列に直接マップできないデータ階層があります。 ここでは、親エンティティとサブ配列を結合することで JSON 階層をフラット化することができます。

次の例では、配列内の 2 番目のオブジェクトは、個人のスキルを表すサブ配列を持っています。 追加の `OPENJSON` 関数呼び出しを使用してすべてのサブオブジェクトを解析できます。

```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = N'[  
  {"id": 2, "info": {"name": "John", "surname": "Smith"}, "age": 25},
  {"id": 5, "info": {"name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"]}, "dob": "2005-11-04T12:00:00"}  
]';

SELECT *  
FROM OPENJSON(@json)  
  WITH (
    id INT 'strict $.id',
    firstName NVARCHAR(50) '$.info.name',
    lastName NVARCHAR(50) '$.info.surname',  
    age INT,
    dateOfBirth DATETIME2 '$.dob',
    skills NVARCHAR(MAX) '$.info.skills' AS JSON
  )
OUTER APPLY OPENJSON(skills)
  WITH (skill NVARCHAR(8) '$');
```

**skills** 配列は、最初の `OPENJSON` で元の JSON テキスト フラグメントとして返され、`APPLY` 演算子を使用して別の `OPENJSON` 関数に渡されます。 2 番目の `OPENJSON` 関数は、JSON 配列を解析し、最初の `OPENJSON` の結果と結合される 1 つの列の行セットとして文字列値を返します。
このクエリの結果は、次の表のようになります。

**結果**

|id|firstName|lastName|age|dateOfBirth|skill|  
|--------|---------------|--------------|---------|-----------------|----------|  
|2|John|Smith|25|||  
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` は、最初のレベルのエンティティをサブ配列と結合し、フラット化された結果セットを返します。 結合により、すべてのスキルで 2 番目の行が繰り返されます。

### <a name="convert-sql-server-data-to-json-or-export-json"></a>SQL Server のデータを JSON に変換または JSON をエクスポートする

>[!NOTE]
>Azure SQL Data Warehouse データの JSON への変換や、JSON のエクスポートは、サポートされていません。

**FOR JSON** 句を **SELECT** ステートメントに追加して、SQL Server データまたは SQL クエリの結果を JSON として書式設定します。 **FOR JSON** を使用して、JSON 出力の形式設定をクライアント アプリケーションから SQL Server に委任します。 詳細については、「[FOR JSON を使用してクエリ結果を JSON として書式設定する (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)」を参照してください。  
  
次の例では、PATH モードを **FOR JSON** 句とともに使用しています。  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth AS dob
FROM People
FOR JSON PATH;
```

[曜日] **FOR JSON** 句は SQL 結果を JSON テキスト形式に設定し、JSON を理解するすべてのアプリケーションで使用できます。 PATH オプションでは、SELECT 句にドット区切りのエイリアスを使用して、クエリ結果内のオブジェクトを入れ子にします。  
  
**結果**

```json  
[
  {
    "id": 2,
    "info": {
      "name": "John",
      "surname": "Smith"
    },
    "age": 25
  },
  {
    "id": 5,
    "info": {
      "name": "Jane",
      "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
  }
]
```  
  
詳細については、「[FOR JSON を使用してクエリ結果を JSON として書式設定する (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)」と「[FOR 句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)」を参照してください。  

## <a name="use-cases-for-json-data-in-sql-server"></a>SQL Server での JSON データのユース ケース

SQL Server と Azure SQL Database での JSON のサポートにより、リレーショナルと NoSQL の概念が統合されます。 リレーショナルから半構造化データへの変換、およびその逆が簡単にできます。 しかし、JSON は既存のリレーショナル モデルに置き換わるものではありません。 ここでは、SQL Server と SQL Database での JSON サポートによる利点が得られるユース ケースをいくつか紹介します。

### <a name="simplify-complex-data-models"></a>複雑なデータ モデルを簡略化する

複数の子テーブルの代わりに JSON フィールドでデータ モデルを非正規化することを検討してください。

### <a name="store-retail-and-e-commerce-data"></a>小売および e コマースのデータを格納する

柔軟性のために非正規化されたモデルにさまざまな変数属性による製品情報を格納します。

### <a name="process-log-and-telemetry-data"></a>ログとテレメトリ データの処理

Transact-SQL 言語を活用して JSON ファイルとして格納されたログ データの読み込み、クエリ、分析を行います。

### <a name="store-semi-structured-iot-data"></a>半構造化された IoT データを格納する

IoT データのリアルタイム分析が必要なときは、受信データをストレージの場所にステージングせずに、データベースに直接読み込みます。

### <a name="simplify-rest-api-development"></a>REST API の開発を簡略化する

データベースのリレーショナル データを、Web サイトをサポートする REST API で使用される JSON 形式に簡単に変換します。

## <a name="combine-relational-and-json-data"></a>リレーショナル データと JSON データを結合する

SQL Server は、標準の Transact-SQL 言語を使用してリレーショナル データと JSON データの両方を格納および処理するハイブリッド モデルを提供します。 テーブル内の JSON ドキュメントのコレクションを整理し、それらの間のリレーションシップを確立、テーブルに格納された厳密に型指定されたスカラー列を JSON 列に格納された柔軟なキーと値のペアに結合し、完全な Transact-SQL を使用して 1 つ以上のテーブルのスカラー値と JSON 値の両方についてクエリを実行します。

JSON テキストは `VARCHAR` または `NVARCHAR` 列に格納され、プレーン テキストとしてインデックスが付けられます。 テキストをサポートするすべての SQL Server の機能またはコンポーネントは JSON をサポートします。そのため、JSON とその他の SQL Server 機能間の対話には、ほとんど制約がありません。 JSON はメモリ内テーブルやテンポラル テーブルに格納できるほか、行レベルのセキュリティの述語を JSON テキストに適用することなどができます。

純粋な JSON ワークロードがあり、JSON ドキュメントの処理のためにカスタマイズされたクエリ言語を使用する場合は、Microsoft Azure [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) の使用をお勧めします。  
  
ここでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で組み込みの JSON サポートの使用方法を示すユース ケースを紹介します。  

## <a name="store-and-index-json-data-in-sql-server"></a>JSON データの SQL Server への格納とインデックスの追加

JSON はテキスト形式なので、SQL Database の `NVARCHAR` 列に JSON ドキュメントを格納できます。 `NVARCHAR` 型は、すべての SQL Server サブシステムでサポートされているので、**CLUSTERED COLUMNSTORE** インデックスが付いたテーブル、**メモリ最適化**テーブル、または OPENROWSET または PolyBase を使用して読み取ることができる外部ファイルに JSON ドキュメントを格納することができます。

JSON データの SQL Server への保存、インデックスの追加、最適化のオプションに関する詳細については、次の記事を参照してください。

- [SQL Server または SQL Database に JSON ドキュメントを格納する](store-json-documents-in-sql-tables.md)
- [JSON データへのインデックスの追加](index-json-data.md)
- [インメモリ OLTP を使用した JSON の処理の最適化](optimize-json-processing-with-in-memory-oltp.md)

### <a name="load-json-files-into-sql-server"></a>SQL Server に JSON ファイルを読み込む  

ファイルに格納された情報は、標準の JSON または行区切りの JSON 形式に書式設定できます。 SQL Server は JSON ファイルのコンテンツをインポートし、**OPENJSON** または **JSON_VALUE** 関数を使用してそれを解析してテーブルに読み込むことができます。  
  
-   JSON ドキュメントが SQL Server がアクセスできるローカル ファイル、共有ネットワーク ドライブ、Azure File の場所に格納されている場合は、一括インポートを使用して SQL Server に JSON データを読み込むことができます。
  
-   行区切りの JSON ファイルが Azure Blob Storage または Hadoop ファイル システムに格納されている場合、PolyBase を使用して JSON テキストを読み込み、Transact-SQL コードでそれを解析してテーブルに読み込むことができます。  

### <a name="import-json-data-into-sql-server-tables"></a>SQL Server に JSON データをインポートする

JSON データを外部サービスから SQL Server に読み込む必要がある場合は、アプリケーション レイヤー内でデータを解析する代わりに、**OPENJSON** を使用してデータを SQL Server にインポートできます。  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX);

SET @jsonVariable = N'[
  {
    "Order": {  
      "Number":"SO43659",  
      "Date":"2011-05-31T00:00:00"  
    },  
    "AccountNumber":"AW29825",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":1  
    }  
  },  
  {  
    "Order": {  
      "Number":"SO43661",  
      "Date":"2011-06-01T00:00:00"  
    },  
    "AccountNumber":"AW73565",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":3  
    }  
  }
]';

-- INSERT INTO <sampleTable>  
SELECT SalesOrderJsonData.*
FROM OPENJSON (@jsonVariable, N'$')
  WITH (
    Number VARCHAR(200) N'$.Order.Number',
    Date DATETIME N'$.Order.Date',
    Customer VARCHAR(200) N'$.AccountNumber',
    Quantity INT N'$.Item.Quantity'
  ) AS SalesOrderJsonData;
```

JSON 変数の内容は、外部 REST サービスによって提供されたり、クライアント側 JavaScript フレームワークからのパラメーターとして送信されたり、外部ファイルから読み込まれたりします。 結果は、JSON テキストから SQL Server テーブルに簡単に挿入、更新、マージできます。

## <a name="analyze-json-data-with-sql-queries"></a>SQL クエリで JSON データを分析する

レポート作成のために JSON データをフィルター処理または集計する必要がある場合は、**OPENJSON** を使用して JSON をリレーショナル形式に変換できます。 その後、標準の [!INCLUDE[tsql](../../includes/tsql-md.md)] と組み込み関数を使用してレポートを用意することができます。  
  
```sql
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM SalesOrderRecord AS Tab
CROSS APPLY OPENJSON (Tab.json, N'$.Orders.OrdersArray')
  WITH (
    Number VARCHAR(200) N'$.Order.Number',
    Date DATETIME N'$.Order.Date',
    Customer VARCHAR(200) N'$.AccountNumber',
    Quantity INT N'$.Item.Quantity'
  ) AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified;
```  
  
同じクエリに標準テーブルの列と JSON テキストからの値の両方を使用できます。 `JSON_VALUE(Tab.json, '$.Status')` 式にインデックスを追加して、クエリのパフォーマンスを向上させることができます。 詳細については、「[JSON データへのインデックスの追加](../../relational-databases/json/index-json-data.md)」を参照してください。

## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>JSON として書式設定された SQL Server テーブルからデータを返す

データベース層からデータを取得し、それを JSON 形式で返す Web サービスがある場合、または JSON 形式に設定されたデータを受け取る JavaScript フレームワークまたはライブラリがある場合、JSON 出力を SQL クエリで直接設定できます。 コードを記述するかライブラリを追加して、表形式のクエリ結果を変換し、それからオブジェクトを JSON 形式にシリアル化する代わりに、**FOR JSON** を使用して JSON 形式への設定を SQL Server に委任できます。  
  
たとえば、OData の仕様に準拠した JSON 出力を生成するとします。 Web サービスは、次の形式の要求と応答を求めています。 
  
- 要求: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  

- 応答: `{"@odata.context": "https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity", "ProductID": 1, "ProductName": "Chai"}`  
  
この OData URL は、`ID` が 1 の製品の ProductID 列と ProductName 列に対する要求を表します。 **FOR JSON** を使用して、出力を SQL Server で求められている形式に設定できます。  
  
```sql  
SELECT 'https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity' AS '@odata.context',
  ProductID,
  Name as ProductName
FROM Production.Product
WHERE ProductID = 1
FOR JSON AUTO;
```  
  
このクエリの出力は、OData 仕様に完全に準拠した JSON テキストになります。形式設定とエスケープは、SQL Server によって処理されます。 SQL Server ではクエリ結果を OData JSON や GeoJSON など、任意の形式に設定することもできます。  
  
## <a name="test-drive-built-in-json-support-with-the-adventureworks-sample-database"></a>AdventureWorks サンプル データベースを使用して、組み込みの JSON サポートを試用できます。

AdventureWorks サンプル データベースを入手するには、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=49502)から最小限のデータベース ファイルとサンプルおよびスクリプト ファイルをダウンロードしてください。

SQL Server 2016 のインスタンスにサンプル データベースを復元したら、サンプル ファイルを展開し、JSON フォルダーから *JSON Sample Queries procedures views and indexes.sql* ファイルを開きます。 このファイルのスクリプトを実行して JSON データとして既存のデータの一部の形式を再度設定し、JSON データに対してサンプル クエリとレポートをテストしてから、JSON データにインデックスを付けて JSON をインポートおよびエクスポートします。  
  
ファイルに含まれているスクリプトでは、次のことを実行できます。  
  
- 既存のスキーマを非正規化して JSON データの列を作成する。

  - SalesReasons、SalesOrderDetails、SalesPerson、Customer、およびその他の販売注文に関する情報を含むテーブルからの情報を、SalesOrder_json テーブルの JSON 列に格納します。  
  
  - EmailAddresses/PersonPhone テーブルからの情報を、Person_json に JSON オブジェクトの配列として格納します。  
  
- JSON データに対してクエリを実行するプロシージャとビューを作成する。  
  
- JSON データにインデックスを追加する。 JSON のプロパティとフルテキスト インデックスにインデックスを作成する。  
  
- JSON をインポートおよびエクスポートする。 Person テーブルと SalesOrder テーブルのコンテンツを JSON の結果としてエクスポートする、および JSON 入力をインポートして Person テーブルと SalesOrder テーブルを更新するプロシージャを作成して実行します。  
  
- サンプル クエリを実行する。 手順 2 と 4 で作成したストアド プロシージャとビューを呼び出すいくつかのクエリを実行します。  
  
- スクリプトをクリーンアップする。 手順 2 と 4 で作成したストアド プロシージャとビューを保持する場合は、この部分を実行しないでください。  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの概要は、次のビデオをご覧ください。

*SQL Server 2016 と Azure SQL Database での JSON の使用*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database/player?WT.mc_id=dataexposed-c9-niner]

*JSON 関数を使用した SQL Server での REST API の作成*
> [!VIDEO https://www.youtube.com/embed/0m6GXF3-5WI]

### <a name="reference-articles"></a>関連記事

- [FOR 句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
- [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
- [JSON 関数 (Transact-SQL)](../../t-sql/functions/json-functions-transact-sql.md)  
  - [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)  
  - [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)  
  - [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
  - [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)  
