---
title: sql:relationship とキーの順序付け規則 (SQLXML 4.0) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 521614f8755261d0348ab95132c527c736c96311
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013510"
---
# <a name="sqlrelationship-and-the-key-ordering-rule-sqlxml-40"></a>sql:relationship とキーの順序付け規則 (SQLXML 4.0)
  XML 一括読み込みでは、ノードがスコープ内に入るときにレコードが生成され、ノードがスコープ外に出るときに、これらのレコードが Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されます。したがって、レコードのデータはノードのスコープ内に存在する必要があります。  
  
 これで、次の XSD スキーマを検討してください間の一対多リレーションシップ **\<顧客 >** と **\<順序 >** 要素 (1 人の顧客は、多数の注文を配置できます)使用して指定された、`<sql:relationship>`要素。  
  
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
  
 として、 **\<顧客 >** 要素ノードがスコープに入った、XML 一括読み込みで顧客レコードが生成されます。 XML 一括読み込みを読み取るまでにこのレコードがまだ **\</Customer >** します。 処理で、 **\<順序 >** 要素ノード、XML 一括読み込みは`<sql:relationship>`から CustOrder テーブルの CustomerID 外部キー列の値を取得する、 **\<顧客 >** ため、要素の親、 **\<順序 >** 要素で指定されていない、 **CustomerID**属性。 つまり、定義で、 **\<顧客 >** 要素が指定する必要があります、 **CustomerID**属性を指定する前に、スキーマで`<sql:relationship>`します。 それ以外の場合、時、 **\<順序 >** 要素がスコープに入った、XML 一括読み込みでは CustOrder テーブルのレコードを生成および、XML 一括読み込みに達すると、  **\</order >** 終了タグに送信するレコード[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]CustomerID 外部キー列の値のないです。  
  
 この例のスキーマを SampleSchema.xml として保存します。  
  
### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  これらのテーブルを作成します。  
  
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
  
     この結果、XML 一括読み込みでは CustOrder テーブルの CustomerID 外部キー列に NULL 値が挿入されます。 XML のサンプル データを変更するとように、  **\<CustomerID >** 前に子要素が表示されます、 **\<順序 >** 予期される結果を取得する子要素。XML 一括読み込みでは、列に指定された外部キーの値を挿入します。  
  
 これは、同等の XDR スキーマです。  
  
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
  
  
