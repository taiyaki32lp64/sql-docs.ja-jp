---
title: 注釈付き XSD スキーマの概要 (SQLXML)
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 81791c2b48e414f4f147bfff47cf1d9166d4a2a5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247057"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>注釈付き XSD スキーマの概要 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML スキーマ定義 (XSD) 言語を使用して、リレーショナル データの XML ビューを作成することができます。 作成したビューには、XML パス言語 (XPath) クエリを実行できます。 これは、CREATE VIEW ステートメントを使用してビューを作成し、そのビューに対して SQL クエリを指定することに似ています。  
  
 XML スキーマでは、XML ドキュメントの構造とドキュメント内のデータに対するさまざまな制約が記述されます。 スキーマに対して XPath クエリを指定した場合、返される XML ドキュメントの構造は、XPath クエリの実行対象のスキーマによって決定されます。  
  
 Xsd スキーマでは、 ** \<xsd: schema>** 要素によってスキーマ全体が囲まれます。すべての要素宣言は、 ** \<xsd: schema>** 要素内に含まれている必要があります。 スキーマが存在する名前空間を定義する属性と、スキーマで** \<xsd: schema>** 要素のプロパティとして使用される名前空間を定義する属性を記述できます。  
  
 有効な xsd スキーマには、 ** \<** 次のように定義された xsd: schema>要素が含まれている必要があります。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 ** \<Xsd: schema>** 要素は、XML スキーマ名前空間の仕様 () http://www.w3.org/2001/XMLSchemaから派生します。  
  
## <a name="annotations-to-the-xsd-schema"></a>XSD スキーマへの注釈  
 データベースへのマッピングを記述する注釈付きの XSD スキーマを使用して、データベースにクエリを実行し、結果を XML ドキュメントの形式で返すことができます。 注釈は、データベースのテーブルと列に XSD スキーマをマップするために指定します。 XSD スキーマで作成した XML ビューに対して XPath クエリを指定すると、データベースにクエリが実行され、結果を XML として取得できます。  
  
> [!NOTE]  
>  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 の XSD スキーマ言語では、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] の注釈付き XML-Data Reduced (XDR) スキーマ言語で挿入された注釈がサポートされます。 ただし、注釈付き XDR は、SQLXML 4.0 では非推奨とされます。  
  
 リレーショナル データベースの場合、任意の XSD スキーマをリレーショナル ストアにマップすると便利です。 これを実行する 1 つの方法は、XSD スキーマに注釈を付けることです。 注釈を持つ XSD スキーマは、*マッピングスキーマ*と呼ばれます。これは、XML データをリレーショナルストアにマップする方法に関する情報を提供します。 マッピング スキーマは、実質的にはリレーショナル データの XML ビューです。 これらのマッピングを使用して、リレーショナル データを XML ドキュメントとして取得できます。  
  
## <a name="namespace-for-annotations"></a>注釈の名前空間  
 XSD スキーマでは、名前空間**urn: schema-microsoft-com: mapping スキーマ**を使用して注釈を指定します。 次の例に示すように、名前空間を指定する最も簡単な方法は、 ** \<xsd: schema>** タグで名前空間を指定することです。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 使用される名前空間プレフィックスは任意です。 このドキュメントでは、 **sql**プレフィックスを使用して、注釈の名前空間を表し、この名前空間内の注釈を他の名前空間内の注釈と区別します。  
  
## <a name="example-of-an-annotated-xsd-schema"></a>注釈付き XSD スキーマの例  
 次の例では、XSD スキーマは** \<Person>** 要素で構成されています。 Employee>要素には、 **ContactID** attribute および** \<FirstName>** および** \<LastName>** 子要素があります。 ** \<**  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 この XSD スキーマに、要素と属性をデータベースのテーブルと列にマップするため、注釈を追加します。  
  
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
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 マッピングスキーマでは、 ** \<Contact>** 要素は、 **sql: relation**注釈を使用して、サンプルの AdventureWorks データベースの Person. Contact テーブルにマップされます。 属性 ConID、FName、および LName は、 **sql: field**注釈を使用して、Person. Contact テーブルの ContactID、FirstName、および LastName 列にマップされます。  
  
 この注釈付きの XSD スキーマによって、リレーショナル データの XML ビューが提供されます。 この XML ビューには、XPath 言語を使用してクエリを実行できます。 XPath クエリを実行すると、SQL クエリによって返される行セットではなく、XML ドキュメントが返されます。  
  
> [!NOTE]  
>  マッピング スキーマに指定するリレーショナル値 (テーブル名や列名など) の大文字小文字の区別は、SQL Server で使用される照合順序の、大文字小文字の区別の設定によって変わります。 詳細については、「 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
## <a name="other-resources"></a>その他のリソース  
 XML スキーマ定義言語 (XSD)、XML パス言語 (XPath)、Extensible Stylesheet Language Transformations (XSLT) の詳細については、次の Web サイトを参照してください。  
  
-   XML スキーマパート 0: 入門、W3C 勧告 (https://www.w3.org/TR/xmlschema-0/)  
  
-   XML スキーマパート 1: 構造体、W3C 勧告 (https://www.w3.org/TR/xmlschema-1/)  
  
-   XML スキーマパート 2: データ型、W3C 勧告 (https://www.w3.org/TR/xmlschema-2/)  
  
-   XML パス言語 (XPath) (https://www.w3.org/TR/xpath)  
  
-   XSL 変換 (XSLT) (https://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;注釈付きスキーマのセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [注釈付き XDR スキーマ &#40;SQLXML 4.0 で非推奨とされました&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
