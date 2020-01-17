---
title: クライアント側とサーバー側の XML 書式設定 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4eaa4667db1e8b6ed789e2adb90bc8d72c1b02e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012349"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>クライアント側とサーバー側の XML 書式設定 (SQLXML 4.0)
  ここでは、SQLXML における、クライアント側とサーバー側の XML 書式設定の一般的な違いについて説明します。  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>クライアント側の書式設定では複数の行セット クエリがサポートされない  
 複数の行セットを生成するクエリは、クライアント側の XML 書式設定を使用するときにはサポートされません。 たとえば、クライアント側の書式設定が指定されている仮想ディレクトリがあるとし、 2 つの SELECT ステートメントには次のサンプル テンプレートで、  **\<sql:query >** ブロックします。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 このテンプレートはアプリケーション コードで実行できます。実行すると、クライアント側の XML 書式設定では複数の行セットの書式設定がサポートされていないため、エラーが返されます。 2 つのクエリを指定する場合は、各 **\<sql:query >** ブロックでは、目的の結果が表示されます。  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>マップとは異なるクライアント vs でのタイムスタンプ。サーバー側の書式設定  
 サーバー側の XML 書式設定では、XMLDATA オプションがクエリで指定される場合、`timestamp` 型のデータベース列が i8 XDR 型にマップされます。  
  
 クライアント側の XML 書式設定では、バイナリの base64 オプションがクエリで指定されているかどうかに従って、`timestamp` 型のデータベース列が `uri` または `bin.base64` XDR 型にマップされます。 `bin.base64` XDR 型は、この型に変換されますので、アップデート グラムや一括読み込み機能を使用する場合に便利です、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `timestamp`型。 この方法で、挿入、更新、または削除操作が成功します。  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>サーバー側の書式設定ではサブタイプの VARIANT 型も使用される  
 サーバー側の XML 書式設定では、サブタイプの VARIANT 型も使用されます。 クライアント側の XML 書式設定を使用する場合、variant は Unicode 文字列に変換され、サブタイプの VARIANT は使用されません。  
  
## <a name="nested-mode-vs-auto-mode"></a>モードとの入れ子になった。AUTO モード  
 クライアント側の FOR XML の NESTED モードは、サーバー側の FOR XML の AUTO モードに似ていますが、次の点が異なります。  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>サーバー側で AUTO モードを使用してビューにクエリを実行すると、ビュー名が結果の XML 内の要素名として返されます。  
 たとえば、Person.Contact テーブル、AdventureWorksdatabase の次のビューが作成されることを想定します。  
  
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
  
 テンプレートを実行すると、次の XML が返されます。 (部分的な結果のみ表示されます。要素名には、クエリの実行対象となるビューの名前に注意してください。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 クライアント側の書式設定を、対応する NESTED モードで指定すると、ベース テーブル名が結果の XML 内の要素名として返されます。 たとえば、次の更新後のテンプレートは、同じ SELECT ステートメントを実行が、クライアント側で実行される XML の書式設定 (つまり、**クライアント側の xml**に設定されてテンプレートの場合は true)。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT *  
    FROM   ContactView  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 このテンプレートを実行するには、次の XML が生成されます。 この場合、ベース テーブル名が要素名になっていることに注意してください。  
  
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
  
 クライアント側の FOR XML を NESTED モードで使用すると、テーブル名が、結果の XML 内の要素名として返されます。 (クエリで指定されているテーブルの別名は使用されません)。たとえば、次のテンプレートを考えてみます。  
  
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
  
 サーバー上で XML の書式設定が行われた場合 (**クライアント側の xml「0」を =** )、dbobject クエリを実行 (指定したエイリアスがある場合) 場合でも実際のテーブルおよび列の名前が返されるを取得する列の別名を使用することができます。 たとえば、次のテンプレートが、クエリを実行し、サーバーで行われる XML の書式設定 (、**クライアント側の xml**オプションが指定されていないと、**クライアントで実行**のオプションが選択されていない、仮想ルート)。 このクエリでは、クライアント側の NESTED モードではなく AUTO モードも指定されています。  
  
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
  
-   指定すると**クライアント側の xml =「0」** (false) のテンプレートで、ユーザーが要求するサーバー側で XML 書式を設定します。 したがって、サーバーでは NESTED オプションが認識されないので、FOR XML NESTED は指定できません。 これにより、エラーが発生します。 この場合、サーバーで認識される AUTO、RAW、または EXPLICIT モードを使用する必要があります。  
  
-   指定すると**クライアント側の xml =「1」** (true) のテンプレートで、ユーザーが要求するクライアント側の XML 書式設定します。 この場合、FOR XML NESTED を指定できます。 FOR XML AUTO を指定すると、XML の書式設定場合は、サーバー側では**クライアント側の xml =「1」** テンプレートで指定されています。  
  
## <a name="see-also"></a>参照  
 [XML のセキュリティに関する考慮事項の&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [クライアント側の XML 書式設定&#40;SQLXML 4.0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [サーバー側の XML 書式設定&#40;SQLXML 4.0&#41;](server-side-xml-formatting-sqlxml-4-0.md)  
  
  
