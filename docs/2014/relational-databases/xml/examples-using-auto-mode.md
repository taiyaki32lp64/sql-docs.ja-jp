---
title: '例 : AUTO モードの使用 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93a26764a7111a01b07d23c61bfbfb5c4a728e72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287807"
---
# <a name="examples-using-auto-mode"></a>例 :AUTO モードの使用
  次の例では、AUTO モードの使用方法を示します。 クエリの多くは、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースの ProductModel テーブルの Instructions 列に格納されている、自転車の製造手順の XML ドキュメントに対して指定されています。  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>例: 顧客情報、注文情報、および注文明細情報の取得  
 このクエリでは、特定の顧客の顧客情報、注文情報、および注文明細情報を取得しています。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 クエリでは `Cust`テーブル、 `OrderHeader`テーブル、 `Detail`テーブル、および `Product` テーブルの別名が識別されるので、 `AUTO` モードにより対応する要素が生成されます。 さらに、 `SELECT` 句で指定した列でテーブルが識別される順序に基づいて、これらの要素の階層が決定されます。  
  
 次に結果の一部を示します。  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>例: GROUP BY と集計関数の指定  
 次のクエリにより、各顧客の ID と顧客が要求した注文数が返されます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>例: AUTO モードでの計算列の指定  
 このクエリでは、各顧客の連結された名前と注文情報が返されます。 計算列はその時点で見つかった最も内側のレベルに割り当てられるので、この例では <`SOH`> 要素に割り当てられます。 連結された顧客名は、<`SOH`> 要素の属性として結果に追加されます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 結果の一部を次に示します。  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 サブ要素としてそれぞれの販売注文ヘッダー情報を含む `Name` 属性を持つ <`IndividualCustomer`> 要素を取得するには、サブ選択を使用してクエリを書き直します。 内部選択により、`IndividualCustomer` 一時テーブルが作成されます。このテーブルには、各顧客の名前を含む計算列があります。 次に、このテーブルを `SalesOrderHeader` テーブルに結合して、結果を取得します。  
  
 `Sales.Customer` テーブルには、顧客の `PersonID` 値など、各顧客の情報が格納されていることに注意してください。 次に、 `PersonID` を使用して `Person.Person` テーブルから連絡担当者名を見つけます。  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 結果の一部を次に示します。  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>例: バイナリ データを返す  
 次のクエリでは、 `ProductPhoto` テーブルから製品の写真が返されます。 `ThumbNailPhoto` は、`ProductPhoto` テーブルの `varbinary(max)` 列です。 既定では、 `AUTO` モードにより、バイナリ データへの参照、つまりクエリが実行されるデータベースの仮想ルートからの相対 URL が返されます。 画像を識別するには、 `ProductPhotoID` キー属性を指定する必要があります。 この例で示すように、画像の参照を取得する場合、 `SELECT` 句でテーブルの主キーを指定して行を一意に識別する必要もあります。  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 結果を次に示します。  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 `BINARY BASE64` オプションを使用して、同じクエリを実行します。 このクエリでは、バイナリ データが base64 エンコード形式で返されます。  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 結果を次に示します。  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 既定では、AUTO モードを使用してバイナリ データを取得すると、バイナリ データではなく、クエリが実行されたデータベースの仮想ルートからの相対 URL への参照が返されます。 BINARY BASE64 オプションを指定しないと、相対 URL への参照が返されます。  
  
 大文字と小文字が区別されないデータベースでは、クエリで指定したテーブル名や列名がデータベース内のテーブル名や列名と一致しない場合でも、AUTO モードによりバイナリ データへの URL 参照が返されると、クエリが実行されます。 ただし、参照として返される文字列が大文字であるか小文字であるかは一貫性がありません。 例 :  
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 結果を次に示します。  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 このことは、特に、大文字と小文字が区別されるデータベースに対して dbobject クエリが実行されるときに問題になる可能性があります。 この問題を回避するには、クエリで指定するテーブル名や列名での大文字と小文字の区別の方法が、データベース内のテーブル名や列名での大文字と小文字の区別の方法と一致している必要があります。  
  
## <a name="example-understanding-the-encoding"></a>例: エンコードについて  
 この例では、結果に表示されるさまざまなエンコードを示します。  
  
 次のテーブルを作成します。  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 テーブルに次のデータを追加します。  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 次のクエリを実行すると、テーブルのデータが返されます。 このクエリでは、FOR XML AUTO モードを指定しています。 このため、バイナリ データは参照として返されます。  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 結果を次に示します。  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 次に、結果の特殊文字がエンコードされる処理を示します。  
  
-   クエリ結果で、返された要素名と属性名に特殊な XML 文字や URL 文字が含まれている場合、それらの文字は対応する Unicode 文字の 16 進数値を使用してエンコードされます。 上記の結果では、要素名 <`Special Chars`> が <`Special_x0020_Chars`> として返されています。 属性名 <`Col#&2`> は <`Col_x0023__x0026_2`> として返されています。 XML と URL の両方の特殊文字がエンコードされます。  
  
-   要素や属性の値に 5 つの標準 XML 文字エンティティ ('、""、\<、>、および &) のいずれかが含まれている場合、これらの特殊な XML 文字は必ず XML 文字エンコードを使用してエンコードされます。 上記の結果では、属性 <`Col1`> の値の `&` という値は `&` とエンコードされています。 ただし、# 文字は特殊な XML 文字ではなく有効な XML 文字なので、# のままです。  
  
-   要素や属性の値に URL で特別な意味を持つ任意の特殊な URL 文字が含まれている場合、それらの文字は、DBOBJECT URL 値であるとき、および特殊文字がテーブル名や列名の一部であるときにのみエンコードされます。 この結果、テーブル名 `#` の一部である文字 `Col#&2` は、 `_x0023_ in the DBOJBECT URL`としてエンコードされます。  
  
## <a name="see-also"></a>参照  
 [FOR XML での AUTO モードの使用](use-auto-mode-with-for-xml.md)  
  
  
