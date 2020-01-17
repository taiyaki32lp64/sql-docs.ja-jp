---
title: '定数要素を使用した作成: は定数 (SQLXML 4.0) |マイクロソフトのドキュメント'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- sql:is-constant
- XSD schemas [SQLXML], constant elements
- element mapping [SQLXML], constant elements
- is-constant annotation
- constant elements [SQLXML]
- annotated XSD schemas, constant elements
ms.assetid: 940eea1b-54f5-445f-b844-c894d9f3941b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc100446eb6dff17125b0df7a60b8c2c82e46277
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013943"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>sql:is-constant を使用した、定数要素の作成 (SQLXML 4.0)
  定数要素を指定する、データベース テーブルまたは列にマップされない XSD スキーマ内の要素は、-使用することができます、`sql:is-constant`注釈。 この注釈はブール値 (0 = false、1 = true) をとります。 指定できる値は 0、1、true、false です。 `sql:is-constant` 注釈は、属性のない要素に指定できます。 この注釈を値 true (または 1) と共に要素に指定した場合、その要素は XML ドキュメント内に表示されますが、データベースにはマップされなくなります。  
  
 `sql:is-constant` 注釈は次の目的に使用できます。  
  
-   最上位要素を XML ドキュメントに追加する。 XML では、ドキュメントに 1 つの最上位要素 (ルート要素) が必要です。  
  
-   コンテナーの要素を作成するなど、 **\<注文 >** すべての注文をラップする要素。  
  
 `sql:is-constant`に注釈を追加できる、  **\<complexType >** 要素。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>A. sql:is-constant を指定してコンテナー要素を追加する  
 この注釈付き XSD スキーマ、  **\<CustomerOrders >** 指定することで、定数要素として定義されているが、`sql:is-constant`属性値は 1 です。 そのため、  **\<CustomerOrders >** はデータベース テーブルまたは列にマップされていません。 この定数要素から成る、 **\<順序 >** 子要素。  
  
 **\<CustomerOrders >** マップされないデータベースのテーブルまたは列を結果の XML を含むコンテナー要素として表示されます、 **\<順序 >** 子要素。  
  
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
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="CustomerOrders" sql:is-constant="1" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"  
                           sql:relationship="CustOrders"   
                           maxOccurs="unbounded" >  
                <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="OrderDate" type="xsd:date" />  
                   <xsd:attribute name="CustomerID" type="xsd:string" />  
                </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>  
         </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 isConstant.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 isConstant.xml を保存したディレクトリに isConstantT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="isConstant.xml">  
            Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (isConstant.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\isConstant.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、結果セットの一部です。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
<Customer CustomerID="1">   
  <CustomerOrders>   
    <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1" />   
    <Order SalesOrderID="44501" OrderDate="2001-11-01" CustomerID="1" />   
    <Order SalesOrderID="45283" OrderDate="2002-02-01" CustomerID="1" />   
    <Order SalesOrderID="46042" OrderDate="2002-05-01" CustomerID="1" />   
    ...  
  </CustomerOrders>   
</Customer>   
</ROOT>  
```  
  
  
