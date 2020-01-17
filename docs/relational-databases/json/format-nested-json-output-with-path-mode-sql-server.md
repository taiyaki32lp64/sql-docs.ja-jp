---
title: PATH モードで入れ子になった JSON 出力を書式設定する
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 61c282e01a03a0b46de0c256025cb59c57304ddb
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245595"
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>PATH モードで入れ子になった JSON 出力を書式設定する (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**FOR JSON** 句の出力を完全に制御するには、**PATH** オプションを指定します。  
  
**PATH** モードでは、ラッパー オブジェクトを作成し、複雑なプロパティを入れ子にすることができます。 結果は JSON オブジェクトの配列として書式設定されます。  
  
または、**AUTO** オプションを使用して、**SELECT** ステートメントの構造に基づいて出力を自動的に書式設定する方法があります。
 -   **AUTO** オプションの詳細については、「[Format JSON Output Automatically with AUTO Mode](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)」 (AUTO モードで自動的に JSON 出力を書式設定する) を参照してください。
 -   両方のオプションの概要については、「[Format Query Results as JSON with FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)」 (FOR JSON を使用してクエリ結果を JSON として書式設定する) を参照してください。
 
以下に、 **FOR JSON** 句で **PATH** オプションを使用した例を示します。 次の例に示すように、ドット区切りの列名を使用するか、入れ子になったクエリを使用して、入れ子になった結果を書式設定します。 既定では、**FOR JSON** 出力に null 値は含まれません。  

## <a name="example---dot-separated-column-names"></a>例: ドット区切りの列名  
次のクエリは、AdventureWorks `Person` テーブルの最初の 5 行を JSON として書式設定します。  

**FOR JSON PATH** 句は、列の別名または列の名前を使用して JSON 出力のキー名を決定します。 別名にドットが含まれている場合、PATH オプションで入れ子になったオブジェクトが作成されます。  

 **クエリ**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH   
```  
  
 **結果**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>例 - 複数のテーブル  
クエリで複数のテーブルを参照すると、**FOR JSON PATH** でその別名を使用して各列が入れ子にされます。 次のクエリは、クエリで結合される (OrderHeader、OrderDetails) ペアごとに 1 つの JSON オブジェクトを作成します。 
  
 **クエリ**  
  
```sql  
SELECT TOP 2 H.SalesOrderNumber AS 'Order.Number',  
        H.OrderDate AS 'Order.Date',  
        D.UnitPrice AS 'Product.Price',  
        D.OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH   
```  
  
 **結果**  
  
```json  
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>参照  
 [FOR 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
