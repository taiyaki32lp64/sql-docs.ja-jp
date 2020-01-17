---
title: 既定のスキーマを使用する OPENJSON の使用
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3e4aac74ac35fc5d75320b420e85b130be110340
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096035"
---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>既定のスキーマを使用する OPENJSON の使用 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  オブジェクトのプロパティごと、または配列内の要素ごとに 1 つの行が含まれたテーブルを返すには、既定のスキーマを使用して **OPENJSON** を使用します。  
  
 ここでは、既定のスキーマを使用して **OPENJSON** を使用する例をいくつか紹介します。 詳細とその他の例については、「 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)」を参照してください。  
  
## <a name="example---return-each-property-of-an-object"></a>例 - オブジェクトの各プロパティを返す  
 **クエリ**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **結果**  
  
|Key|[値]|  
|---------|-----------|  
|NAME|John|  
|姓|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>例 - 配列の各要素を返す  
 **クエリ**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **結果**  
  
|Key|[値]|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr という|  
  
## <a name="example---convert-json-to-a-temporary-table"></a>例 - JSON を一時テーブルに変換する  
 次のクエリのすべてのプロパティを返します、 **情報** オブジェクトです。  
  
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'

SELECT *
FROM OPENJSON(@json,N'lax $.info')
```  
  
 **[結果]**  
  
|Key|[値]|型|  
|---------|-----------|----------|  
|型|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|タグ|[「スポーツ」、「Water ポーロ」]|4|  
  
## <a name="example---combine-relational-data-and-json-data"></a>例 - リレーショナル データと JSON データを結合する  
 次の例では、JSON 形式で SalesOrderReasons の配列を含む SalesReason テキスト列が、SalesOrderHeader テーブルにあります。 SalesOrderReasons オブジェクトには、"製造元" と "品質" のようなプロパティが含まれます。 この例では、販売理由が別個の子テーブルに含まれているかのように販売理由の JSON 配列を展開して、すべての販売注文行を関連する販売理由に結合するレポートを作成します。  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
 この例では、OPENJSON から販売理由のテーブルが返されます。このテーブルでは、販売理由が値列として示されます。 CROSS APPLY 演算子は、OPENJSON テーブル値関数によって返される行に各販売注文の行を結合します。  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
