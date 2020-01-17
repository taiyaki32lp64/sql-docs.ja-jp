---
title: 入れ子になった FOR XML クエリを使用した XML の構造化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], nested FOR XML
- XML [SQL Server], FOR XML queries
ms.assetid: 8dc42c05-16e8-4b7b-a5d3-550b55acae26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0a5fded413944c304dfe02675b3577b699adfc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231234"
---
# <a name="shape-xml-with-nested-for-xml-queries"></a>入れ子になった FOR XML クエリを使用した XML の構造化
  次の例では、`Production.Product` テーブルにクエリを実行し、特定の製品の `ListPrice` 値と `StandardCost` 値を取得します。 ここでは、例示を目的として、両方の価格を <`Price`> 要素に返します。各 <`Price`> 要素には、`PriceType` 属性があります。  
  
## <a name="example"></a>例  
 次に、想定する XML の構造を示します。  
  
```  
<xsd:schema xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet2" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet2" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.Product" type="xsd:anyType" />  
</xsd:schema>  
<Production.Product xmlns="urn:schemas-microsoft-com:sql:SqlRowSet2" ProductID="520">  
  <Price xmlns="" PriceType="ListPrice">133.34</Price>  
  <Price xmlns="" PriceType="StandardCost">98.77</Price>  
</Production.Product>  
```  
  
 次に、入れ子になった FOR XML クエリを示します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Product.ProductID,   
          (SELECT 'ListPrice' as PriceType,   
                   CAST(CAST(ListPrice as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE),  
          (SELECT  'StandardCost' as PriceType,   
                   CAST(CAST(StandardCost as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE)  
FROM Production.Product  
WHERE ProductID=520  
for XML AUTO, TYPE, XMLSCHEMA  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   外側の SELECT ステートメントで <`Product`> 要素が構築されます。この要素には **ProductID** 属性と 2 つの <`Price`> 子要素があります。  
  
-   2 つの内側の SELECT ステートメントで <`Price`> 要素が 2 つ構築されます。各要素には **PriceType** 属性と製品価格を返す XML があります。  
  
-   外側の SELECT ステートメントの XMLSCHEMA ディレクティブで、結果の XML の構造を記述するインライン XSD スキーマが生成されます。  
  
 サンプルとして効果の高いクエリにするには、次のクエリに示すように、FOR XML クエリを記述し、その結果に対して XQuery を記述して、XML の構造を変更します。  
  
```  
SELECT ProductID,   
 ( SELECT p2.ListPrice, p2.StandardCost  
   FROM Production.Product p2   
   WHERE Product.ProductID = p2.ProductID  
   FOR XML AUTO, ELEMENTS XSINIL, type ).query('  
                                   for $p in /p2/*  
                                   return   
                                    <Price PriceType = "{local-name($p)}">  
                                     { data($p) }  
                                    </Price>  
                                  ')  
FROM Production.Product  
WHERE ProductID = 520  
FOR XML AUTO, TYPE  
```  
  
 上の例では `query()` データ型の `xml` メソッドを使用し、内側の FOR XML クエリで返される XML に対してクエリを実行し、必要な結果を構築しています。  
  
 結果を次に示します。  
  
```  
<Production.Product ProductID="520">  
  <Price PriceType="ListPrice">133.3400</Price>  
  <Price PriceType="StandardCost">98.7700</Price>  
</Production.Product>  
```  
  
## <a name="see-also"></a>関連項目  
 [入れ子になった FOR XML クエリの使用](use-nested-for-xml-queries.md)  
  
  
