---
title: XML 一括読み込みの例 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f70e66a02637b65e96cccc6001c9702d5253d5cd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257374"
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>XML 一括読み込みの例 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  以下の例では、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の XML 一括読み込み機能について示します。 それぞれの例では、XSD スキーマと、同等の XDR スキーマを提供します。  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>一括読み込みスクリプト (ValidateAndBulkload.vbs)  
 次のスクリプトは[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) で記述されており、xml DOM に xml ドキュメントを読み込みます。スキーマに対して検証します。また、ドキュメントが有効な場合、は XML 一括読み込みを実行して XML を[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]テーブルに読み込みます。 このスクリプトは、後に示す個々の例で使用できます。  
  
> [!NOTE]  
>  XML 一括読み込みでは、データ ファイルから内容がアップロードされなくても警告またはエラーは返されません。 このため、一括読み込み操作を実行する前に XML データ ファイルを検証することをお勧めします。  
  
```vbs  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. 単一テーブルでの XML の一括読み込み  
 この例では、ConnectionString プロパティ (MyServer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ) で指定されているのインスタンスへの接続を確立します。 この例では、ErrorLogFile プロパティも指定しています。 エラー出力は指定したファイル ("C:\error.log") に保存されます。ファイルの保存場所は変更することもできます。 また、Execute メソッドのパラメーターは、マッピングスキーマファイル (Sampleschema.xml) と XML データファイル (Samplexmldata.xml) の両方であることに注意してください。 一括読み込みを実行すると、 **tempdb**データベースで作成した Cust テーブルには、XML データファイルの内容に基づく新しいレコードが格納されます。  
  
#### <a name="to-test-a-sample-bulk-load"></a>一括読み込みのサンプルをテストするには  
  
1.  次のテーブルを作成します。  
  
    ```sql  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに次の XSD スキーマを追加します。  
  
    ```xml  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに、次の XML ドキュメントを追加します。  
  
    ```xml  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、このトピックの冒頭で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名に変更します。 Execute メソッドのパラメーターとして指定されたファイルの適切なパスを指定します。  
  
5.  VBScript コードを実行します。 XML 一括読み込みによって、XML が Cust テーブルに読み込まれます。  
  
 これは、これと同等の XDR スキーマです。  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>B. 複数テーブルでの XML データの一括読み込み  
 この例では、XML ドキュメントは** \<顧客>** と** \<注文>** 要素で構成されています。  
  
```xml  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 この例では、XML データを**Cust**および**custorder**という2つのテーブルに一括読み込みします。  
  
-   Cust (CustomerID、CompanyName、City)  
  
-   CustOrder (OrderID, CustomerID)  
  
 次の XSD スキーマでは、これらのテーブルの XML ビューが定義されています。 スキーマは、 ** \<Customer>** と** \<Order>** 要素の間の親子リレーションシップを指定します。  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Customers" sql:relation="Cust" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="CustomerID"  type="xsd:integer" />  
              <xsd:element name="CompanyName" type="xsd:string" />  
              <xsd:element name="City"        type="xsd:string" />  
              <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
                <xsd:complexType>  
                  <xsd:attribute name="OrderID" type="xsd:integer" />  
                </xsd:complexType>  
              </xsd:element>  
             </xsd:sequence>  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 XML 一括読み込みでは、上で指定された** \<Cust>** と** \<custorder>** 要素の間の主キー/外部キーのリレーションシップを使用して、データを両方のテーブルに一括読み込みします。  
  
#### <a name="to-test-a-sample-bulk-load"></a>一括読み込みのサンプルをテストするには  
  
1.  **Tempdb**データベースに2つのテーブルを作成します。  
  
    ```sql  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに、この例で示した XSD スキーマを追加します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleData.xml として保存します。 このファイルに、この例で前に示した XML ドキュメントを追加します。  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、このトピックの冒頭で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドのパラメーターとして指定されたファイルの適切なパスを指定します。  
  
5.  上の VBScript コードを実行します。 XML 一括読み込みによって、XML ドキュメントが Cust テーブルと CustOrder テーブルに読み込まれます。  
  
 これは、これと同等の XDR スキーマです。  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
<sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. スキーマでチェーン リレーションシップを使用して XML の一括読み込みを行う  
 この例では、XML 一括読み込みにおいて、マッピング スキーマで指定されている M:N リレーションシップを使用し、M:N リレーションシップを表すテーブルにデータを読み込む方法を示します。  
  
 たとえば、次の XSD スキーマを考えてみます。  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 このスキーマでは、 ** \<Product>** 子要素を持つ** \<Order>** 要素を指定します。 ** \<Order>** 要素は Ord テーブルにマップされ、 ** \<product>** 要素はデータベースの product テーブルにマップされます。 Product>要素に指定されているチェーンリレーションシップでは、orderdetail テーブルによって表される M:N リレーションシップが識別されます。 ** \<** つまり、1 つの注文には複数の製品が含まれ、1 つの製品は複数の注文に含まれるという関係です。  
  
 このスキーマで XML ドキュメントの一括読み込みを行うと、Ord テーブル、Product テーブル、および OrderDetail テーブルにレコードが追加されます。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  次の 3 つのテーブルを作成します。  
  
    ```sql  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  この例の最初で提供されているスキーマを SampleSchema.xml として保存します。  
  
3.  次のサンプル XML データを SampleXMLData.xml として保存します。  
  
    ```xml  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、このトピックの冒頭で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 この例のソース コードで、次の行のコメント指定をはずします。  
  
    ```vbs  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  VBScript コードを実行します。 XML 一括読み込みによって、XML ドキュメントが Ord テーブルと Product テーブルに読み込まれます。  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. ID 型の列に一括読み込みを行う  
 この例では、一括読み込みでの ID 型列の扱いについて説明します。 この例では、3 つのテーブル (Ord、Product、OrderDetail) にデータの一括読み込みが行われます。  
  
 これらのテーブルには、次の条件が設定されています。  
  
-   Ord テーブルの OrderID は ID 型の列です。  
  
-   Product テーブルの ProductID は ID 型の列です。  
  
-   OrderDetail の OrderID および ProductID 列は、Ord テーブルおよび Product テーブル内の対応する主キー列を参照する外部キー列です。  
  
 この例のテーブル スキーマを次に示します。  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 この XML 一括読み込みの例では、BulkLoad オブジェクトモデルの KeepIdentity プロパティが false に設定されています。 このため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、Product テーブルおよび Ord テーブルの ProductID 列および OrderID 列に ID 値がそれぞれ生成されます。一括読み込みの対象ドキュメントで指定されている値は無視されます。  
  
 この場合、XML 一括読み込みでは、テーブル間の主キー/外部キーのリレーションシップが識別されます。 一括読み込みでは、主キーのあるテーブルにレコードが挿入された後、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で生成された ID 値が、外部キー列のあるテーブルに格納されます。 次の XML 一括読み込みの例では、次の順序でテーブルにデータが挿入されます。  
  
1.  製品  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  この処理ロジックでは、Products テーブルと Orders テーブルで生成された ID 値を後で OrderDetails テーブルに挿入できるよう、XML 一括読み込みによってこれらの値が保持されます。 これにはまず、XML 一括読み込みで中間テーブルが作成され、このテーブルにデータが格納されます。格納された値は、後で削除されます。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  次のテーブルを作成します。  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 この XSD スキーマをこのファイルに追加します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに次の VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 **Execute**メソッドのパラメーターとして機能するファイルの適切なパスを指定します。  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  VBScript コードを実行します。 XML 一括読み込みによって、適切なテーブルにデータが読み込まれます。  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. 一括読み込み前にテーブル スキーマを生成する  
 一括読み込み前にテーブルが存在しない場合、XML 一括読み込みでテーブルを作成するように指定できます。 SQLXMLBulkLoad オブジェクトの SchemaGen プロパティを TRUE に設定すると、これが行われます。 また、必要に応じて、SGDropTables プロパティを TRUE に設定して、既存のテーブルを削除して再作成するために、XML 一括読み込みを要求することもできます。 次の VBScript の例では、これらのプロパティの使用法を示します。  
  
 また、この例では、これらの他に次の 2 つのプロパティを TRUE に設定します。  
  
-   CheckConstraints. : このプロパティを TRUE に設定すると、テーブルに指定されている制約違反が、テーブルに挿入されるデータによって発生するのを回避できます。この場合の制約は、Cust テーブルと CustOrder テーブル間に指定されている PRIMARY KEY/FOREIGN KEY 制約です。 制約違反が発生すると、一括読み込みは失敗します。  
  
-   XMLFragment. : サンプル XML ドキュメント (データ ソース) はフラグメントであり、単一の最上位要素が含まれていません。したがって、このプロパティを TRUE に設定する必要があります。  
  
 この VBScript コードは次のとおりです。  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに、前の例「スキーマでチェーン リレーションシップを使用して XML の一括読み込みを行う」で示した XSD スキーマを追加します。  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに、前の例「スキーマでチェーン リレーションシップを使用して XML の一括読み込みを行う」で示した XML ドキュメントを追加します。 \<ルート> 要素を (フラグメントにするために) ドキュメントから削除します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、この例で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドのパラメーターとして指定されたファイルの適切なパスを指定します。  
  
4.  VBScript コードを実行します。 XML 一括読み込みによって、指定されたマッピング スキーマを基に必要なテーブルが作成され、このテーブルにデータの一括読み込みが行われます。  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. ストリームから一括読み込みを行う  
 XML 一括読み込みオブジェクトモデルの Execute メソッドには、2つのパラメーターがあります。 最初のパラメーターはマッピング スキーマ ファイルであり、 もう 1 つのパラメーターは、データベースに読み込まれる XML データを指定するものです。 Xml データを XML 一括読み込みの Execute メソッドに渡すには、次の2つの方法があります。  
  
-   ファイル名をパラメーターとして指定する。  
  
-   XML データを含むストリームを渡す。  
  
 この例では、ストリームから一括読み込みを行う方法を示します。  
  
 VBScript はまず SELECT ステートメントが実行され、Northwind データベースの Customers テーブルから顧客情報が取得されます。 SELECT ステートメントには、FOR XML 句 (と ELEMENTS オプション) が指定されているため、クエリを実行すると、次の形式の、要素中心の XML ドキュメントが返されます。  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 次に、スクリプトは、2番目のパラメーターとして XML をストリームとして Execute メソッドに渡します。 Execute メソッドは、Cust テーブルにデータを一括読み込みします。  
  
 このスクリプトは、SchemaGen プロパティを TRUE に設定し、SGDropTables プロパティを TRUE に設定するため、XML 一括読み込みでは、指定されたデータベースに Cust テーブルが作成されます。 テーブルが存在する場合は、最初にテーブルが削除された後に再作成されます。  
  
 この VBScript の例を次に示します。  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 次の XSD マッピング スキーマでは、テーブルの作成に必要な情報が指定されます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 XDR スキーマの場合は次のようになります。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>既存のファイルのストリームを開く  
 また、既存の XML データファイルでストリームを開き、パラメーターとしてストリームをパラメーターとして渡すこともできます (ファイル名をパラメーターとして渡すのではなく)。  
  
 ストリームをパラメーターとして渡す Visual Basic の例を次に示します。  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 アプリケーションをテストするには、次の XML ドキュメントをファイル (SampleData.xml) に保存し、この例で提供されている XSD スキーマと共に使用します。  
  
 XML ソース データ (SampleData.xml) は次のとおりです。  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Hanari Carnes</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Toms Spezialitten</CompanyName>  
     <City>LA</City>  
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Victuailles en stock</CompanyName>  
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. オーバーフロー列に一括読み込みを行う  
 マッピングスキーマで**sql: overflow フィールド**の注釈を使用してオーバーフロー列が指定されている場合、XML 一括読み込みでは、ソースドキュメントからこの列にすべての未使用データがコピーされます。  
  
 次の XSD スキーマを考えてみます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 このスキーマでは、Cust テーブルにオーバーフロー列 (OverflowColumn) が指定されています。 その結果、各** \<顧客>** 要素のすべての未使用 XML データがこの列に追加されます。  
  
> [!NOTE]  
>  すべての抽象要素 ( **abstract = "true"** が指定されている要素) と、禁止されているすべての属性 ( **"true"** が指定されている属性) は、XML 一括読み込みによってオーバーフローと見なされ、指定されている場合はオーバーフロー列に追加されます。 それ以外の場合は無視されます。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  **Tempdb**データベースに2つのテーブルを作成します。  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに、この例で示した XSD スキーマを追加します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
        <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに次の Microsoft Visual Basic Scripting Edition (VBScript) コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドのパラメーターとして指定されたファイルの適切なパスを指定します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  VBScript コードを実行します。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"   
                       sql:overflow-field="OverflowColumn"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H. トランザクション モードで一時ファイル用のファイル パスを指定する  
 トランザクションモードで一括読み込みを行う場合 (つまり、Transaction プロパティが TRUE に設定されている場合)、次のいずれかの条件に該当する場合は、TempFilePath プロパティも設定する必要があります。  
  
-   リモート サーバーに一括読み込みを行う。  
  
-   トランザクション モードで作成される一時ファイルの格納に、TEMP 環境変数で指定されているパスとは別のローカル ドライブまたはフォルダーを使用する。  
  
 たとえば、次の VBScript コードでは、SampleXMLData.xml ファイルからデータベース テーブルに、トランザクション モードでデータの一括読み込みが行われます。 TempFilePath プロパティは、トランザクションモードで生成される一時ファイルのパスを設定するために指定されます。  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  一時ファイルのパスは、対象の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのサービス アカウントと、一括読み込みアプリケーションを実行するアカウントからの共有アクセスが可能な場所にする必要があります。 ローカルサーバーで一括読み込みを行う場合を除き、一時ファイルのパスは UNC パス (\servername\sharename など\\) である必要があります。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  **Tempdb**データベースに次のテーブルを作成します。  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 次の XSD スキーマをファイルに追加します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに次の VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドのパラメーターとして指定されたファイルの適切なパスを指定します。 また、TempFilePath プロパティに適切なパスを指定します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  VBScript コードを実行します。  
  
     **Customerid**の値が、次のように中かっこ ({および}) を含む GUID として指定されている場合、スキーマでは**customerid**属性に対応する**sql: datatype**を指定する必要があります。  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     更新されたスキーマは次のようになります。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     列の型が**uniqueidentifier**として指定されて**いる場合、** 一括読み込み操作では、列に挿入する前に、 **CustomerID**値から中かっこ ({および}) を削除します。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. 既存のデータベース接続で ConnectionCommand プロパティを使用する  
 既存の ADO 接続を使用して、XML の一括読み込みを行うことができます。 これは、データ ソースに実行する多くの操作のうちの 1 つとして XML 一括読み込みを行う場合に便利です。  
  
 ConnectionCommand プロパティを使用すると、ADO コマンドオブジェクトを使用して、既存の ADO 接続を使用できます。 この Visual Basic の例を次に示します。  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  **Tempdb**データベースに2つのテーブルを作成します。  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 次の XSD スキーマをファイルに追加します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="CustCustOrder"  
              parent="Cust"  
              parent-key="CustomerID"  
              child="CustOrder"  
              child-key="CustomerID" />  
      </xsd:appinfo>  
    </xsd:annotation>  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:sequence>  
           <xsd:element name="CustomerID"  type="xsd:integer" />  
           <xsd:element name="CompanyName" type="xsd:string" />  
           <xsd:element name="City"        type="xsd:string" />  
           <xsd:element name="Order"   
                              sql:relation="CustOrder"  
                              sql:relationship="CustCustOrder" >  
             <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Visual Basic (標準 EXE) アプリケーションと、上のコードを作成し、 プロジェクトに次の参照を追加します。  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  アプリケーションを実行します。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
         <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. xml データ型の列に一括読み込みを行う  
 マッピングスキーマで**sql: datatype = "xml"** 注釈を使用して[xml データ型](../../../t-sql/xml/xml-transact-sql.md)の列が指定されている場合、xml 一括読み込みでは、マップされたフィールドの xml 子要素をソースドキュメントからこの列にコピーできます。  
  
 次の XSD スキーマを考えてみます。この XSD スキーマでは、サンプル データベース AdventureWorks の Production.ProductModel テーブルのビューがマップされます。 このテーブルでは、 **xml**データ型の catalogdescription フィールドは、 **sql: field**および**sql: datatype = "xml"** 注釈を使用して** \<Desc>** 要素にマップされます。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  サンプル データベース AdventureWorks がインストールされていることを確認します。  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに上の XSD スキーマをコピーして貼り付け、ファイルを保存します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントをコピーして貼り付け、前の手順と同じフォルダーに保存します。  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="https://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、BulkloadXml.vbs として保存します。 このファイルに次の VBScript コードをコピーして貼り付け、 前の XML データ ファイルとスキーマ ファイルを保存したフォルダーに保存します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  スクリプト BulkloadXml.vbs を実行します。  
  
  
