---
title: 使用したリレーションシップ sql:relationship (SQLXML 4.0) の指定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f27b47ae8216fa64b537d4c8b22b612c535a1869
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013672"
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>sql:relationship を使用した、リレーションシップの指定 (SQLXML 4.0)
  XML ドキュメント内の要素は関連付けることができます。 要素は階層的に入れ子にでき、要素間に ID、IDREF、または IDREFS のリレーションシップを指定することができます。  
  
 XSD スキーマでなど、 **\<顧客 >** 要素が含まれます **\<順序 >** 子要素。 AdventureWorks のデータベースにスキーマがマップされている場合、 **\<顧客 >** 要素は Sales.Customer テーブルにマップし、 **\<順序 >** 要素にマップされます、Sales.SalesOrderHeader テーブル。 顧客が注文を行うため、これらの基になるテーブル、Sales.Customer および Sales.SalesOrderHeader に関連します。 ここで、Sales.SalesOrderHeader テーブル内の CustomerID は、Sales.Customer テーブル内の CustomerID 主キーを参照する外部キーです。 使用してマッピング スキーマで要素間のリレーションシップを確立することができます、`sql:relationship`注釈。  
  
 注釈付き XSD スキーマでは、`sql:relationship` 注釈を使用して、要素のマップ先テーブルにおける主キーと外部キーのリレーションシップを基にスキーマ要素を階層的に入れ子にできます。 指定するときに、`sql:relationship`注釈、以下を識別する必要があります。  
  
-   親テーブル (Sales.Customer) と子テーブル (Sales.SalesOrderHeader)。  
  
-   親テーブルと子テーブル間のリレーションシップを構成する列。 たとえば、親テーブルと子テーブル両方にある CustomerID 列を指定します。  
  
 これらの情報を使用して、適切な階層が生成されます。  
  
 テーブルの名前と必要な結合情報を提供するには、次の属性で指定されます、`sql:relationship`注釈。 これらの属性がでのみ有効ですが、  **\<sql:relationship >** 要素。  
  
 **名前**  
 リレーションシップの一意な名前を指定します。  
  
 **Parent**  
 親リレーション (テーブル) を指定します。 これは省略可能な属性です。この属性を指定しない場合、親テーブル名はドキュメント内の子階層の情報から取得されます。 スキーマを使用して、同じ 2 つの親子階層を指定する場合 **\<sql:relationship >** 、別の親要素の親属性指定しないが、  **\<sql:リレーションシップ >** します。 この情報はスキーマ内の階層から取得されます。  
  
 **parent-key**  
 親の親キーを指定します。 親キーが複数の列で構成される場合は、値をスペースで区切って指定します。 複数列キーに指定される値と、それに対応する子キーに指定される値の間では、位置的なマッピングが行われます。  
  
 **子**  
 子リレーション (テーブル) を指定します。  
  
 **child-key**  
 親の parent-key を参照する子の、子キーを指定します。 子キーが複数の属性 (列) で構成される場合、child-key の値は、スペースで区切って指定します。 複数列キーに指定される値と、それに対応する親キーに指定される値の間では、位置的なマッピングが行われます。  
  
 **逆関数**  
 この属性で指定された **\<sql:relationship >** アップデート グラムで使用されます。 詳細については、次を参照してください。 [sql:relationship での sql:inverse 属性指定](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)します。  
  
 `sql:key-fields`を持つ子要素を含む要素に注釈を指定する必要があります、  **\<sql:relationship >** 要素と子要素の間に定義し、の主キーを行いませんが、親要素で指定したテーブル。 スキーマで指定されていない場合でも **\<sql:relationship >** を指定する必要があります`sql:key-fields`適切な階層を生成するためにします。 詳細については、次を参照してください。 [sql:key を使用して、キー列を識別する-フィールド](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)します。  
  
 結果内の適切な入れ子を生成することが推奨されます`sql:key-fields`はすべてのスキーマで指定します。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>A. 要素に sql:relationship 注釈を指定する  
 次の注釈付き XSD スキーマを含む **\<顧客 >** と **\<順序 >** 要素。 **\<順序 >** 要素が子要素の **\<顧客 >** 要素。  
  
 スキーマで、`sql:relationship`注釈が指定されて、 **\<順序 >** 子要素。 リレーションシップ自体がで定義されている、  **\<xsd:appinfo >** 要素。  
  
 **\<リレーションシップ >** 要素は、Sales.SalesOrderHeader テーブルの CustomerID を Sales.Customer テーブル内の CustomerID 主キーを参照する外部キーとして指定します。 したがって、顧客の注文の子要素として表示されます。 **\<顧客 >** 要素。  
  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 上のスキーマでは名前付きリレーションシップを使用しましたが、 名前のないリレーションシップを指定することもできます。 この結果は同じです。  
  
 次は、スキーマを変更し、名前のないリレーションシップを指定した例です。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 sql-relationship.xml として保存します。  
  
2.  次の次のテンプレートをコピーしてテキスト ファイルに貼り付けます。 sql-relationship.xml を保存したディレクトリに sql-relationshipT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (sql-relationship.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 Here is the result set:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>B. リレーションシップ チェーンを指定する  
 この例では、AdventureWorks データベースから取得したデータを使用して、次の XML ドキュメントを要求するとします。  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 XML ドキュメントでは、Sales.SalesOrderHeader テーブル内の注文ごとに 1 つ **\<順序 >** 要素。 それぞれ **\<順序 >** 要素のリストがある **\<製品 >** 子要素、注文した製品ごとに 1 つ。  
  
 この階層を生成する XSD スキーマを指定するには、2 つのリレーションシップを指定する必要があります。指定され、OrderOD と ODProduct します。 OrderOD リレーションシップでは、Sales.SalesOrderHeader テーブルと Sales.SalesOrderDetail テーブル間の親子リレーションシップを指定します。 ODProduct リレーションシップでは、Sales.SalesOrderDetail テーブルと Production.Product テーブル間のリレーションシップを指定します。  
  
 次のスキーマで、`msdata:relationship`注釈、 **\<製品 >** 要素が 2 つの値を指定します。指定され、OrderOD と ODProduct します。 これらの値の指定順序は重要です。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 名前付きリレーションシップを指定する代わりに、匿名のリレーションシップを指定することもできます。 ここでのコンテンツ全体 **\<注釈 >** . **\</annotation >** 、2 つのリレーションシップについて説明しますの子要素として表示される **\<製品 >** します。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationshipChain.xml として保存します。  
  
2.  次の次のテンプレートをコピーしてテキスト ファイルに貼り付けます。 relationshipChain.xml を保存したディレクトリに relationshipChainT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationshipChain.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 Here is the result set:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>C. 属性にリレーションシップ注釈を指定する  
 この例では、スキーマが含まれています、\<顧客 > を持つ要素を\<CustomerID > 子要素と IDREFS 型の OrderIDList 属性です。 \<顧客 > 要素が AdventureWorks データベースの Sales.Customer テーブルにマップします。 既定では、このマッピングのスコープがすべての子要素に適用されます、または属性の場合を除き、`sql:relation`が指定されています、子要素または属性に、この場合は、を使用して、適切なプライマリ-キー/外部キーリレーションシップを定義する必要があります\<リレーションシップ > 要素。 子要素または属性で `relation` 注釈を使って異なるテーブルを指定する場合は、`relationship` 注釈も指定する必要があります。  
  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationship-on-attribute.xml として保存します。  
  
2.  次のテンプレートをコピーして、ファイルに貼り付け、 relationship-on-attribute.xml を保存したディレクトリに relationship-on-attributeT.xml として保存します。 このテンプレートのクエリでは、CustomerID が 1 の顧客が選択されます。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationship-on-attribute.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 Here is the result set:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>D. 複数の要素に sql:relationship を指定する  
 この例では、注釈付き XSD スキーマを含む、 **\<顧客 >** 、 **\<順序 >** と **\<OrderDetail >** 要素。  
  
 **\<順序 >** 要素が子要素の **\<顧客 >** 要素。 **\<sql:relationship >** が指定されて、 **\<順序 >** の子要素の子要素として、顧客の注文を表示するため、 **\<顧客 >** .  
  
 **\<順序 >** 要素が含まれています、  **\<OrderDetail >** 子要素。 **\<sql:relationship >** が指定されています **\<OrderDetail >** の子要素の子要素として、注文に関連する注文の詳細が表示されるように **\<順序 >** 要素。  
  
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
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationship-multiple-elements.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 relationship-multiple-elements.xml を保存したディレクトリに relationship-multiple-elementsT.xml として保存します。 このテンプレート内のクエリでは、CustomerID が 1、SalesOrderID が 43860 の顧客の注文情報が返されます。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationship-multiple-elements.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 Here is the result set:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>E. 指定する、 \<sql:relationship > 親属性なし  
 この例では、指定する、  **\<sql:relationship >** せず、**親**属性。 たとえば、次の従業員テーブルがあるとします。  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 次の XML ビューには、  **\<Emp1 >** と **\<Emp2 >** 要素は、Sales.Emp1 および Sales.Emp2 テーブルにマップします。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 スキーマの両方、  **\<Emp1 >** 要素と **\<Emp2 >** 要素は型`EmpType`します。 型`EmpType`について説明します、 **\<順序 >** 子要素と、対応する **\<sql:relationship >** します。 この場合、指定できる 1 つの親はありません **\<sql:relationship >** を使用して、**親**属性。 指定しないこのような状況で、**親**属性 **\<sql:relationship >** 、**親**から属性情報を取得、スキーマ内の階層。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  AdventureWorks データベース内に次のテーブルを作成します。  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  テーブルに次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 relationship-noparent.xml として保存します。  
  
4.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 relationship-noparent.xml を保存したディレクトリに relationship-noparentT.xml として保存します。 テンプレートのクエリは、すべてを選択、 \<Emp1 > 要素 (そのため、親は emp1 です)。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (relationship-noparent.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 結果セットの一部を次に示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
