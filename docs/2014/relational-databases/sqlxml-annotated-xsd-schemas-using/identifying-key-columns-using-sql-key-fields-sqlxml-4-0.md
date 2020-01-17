---
title: Sql:key のキー列を使用して特定のフィールド (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc3c063da7bb9133f8687a908c4bd7e0e13bae8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013818"
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>sql:key-fields を使用した、キー列の指定 (SQLXML 4.0)
  XSD スキーマに対して XPath クエリを指定する場合、結果内に適切な入れ子を生成するには、多くの場合キー情報が必要です。 `sql:key-fields` 注釈の指定は、適切な階層を確実に生成するための 1 つの方法です。  
  
> [!NOTE]  
>  適切な入れ子を生成するには、テーブルにマップする要素に `sql:key-fields` を指定することをお勧めします。 作成される XML は、基になる結果セットの順序指定に影響を受けます。 `sql:key-fields` を指定しない場合、適切な XML が作成されない可能性があります。  
  
 `sql:key-fields` の値で、リレーションの行を一意に識別する列を指定します。 1 つ以上の列は行を一意に識別するために必要な列の値はスペースで区切られます。  
  
 使用する必要があります、`sql:key-fields`注釈要素が含まれている場合、  **\<sql:relationship >** を要素と子要素の間で指定されているテーブルの主キーは提供されません親要素。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. ときに適切な入れ子を生成\<sql:relationship > 十分な情報は提供されません  
 この例では、`sql:key-fields` をどこに指定すればよいかを示します。  
  
 次のスキーマを検討してください。 スキーマ間の階層の指定、 **\<順序 >** と **\<顧客 >** いる要素、 **\<順序 >** 要素は親と **\<顧客 >** 要素は、子。  
  
 **\<Sql:relationship >** 親子リレーションシップを指定するタグを使用します。 このタグでは、Sales.SalesOrderHeader テーブルの CustomerID を親キーとして識別し、Sales.Customer テーブルの子キー CustomerID を参照します。 提供される情報 **\<sql:relationship >** 親テーブル (Sales.SalesOrderHeader) 内の行を一意に識別するには不十分です。 `sql:key-fields` 注釈を指定しないと、不正確な階層が生成されます。  
  
 `sql:key-fields`で指定した **\<順序 >** 注釈は、親 (Sales.SalesOrderHeader テーブル) 内の行を一意に識別して、その子要素がその親の下に表示します。  
  
 スキーマは次のようになります。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>このスキーマの実際のサンプルを作成するには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 KeyFields1.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 KeyFields1.xml を保存したディレクトリに KeyFields1T.xml として保存します。 テンプレートの XPath クエリでは、すべてを返します、 **\<順序 >** 3 未満の顧客 Id を持つ要素。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (KeyFields1.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、結果セットの一部です。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. sql:key-fields を指定して結果内に適切な入れ子を生成する  
 次のスキーマを使用して指定された階層はありません **\<sql:relationship >** します。 `sql:key-fields` 注釈を指定して、HumanResources.Employee テーブルの従業員を一意に識別する必要があります。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>このスキーマの実際のサンプルを作成するには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 KeyFields2.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 KeyFields2.xml を保存したディレクトリに KeyFields2T.xml として保存します。 テンプレートの XPath クエリでは、すべてを返します、  **\<HumanResources.Employee >** 要素。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (KeyFields2.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、次を参照してください。 [SQLXML クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、結果です。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
