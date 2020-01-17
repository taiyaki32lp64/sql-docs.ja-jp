---
title: Sql:prefix 有効な ID、IDREF、IDREFS 型属性を使用した (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- annotated XSD schemas, ID type attribute
- IDREF type attribute [SQLXML]
- annotated XSD schemas, IDREFS type attribute
- ID type attribute [SQLXML]
- sql:prefix
- prefix annotation
- IDREF relationships [SQLXML]
- IDREFS type attribute [SQLXML]
- annotated XSD schemas, IDREF type attribute
- ID relationships [SQLXML]
ms.assetid: 1c7f77d3-81f3-4820-bb63-c4aaa4ea9aa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48ae7034ec0c133c1140e4c581794302ca8bad77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013921"
---
# <a name="creating-valid-id-idref-and-idrefs-type-attributes-using-sqlprefix-sqlxml-40"></a>sql:prefix を使用した、有効な ID 型、IDREF 型、IDREFS 型の属性の作成 (SQLXML 4.0)
  属性を ID 型属性として指定することができます。 ID 型属性を指定すると、IDREF または IDREFS として指定した属性から ID 型属性を参照でき、ドキュメント間をリンクできるようになります。  
  
 ID、IDREF、IDREFS は、データベースの PK と FK (主キーと外部キー) のリレーションシップにほぼ対応し、ほとんど違いはありません。 XML ドキュメントの ID 型属性の値を個別にある必要があります。 場合**CustomerID**と**OrderID**属性が XML ドキュメントの ID 型として指定はこれらの値は一意である必要があります。 一方データベースでは、CustomerID 列と OrderID 列の値は同じにできます。 たとえば、CustomerID = 1、OrderID = 1 はデータベース内で有効です。  
  
 ID 属性、IDREF 属性、および IDREFS 属性が有効であるためには、次の条件を満たしている必要があります。  
  
-   ID の値が XML ドキュメント内で一意であること。  
  
-   各 IDREF および IDREFS について、XML ドキュメント内に参照される ID が存在すること。  
  
-   ID、IDREF、IDREFS の値が名前付きトークンであること。 たとえば、整数値 101 は ID 値にできません。  
  
-   ID、IDREF、IDREFS 型の属性は、型の列にマップすることはできません`text`、 `ntext`、または`image`またはその他の任意のバイナリ データ型 (たとえば、 `timestamp`)。  
  
 XML ドキュメントに複数の Id が含まれている場合は、使用、`sql:prefix`値が一意であることを確認する注釈。  
  
 `sql:prefix` 注釈は、XSD 固定属性では使用できないことに注意してください。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-id-and-idrefs-types"></a>A. ID 型と IDREFS 型を指定する  
 次のスキーマで、 **\<顧客 >** 要素から成る、 **\<順序 >** 子要素。 **\<順序 >** 要素が子要素にも、  **\<OrderDetail >** 要素。  
  
 **OrderIDList**属性の **\<顧客 >** IDREFS 型の属性を参照するには、 **OrderID**の属性、 **\<順序 >** 要素。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
                 parent="Sales.Customer"  
                 parent-key="CustomerID"  
                 child="Sales.SalesOrderHeader"  
                 child-key="CustomerID" />  
    <sql:relationship name="OrderOrderDetail"  
                 parent="Sales.SalesOrderHeader"  
                 parent-key="SalesOrderID"  
                 child="Sales.SalesOrderDetail"  
                 child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
               sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                   sql:relationship="OrderOrderDetail"   
                   maxOccurs="unbounded" >  
                  <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="ProductID" type="xsd:string" />  
                   <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
               </xsd:element>  
             </xsd:sequence>  
             <xsd:attribute name="SalesOrderID"   
                            type="xsd:ID" sql:prefix="ord-" />  
             <xsd:attribute name="OrderDate" type="xsd:date" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CustomerID" type="xsd:string" />  
    <xsd:attribute name="OrderIDList" type="xsd:IDREFS"   
                   sql:relation="Sales.SalesOrderHeader" sql:field="SalesOrderID"  
                   sql:relationship="CustOrders" sql:prefix="ord-">  
    </xsd:attribute>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 sqlPrefix.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 sqlPrefix.xml を保存したディレクトリに sqlPrefixT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="sqlPrefix.xml">  
        /Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (sqlPrefix.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlPrefix.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 結果の一部を次に示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" OrderIDList="ord-43860 ord-44501 ord-45283 ord-46042">  
    <Order SalesOrderID="ord-43860" OrderDate="2001-08-01" CustomerID="1">  
      <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
      ...  
    </Order>  
    ...  
 </Customer>  
</ROOT>  
```  
  
  
