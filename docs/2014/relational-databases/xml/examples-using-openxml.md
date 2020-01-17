---
title: '例: OPENXML の使用 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- XML [SQL Server], mapping data
- OPENXML statement, about OPENXML statement
- overflow in XML document [SQL Server]
- mapping XML data [SQL Server]
- combining attribute-centric and element centric mapping
- unconsumed data
- attribute-centric mapping
- column patterns [XML in SQL Server]
- XML [SQL Server], overflow handling
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- flags parameter
- element-centric mapping [SQL Server]
- edge tables
ms.assetid: 689297f3-adb0-4d8d-bf62-cfda26210164
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61c5fc1cb0692d22f110958b894ac2eb7c2af4cf
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874694"
---
# <a name="examples-using-openxml"></a>例: OPENXML の使用
  このトピックの例では、OPENXML を使用して XML ドキュメントの行セット ビューを作成する方法を示します。 OPENXML の構文の詳細については、「 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)」を参照してください。 ここに示す例では、OPENXML でのメタプロパティの指定を除く OPENXML のすべての側面を示します。 OPENXML のメタプロパティの指定方法の詳細については、「 [OPENXML 内でのメタプロパティの指定](specify-metaproperties-in-openxml.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 データを取得する際に、 *rowpattern* を使用して、XML ドキュメント内の行を決定するノードを識別します。 また、 *rowpattern* は、MSXML XPath の実装で使用される XPath パターン言語で表現されます。 たとえば、パターンが要素や属性になる場合、 *rowpattern*で選択される要素や属性のノードごとに行が作成されます。  
  
 *flags* 値は、既定のマッピングを指定します。 *SchemaDeclaration* で *ColPattern*が指定されていない場合、 *flags* で指定されたマッピングが想定されます。 *SchemaDeclaration* で *ColPattern* が指定されている場合、 *flags*の値は無視されます。 指定された *ColPattern* により、マッピング、属性中心か要素中心か、さらにオーバーフロー データと未使用データを処理するときの動作が決まります。  
  
### <a name="a-executing-a-simple-select-statement-with-openxml"></a>A. OPENXML を使用した単純な SELECT ステートメントの実行  
 この例の XML ドキュメントは、<`Customer`> 要素、<`Order`> 要素、および <`OrderDetail`> 要素で構成されます。 OPENXML ステートメントでは、XML ドキュメントから顧客情報が 2 列の行セット (**CustomerID** と **ContactName**) で取得されます。  
  
 最初に、 **sp_xml_preparedocument** ストアド プロシージャを呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルを OPENXML に渡します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   *rowpattern* (/ROOT/Customer) により、処理する <`Customer`> ノードが識別されます。  
  
-   *flags* パラメーター値を **1** に設定し、属性中心のマッピングを示します。 その結果、XML 属性は *SchemaDeclaration*で定義される行セットの列にマップされます。  
  
-   WITH 句の *SchemaDeclaration*では、指定された *ColName* 値は対応する XML 属性の名前と一致します。 したがって、 *SchemaDeclaration* では *ColPattern*パラメーターが指定されていません。  
  
 次に、SELECT ステートメントにより、OPENXML で提供される行セット内のすべての列が取得されます。  
  
```  
DECLARE @DocHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @DocHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@DocHandle, '/ROOT/Customer',1)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @DocHandle  
```  
  
 結果を次に示します。  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 `Customer`flags*を要素中心のマッピングを示す*2 **に設定して同じ SELECT ステートメントを実行すると、<** > 要素にはサブ要素がないので、両方の顧客の **CustomerID** と **ContactName** の値が NULL として返されます。  
  
 また、@xmlDocument を **xml** 型や **(n)varchar(max)** 型にすることもできます。  
  
 XML ドキュメント内で <`CustomerID`> と <`ContactName`> がサブ要素の場合は、要素中心のマッピングにより値が取得されます。  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer>  
   <CustomerID>VINET</CustomerID>  
   <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer>     
   <CustomerID>LILAS</CustomerID>  
   <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT    *  
FROM      OPENXML (@XmlDocumentHandle, '/ROOT/Customer',2)  
           WITH (CustomerID  varchar(10),  
                 ContactName varchar(20))  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 結果を次に示します。  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 **sp_xml_preparedocument** から返されたドキュメント ハンドルは、セッション内ではなく、バッチが実行されている間は有効であることに注意してください。  
  
### <a name="b-specifying-colpattern-for-mapping-between-rowset-columns-and-the-xml-attributes-and-elements"></a>b. 行セットの列と XML の属性や要素の間でマッピングを行うための ColPattern の指定  
 この例では、省略可能な *ColPattern* パラメーターに XPath パターンを指定して、行セットの列と XML の属性や要素の間でマッピングを行う方法を示します。  
  
 この例の XML ドキュメントは、<`Customer`> 要素、<`Order`> 要素、および <`OrderDetail`> 要素で構成されます。 OPENXML ステートメントにより、XML ドキュメントから顧客情報と注文情報が 1 つの行セット (**CustomerID**、**OrderDate**、**ProdID**、および **Qty**) として取得されます。  
  
 最初に、 **sp_xml_preparedocument** ストアド プロシージャを呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルを OPENXML に渡します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail) により、処理する <`OrderDetail`> ノードが識別されます。  
  
 ここでは説明のために、*flags* パラメーター値を **2** に設定して、要素中心のマッピングを示しています。 ただし、このマッピングは *ColPattern* に指定したマッピングによって上書きされます。 つまり、 *ColPattern* に指定した XPath パターンにより、行セットの列が属性にマップされます。 この結果、属性中心のマッピングになります。  
  
 WITH 句の *SchemaDeclaration*では、 *ColName* パラメーターと *ColType* パラメーターを使用して *ColPattern* も指定されています。 省略可能な *ColPattern* は指定された XPath パターンで、次のことを示します。  
  
-   行セットの **OrderID** 列、**CustomerID** 列、および **OrderDate** 列は *rowpattern* によって識別されたノードの親の属性にマップされ、*rowpattern* によって <`OrderDetail`> ノードが識別されます。 したがって、**CustomerID** 列と **OrderDate** 列は < **> 要素の** CustomerID**属性と**OrderDate`Order` 属性にマップされます。  
  
-   行セットの **ProdID** 列と **Qty** 列は、**rowpattern** で識別されたノードの **ProductID** 属性と *Quantity* 属性にマップされます。  
  
 次に、SELECT ステートメントにより、OPENXML で提供される行セット内のすべての列が取得されます。  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT stmt using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@XmlDocumentHandle, '/ROOT/Customer/Order/OrderDetail',2)  
WITH (OrderID     int         '../@OrderID',  
      CustomerID  varchar(10) '../@CustomerID',  
      OrderDate   datetime    '../@OrderDate',  
      ProdID      int         '@ProductID',  
      Qty         int         '@Quantity')  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 結果を次に示します。  
  
```  
OrderID CustomerID        OrderDate          ProdID    Qty  
-------------------------------------------------------------  
10248    VINET     1996-07-04 00:00:00.000     11       12  
10248    VINET     1996-07-04 00:00:00.000     42       10  
10283    LILAS     1996-08-16 00:00:00.000     72        3  
```  
  
 *ColPattern* として指定した XPath パターンを、行セットの列に XML 要素をマップするために指定することもできます。 この結果、要素中心のマッピングになります。 次の例では、XML ドキュメントの <`CustomerID`> と <`OrderDate`> は、<`Orders`> 要素のサブ要素です。 *ColPattern* により *flags* パラメーターに指定されたマッピングが上書きされるので、OPENXML では *flags* パラメーターを指定しません。  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order EmployeeID="5" >  
      <OrderID>10248</OrderID>  
      <CustomerID>VINET</CustomerID>  
      <OrderDate>1996-07-04T00:00:00</OrderDate>  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order  EmployeeID="3" >  
      <OrderID>10283</OrderID>  
      <CustomerID>LILAS</CustomerID>  
      <OrderDate>1996-08-16T00:00:00</OrderDate>  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail')  
WITH (CustomerID  varchar(10)   '../CustomerID',  
      OrderDate   datetime      '../OrderDate',  
      ProdID      int           '@ProductID',  
      Qty         int           '@Quantity')  
EXEC sp_xml_removedocument @docHandle  
```  
  
### <a name="c-combining-attribute-centric-and-element-centric-mapping"></a>C. 属性中心のマッピングと要素中心のマッピングの組み合わせ  
 この例では、 *flags* パラメーターを **3** に設定し、属性中心のマッピングと要素中心のマッピングの両方が適用されることを示します。 この場合、まだ処理されていないすべての列に対して、まず属性中心のマッピングが適用されてから、次に要素中心のマッピングが適用されます。  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument =N'<ROOT>  
<Customer CustomerID="VINET"  >  
     <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" >   
     <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer',3)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @docHandle  
```  
  
 結果  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 **CustomerID** に属性中心のマッピングが適用されます。 < **> 要素には** ConzｘtactName`Customer` 属性がありません。 そのため、要素中心のマッピングが適用されます。  
  
### <a name="d-specifying-the-text-xpath-function-as-colpattern"></a>D. ColPattern としての text() XPath 関数の指定  
 この例の XML ドキュメントは、<`Customer`> 要素および <`Order`> 要素で構成されます。 OPENXML ステートメントにより、< **> 要素の** oid`Order` 属性、*rowpattern* で識別されるノードの親の ID、および要素のコンテンツのリーフ値の文字列で構成される行セットが取得されます。  
  
 最初に、 **sp_xml_preparedocument** ストアド プロシージャを呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルを OPENXML に渡します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   *rowpattern* (/root/Customer/Order) により、処理する <`Order`> ノードが識別されます。  
  
-   *flags* パラメーター値を **1** に設定し、属性中心のマッピングを示します。 その結果、XML 属性は *SchemaDeclaration*で定義される行セットの列にマップされます。  
  
-   WITH 句の *SchemaDeclaration* では、行セットの列名である **oid** と **amount** が対応する XML 属性の名前と一致します。 したがって、 *ColPattern* パラメーターは指定されません。 行セット内の **comment** 列では、XPath 関数 **text()** が *ColPattern*に指定されています。 これにより、 *flags*に指定された属性中心のマッピングが上書きされ、列には要素コンテンツのリーフ値の文字列が含まれます。  
  
 次に、SELECT ステートメントにより、OPENXML で提供される行セット内のすべての列が取得されます。  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied  
      </Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
            <Urgency>Important</Urgency>  
            Happy Customer.  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH (oid     char(5),   
           amount  float,   
           comment ntext 'text()')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 結果を次に示します。  
  
```  
oid   amount        comment  
----- -----------   -----------------------------  
O1    3.5           NULL  
O2    13.4          Customer was very satisfied  
O3    100.0         Happy Customer.  
O4    10000.0       NULL  
```  
  
### <a name="e-specifying-tablename-in-the-with-clause"></a>E. WITH 句での TableName の指定  
 この例では、WITH 句に *SchemaDeclaration* ではなく *TableName*を指定します。 この指定は、目的の構造のテーブルがあり、列パターンの *ColPattern* パラメーターが必要ない場合に役立ちます。  
  
 この例の XML ドキュメントは、<`Customer`> 要素および <`Order`> 要素で構成されます。 OPENXML ステートメントでは、XML ドキュメントから注文情報が 3 列の行セット (**oid**、**date**、および **amount**) に取得されます。  
  
 最初に、 **sp_xml_preparedocument** ストアド プロシージャを呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルを OPENXML に渡します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   *rowpattern* (/root/Customer/Order) により、処理する <`Order`> ノードが識別されます。  
  
-   WITH 句には *SchemaDeclaration* がありません。 代わりに、テーブル名が指定されています。 そのため、行セット スキーマとしてテーブル スキーマが使用されます。  
  
-   *flags* パラメーター値を **1** に設定し、属性中心のマッピングを示します。 したがって、 *rowpattern*で識別される要素の属性は、同じ名前の行セット列にマップされます。  
  
 次に、SELECT ステートメントにより、OPENXML で提供される行セット内のすべての列が取得されます。  
  
```  
-- Create a test table. This table schema is used by OPENXML as the  
-- rowset schema.  
CREATE TABLE T1(oid char(5), date datetime, amount float)  
GO  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
-- Sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH T1  
EXEC sp_xml_removedocument @docHandle  
```  
  
 結果を次に示します。  
  
```  
oid   date                        amount  
----- --------------------------- ----------  
O1    1996-01-20 00:00:00.000     3.5  
O2    1997-04-30 00:00:00.000     13.4  
O3    1999-07-14 00:00:00.000     100.0  
O4    1996-01-20 00:00:00.000     10000.0  
```  
  
### <a name="f-obtaining-the-result-in-an-edge-table-format"></a>F. エッジ テーブル形式での結果の取得  
 この例では、OPENXML ステートメントに WITH 句が指定されていません。 その結果、OPENXML で生成される行セットがエッジ テーブル形式になります。 SELECT ステートメントにより、エッジ テーブル内のすべての列が返されます。  
  
 この例のサンプル XML ドキュメントは、<`Customer`> 要素、<`Order`> 要素、および <`OrderDetail`> 要素で構成されます。  
  
 最初に、 **sp_xml_preparedocument** ストアド プロシージャを呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルを OPENXML に渡します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   *rowpattern* (/ROOT/Customer) により、処理する <`Customer`> ノードが識別されます。  
  
-   WITH 句は指定されていません。 したがって、OPENXML により、行セットがエッジ テーブル形式で返されます。  
  
 次に、SELECT ステートメントにより、エッジ テーブル内のすべての列が取得されます。  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
SET @xmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer')  
  
EXEC sp_xml_removedocument @docHandle  
```  
  
 結果はエッジ テーブルとして返されます。 エッジ テーブルに対するクエリを作成して、情報を取得できます。 例 :  
  
-   次のクエリにより、ドキュメント内の **Customer** ノードの数が返されます。 WITH 句が指定されていないので、OPENXML からエッジ テーブルが返されます。 SELECT ステートメントにより、エッジ テーブルへのクエリが実行されます。  
  
    ```  
    SELECT count(*)  
    FROM OPENXML(@docHandle, '/')  
    WHERE localname = 'Customer'  
    ```  
  
-   次のクエリにより、要素型の XML ノードのローカル名が返されます。  
  
    ```  
    SELECT distinct localname   
    FROM OPENXML(@docHandle, '/')   
    WHERE nodetype = 1   
    ORDER BY localname  
    ```  
  
### <a name="g-specifying-rowpattern-ending-with-an-attribute"></a>G. 属性で終了する rowpattern の指定  
 この例の XML ドキュメントは、<`Customer`> 要素、<`Order`> 要素、および <`OrderDetail`> 要素で構成されます。 OPENXML ステートメントにより、XML ドキュメントから注文明細の情報が 3 列の行セット (**ProductID**、**Quantity**、および **OrderID**) で取得されます。  
  
 最初に、 **sp_xml_preparedocument** を呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルを OPENXML に渡します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail/\@ProductID) は、XML 属性 **ProductID** で終了します。 結果の行セットでは、XML ドキュメント内で選択した属性ノードごとに行が作成されます。  
  
-   この例では、 *flags* パラメーターは指定されていません。 代わりに、 *ColPattern* パラメーターによってマッピングを指定します。  
  
 WITH 句の *SchemaDeclaration* では、 *ColName* パラメーターと *ColType* パラメーターを使用して *ColPattern* も指定されています。 省略可能な *ColPattern* は、次のことを示すために指定する XPath パターンです。  
  
-   行セット内の **ProdID** 列の *ColPattern* に指定された XPath パターン ( **.** ) により、コンテキスト ノード (現在のノード) が識別されます。 指定された *rowpattern* によって、これは、< **> 要素の** ProductID`OrderDetail` 属性となります。  
  
-   行セット内の *Qty* 列に指定された **ColPattern\@ である** ../**Quantity** により、コンテキスト ノード **ProductID> の親ノードである <** > の `OrderDetail`Quantity\< 属性が識別されます。  
  
-   同様に、行セット内の *OID* 列に指定された **ColPattern\@ である** ../../**OrderID** により、コンテキスト ノードの親ノードの親である < **> の** OrderID`Order` 属性が識別されます。 親ノードは <`OrderDetail`> で、コンテキスト ノードは <`ProductID`> です。  
  
 次に、SELECT ステートメントにより、OPENXML で提供される行セット内のすべての列が取得されます。  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--Sample XML document  
SET @xmlDocument =N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail/@ProductID')  
       WITH ( ProdID  int '.',  
              Qty     int '../@Quantity',  
              OID     int '../../@OrderID')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 結果を次に示します。  
  
```  
ProdID      Qty         OID  
----------- ----------- -------   
11          12          10248  
42          10          10248  
72          3           10283  
```  
  
### <a name="h-specifying-an-xml-document-that-has-multiple-text-nodes"></a>H. 複数のテキスト ノードを含む XML ドキュメントの指定  
 XML ドキュメント内に複数のテキスト ノードがある場合、 *ColPattern*である **text()** が指定された SELECT ステートメントにより、すべてのテキスト ノードではなく最初のテキスト ノードだけが返されます。 例 :  
  
```  
DECLARE @h int  
EXEC sp_xml_preparedocument @h OUTPUT,  
         N'<root xmlns:a="urn:1">  
           <a:Elem abar="asdf">  
             T<a>a</a>U  
           </a:Elem>  
         </root>',  
         '<ns xmlns:b="urn:1" />'  
  
SELECT * FROM openxml(@h, '/root/b:Elem')  
      WITH (Col1 varchar(20) 'text()')  
EXEC sp_xml_removedocument @h  
```  
  
 SELECT ステートメントでは、結果として **TaU** ではなく **T**が返されます。  
  
### <a name="i-specifying-the-xml-data-type-in-the-with-clause"></a>I. WITH 句での xml データ型の指定  
 WITH 句では、 **xml** データ型の列にマップされる列パターンが型指定されているかどうかにかかわらず、この列パターンから、空のシーケンスまたは要素のシーケンス、処理命令、テキスト ノード、およびコメントが返されます。 データは **xml** データ型にキャストされます。  
  
 次の例では、WITH 句のテーブル スキーマ宣言に **xml** 型の列が含まれています。  
  
```  
DECLARE @h int  
DECLARE @x xml  
set @x = '<Root>  
  <row id="1"><lname>Duffy</lname>  
   <Address>  
            <Street>111 Maple</Street>  
            <City>Seattle</City>  
   </Address>  
  </row>  
  <row id="2"><lname>Wang</lname>  
   <Address>  
            <Street>222 Pine</Street>  
            <City>Bothell</City>  
   </Address>  
  </row>  
</Root>'  
  
EXEC sp_xml_preparedocument @h output, @x  
SELECT *  
FROM   OPENXML (@h, '/Root/row', 10)  
      WITH (id int '@id',  
  
            lname    varchar(30),  
            xmlname  xml 'lname',  
            OverFlow xml '@mp:xmltext')  
EXEC sp_xml_removedocument @h  
```  
  
 具体的には、**xml** 型の変数 (\@x) を **sp_xml_preparedocument()** 関数に渡しています。  
  
 結果を次に示します。  
  
```  
id  lname   xmlname                   OverFlow  
--- ------- ------------------------------ -------------------------------  
1   Duffy   <lname>Duffy</lname>  <row><Address>  
                                   <Street>111 Maple</Street>  
                                   <City>Seattle</City>  
                                  </Address></row>  
2   Wang    <lname>Wang</lname>   <row><Address>  
                                    <Street>222 Pine</Street>  
                                    <City>Bothell</City>  
                                   </Address></row>  
```  
  
 結果では、次の点に注意してください。  
  
-   **varchar(30)** 型の **lname** 列の場合、この列の値が対応する <`lname`> 要素から取得されます。  
  
-   **xml** 型の **xmlname** 列では、この列の値として同じ名前の要素が返されます。  
  
-   フラグは 10 に設定されます。 10 は 2 + 8 を意味し、2 は要素中心のマッピングを示します。8 は未使用の XML データのみを WITH 句で定義した OverFlow 列に追加する必要があることを示します。 フラグを 2 に設定すると、WITH 句で指定された OverFlow 列に XML ドキュメント全体がコピーされます。  
  
-   WITH 句の列が型指定された XML 列で、XML インスタンスがスキーマに準拠しない場合、エラーが返されます。  
  
### <a name="j-retrieving-individual-values-from-multivalued-attributes"></a>J. 複数の値の属性から個別の値の取得  
 XML ドキュメントには、複数の値を指定できる属性を含めることができます。 たとえば、 **IDREFS** 属性には複数の値を指定できます。 XML ドキュメントでは、複数の値の属性値を、各値をスペースで区切った文字列として指定します。 次の XML ドキュメントでは、**Student> 要素の** attends\< 属性と **Class> 要素の** attendedBy\< 属性に複数の値を指定できます。 複数の値を指定できる XML 属性から値を個別に取得し、各値をデータベース内の別々の行に格納するには、新たな作業が必要です。 この例ではその処理を示します。  
  
 このサンプル XML ドキュメントは、次の要素で構成されます。  
  
-   \<Student>  
  
     **id** (学生 ID) 属性、**name** 属性、および **attends** 属性。 **attends** 属性には複数の値を指定できます。  
  
-   \<Class>  
  
     **id** (クラス ID) 属性、**name** 属性、および **attendedBy** 属性。 **attendedBy** 属性には複数の値を指定できます。  
  
 **Student> の** attends\< 属性と **Class> の** attendedBy\< 属性は、Student テーブルと Class テーブル間の **m:n** リレーションシップを表します。 学生は多くのクラスを受講でき、クラスは多くの学生を受け入れることができます。  
  
 次に示すように、このドキュメントを細分化し、データベースに保存するとします。  
  
-   \<Student> データは Students テーブルに保存します。  
  
-   \<Class> データは Courses テーブルに保存します。  
  
-   Student と Class 間の **m:n** リレーションシップ データは、CourseAttendence テーブルに保存します。 値を抽出するには、新たな作業が必要です。 この情報を取得し、テーブルに格納するには、次のストアド プロシージャを使用します。  
  
    -   **Insert_Idrefs_Values**  
  
         コース ID と学生 ID の値を CourseAttendence テーブルに挿入します。  
  
    -   **Extract_idrefs_values**  
  
         各 \<Course> 要素から個別の学生 ID を抽出します。 エッジ テーブルを使用して、これらの値を取得します。  
  
 次に手順を示します。  
  
```  
-- Create these tables:  
DROP TABLE CourseAttendance  
DROP TABLE Students  
DROP TABLE Courses  
GO  
CREATE TABLE Students(  
                id   varchar(5) primary key,  
                name varchar(30)  
                )  
GO  
CREATE TABLE Courses(  
               id       varchar(5) primary key,  
               name     varchar(30),  
               taughtBy varchar(5)  
)  
GO  
CREATE TABLE CourseAttendance(  
             id         varchar(5) references Courses(id),  
             attendedBy varchar(5) references Students(id),  
             constraint CourseAttendance_PK primary key (id, attendedBy)  
)  
go  
-- Create these stored procedures:  
DROP PROCEDURE f_idrefs  
GO  
CREATE PROCEDURE f_idrefs  
    @t      varchar(500),  
    @idtab  varchar(50),  
    @id     varchar(5)  
AS  
DECLARE @sp int  
DECLARE @att varchar(5)  
SET @sp = 0  
WHILE (LEN(@t) > 0)  
BEGIN   
    SET @sp = CHARINDEX(' ', @t+ ' ')  
    SET @att = LEFT(@t, @sp-1)  
    EXEC('INSERT INTO '+@idtab+' VALUES ('''+@id+''', '''+@att+''')')  
    SET @t = SUBSTRING(@t+ ' ', @sp+1, LEN(@t)+1-@sp)  
END  
Go  
  
DROP PROCEDURE fill_idrefs  
GO  
CREATE PROCEDURE fill_idrefs   
    @xmldoc     int,  
    @xpath      varchar(100),  
    @from       varchar(50),  
    @to         varchar(50),  
    @idtable    varchar(100)  
AS  
DECLARE @t varchar(500)  
DECLARE @id varchar(5)  
  
/* Temporary edge table */  
SELECT *   
INTO #TempEdge   
FROM OPENXML(@xmldoc, @xpath)  
  
DECLARE fillidrefs_cursor CURSOR FOR  
    SELECT CAST(iv.text AS nvarchar(200)) AS id,  
           CAST(av.text AS nvarchar(4000)) AS refs  
    FROM   #TempEdge c, #TempEdge i,  
           #TempEdge iv, #TempEdge a, #TempEdge av  
    WHERE  c.id = i.parentid  
    AND    UPPER(i.localname) = UPPER(@from)  
    AND    i.id = iv.parentid  
    AND    c.id = a.parentid  
    AND    UPPER(a.localname) = UPPER(@to)  
    AND    a.id = av.parentid  
  
OPEN fillidrefs_cursor  
FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    IF (@@FETCH_STATUS <> -2)  
    BEGIN  
        execute f_idrefs @t, @idtable, @id  
    END  
    FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
END  
CLOSE fillidrefs_cursor  
DEALLOCATE fillidrefs_cursor  
Go  
-- This is the sample document that is shredded and the data is stored in the preceding tables.  
DECLARE @h int  
EXECUTE sp_xml_preparedocument @h OUTPUT, N'<Data>  
  <Student id = "s1" name = "Student1"  attends = "c1 c3 c6"  />  
  <Student id = "s2" name = "Student2"  attends = "c2 c4" />  
  <Student id = "s3" name = "Student3"  attends = "c2 c4 c6" />  
  <Student id = "s4" name = "Student4"  attends = "c1 c3 c5" />  
  <Student id = "s5" name = "Student5"  attends = "c1 c3 c5 c6" />  
  <Student id = "s6" name = "Student6" />  
  
  <Class id = "c1" name = "Intro to Programming"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c2" name = "Databases"   
         attendedBy = "s2 s3" />  
  <Class id = "c3" name = "Operating Systems"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c4" name = "Networks" attendedBy = "s2 s3" />  
  <Class id = "c5" name = "Algorithms and Graphs"   
         attendedBy =  "s4 s5"/>  
  <Class id = "c6" name = "Power and Pragmatism"   
         attendedBy = "s1 s3 s5" />  
</Data>'  
  
INSERT INTO Students SELECT * FROM OPENXML(@h, '//Student') WITH Students  
  
INSERT INTO Courses SELECT * FROM OPENXML(@h, '//Class') WITH Courses  
/* Using the edge table */  
EXECUTE fill_idrefs @h, '//Class', 'id', 'attendedby', 'CourseAttendance'  
  
SELECT * FROM Students  
SELECT * FROM Courses  
SELECT * FROM CourseAttendance  
  
EXECUTE sp_xml_removedocument @h  
```  
  
### <a name="k-retrieving-binary-from-base64-encoded-data-in-xml"></a>K. XML 内の base64 エンコードされたデータからのバイナリ データの取得  
 多くの場合、バイナリ データは base64 エンコードを使用して XML に含められます。 OPENXML を使用してこの XML を細分化するときに、base64 エンコードされたデータを受け取ります。 この例では、base64 エンコードされたデータをバイナリ データに変換する方法を示します。  
  
-   サンプル バイナリ データを含むテーブルを作成します。  
  
-   FOR XML クエリと BINARY BASE64 オプションを使用して、base64 としてエンコードされるバイナリ データを含む XML を構築します。  
  
-   OPENXML を使用して XML を細分化します。 OPENXML から返されるデータは base64 エンコードされたデータです。 次に、.value 関数を呼び出してデータをバイナリ データに変換します。  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 varbinary(100))  
go  
-- Insert sample binary data  
INSERT T VALUES(1, 0x1234567890)   
go  
 -- Create test XML document that has base64 encoded binary data (use FOR XML query and specify BINARY BASE64 option)  
SELECT * FROM T  
FOR XML AUTO, BINARY BASE64  
go  
-- result  
-- <T Col1="1" Col2="EjRWeJA="/>  
  
-- Now shredd the sample XML using OPENXML.   
-- Call the .value function to convert   
-- the base64 encoded data returned by OPENXML to binary.  
DECLARE @h int ;  
EXEC sp_xml_preparedocument @h OUTPUT, '<T Col1="1" Col2="EjRWeJA="/>' ;  
SELECT Col1,   
CAST('<binary>' + Col2 + '</binary>' AS XML).value('.', 'varbinary(max)') AS BinaryCol   
FROM openxml(@h, '/T')   
WITH (Col1 integer, Col2 varchar(max)) ;  
EXEC sp_xml_removedocument @h ;  
GO  
```  
  
 結果は次のとおりです。 返されるバイナリ データは、テーブル T 内の元のバイナリ データです。  
  
```  
Col1        BinaryCol  
----------- ---------------------  
1           0x1234567890  
```  
  
## <a name="see-also"></a>参照  
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)   
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](openxml-sql-server.md)  
  
  
