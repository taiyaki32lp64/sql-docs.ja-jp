---
title: テーブルまたは列へのカスタム XSD マッピング (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5fafcd918dda0001c316fd68cae3b19e6cd805a3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257429"
---
# <a name="custom-xsd-mappings-to-tablescolumns-sqlxml"></a>テーブルまたは列へのカスタム XSD マッピング (SQLXML)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD スキーマを使用してリレーショナル データベースの XML ビューを作成するときには、スキーマの要素と属性をデータベースのテーブルと列にマップする必要があります。 データベースのテーブルおよびビューの行は、XML ドキュメントの要素にマップされます。 データベースの列値は属性または要素にマップされます。  
  
 注釈付き XSD スキーマに対して XPath クエリを指定する場合、スキーマ内の要素と属性のデータは、マップ先のテーブルと列から取得されます。 データベースから単一の値を取得するには、XSD スキーマに指定されているマッピングに、リレーションとフィールドの両方の指定が必要です。 要素または属性の名前がマップ先のテーブル/ビューまたは列名と同じでない場合、 **sql: relation**注釈と**sql: field**注釈を使用して、XML ドキュメント内の要素または属性と、データベース内のテーブル (ビュー) または列との間のマッピングを指定します。  
  
## <a name="sql-relation"></a>sql-relation  
 XSD スキーマの XML ノードをデータベーステーブルにマップするために、 **sql: relation**注釈が追加されました。 テーブルの名前 (ビュー) は、 **sql: relation**注釈の値として指定されます。  
  
 要素に**sql: relation**が指定されている場合、この注釈のスコープは、その要素の複合型定義に記述されているすべての属性と子要素に適用されるため、注釈を記述するショートカットが提供されます。  
  
 **Sql: relation**注釈は、で[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有効な識別子が XML で有効でない場合にも役立ちます。 たとえば、"Order Details" は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では有効なテーブル名ですが、XML では無効です。 このような場合、 **sql: relation**注釈を使用してマッピングを指定できます。次に例を示します。  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 **Sql フィールド**の注釈は、要素または属性をデータベース列にマップします。 スキーマ内の XML ノードをデータベース列にマップするために、 **sql: field**注釈が追加されました。 空のコンテンツ要素に**sql: field**を指定することはできません。  
  
## <a name="examples"></a>例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、「 [SQLXML の例を実行するための要件](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)」を参照してください。  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. sql:relation 注釈と sql:field 注釈を指定する  
 この例では、XSD スキーマは、 ** \<FName>** と** \<LName>** 子要素および**ContactID**属性を持つ複合型の** \<Contact>** 要素で構成されています。  
  
 **Sql: relation**注釈によっ** \<て、contact>** 要素が AdventureWorks データベースの Person. contact テーブルにマップされます。 **Sql: field**注釈は、 ** \<FName>** 要素を FirstName 列に、 ** \<LName>** 要素を LastName 列にマップします。  
  
 **ContactID**属性に注釈が指定されていません。 このため、既定のマッピングが使用され、属性が同じ名前の列にマップされます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 MySchema-annotated.xml として保存します。  
  
2.  次のテンプレートをコピーし、テキストファイルに貼り付けます。 MySchema-annotated.xml を保存したディレクトリに MySchema-annotatedT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (MySchema-annotated.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 次に結果セットの一部を示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
