---
title: DiffGram の例 (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6fe05c49f44bc0e210687b63e0eb8878b479a07f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257265"
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram の例 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  ここでは、データベースに対して挿入、変更、および削除の各操作を実行する DiffGram の例を示します。 例を使用する前に、次のことに注意してください。  
  
-   例では、2 つのテーブル (Cust と Ord) を使用します。したがって、DiffGram の例をテストするにはこれらを作成する必要があります。  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   ほとんどの例では、次の XSD スキーマを使用します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     このスキーマを、例で使用する他のファイルと同じフォルダーに DiffGramSchema.xml として保存してください。  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. DiffGram を使用してレコードを削除する  
 この例の DiffGram では、CustomerID が ALFKI の顧客レコードを Cust テーブルから削除し、OrderID が 1 の、対応する注文レコードを Ord テーブルから削除します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 ** \<** ** \<Before>** block には、Order>要素 (Customer1 **: id = "Order1"**) と** \<Customer>** 要素 (**diffgram: id = ""**) があります。 これらの要素はデータベースの既存のレコードを表します。 ** \<Datainstance>** 要素には、対応するレコードがありません (同一の場合は、 **id**)。 これは削除操作を表します。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  これらのテーブルを**tempdb**データベースに作成します。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. DiffGram を使用してレコードを挿入する  
 この例の DiffGram では、Cust テーブルと Ord テーブルにレコードを挿入します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 この DiffGram では** \<>** ブロックが指定されていません (既存のデータベースレコードが特定されていません)。 Cust テーブルと Ord テーブルにマップされている2つのレコードインスタンス ( ** \<顧客>** と** \<** 、 ** \<datainstance>** block の>要素によって識別される) があります。 これらの要素はどちらも **、** "属性の変更" 属性 (**haschanges = "inserted"**) を指定します。 これは挿入操作を表します。 この DiffGram では、 **Haschanges = "modified"** を指定した場合、存在しないレコードを変更しようとするとエラーになります。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  これらのテーブルを**tempdb**データベースに作成します。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. DiffGram を使用して既存のレコードを更新する  
 この例では、DiffGram で顧客 ALFKI の顧客情報 (CompanyName と ContactName) を更新します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 ** \<Before>** ブロックには、 ** \<Customer>** 要素 (**Customer1**) が含まれています。 ** \<Datainstance>** block には、同じ**id**を持つ対応する** \<Customer>** 要素が含まれています。Newdataset>の** \<customer>** 要素では、[変更後のデータ] を指定することもできます。 **haschanges = "modified"** です。 ** \<** これは更新操作であることを示し、 **Cust**テーブルの顧客レコードがそれに応じて更新されます。 DiffGram **: hasChanges**属性が指定されていない場合、diffgram 処理ロジックはこの要素を無視し、更新は実行されないことに注意してください。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  これらのテーブルを**tempdb**データベースに作成します。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. DiffGram を使用して、レコードの挿入、更新、および削除を実行する  
 この例では、比較的複雑な DiffGram を使用して、挿入、更新、および削除操作を実行します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 この DiffGram は、DiffGram のロジックにより次のように処理されます。  
  
-   DiffGram 処理ロジックに従うと、マッピングスキーマで説明されているように、 ** \<before>** ブロックの最上位レベルのすべての要素が対応するテーブルにマップされます。  
  
-   ** \<Before>** ブロックには、 ** \<Order>** 要素 (**dffgr: id = "Order1"**) と** \<Customer>** 要素 (**Customer1**) があります。この要素は、 ** \<datainstance>** ブロック (同じ id) に対応する要素が存在しません。 これは削除操作を表し、レコードは Cust テーブルと Ord テーブルから削除されます。  
  
-   ** \<** ** \<** ** \<Before>** ブロックには、customer>要素 (例 **: id = "Customer2"**) があります。この要素には、(同じ id の) datainstance>ブロックに対応する customer>要素があります。 ** \<** Datainstance>ブロック内の要素では、次のように指定します。 **haschanges = "modified"**。 ** \<** これは更新操作であり、顧客 ANATR に対して、 ** \<datainstance>** block で指定された値を使用して、Cust テーブルの CompanyName との情報が更新されます。  
  
-   ** \<** ** \<** **** ** \<Datainstance>** ブロックには、Customer>要素 (Order3: id = "Customer3") と Order>要素 (**diffgram: id = ""**) があります。 これらの要素のどちらにも、 **diffgram: hasChanges**属性が指定されていません。 このため、DiffGram の処理ロジックで、これらの要素は無視されます。  
  
-   ** \<** \< ** \<** **** ** \<Datainstance>** ブロックには、Customer>要素 (Order4 **: id = "Customer4"**) と Order>要素 () があります。この要素には、before> ブロックに対応する要素がありません。 Datainstance>ブロック内のこれらの要素は、次のように指定します **: haschanges = "inserted"**。 ** \<** このため、新しいレコードが Cust テーブルと Ord テーブルに追加されます。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  次のテーブルを**tempdb**データベースに作成します。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  次のサンプル データを追加します。  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. DiffGram で diffgr:parentID 注釈を指定して更新を適用する  
 この例は、更新プログラムを適用するときに、DiffGram の** \<before>** ブロックで指定されている**parentID**注釈を使用する方法を示しています。  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 この DiffGram では、 ** \<before>** ブロックのみが存在するため、削除操作を指定します。 DiffGram では、 **parentID**注釈を使用して、注文と注文の詳細の間に親子リレーションシップを指定します。 SQLXML でレコードが削除されるときには、このリレーションシップで指定された子テーブルからレコードが削除された後、対応する親テーブルからレコードが削除されます。  
  
  
