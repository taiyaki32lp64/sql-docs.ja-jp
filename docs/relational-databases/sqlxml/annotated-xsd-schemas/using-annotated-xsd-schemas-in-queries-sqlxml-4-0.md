---
title: クエリでの注釈付き XSD スキーマの使用 (SQLXML)
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a53e53f27b9b0c9c94519cb55aa136349f6ff7c5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246997"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>クエリでの注釈付き XSD スキーマの使用 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  注釈付きスキーマに対してクエリを指定し、XSD スキーマに対してテンプレートで XPath クエリを指定して、データベースからデータを取得することができます。  
  
 **Sql: xpath クエリ>要素を使用すると、注釈付きスキーマで定義されている XML ビューに対して xpath クエリを指定できます。 \<** Xpath クエリの実行対象となる注釈付きスキーマは、 ** \<sql: xpath クエリ>** 要素の**mapping-schema**属性を使用して識別されます。  
  
 テンプレートは、1 つ以上のクエリを含む有効な XML ドキュメントです。 FOR XML クエリと XPath クエリでは、ドキュメント フラグメントが返されますが、 テンプレートは、ドキュメントフラグメントのコンテナーとして機能します。そのため、1つの最上位要素を指定する方法が用意されています。  
  
 このトピックの例では、テンプレートを使用して注釈付きスキーマに対する XPath クエリを指定し、データベースからデータを取得します。  
  
 たとえば、次の注釈付きスキーマを考えてみます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 わかりやすくするため、この XSD スキーマは Schema2.xml というファイルに格納されているものとします。 ここで、次のテンプレート ファイル (Schema2T.xml) で指定されている注釈付きスキーマに対し、XPath クエリを指定できます。  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 SQLXML 4.0 のテスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用すると、テンプレート ファイルの一部としてクエリを実行できます。 詳細については、「 [SQLXML 4.0&#41;で非推奨とされた注釈付き XDR スキーマ &#40;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)」を参照してください。  
  
## <a name="using-inline-mapping-schemas"></a>インライン マッピング スキーマの使用  
 注釈付きスキーマはテンプレートに直接含めることができます。このテンプレートで、インライン スキーマに対する XPath クエリを指定できます。 テンプレートはアップデートグラムとしても使用できます。  
  
 テンプレートには複数のインライン スキーマを含めることができます。 テンプレートに含まれているインラインスキーマを使用するには、 ** \<xsd: schema>** 要素で一意の値を持つ**id**属性を指定し、 **#idvalue**を使用してインラインスキーマを参照します。 **Id**属性は、XDR スキーマで使用される**sql: id** ({urn: schema-microsoft-com: xml} id) と同じ動作です。  
  
 たとえば、次のテンプレートでは、2 つのインライン注釈付きスキーマを指定しています。  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 このテンプレートでは 2 つの XPath クエリも指定しています。 各** \<xpath クエリ>** 要素は、**マッピング**スキーマ属性を指定することによって、マッピングスキーマを一意に識別します。  
  
 テンプレートでインラインスキーマを指定する場合は、 ** \<xsd: schema>** 要素で**sql:: mapping-schema**注釈も指定する必要があります。 **Sql: のマッピングスキーマ**はブール値 (0 = false、1 = true) を取ります。 **Sql:-mapping-schema = "1"** のインラインスキーマは、インライン注釈が付けられたスキーマとして扱われ、XML ドキュメントでは返されません。  
  
 **Sql: マッピングスキーマ**の注釈は、テンプレート名前空間**urn: schema-microsoft-com: xml**に属しています。  
  
 この例をテストするには、テンプレート (InlineSchemaTemplate.xml) をローカルのディレクトリに保存した後、SQLXML 4.0 テスト スクリプト (Sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。 詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 テンプレート内の** \<sql: xpath クエリ>** 要素、またはアップデートグラムの** \<updg: sync>** 要素に対して**マッピングスキーマ**属性を指定することに加えて、次の操作を実行できます。  
  
-   テンプレートの** \<ルート>** 要素 (グローバル宣言) で**マッピングスキーマ**属性を指定します。 このマッピングスキーマは、明示的な**マッピングスキーマ**の注釈がないすべての XPath およびアップデートグラムノードで使用される既定のスキーマになります。  
  
-   ADO**コマンド**オブジェクトを使用して、**マッピングスキーマ**の属性を指定します。  
  
 Xpath クエリ>または** \<updg: sync>** 要素で指定されている**マッピングスキーマ**属性が最も優先順位が高くなります。 ** \<** ADO**コマンド**オブジェクトの優先順位は最も低くなります。  
  
 テンプレートで XPath クエリを指定し、XPath クエリの実行対象となるマッピングスキーマを指定しない場合、XPath クエリは**dbobject**型クエリとして扱われることに注意してください。 たとえば、次のテンプレートを考えてみます。  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 このテンプレートでは、XPath クエリが指定されていますが、マッピング スキーマが指定されていません。 したがって、このクエリは**dbobject**型クエリとして扱われます。 productphoto はテーブル名、 @ProductPhotoID= ' 100 ' は、ID 値が100の製品写真を検索する述語です。 @LargePhoto値の取得元の列を指定します。  
  
  
