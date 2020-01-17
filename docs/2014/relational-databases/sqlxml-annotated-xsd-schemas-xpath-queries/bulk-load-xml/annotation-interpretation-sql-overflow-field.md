---
title: sql:overflow-フィールド (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 594ebdbad3968ba2efe7e255b28379194d2fb77f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013470"
---
# <a name="sqloverflow-field-sqlxml-40"></a>sql:overflow-field (SQLXML 4.0)
  スキーマでは、XML ドキュメントからのすべての未使用データを受け取るオーバーフロー列を指定することができます。 この列は、スキーマ内で `sql:overflow-field` 注釈により指定します。 オーバーフロー列は複数指定することもできます。  
  
 `sql:overflow-field` 注釈が定義されている XML ノード (要素または属性) がスコープ内に入るとオーバーフロー列がアクティブになり、未使用データがこの列に挿入されます。 ノードがスコープ外に出ると、オーバーフロー列はアクティブではなくなります。それまでのオーバーフロー フィールドがある場合は、XML 一括読み込みによってそのフィールドがアクティブになります。  
  
 XML 一括読み込みでは、オーバーフロー列へのデータの格納時に、`sql:overflow-field` が定義されている親要素の開始タグと終了タグも格納されます。  
  
 たとえば、次のスキーマについて説明します、 **\<顧客 >** と **\<CustOrder >** 要素。 これらの要素それぞれに、オーバーフロー列が指定されています。  
  
```  
<?xml version="1.0" ?>  
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
 <xsd:element name="ROOT" sql:is-constant="1">  
  <xsd:complexType>  
    <xsd:sequence>   
      <xsd:element name="Customers"   
                   sql:relation="Cust"  
                   sql:overflow-field="OverflowColumn">  
        <xsd:complexType>  
             <xsd:sequence>   
             <xsd:element name="CustomerID" type="xsd:integer"/>  
             <xsd:element name="CompanyName"  type="xsd:string"/>  
             <xsd:element name="City" type="xsd:string"/>  
             <xsd:element name="Order"  
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder"  
                          sql:overflow-field="OverflowColumn">  
               <xsd:complexType>  
                 <xsd:attribute name="OrderID"/>  
                 <xsd:attribute name="CustomerID"/>  
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
  
 スキーマで、 **\<顧客 >** 要素は Cust テーブルにマップし、 **\<順序 >** 要素は CustOrder テーブルにマップされます。  
  
 両方の **\<顧客 >** と **\<順序 >** 要素は、オーバーフロー列を識別します。 したがって、XML 一括読み込みを保存します未使用のすべての子の要素と属性、 **\<顧客 >** Cust テーブルのオーバーフロー列内の要素と、未使用の子要素と、の属性をすべて **\<順序 >** CustOrder テーブルのオーバーフロー列内の要素。  
  
### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  この例のスキーマを SampleSchema.xml として保存します。  
  
2.  これらのテーブルを作成します。  
  
    ```  
    CREATE TABLE Cust (  
              CustomerID     int         PRIMARY KEY,  
              CompanyName    varchar(20) NOT NULL,  
              City           varchar(20) DEFAULT 'Seattle',  
              OverflowColumn nvarchar(200))  
    GO  
    CREATE TABLE CustOrder (  
              OrderID        int         PRIMARY KEY,  
              CustomerID     int         FOREIGN KEY REFERENCES  
                                              Cust(CustomerID),  
              OverflowColumn nvarchar(200))  
    GO  
    ```  
  
3.  次のサンプル XML データを SampleXMLData.xml として保存します。  
  
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
       <City><![CDATA[LA]]> </City>  
       <xyz><address>111 Maple, Seattle</address></xyz>     
       <Order OrderID="3" />  
     </Customers>  
       <Customers>  
       <CustomerID>1113</CustomerID>  
       <CompanyName>Victuailles en stock</CompanyName>  
       <Order OrderID="4" />  
      </Customers>  
    </ROOT>  
    ```  
  
4.  XML 一括読み込みを実行するには、この [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) の例を Sample.vbs として保存し実行します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
