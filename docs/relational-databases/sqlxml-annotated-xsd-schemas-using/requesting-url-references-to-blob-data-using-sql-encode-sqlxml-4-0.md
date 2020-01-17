---
title: 'Sql: encode (SQLXML) を使用して BLOB データへの URL 参照を取得する'
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1cd65cce635c89cb7ece1b88851d5f4a9b7cb09
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257417"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>sql:encode を使用した、BLOB データへの URL 参照の要求 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  注釈付き XSD スキーマで、属性 (または要素) が Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の BLOB 列にマップされた場合、XML 内に返されるデータは Base 64 エンコード形式になります。  
  
 バイナリ形式で BLOB データを取得するために後で使用できるデータ (URI) への参照が必要な場合は、 **sql: encode**注釈を指定します。 **Sql: encode**は、単純型の属性または要素に対して指定できます。  
  
 フィールドの値の代わりにフィールドへの URL が返されることを示すには、 **sql: encode**注釈を指定します。 **sql: encode**は、URL でシングルトン select を生成する主キーに依存します。 主キーは、 **sql: キーフィールド**の注釈を使用して指定できます。  
  
 **Sql: encode**注釈には、"url" または "default" の値を割り当てることができます。 "default" の場合、データは Base 64 エンコード形式で返されます。  
  
 Sql: **encode**注釈は、sql と共に使用することはできません **: cdata** 、または ID、IDREF、IDREFS、NMTOKEN、または NMTOKENS 属性の型。 XSD **fixed**属性と共に使用することもできません。  
  
> [!NOTE]  
>  BLOB 型の列は、キーの一部または外部キーとして使用することはできません。  
  
## <a name="examples"></a>例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、「 [SQLXML の例を実行するための要件](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)」を参照してください。  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. BLOB データへの URL 参照を取得するため、sql:encode を指定する  
 この例では、マッピングスキーマによって、 **LargePhoto**属性に**sql: encode**が指定されており、特定の製品写真への URI 参照が取得されます (Base 64 エンコード形式でバイナリデータを取得するのではありません)。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>スキーマに対してサンプル XPath クエリをテストするには  
  
1.  上のスキーマのコードをコピーして、テキスト ファイルに貼り付け、 sqlEncode.xml として保存します。  
  
2.  次のテンプレートをコピーして、テキスト ファイルに貼り付け、 sqlEncode.xml を保存したディレクトリに sqlEncodeT.xml として保存します。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     マッピング スキーマ (sqlEncode.xml) に指定するディレクトリ パスは、テンプレートを保存するディレクトリに対する相対パスです。 次のように、絶対パスを指定することもできます。  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  SQLXML 4.0 テスト スクリプト (sqlxml4test.vbs) を作成し、それを使用してテンプレートを実行します。  
  
     詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
 結果を次に示します。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
