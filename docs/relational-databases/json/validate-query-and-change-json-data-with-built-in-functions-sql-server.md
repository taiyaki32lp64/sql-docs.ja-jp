---
title: 組み込み関数を使用した JSON データの検証、クエリ、変更
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ddc5fb198a62374fc43ebacb5fa7423ac9fadd5
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096066"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>組み込み関数を使用した JSON データの検証、クエリ、変更 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

JSON の組み込みのサポートには、次の組み込み関数が含まれています。このトピックでは、これらの関数について簡単に説明します。  
  
-   [ISJSON](#ISJSON) 。文字列に有効な JSON が含まれているかどうかをテストします。  
  
-   [JSON_VALUE](#VALUE) 。JSON 文字列からスカラー値を抽出します。  
  
-   [JSON_QUERY](#QUERY) 。JSON 文字列からオブジェクトまたは配列を抽出します。  
  
-   [JSON_MODIFY](#MODIFY) 。JSON 文字列内のプロパティの値を更新し、更新された JSON 文字列を返します。  
 
## <a name="json-text-for-the-examples-on-this-page"></a>このページの例の JSON テキスト

このページの例では、次の例に示す内容のような JSON テキストを使用します。

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller",
         "givenName": "Lisa",
         "gender": "female",
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

入れ子になった複雑な要素が含まれるこの JSON ドキュメントは、次のサンプル テーブルに格納されます。

```sql
CREATE TABLE Families (
   id int identity constraint PK_JSON_ID primary key,
   doc nvarchar(max)
)
``` 

##  <a name="ISJSON"></a> ISJSON 関数を使用して JSON テキストを検証する  
 **ISJSON** 関数は、文字列に有効な JSON が含まれているかどうかをテストします。  
  
次の例では、JSON 列に有効な JSON テキストが含まれる行が返されます。 明示的な JSON 制約がない場合、NVARCHAR 列には任意のテキストを入力できることに注意してください。  
  
```sql  
SELECT *
FROM Families
WHERE ISJSON(doc) > 0 
```  

詳細については、「 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)」を参照してください。  
  
##  <a name="VALUE"></a> JSON_VALUE 関数を使用して、JSON テキストから値を抽出する  
**JSON_VALUE** 関数は、JSON 文字列からスカラー値を抽出します。 次のクエリでは、`id` JSON フィールドが `AndersenFamily` の値と一致するドキュメントが、`city` および `state` JSON フィールドで並べ替えられて返されます。

```sql  
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       JSON_VALUE(f.doc, '$.address.county') AS County
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
ORDER BY JSON_VALUE(f.doc, '$.address.city') DESC, JSON_VALUE(f.doc, '$.address.state') ASC
```  

このクエリの結果は次の表のようになります。

| [オブジェクト名] | City | County |
| --- | --- | --- |
| AndersenFamily | NY | Manhattan |

詳細については、「 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)」をご覧ください。  
  
##  <a name="QUERY"></a> JSON_QUERY 関数を使用して JSON テキストからオブジェクトまたは配列を抽出する  

**JSON_QUERY** 関数は、JSON 文字列からオブジェクトまたは配列を抽出します。 次の例では、クエリの結果には JSON フラグメントを返す方法を示します。  
  
```sql
SELECT JSON_QUERY(f.doc, '$.address') AS Address,
       JSON_QUERY(f.doc, '$.parents') AS Parents,
       JSON_QUERY(f.doc, '$.parents[0]') AS Parent0
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
```  
このクエリの結果は次の表のようになります。

| Address | Parents | Parent0 |
| --- | --- | --- |
| { "state":"NY", "county":"Manhattan", "city":"NY" } | [{ "familyName":"Wakefield", "givenName":"Robin" }, {"familyName":"Miller", "givenName":"Ben" } ]| { "familyName":"Wakefield", "givenName":"Robin" } |

詳細については、「[JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)」を参照してください。  

## <a name="parse-nested-json-collections"></a>入れ子になった JSON コレクションを解析する

`OPENJSON` 関数を使用すると、JSON サブ配列を行セットに変換し、親要素と結合することができます。 たとえば、すべてのファミリ ドキュメントを返し、それらを内部 JSON 配列として格納されている `children` オブジェクトと "結合" することができます。

```sql
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       c.givenName, c.grade
FROM Families f
        CROSS APPLY OPENJSON(f.doc, '$.children')
            WITH(grade int, givenName nvarchar(100))  c
```

このクエリの結果は次の表のようになります。

| [オブジェクト名] | City | givenName | grade |
| --- | --- | --- | --- |
| AndersenFamily | NY | Jesse | 1 |
| AndersenFamily | NY | Lisa | 8 |

1 つの親行が、子サブ配列の 2 つの要素を解析することによって生成される 2 つの子行と結合されるため、結果として 2 つの行が取得されます。 `OPENJSON` 関数では、`doc` 列からの `children` フラグメントが解析されて、各要素の `grade` と `givenName` が行のセットとして返されます。 この行セットを親ドキュメントと結合できます。
 
## <a name="query-nested-hierarchical-json-sub-arrays"></a>入れ子になった階層的な JSON サブ配列のクエリを実行する

入れ子になった JSON 構造のクエリを実行するために、`CROSS APPLY OPENJSON` の複数の呼び出しを適用できます。 この例で使用される JSON ドキュメントには、`children` という名前の入れ子になった配列が含まれ、各子には `pets` の入れ子になった配列があります。 次のクエリでは、各ドキュメントの子が解析されて、各配列オブジェクトが行として返された後、`pets` 配列が解析されます。

```sql
SELECT  familyName,
    c.givenName AS childGivenName,
    c.firstName AS childFirstName,
    p.givenName AS petName 
FROM Families f 
    CROSS APPLY OPENJSON(f.doc) 
        WITH (familyName nvarchar(100), children nvarchar(max) AS JSON)
        CROSS APPLY OPENJSON(children) 
        WITH (givenName nvarchar(100), firstName nvarchar(100), pets nvarchar(max) AS JSON) as c
            OUTER APPLY OPENJSON (pets)
            WITH (givenName nvarchar(100))  as p
```

`OPENJSON` の最初の呼び出しでは、AS JSON 句を使用して `children` 配列のフラグメントが返されます。 この配列フラグメントは、`givenName`、各子の `firstName`、および `pets` の配列を返す、2 番目の `OPENJSON` 関数に提供されます。 `pets` の配列は、ペットの `givenName` を返す 3 番目の `OPENJSON` 関数に提供されます。
このクエリの結果は次の表のようになります。

| familyName | childGivenName | childFirstName | petName |
| --- | --- | --- | --- |
| AndersenFamily | Jesse | Merriam | Goofy |
| AndersenFamily | Jesse | Merriam | Shadow |
| AndersenFamily | Lisa | Miller| `NULL` |

ルート ドキュメントは、最初の `OPENJSON(children)` の呼び出しによって返される 2 つの `children` 行と結合されて、2 つの行 (またはタプル) が作成されます。 その後、各行は、`OUTER APPLY` 演算子を使用して `OPENJSON(pets)` によって生成される新しい行と結合されます。 Jesse にはペットが 2 匹いるため、`(AndersenFamily, Jesse, Merriam)` は Goofy および Shadow に対して生成される 2 つの行と結合されます。 Lisa にはペットがいないため、このタプルに対して `OPENJSON(pets)` によって返される行はありません。 ただし、`OUTER APPLY` を使用しているため、列には `NULL` が設定されます。 `OUTER APPLY` の代わりに `CROSS APPLY` を指定した場合、このタプルと結合できるペット行がないので、Lisa についての結果は返されません。

##  <a name="JSONCompare"></a> JSON_VALUE と JSON_QUERY を比較する  
**JSON_VALUE** と **JSON_QUERY** の主な違いは、 **JSON_VALUE** はスカラー値を返しますが、 **JSON_QUERY** はオブジェクトまたは配列を返す点です。  
  
次のようなサンプル JSON テキストがあるとします。  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
このサンプル JSON テキストでは、データ メンバー "a" と "c" は文字列値ですが、データ メンバー "b" は配列です。 **JSON_VALUE** と **JSON_QUERY** は、次の結果を返します。  
  
|[パス]|**JSON_VALUE** が返す結果|**JSON_QUERY** が返す結果|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL またはエラー|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL またはエラー|  
|**$.b**|NULL またはエラー|[1,2]|  
|**$.b[0]**|1|NULL またはエラー|  
|**$.c**|hi|NULL またはエラー|  
  
## <a name="test-json_value-and-json_query-with-the-adventureworks-sample-database"></a>AdventureWorks サンプル データベースを使用して JSON_VALUE と JSON_QUERY をテストする  
このトピックで説明した組み込み関数をテストするには、AdventureWorks サンプル データベースを使用して次の例を実行します。 AdventureWorks の入手先と、スクリプトを実行してテストするための JSON データの追加方法について詳しくは、「[組み込みの JSON サポートを試用する](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database)」をご覧ください。
  
次の例では、`SalesOrder_json` テーブルの `Info` 列に JSON テキストが含まれています。  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>例 1: 標準の列と JSON データの両方を返す  
次のクエリは、標準のリレーショナル列と JSON 列の両方から値を返します。  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>例 2: JSON 値の集計とフィルター  
次のクエリは、(JSON に格納されている) 顧客名と (通常の列に格納されている) 状態別に小計を集計します。 次に、(JSON に格納されている) 市区町村と (通常の列に格納されている) OrderDate で結果をフィルターします。  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> JSON_MODIFY 関数を使用して JSON テキストのプロパティ値を更新する  
**JSON_MODIFY** 関数は、JSON 文字列内のプロパティの値を更新し、更新された JSON 文字列を返します。  
  
次の例では、JSON を格納する変数の JSON プロパティの値を更新します。  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 詳細については、「 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)」を参照してください。  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
