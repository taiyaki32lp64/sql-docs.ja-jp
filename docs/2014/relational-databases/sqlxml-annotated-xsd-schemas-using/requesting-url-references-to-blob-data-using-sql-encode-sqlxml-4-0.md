---
title: '使用した BLOB データへの URL 参照の要求: (SQLXML 4.0) のエンコード |マイクロソフトのドキュメント'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: 153a88bcb31f65d4e6aff007cfbee7d1f7afc6df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013728"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>sql:encode を使用した、BLOB データへの URL 参照の要求 (SQLXML 4.0)
  注釈付き XSD スキーマで、属性 (または要素) が Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の BLOB 列にマップされた場合、XML 内に返されるデータは Base 64 エンコード形式になります。  
  
 後で BLOB データをバイナリ形式で取得するときに使用できるよう、データへの参照 (URI) を返す場合は、`sql:encode` 注釈を指定します。 `sql:encode` は、単純型の属性または要素に指定できます。  
  
 `sql:encode` 注釈を指定すると、フィールド値の代わりにフィールドへの URL を返すことができます。 `sql:encode` では主キーに基づいて、URL での単一選択が生成されます。 使用して主キーを指定することができます、`sql:key-fields`注釈。  
  
 `sql:encode` 注釈には、"url" または "default" の値を割り当てることができます。 "default" の場合、データは Base 64 エンコード形式で返されます。  
  
 `sql:encode` 注釈は、`sql:use-cdata` と共に使用したり、ID、IDREF、IDREFS、NMTOKEN、または NMTOKENS 属性型に指定したり、 ないこともできます XSD で**固定**属性。  
  
> [!NOTE]  
>  BLOB 型の列は、キーの一部または外部キーとして使用することはできません。  
  
## <a name="examples"></a>使用例  
 次の例を使用した実際のサンプルを作成するには、特定の条件を満たす必要があります。 詳細については、次を参照してください。 [SQLXML の例を実行するための要件](../sqlxml/requirements-for-running-sqlxml-examples.md)します。  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. BLOB データへの URL 参照を取得するため、sql:encode を指定する  
 この例では、マッピング スキーマを指定します`sql:encode`上、 **LargePhoto** (Base 64 エンコード形式でバイナリ データの取得) ではなく特定の製品写真への URI 参照を取得する属性。  
  
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
  
     詳細については、次を参照してください。 [SQLXML 4.0 クエリの実行に ADO を使用する](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)します。  
  
 これは、結果です。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
