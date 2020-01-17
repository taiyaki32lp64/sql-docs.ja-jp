---
title: 'Sql: 定数 (SQLXML) を使用して定数要素を作成する'
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 45ab0c13ad2c631a438e2a8637e36d192165094b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257478"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>sql:is-constant を使用した、定数要素の作成 (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  定数要素 (つまり、データベースのテーブルまたは列にマップされない XSD スキーマの要素) を指定するには、 **sql:: 定数**注釈を使用します。 この注釈はブール値 (0 = false、1 = true) をとります。 指定できる値は 0、1、true、false です。 **Sql:: 定数**注釈は、属性を持たない要素に対して指定できます。 この注釈を値 true (または 1) と共に要素に指定した場合、その要素は XML ドキュメント内に表示されますが、データベースにはマップされなくなります。  
  
 **Sql: 定数**注釈は、次の場合に使用できます。  
  
-   最上位要素を XML ドキュメントに追加する。 XML では、ドキュメントに 1 つの最上位要素 (ルート要素) が必要です。  
  
-   すべての注文をラップする** \<注文>** 要素などのコンテナー要素を作成する。  
  
 **Sql: 定数**注釈は、 ** \<complexType>** 要素に追加できます。  
  
## <a name="examples"></a>例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、「 [SQLXML の例を実行するための要件](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)」を参照してください。  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>A. sql:is-constant を指定してコンテナー要素を追加する  
 この注釈付き XSD スキーマでは、値が1の**sql:** CustomerOrders 属性を指定することにより、 ** \<>** が定数要素として定義されます。 したがって、 ** \<CustomerOrders>** は、どのデータベーステーブルまたは列にもマップされません。 この定数要素は、 ** \<子要素>順序**で構成されます。  
  
 CustomerOrders>はどのデータベーステーブルまたは列にもマップされませんが、結果の XML には、 ** \<順序>** 子要素を含むコンテナー要素として表示されます。 ** \<**  
  
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

     詳細については、「ADO を使用した[SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果セットの一部を次に示します。  
  
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
  
  
