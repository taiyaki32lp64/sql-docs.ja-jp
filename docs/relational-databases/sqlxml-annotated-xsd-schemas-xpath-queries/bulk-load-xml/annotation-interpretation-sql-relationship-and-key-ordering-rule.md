---
title: 'sql: relationship とキーの順序付け規則 (SQLXML)'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c04b14f474e2afc0e6feb18eaa0bd321fdbb5e0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246771"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>注釈の解釈 - sql:relationship とキーの順序付けルール
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 一括読み込みでは、ノードがスコープ内に入るときにレコードが生成され、ノードがスコープ外に出るときに、これらのレコードが Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。したがって、レコードのデータはノードのスコープ内に存在する必要があります。  
  
 次の XSD スキーマについて考えてみます。このスキーマでは、 ** \<顧客の>** と** \<注文>** の要素 (1 人の顧客が多数の注文を配置できます) の間の一対多リレーションシップが、 ** \<sql: relationship>** 要素を使用して指定されています。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
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
</xsd:schema>  
```  
  
 ** \<Customer>** 要素ノードがスコープ内に入ると、XML 一括読み込みでは顧客レコードが生成されます。 このレコードは、XML 一括読み込みによって、または** \<顧客>** が読み取られるまで続きます。 Order ** \<>** 要素で**customerid**属性が指定されていないため、 ** \<order>** 要素ノードの処理では、XML 一括読み込みでは、 ** \<sql: relationship>** を使用して、 ** \<顧客>** 親要素から custorder テーブルの customerid 外部キー列の値を取得します。 これは、 ** \<Customer>** 要素を定義する際に、 ** \<sql: relationship>** を指定する前に、スキーマで**CustomerID**属性を指定する必要があることを意味します。 このようにしないと、 ** \<Order>** 要素がスコープに入ると、xml 一括読み込みでは custorder テーブルのレコードが生成されます。また、xml 一括読み込みでは、xml [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]一括読み込みが** \</order>** 終了タグに達すると、CustomerID 外部キー列の値なしでレコードがに送信されます。  
  
 この例のスキーマを SampleSchema.xml として保存します。  
  
### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  次のテーブルを作成します。  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  次のサンプル データを SampleXMLData.xml として保存します。  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  XML 一括読み込みを実行するには、次の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) の例を MySample.vbs として保存し、実行します。  

    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     この結果、XML 一括読み込みでは CustOrder テーブルの CustomerID 外部キー列に NULL 値が挿入されます。 Xml サンプルデータを変更して、 ** \<CustomerID>** 子要素が** \<Order>** 子要素の前にあるようにすると、xml 一括読み込みでは、指定された外部キー値が列に挿入されます。  
  
 これは、これと同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
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
  
  
