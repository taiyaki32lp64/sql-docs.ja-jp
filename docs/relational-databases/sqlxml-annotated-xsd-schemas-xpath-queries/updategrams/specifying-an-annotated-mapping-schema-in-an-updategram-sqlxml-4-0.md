---
title: アップデートグラム用の注釈付きマッピングスキーマ (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4feb8e282390b4808b69493a299cbad990f1e91b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243565"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>アップデートグラムでの注釈付きマッピング スキーマの指定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  ここでは、アップデートグラムで指定したマッピング スキーマ (XSD または XDR) が、更新の処理にどのように使用されるかについて説明します。 アップデートグラムでは、アップデートグラムの要素と属性をの[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]テーブルと列にマップするときに使用する、注釈付きマッピングスキーマの名前を指定できます。 アップデートグラムでマッピング スキーマを指定する場合、アップデートグラムで指定する要素と属性名は、マッピング スキーマ内の要素と属性にマップされる必要があります。  
  
 マッピングスキーマを指定するには、 ** \<sync>** 要素の**マッピングスキーマ**属性を使用します。 次の例では、単純なマッピング スキーマを使用するアップデートグラムと、より複雑なスキーマを使用するアップデートグラムの 2 つのアップデートグラムを示します。  
  
> [!NOTE]  
>  このドキュメントは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でサポートされるテンプレートとマッピング スキーマについて理解していることを前提としています。 詳細については、「[注釈付き XSD スキーマの概要 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)」を参照してください。 XDR を使用するレガシアプリケーションでは、 [SQLXML 4.0&#41;では、注釈付き Xdr スキーマ &#40;非推奨](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)とされています。  
  
## <a name="dealing-with-data-types"></a>データ型の扱い  
 スキーマで**image**、 **binary**、または**varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型 ( **sql: datatype**を使用) が指定されており、xml データ型が指定されていない場合、アップデートグラムでは xml データ型が**バイナリベース 64**であると想定されます。 データが**bin. 基本**型の場合は、型 (**dt: type = bin. base**または**Type = "xsd: hexBinary"**) を明示的に指定する必要があります。  
  
 スキーマで**dateTime**、 **date**、または**time**のいずれかの XSD データ型を指定する場合は[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、 **sql: datatype = "dateTime"** を使用して、対応するデータ型も指定する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Money**型のパラメーターを処理する場合は、マッピングスキーマの適切なノードに**sql: datatype = "money"** を明示的に指定する必要があります。  
  
## <a name="examples"></a>例  
 次の例を使用して実際のサンプルを作成するには、 [SQLXML の例を実行するための要件](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)を満たす必要があります。  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. 単純なマッピング スキーマを使用するアップデートグラムを作成する  
 次の XSD スキーマ (sampleschema.xml) は、 ** \<customer>** 要素を Sales. customer テーブルにマップするマッピングスキーマです。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 次のアップデートグラムでは、Sales.Customer テーブルにレコードを挿入します。ここでは上のマッピング スキーマに従って、このデータをテーブルに適切にマップします。 アップデートグラムでは、スキーマで定義されているのと同じ要素名 ( ** \<Customer>**) が使用されていることに注意してください。 アップデートグラムで特定のスキーマを指定するときには、これが必須となります。  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 SampleUpdateSchema.xml として保存します。  
  
2.  下のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 SampleUpdateSchema.xml を保存したディレクトリに SampleUpdategram.xml として保存します。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (SampleUpdateSchema.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. マッピング スキーマに指定されている親子リレーションシップを使用して、レコードを挿入する  
 スキーマ要素は関連付けることができます。 ** \<Sql: relationship>** 要素は、スキーマ要素間の親子リレーションシップを指定します。 この情報は、主キー/外部キーのリレーションシップがある対応するテーブルを更新するときに使用されます。  
  
 次のマッピングスキーマ (sampleschema.xml) は、 ** \<順序>** と** \<OD>** の2つの要素で構成されています。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 次のアップデートグラムでは、この XSD スキーマを使用して、注文43860の新しい注文明細レコード ( ** \<after>** ブロックに** \<OD>** 要素) を追加します。 **マッピング**スキーマ属性は、アップデートグラムでマッピングスキーマを指定するために使用されます。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 SampleUpdateSchema.xml として保存します。  
  
2.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 SampleUpdateSchema.xml を保存したディレクトリに SampleUpdategram.xml として保存します。  
  
     マッピング スキーマ (SampleUpdateSchema.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. XSD スキーマで指定されている親子リレーションシップと inverse 注釈を使用して、レコードを挿入する  
 この例では、更新プログラムを処理するために、アップデートグラムのロジックが XSD で指定されている親子関係を使用する方法と、**逆**の注釈の使用方法を示します。 **逆**の注釈の詳細については、「 [sql: relationship での Sql: 逆属性の指定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)」を参照してください。  
  
 この例では、次のテーブルが**tempdb**データベースにあることを前提としています。  
  
-   
  `Cust (CustomerID, CompanyName)`。ここでは `CustomerID` は主キーです。  
  
-   
  `Ord (OrderID, CustomerID)`。ここでは `CustomerID` は外部キーで、`CustomerID` テーブル内の `Cust` 主キーを参照します。  
  
 このアップデートグラムでは次の XSD スキーマを使用して、Cust および Ord テーブルにレコードを挿入します。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 この例の XSD スキーマには、 ** \<Customer>** と** \<Order>** の要素があり、2つの要素間の親子リレーションシップが指定されています。 親要素と** \<顧客**が子要素として>する** \<順序>** を識別します。  
  
 アップデートグラム処理ロジックでは、親子リレーションシップに関する情報に基づいて、レコードがテーブルに挿入される順序が決定されます。 この例では、アップデートグラムロジックはまず、Ord テーブルにレコードを挿入しようとします ( ** \<注文>** が親であるため)。次に、Cust テーブルにレコードを挿入しようとします ( ** \<Customer>** は子であるため)。 しかし、データベース テーブル スキーマに含まれる主キー/外部キーの情報に対して、この挿入操作はデータベースの外部キー違反となるため、挿入は失敗します。  
  
 更新操作中に親子関係を反転するようにアップデートグラムのロジックを指定するには、 ** \<リレーションシップの>** 要素に**逆**注釈を指定します。 こうすると、最初に Cust テーブル、次に Ord テーブルにレコードが追加され、操作は成功します。  
  
 次のアップデートグラムでは、指定された XSD スキーマを使用して、Ord テーブルに注文 (OrderID=2)、Cust テーブルに顧客 (CustomerID='AAAAA') を挿入します。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>アップデートグラムをテストするには  
  
1.  次のテーブルを**tempdb**データベースに作成します。  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 SampleUpdateSchema.xml として保存します。  
  
3.  上のアップデートグラムのテンプレートをコピーして、テキスト ファイルに貼り付け、 SampleUpdateSchema.xml を保存したディレクトリに SampleUpdategram.xml として保存します。  
  
     マッピング スキーマ (SampleUpdateSchema.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;アップデートグラムのセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
