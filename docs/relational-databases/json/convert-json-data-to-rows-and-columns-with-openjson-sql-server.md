---
title: OPENJSON で JSON データを解析し、変換する
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: feac4a3e00164837373f9b3024c322dbf7c49818
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095823"
---
# <a name="parse-and-transform-json-data-with-openjson-sql-server"></a>OPENJSON を使用して JSON データを解析して変換する (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

**OPENJSON** 行セット関数は、JSON テキストを行と列のセットに変換します。 **OPENJSON** を使用して JSON コレクションを行セットに変換したら、返されたデータで SQL クエリを実行したり、行セットをテーブルに挿入したりできます。 
  
**OPENJSON** 関数は、1 つまたは集合の JSON オブジェクトを受け取り、1 つまたは複数の行に変換します。 既定では、**OPENJSON** 関数からは、次のデータが返されます。
-   JSON オブジェクトからは、最初のレベルで検出されたすべてのキーと値のペアを返します。
-   JSON 配列からは、配列のすべての要素とそれらのインデックスを返します。  

オプションの **WITH** 句を追加して、出力の構造を明示的に定義するスキーマを指定できます。  
  
## <a name="option-1---openjson-with-the-default-output"></a>オプション 1 - 既定の出力を使用する OPENJSON
結果の明示的なスキーマ (つまり **OPENJSON** の後の **WITH** 句) を指定せずに **OPENJSON** 関数を使用すると、関数は、次の 3 つの列を含むテーブルを返します。
1.  入力オブジェクトのプロパティの**名前** (または入力配列の要素のインデックス)。
2.  プロパティまたは配列要素の**値**。
3.  **型** (たとえば、文字列、数値、ブール値、配列、オブジェクト)。

**OPENJSON** は、JSON オブジェクトの各プロパティ、または配列の各要素を、個別の行として返します。  

これは、既定のスキーマ (つまり、オプションの **WITH** 句を指定しない) で **OPENJSON** を使用した簡単な例です。この例では JSON オブジェクトのプロパティごとに 1 つの行が返されています。  

**例**

```sql
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**結果**
  
|キー (key)|value|型|  
|---------|-----------|----------|  
|NAME|John|1|  
|姓|Doe|1|  
|有効期間|45|2|  
|スキル|["SQL","C#","MVC"]|4|

### <a name="more-info-about-openjson-with-the-default-schema"></a>既定のスキーマを使用する OPENJSON に関する詳細情報

詳細と例については、「[既定のスキーマを使用する OPENJSON の使用 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)」を参照してください。

構文と使用法については、「 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)でのみ使用できます。 

## <a name="option-2---openjson-output-with-an-explicit-structure"></a>オプション 2 - 明示的な構造を指定した OPENJSON 出力

**OPENJSON** 関数の **WITH** 句を使用して結果のスキーマを指定すると、**WITH** 句に定義した列のみを持つテーブルが返されます。 オプションの **WITH** 句では、いくつかの出力列、各列の型、各出力値の JSON ソース プロパティのパスを指定します。 **OPENJSON** は JSON オブジェクトの配列を繰り返し処理し、列ごとに指定されたパスで値を読み取り、値を指定の型に変換します。  

**WITH** 句で出力のスキーマを明示的に指定して **OPENJSON** を使用する簡単な例は次のようになります。  
  
**例**
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =   
  N'[  
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
 ]'  
   
SELECT * FROM  
 OPENJSON ( @json )  
WITH (   
              Number   varchar(200) '$.Order.Number' ,  
              Date     datetime     '$.Order.Date',  
              Customer varchar(200) '$.AccountNumber',  
              Quantity int          '$.Item.Quantity'  
 ) 
```  
  
**結果**
  
|数値|date|Customer|Quantity|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-により、|AW29825|1|  
|として SO43661|2011-06-01T00:00:00|AW73565|3|  
  
この関数は JSON 配列の要素を返し、書式設定します。  
  
-   JSON 配列の要素ごとに、 **OPENJSON** によって出力テーブルに新しい行が生成されます。 JSON 配列の 2 つの要素が、返されるテーブルで、2 つの行に変換されます。  
  
-   `colName type json_path` 構文を使用して指定された列ごとに、**OPENJSON** 関数は、指定したパスの配列要素で検出された値を指定の型に変換します。 この例では、`Date` 列の値がパス `$.Order.Date` の各要素から取得され、datetime 値に変換されます。  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>明示的なスキーマを指定した OPENJSON に関する詳細情報

詳細と例については、「[明示的なスキーマで OPENJSON を使用する &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)」を参照してください。

構文と使用法については、「 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)でのみ使用できます。

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON には、互換性レベル 130 が必要

**OPENJSON** 関数は、 **互換性レベル 130**でのみ使用できます。 データベースの互換性レベルが 130 よりも低い場合、SQL Server は **OPENJSON** 関数を見つけて実行することができません。 他の組込み JSON 関数は、すべての互換性レベルで使用できます。

`sys.databases` ビューまたはデータベース プロパティで互換性レベルを確認できます。

次のコマンドを利用し、データベースの互換性レベルを変更できます。   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

- [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

- [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

- [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  