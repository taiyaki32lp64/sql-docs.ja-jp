---
title: インライン XSD スキーマの生成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b6c8233b95f3f95235bb4f618358d4680d3088f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287481"
---
# <a name="generate-an-inline-xsd-schema"></a>インライン XSD スキーマの生成
  FOR XML 句では、クエリからクエリ結果と共にインライン スキーマを返すように要求できます。 XDR スキーマが必要な場合は、FOR XML 句に XMLDATA キーワードを指定します。 XSD スキーマが必要な場合は、XMLSCHEMA キーワードを指定します。  
  
 このトピックでは、XMLSCHEMA キーワードとこのキーワードで生成されるインライン XSD スキーマについて説明します。 次に、インライン スキーマを要求するときの制限事項を示します。  
  
-   XMLSCHEMA は、RAW モードと AUTO モードでのみ指定できます。EXPLICIT モードでは指定できません。  
  
-   入れ子になった FOR XML クエリで TYPE ディレクティブを指定すると、そのクエリ結果は `xml` 型になるので、この結果は型指定されていない XML データのインスタンスとして処理されます。 詳細については、「[XML データ &#40;SQL Server&#41;](xml-data-sql-server.md)」を参照してください。  
  
 FOR XML クエリに XMLSCHEMA を指定すると、クエリ結果としてスキーマと XML データの両方が返されます。 データの最上位レベルの各要素が既定の名前空間宣言を使用して前のスキーマを参照し、次に、既定の名前空間宣言がインライン スキーマの対象の名前空間を参照します。  
  
 例 :  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 クエリ結果には、XML スキーマと XML 結果が含まれます。 結果内の最上位レベルにある <`ProductModel`> 要素では、既定の名前空間宣言 xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" を使用してスキーマが参照されます。  
  
 結果のスキーマ部分には、複数の名前空間を説明する複数のスキーマ ドキュメントが含まれることがあります。 少なくとも次の 2 つのスキーマ ドキュメントが返されます。  
  
-   **Sqltypes** 名前空間のスキーマ ドキュメント。このドキュメントには SQL の基本データ型が返されます。  
  
-   FOR XML クエリの結果の構造が記述されたスキーマ ドキュメント。  
  
 型指定された `xml` データ型がクエリ結果に含まれている場合は、それらの型指定された `xml` データ型に関連付けられたスキーマも含まれます。  
  
 FOR XML クエリ結果の構造が記述されたスキーマ ドキュメントの対象の名前空間には、固定部分と自動的に値が増加する数値部分があります。 この名前空間の形式を次に示します。 *n* は正の整数です。 たとえば、上記のクエリでは urn:schemas-microsoft-com:sql:SqlRowSet1 が対象の名前空間です。  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 クエリを実行するたびに、返される結果の対象の名前空間が変化することは望ましくありません。 たとえば、返された XML へのクエリを実行する場合に、対象の名前空間が変化すると、クエリの更新が必要になります。 XMLSCHEMA オプションを FOR XML 句に追加するときに、必要に応じて対象の名前空間を指定できます。 返される XML には指定した名前空間が含まれ、何度そのクエリを実行しても変化しません。  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>エンティティ要素  
 クエリ結果として生成される XSD スキーマ構造の詳細を説明するには、まずエンティティ要素について説明する必要があります。  
  
 FOR XML クエリで返される XML データのエンティティ要素は、列ではなくテーブルから生成される要素です。 たとえば、次の FOR XML クエリを実行すると、 `Person` データベースの `AdventureWorks2012` テーブルから連絡先に関する情報が返されます。  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 結果を次に示します。  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 この結果では、<`Person`> がエンティティ要素です。 XML 結果には複数のエンティティ要素が含まれることもあります。各エンティティ要素のインライン XSD スキーマには、グローバル宣言が含まれます。 たとえば、次のクエリを実行すると、特定の注文の販売注文ヘッダーと詳細情報が取得されます。  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 このクエリには ELEMENTS ディレクティブが指定されているので、返される XML は要素中心になります。 また、このクエリには XMLSCHEMA ディレクティブも指定されています。 したがって、インライン XSD スキーマが返されます。 結果を次に示します。  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 上のクエリに関して、次の点に注意してください。  
  
-   このクエリ結果では、<`SalesOrderHeader`> と <`SalesOrderDetail`> がエンティティ要素です。 したがって、これらの要素はスキーマ内でグローバルに宣言されます。 つまり、宣言は <`Schema`> 要素内の最上位レベルに記述されます。  
  
-   <`SalesOrderID`>、<`ProductID`>、および <`OrderQty`> は列にマップされるので、エンティティ要素ではありません。 ELEMENTS ディレクティブを指定したので、列データは XML の要素として返されます。 これらの要素は、エンティティ要素の複合型のローカル要素にマップされます。 ELEMENTS ディレクティブを指定しないと、 `SalesOrderID`、 `ProductID` 、および `OrderQty` の各値は、対応するエンティティ要素の複合型のローカル属性にマップされることに注意してください。  
  
## <a name="attribute-name-clashes"></a>属性名の競合  
 次の説明は、 `CustOrder` テーブルと `CustOrderDetail` テーブルに基づいています。 次のサンプルをテストするには、これらのテーブルを作成し、独自のサンプル データを追加してください。  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 FOR XML では、同じ名前でさまざまなプロパティや属性が示されることがあります。 たとえば、次の属性中心の RAW モードのクエリを実行すると、OrderID という同じ名前の 2 つの属性が生成されます。 これにより、エラーが発生します。  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 ただし、2 つの要素が同じ名前になることは許容されるので、次のように ELEMENTS ディレクティブを追加することでこの問題を解決できます。  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 結果は次のとおりです。 インライン XSD スキーマで OrderID 要素が 2 回定義されていることに注意してください。 一方の宣言では、CustOrderDetail テーブルの OrderID に合わせて、minOccurs が 0 に設定されます。もう一方の宣言は、minOccurs が既定で 1 に設定される `CustOrder` テーブルの OrderID 主キー列にマップされます。  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>要素名の競合  
 FOR XML では、同じ名前で 2 つのサブ要素を示すことができます。 たとえば、次のクエリでは製品の ListPrice と DealerPrice の値が取得されますが、これら 2 つの列に Price という同じ別名が指定されます。 したがって、返される行セットには同じ名前の列が 2 つ含まれます。  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>ケース 1: 2 つのサブ要素が同じ型の非キー列でどちらも NULL 値が許容される場合  
 次のクエリの 2 つのサブ要素は同じ型の非キー列で、どちらも NULL 値が許容されます。  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 このクエリを実行すると、次のような XML が生成されます。 インライン XSD の一部のみを示します。  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 このインライン XSD スキーマでは、次の点に注意してください。  
  
-   ListPrice と DealerPrice は `money` という同じ型で、テーブルではどちらも NULL 値が許容されます。 したがって、これらの要素は返される XML に含まれないので、<`row`> 要素の複合型の宣言には、minOccurs が 0、maxOccurs が 2 に指定された 1 つの <`Price`> 子要素のみが含まれます。  
  
-   テーブルの `DealerPrice` の値が NULL なので、クエリ結果には、`ListPrice` のみが <`Price`> 要素として返されます。 `XSINIL` パラメーターを ELEMENTS ディレクティブに追加すると、返される両方の要素で、DealerPrice に対応する <`Price`> 要素の `xsi:nil` の値が TRUE に設定されます。 また、インライン XSD スキーマの <`row`> の複合型の定義として 2 つの <`Price`> 子要素が返されます。どちらの要素でも `nillable` 属性が TRUE に設定されます。 結果の一部を次に示します。  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>ケース 2: 同じ型でも一方がキー列で他方が非キー列の場合  
 次のクエリでは、型が同じ型でも一方がキー列で他方が非キー列の場合について説明します。  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 テーブル **T** に対する次のクエリでは、Col1 と Col2 に同じ別名を指定します。主キー Col1 では NULL 値が許容されませんが、Col2 では NULL 値が許容されます。 このクエリを実行すると、<`row`> 要素の子要素である 2 つの兄弟要素が生成されます。  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 結果は次のとおりです。 インライン XSD スキーマの一部のみを示します。  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 インライン XSD スキーマで、Col2 に対応する <`Col`> 要素の minOccurs が 0 に設定されていることに注意してください。  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>ケース 3: 2 つの要素の型が異なり、対応する列で NULL 値が許容される場合  
 ケース 2 で示したサンプル テーブルに対して、次のクエリを指定します。  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 次のクエリでは、Col2 と Col3 に同じ別名を指定します。 このクエリを実行すると、同じ名前の 2 つの兄弟要素がクエリ結果として生成され、両方とも <`raw`> 要素の子要素になります。 これらの列の型はそれぞれ異なり、どちらも NULL 値が許容されます。 結果は次のとおりです。 インライン XSD スキーマの一部のみを示します。  
  
 `...`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 このインライン XSD スキーマでは、次の点に注意してください。  
  
-   Col2 と Col3 の両方で NULL 値が許容されるので、<`Col`> 要素の宣言により、minOccurs が 0、maxOccurs が 2 にそれぞれ指定されます。  
  
-   これらの <`Col`> 要素は兄弟なので、スキーマに含まれる要素の宣言は 1 つです。 また、型は異なりますが、どちらの要素も単純型なので、スキーマ内の要素の型は `xsd:anySimpleType` になります。 結果では、`xsi:type` 属性により、それぞれのインスタンスの型が識別されます。  
  
-   クエリ結果の <`Col`> 要素のインスタンスはすべて、`xsi:type` 属性を使用して、インスタンスの型を参照します。  
  
  
