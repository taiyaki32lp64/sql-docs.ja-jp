---
title: クライアント側とサーバー側の XML 書式設定 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- FOR XML clause, formatting
- client-side XML formatting
- server-side XPath
- server-side XML formatting
- AUTO mode
- client-side XPath
ms.assetid: f807ab7a-c5f8-4e61-9b00-23aebfabc47e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 421c48590098f9dbf4ce075c213fcd1cda720649
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247010"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>クライアント側とサーバー側の XML 書式設定 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  ここでは、SQLXML における、クライアント側とサーバー側の XML 書式設定の一般的な違いについて説明します。  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>クライアント側の書式設定では複数の行セット クエリがサポートされない  
 複数の行セットを生成するクエリは、クライアント側の XML 書式設定を使用するときにはサポートされません。 たとえば、クライアント側の書式設定が指定されている仮想ディレクトリがあるとし、 このサンプルテンプレートを考えてみましょう。このテンプレートには、 ** \<sql: query>** block に2つの SELECT ステートメントがあります。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 このテンプレートはアプリケーション コードで実行できます。実行すると、クライアント側の XML 書式設定では複数の行セットの書式設定がサポートされていないため、エラーが返されます。 2つの個別** \<の sql: query>** ブロックでクエリを指定した場合は、目的の結果が得られます。  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>クライアント側とサーバー側の XML 書式設定では timestamp 型のマッピングが異なる  
 サーバー側の XML 書式設定では、 **timestamp**型のデータベース列は i8 XDR 型にマップされます (XMLDATA オプションがクエリで指定されている場合)。  
  
 クライアント側の XML 書式設定では、 **timestamp**型のデータベース列は**uri**または**bin. base64** XDR 型にマップされます (クエリで binary base64 オプションが指定されているかどうかによって異なります)。 この型は[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **timestamp**型に変換されるため、アップデートグラムと bulkload 機能を使用する場合は、 **.bin** XDR 型が役立ちます。 この方法で、挿入、更新、または削除操作が成功します。  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>サーバー側の書式設定ではサブタイプの VARIANT 型も使用される  
 サーバー側の XML 書式設定では、サブタイプの VARIANT 型も使用されます。 クライアント側の XML 書式設定を使用する場合、variant は Unicode 文字列に変換され、サブタイプの VARIANT は使用されません。  
  
## <a name="nested-mode-vs-auto-mode"></a>NESTED モードと AUTO モード  
 クライアント側の FOR XML の NESTED モードは、サーバー側の FOR XML の AUTO モードに似ていますが、次の点が異なります。  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>サーバー側で AUTO モードを使用してビューにクエリを実行すると、ビュー名が結果の XML 内の要素名として返されます。  
 たとえば、次のビューが AdventureWorksdatabase の Person テーブルに作成されているとします。  
  
```  
CREATE VIEW ContactView AS (SELECT ContactID as CID,  
                               FirstName  as FName,  
                               LastName  as LName  
                        FROM Person.Contact)  
```  
  
 次のテンプレートでは、ContactView ビューに対するクエリと、サーバー側の XML 書式設定が指定されています。  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT *  
    FROM   ContactView  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 テンプレートを実行すると、次の XML が返されます。 (部分的な結果のみが表示されます)。要素名は、クエリの実行対象となるビューの名前であることに注意してください。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 クライアント側の書式設定を、対応する NESTED モードで指定すると、ベース テーブル名が結果の XML 内の要素名として返されます。 たとえば、次の変更後のテンプレートでは、同じ SELECT ステートメントが実行されますが、XML の書式設定はクライアント側で実行されます (つまり、テンプレートでは、**クライアント側の xml**は true に設定されます)。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT *  
    FROM   ContactView  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 このテンプレートを実行すると、次の XML が生成されます。 この場合、ベース テーブル名が要素名になっていることに注意してください。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact CID="1" FName="Gustavo" LName="Achong" />   
  <Person.Contact CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
### <a name="when-you-use-auto-mode-of-the-server-side-for-xml-the-table-aliases-specified-in-the-query-are-returned-as-element-names-in-the-resulting-xml"></a>サーバー側の FOR XML を AUTO モードで使用すると、クエリで指定されたテーブルの別名が、結果の XML 内の要素名として返されます。  
 たとえば、次のテンプレートを考えてみます。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 このテンプレートを実行すると、次の XML が生成されます。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <C fname="Gustavo" lname="Achong" />   
  <C fname="Catherine" lname="Abel" />   
...  
</ROOT>   
```  
  
 クライアント側の FOR XML を NESTED モードで使用すると、テーブル名が、結果の XML 内の要素名として返されます。 (クエリで指定されたテーブルの別名は使用されません)。たとえば、次のテンプレートを考えてみます。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 このテンプレートを実行すると、次の XML が生成されます。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact fname="Gustavo" lname="Achong" />   
  <Person.Contact fname="Catherine" lname="Abel" />   
...  
</ROOT>  
```  
  
### <a name="if-you-have-a-query-that-returns-columns-as-dbobject-queries-you-cannot-use-aliases-for-these-columns"></a>列を dbobject クエリとして返すクエリでは、これらの列に対して別名は使用できません。  
 たとえば、次のテンプレートを考えてみます。このテンプレートには、製品写真 ID と写真を返すクエリが含まれています。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query client-side-xml="1">  
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML NESTED, elements  
</sql:query>  
</ROOT>  
```  
  
 このテンプレートを実行すると、Photo 列が dbobject クエリとして返されます。 この dbobject クエリでは、`@P` で存在しない列名が参照されています。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@P</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
 XML の書式設定がサーバーで実行されている場合 (**クライアント側 xml = "0"**)、列の別名を使用して、実際のテーブル名と列名が返される dbobject クエリ (別名が指定されている場合でも) を返すことができます。 たとえば、次のテンプレートはクエリを実行し、XML の書式設定はサーバーで実行されます (**クライアント側の xml**オプションが指定されておらず、仮想ルートに対して **[クライアントで実行**] オプションが選択されていません)。 このクエリでは、クライアント側の NESTED モードではなく AUTO モードも指定されています。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query   
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML AUTO, elements  
</sql:query>  
</ROOT>  
```  
  
 このテンプレートを実行すると、次の XML ドキュメントが返されます。LargePhoto 列に対する dbobject クエリでは、別名が使用されていないことに注意してください。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@LargePhoto</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
### <a name="client-side-vs-server-side-xpath"></a>クライアント側とサーバー側の XPath  
 クライアント側の XPath とサーバー側の XPath は類似していますが、次の点が異なります。  
  
-   クライアント側の XPath クエリを使用するときに適用されるデータ変換は、サーバー側の XPath クエリを使用するときに適用されるものとは異なります。 クライアント側の XPath では、CONVERT モード 126 の代わりに CAST が使用されます。  
  
-   テンプレートで**クライアント側 xml = "0"** (false) を指定すると、サーバー側の xml 書式設定が要求されます。 したがって、サーバーでは NESTED オプションが認識されないので、FOR XML NESTED は指定できません。 これにより、エラーが発生します。 この場合、サーバーで認識される AUTO、RAW、または EXPLICIT モードを使用する必要があります。  
  
-   テンプレートで**クライアント側 xml = "1"** (true) を指定すると、クライアント側の xml 書式設定が要求されます。 この場合、FOR XML NESTED を指定できます。 FOR XML AUTO を指定した場合、XML の書式設定はサーバー側で行われますが、テンプレートには**クライアント側 xml = "1"** が指定されています。  
  
## <a name="see-also"></a>参照  
 [XML のセキュリティに関する考慮事項 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [クライアント側の XML 書式設定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [サーバー側の XML 書式設定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/server-side-xml-formatting-sqlxml-4-0.md)  
  
  
