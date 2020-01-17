---
title: アップデート グラム (SQLXML 4.0) で注釈付きマッピング スキーマの指定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 627ab54ed35cbc0a43c5a0eac26a1397199edbd8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014666"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>アップデートグラムでの注釈付きマッピング スキーマの指定 (SQLXML 4.0)
  ここでは、アップデートグラムで指定したマッピング スキーマ (XSD または XDR) が、更新の処理にどのように使用されるかについて説明します。 アップデート グラムでのテーブルと列を要素と属性のアップデート グラムのマッピングで使用する、注釈付きマッピング スキーマの名前を行うことができます[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。 アップデートグラムでマッピング スキーマを指定する場合、アップデートグラムで指定する要素と属性名は、マッピング スキーマ内の要素と属性にマップされる必要があります。  
  
 使用するマッピング スキーマを指定する、`mapping-schema`の属性、 **\<同期 >** 要素。 次の例では、単純なマッピング スキーマを使用するアップデートグラムと、より複雑なスキーマを使用するアップデートグラムの 2 つのアップデートグラムを示します。  
  
> [!NOTE]  
>  このドキュメントは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でサポートされるテンプレートとマッピング スキーマについて理解していることを前提としています。 詳細については、次を参照してください。[注釈付き XSD スキーマの概要&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)します。 XDR を使用する従来のアプリケーションでは、次を参照してください。[注釈付き XDR スキーマ&#40;SQLXML 4.0 では非推奨&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)します。  
  
## <a name="dealing-with-data-types"></a>データ型の扱い  
 スキーマが指定されている場合、 `image`、 `binary`、または`varbinary`[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型 (を使用して`sql:datatype`)、XML データ型を指定しないと、アップデート グラムでは、XML データ型が`binary base 64`します。 データが `bin.base` 型の場合は、明示的に型 (`dt:type=bin.base` または `type="xsd:hexBinary"`) を指定する必要があります。  
  
 `dateTime`、`date`、または `time` の XSD データ型を指定する場合は、`sql:datatype="dateTime"` を使用して、対応する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型も指定する必要があります。  
  
 パラメーターを処理するときに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]`money`型、明示的に指定してください`sql:datatype="money"`マッピング スキーマで適切なノード。  
  
## <a name="examples"></a>使用例  
 次の例を使用して実際のサンプルを作成するで指定された要件を満たす必要があります[SQLXML の例を実行するための要件](../../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. 単純なマッピング スキーマを使用するアップデートグラムを作成する  
 次の XSD スキーマ (SampleSchema.xml) は、マップするマッピング スキーマ、 **\<顧客 >** 要素は Sales.Customer テーブルにします。  
  
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
  
 次のアップデートグラムでは、Sales.Customer テーブルにレコードを挿入します。ここでは上のマッピング スキーマに従って、このデータをテーブルに適切にマップします。 アップデート グラムでは、要素名が同じ通知 **\<顧客 >** スキーマで定義されています。 アップデートグラムで特定のスキーマを指定するときには、これが必須となります。  
  
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
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、同等の XDR スキーマです。  
  
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
 スキーマ要素は関連付けることができます。 **\<Sql:relationship >** 要素がスキーマ要素間の親子リレーションシップを指定します。 この情報は、主キー/外部キーのリレーションシップがある対応するテーブルを更新するときに使用されます。  
  
 次のマッピング スキーマ (SampleSchema.xml) は、2 つの要素で構成されます **\<順序 >** と **\<OD >** :  
  
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
  
 次のアップデート グラムでは、この XSD スキーマを使用して、新しい注文明細レコードを追加する (、 **\<OD >** 内の要素、 **\<後 >** ブロック) 注文 43860 の。 `mapping-schema` 属性は、アップデートグラム内でマッピング スキーマを指定するために使用されます。  
  
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
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、同等の XDR スキーマです。  
  
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
 この例では、XSD で指定される親子リレーションシップがアップデートグラム ロジックでどのように使用され、更新が処理されるかと、`inverse` 注釈がどのように使用されるかを示します。 詳細については、`inverse`注釈を参照してください[sql:relationship での sql:inverse 属性指定&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)します。  
  
 この例では、次の表にある、 **tempdb**データベース。  
  
-   `Cust (CustomerID, CompanyName)`。ここでは `CustomerID` は主キーです。  
  
-   `Ord (OrderID, CustomerID)`。ここでは `CustomerID` は外部キーで、`CustomerID` テーブル内の `Cust` 主キーを参照します。  
  
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
  
 この例では、XSD スキーマが **\<顧客 >** と **\<順序 >** され、2 つの要素間の親子リレーションシップを指定します。 識別 **\<順序 >** 親要素としてと **\<顧客 >** の子要素として。  
  
 アップデートグラム処理ロジックでは、親子リレーションシップに関する情報に基づいて、レコードがテーブルに挿入される順序が決定されます。 この例では、アップデート グラム ロジックまずしよう Ord テーブルにレコードを挿入 (ため **\<順序 >** 親である)、Cust テーブルにレコードを挿入しようと (ため **\<顧客 >** 子である)。 しかし、データベース テーブル スキーマに含まれる主キー/外部キーの情報に対して、この挿入操作はデータベースの外部キー違反となるため、挿入は失敗します。  
  
 更新操作中に親子リレーションシップを逆に、アップデート グラム ロジックに指示する、`inverse`注釈が指定されて、 **\<リレーションシップ >** 要素。 こうすると、最初に Cust テーブル、次に Ord テーブルにレコードが追加され、操作は成功します。  
  
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
  
1.  これらのテーブルを作成、 **tempdb**データベース。  
  
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
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
## <a name="see-also"></a>参照  
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
