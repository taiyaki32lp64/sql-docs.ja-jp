---
title: DiffGram の例 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 38bee43ed5b727bca552c1b44010dd692012d823
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012972"
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram の例 (SQLXML 4.0)
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
  
 **\<する前に >** が、ブロック、 **\<順序 >** 要素 (**diffgr:id ="Order1"** ) と **\<顧客 >** 要素 (**diffgr:id ="Customer1"** )。 これらの要素はデータベースの既存のレコードを表します。 **\<DataInstance >** 要素に対応するレコードがありません (同じ **diffgr:id**)。 これは削除操作を表します。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  これらのテーブルを作成、 **tempdb**データベース。  
  
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
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
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
  
 この DiffGram で、 **\<する前に >** ブロックが指定されていない (既存のデータベース レコード)。 2 つのレコード インスタンスがある (で識別される、 **\<顧客 >** と **\<順序 >** 内の要素、  **\<DataInstance >** ブロック) それぞれ Cust と Ord テーブルにマップされます。 これらの要素の両方を指定、 **diffgr:hasChanges**属性 (**hasChanges ="inserted"** )。 これは挿入操作を表します。 指定した場合、この DiffGram で**hasChanges ="modified"** 、その結果、エラーが存在しないレコードを変更することを示します。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  これらのテーブルを作成、 **tempdb**データベース。  
  
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
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
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
  
 **\<する前に >** ブロックが含まれています、 **\<顧客 >** 要素 (**diffgr:id ="Customer1"** )。 **\<DataInstance >** ブロックに含まれる、対応する **\<顧客 >** 要素と同じ **id**します。 **\<顧客 >** 内の要素、 **\<NewDataSet >** も指定 **diffgr:hasChanges ="modified"** します。 これは、更新操作、および顧客レコードを示します、 **Cust**テーブルがそれに応じて更新されます。 その場合、 **diffgr:hasChanges**属性が指定されていない、DiffGram の処理ロジックがこの要素は無視されます、および更新は実行されません。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  これらのテーブルを作成、 **tempdb**データベース。  
  
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
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
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
  
-   DiffGram の処理ロジックで内のすべての最上位要素、 **\<する前に >** マッピング スキーマ」の説明に従って、対応するテーブルにマップをブロックします。  
  
-   **\<する前に >** ブロックには、 **\<順序 >** 要素 (**dffgr:id ="Order1"** ) と **\<顧客>** 要素 (**diffgr:id ="Customer1"** ) がないの対応する要素の **\<DataInstance >** (同じ ID) をブロックします。 これは削除操作を表し、レコードは Cust テーブルと Ord テーブルから削除されます。  
  
-   **\<する前に >** ブロックには、 **\<顧客 >** 要素 (**diffgr:id ="Customer2"** ) が対応する **\<顧客 >** 内の要素、 **\<DataInstance >** (同じ ID) をブロックします。 内の要素、  **\<DataInstance >** ブロックを指定します**diffgr:hasChanges ="modified"** します。 これは顧客 ANATR、CompanyName と ContactName の情報が更新で指定されている値を使用して、Cust テーブルに update 操作、  **\<DataInstance >** ブロックします。  
  
-   **\<DataInstance >** ブロックには、 **\<顧客 >** 要素 (**diffgr:id ="Customer3"** ) および **\<順序 >** 要素 (**diffgr:id ="Order3"** )。 これらの要素のどちらが指定されて、 **diffgr:hasChanges**属性。 このため、DiffGram の処理ロジックで、これらの要素は無視されます。  
  
-   **\<DataInstance >** ブロックには、 **\<顧客 >** 要素 (**diffgr:id ="Customer4"** ) および **\<順序 >** 要素 (**diffgr:id ="Order4"** ) がないに対応する要素、\<する前に > ブロックします。 これらの要素を **\<DataInstance >** ブロック指定**diffgr:hasChanges ="inserted"** します。 このため、新しいレコードが Cust テーブルと Ord テーブルに追加されます。  
  
#### <a name="to-test-the-diffgram"></a>DiffGram をテストするには  
  
1.  次のテーブルを作成、 **tempdb**データベース。  
  
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
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  上の DiffGram をコピーして、テキスト ファイルに貼り付け、 前の手順と同じフォルダーに MyDiffGram.xml として保存します。  
  
4.  前で提供されている DiffGramSchema をコピーして、テキスト ファイルに貼り付け、 DiffGramSchema.xml として保存します。  
  
5.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用して DiffGram を実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. DiffGram で diffgr:parentID 注釈を指定して更新を適用する  
 この例では方法、 **parentID**注釈で指定されている、 **\<する前に >** 更新プログラムを適用することで、DiffGram のブロックを使用します。  
  
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
  
 のみがあるため、この DiffGram は削除操作を指定します、 **\<する前に >** ブロックします。 Diffgram で、 **parentID**注釈を使用して、注文と注文の詳細の間の親子リレーションシップを指定します。 SQLXML でレコードが削除されるときには、このリレーションシップで指定された子テーブルからレコードが削除された後、対応する親テーブルからレコードが削除されます。  
  
  
