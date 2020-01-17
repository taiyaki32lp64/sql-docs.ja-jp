---
title: 未使用データを使用して、sql:overflow を取得する-(SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18651b91ee2a47819360eae4c57c18ac3eae672b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013776"
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>sql:overflow-field を使用した、未使用データの取得 (SQLXML 4.0)
  [!INCLUDE[tsql](../../includes/tsql-md.md)] OPENXML 関数を使用して XML ドキュメントからデータベースにレコードを挿入するときに、ソース XML ドキュメントのすべての未使用データを 1 つの列に格納することができます。 注釈付きスキーマを使用してデータベースからデータを取得するときには、`sql:overflow-field` 属性を指定して、オーバーフロー データを格納するテーブルの列を指定できます。 `sql:overflow-field`属性に指定できる **\<要素 >** します。  
  
 データは次のように取得されます。  
  
-   オーバーフロー列に格納された属性が、`sql:overflow-field` 注釈を含む要素に追加されます。  
  
-   データベースのオーバーフロー列に格納された子要素とその子孫が、スキーマで明示的に指定されたコンテンツの後に子要素として追加されます。 このとき、順序は維持されません。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>A. 要素に sql:overflow-field を指定する  
 この例では、次のスクリプトを実行して tempdb データベースにテーブル Customers2 が作成済みであることを前提としています。  
  
```  
USE tempdb  
CREATE TABLE Customers2 (  
CustomerID       VARCHAR(10),   
ContactName    VARCHAR(30),   
AddressOverflow    NVARCHAR(500))  
  
GO  
INSERT INTO Customers2 VALUES (  
'ALFKI',   
'Joe',  
'<Address>  
  <Address1>Maple St.</Address1>  
  <Address2>Apt. E105</Address2>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98147</Zip>  
 </Address>')  
GO  
```  
  
 さらに、tempdb データベース用の仮想ディレクトリを作成する必要があります-のテンプレート仮想名と`template`"template"という名前の型。  
  
 次の例では、マッピング スキーマで、Customers2 テーブルの AddressOverflow 列に格納されている未使用データを取得します。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customers2" sql:overflow-field="AddressOverflow" >  
    <xsd:complexType>  
      <xsd:attribute name="CustomerID"  type="xsd:integer"/>  
      <xsd:attribute name="ContactName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 Overflow.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 Overflow.xml を保存したディレクトリに OverflowT.xml として保存します。 このテンプレートのクエリでは、Customers2 テーブル内のレコードが選択されます。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Overflow.xml">  
            /Customers2  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (Overflow.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\Overflow.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 Here is the result set:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers2 CustomerID="ALFKI" ContactName="Joe">  
    <Address1>Maple St.</Address1>   
    <Address2>Apt. E105</Address2>   
    <City>Seattle</City>   
    <State>WA</State>   
    <Zip>98147</Zip>   
  </Customers2>  
</ROOT>  
```  
  
  
