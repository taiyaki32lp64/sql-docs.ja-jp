---
title: WITH XMLNAMESPACES を使用したクエリへの名前空間の追加 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbb7cbdda657ef59491cfbb2c1651b969d04428
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287719"
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>WITH XMLNAMESPACES を使用したクエリへの名前空間の追加
  [WITH XMLNAMESPACES (Transact-SQL)](/sql/t-sql/xml/with-xmlnamespaces) は、次の方法で名前空間 URI のサポートを提供します。  
  
-   [FOR XML クエリを使用した XML の構築](for-xml-sql-server.md) の際に、URI マッピングの名前空間プレフィックスを使用できるようにします。  
  
-   [xml データ型メソッド](/sql/t-sql/xml/xml-data-type-methods)の静的な名前空間コンテキストに、URI マッピングの名前空間を使用できるようにします。  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>FOR XML クエリでの WITH XMLNAMESPACES の使用  
 WITH XMLNAMESPACES を使用すると、FOR XML クエリに XML 名前空間を含めることができます。 たとえば、次の FOR XML クエリについて考えてみます。  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 結果を次に示します。  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 FOR XML クエリにより構築された XML に名前空間を追加するには、まず WITH NAMESPACES 句を使用して URI マッピングの名前空間プレフィックスを指定します。 次に、名前空間プレフィックスを使用して、次に示す変更後のクエリのように、クエリに名前を指定します。 WITH XMLNAMESPACES 句で URI (`ns1`) マッピングの名前空間プレフィックス (`uri`) を指定していることに注意してください。 FOR XML クエリにより構築された要素名と属性名を指定する際に `ns1` プレフィックスを使用します。  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 結果の XML には、指定した名前空間プレフィックスが含まれています。  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 WITH XMLNAMESPACES 句には、次の制約があります。  
  
-   FOR XML クエリの RAW、AUTO、PATH モードしかサポートしていません。 EXPLICIT モードはサポートしていません。  
  
-   FOR XML クエリの名前空間プレフィックスおよび **xml** データ型メソッドにしか影響しません。XML パーサーには影響しません。 たとえば、次のクエリは、XML ドキュメントで myNS プレフィックスの名前空間が宣言されていないため、エラーを返します。  
  
-   WITH XMLNAMESPACES 句が使用されている場合、FOR XML の XMLSCHEMA ディレクティブおよび XMLDATA ディレクティブは使用できません。  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('http://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>XSINIL ディレクティブの使用  
 ELEMENTS XSINIL ディレクティブを使用している場合は、WITH XMLNAMESPACES 句に xsi プレフィックスは定義できません。 代わりに、ELEMENTS XSINIL を使用すると、自動的に xsi プレフィックスが追加されます。 次のクエリは、要素中心型の XML を生成する ELEMENTS XSINIL を使用しています。生成された XML では、NULL 値が **xsi:nil** 属性が True に設定されている要素にマップされます。  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 結果を次に示します。  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>既定の名前空間の指定  
 名前空間プレフィックスを宣言する代わりに、DEFAULT キーワードを使用して既定の名前空間を宣言することもできます。 DEFAULT キーワードは、FOR XML クエリ中で、既定の名前空間を結果の XML の XML ノードにバインドします。 次の例では、WITH XMLNAMESPACES によって、2 つの名前空間プレフィックスを同時に 1 つの既定の名前空間に定義しています。  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 この FOR XML クエリは、要素中心の XML を生成します。 このクエリでは、どちらの名前空間プレフィックスもノードの命名に使用されていることに注意してください。 SELECT 句内では、ProductID、Name、Color のいずれもプレフィックスを使った名前を指定していません。 その結果、結果の XML の対応する要素は、既定の名前空間に属することになります。  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 次のクエリは前のクエリとほぼ同じですが、FOR XML AUTO モードが指定されています。  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>事前定義された名前空間の使用  
 事前定義された名前空間を使用する場合は、ELEMENTS XSINIL 使用時の xml 名前空間と xsi 名前空間を除き、WITH XMLNAMESPACES を使用して名前空間のバインドを明示的に指定する必要があります。 次のクエリは、事前定義された名前空間 (`urn:schemas-microsoft-com:xml-sql`) 用に、URI の名前空間プレフィックスのバインドを明示的に定義しています。  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 結果は次のとおりです。 SQLXML では、この XML テンプレートがよく使用されます。 詳細については、「 [SQLXML 4.0 のプログラミング概念](../sqlxml/sqlxml-4-0-programming-concepts.md)」を参照してください。  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 次の PATH モード クエリで示すように、WITH XMLNAMESPACES を使用して明示的に定義せずに使用できる名前空間プレフィックスは xml のみです。 また、プレフィックスが宣言されている場合は、 http://www.w3.org/XML/1998/namespace 名前空間にバインドする必要があります。 SELECT 句に指定されている名前は、WITH XMLNAMESPACES を使用して明示的に定義されていない xml 名前空間を参照します。  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 @xml:lang 属性は、事前定義された xml 名前空間を使用します。 XML のバージョン 1.0 では、xml 名前空間のバインドを明示的に宣言する必要がないので、結果には名前空間のバインドの明示的な宣言が含まれません。  
  
 結果を次に示します。  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>xml データ型メソッドでの WITH XMLNAMESPACES の使用  
 SELECT クエリ ( [modify()](/sql/t-sql/xml/xml-data-type-methods) メソッドを使用している場合は UPDATE クエリ) に指定された **xml データ型メソッド** は、それぞれのプロローグの中で名前空間の宣言を個別に行う必要があります。 この作業には時間のかかる場合があります。 たとえば、次のクエリでは、カタログの説明に仕様が含まれる製品モデル ID を取得します。 つまり、<`Specifications`> 要素が含まれます。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 上記のクエリでは、**query()** メソッドと **exist()** メソッドのいずれのプロローグでも、同じ名前空間が宣言されています。 以下に例を示します。  
  
```  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 代わりに、WITH XMLNAMESPACES を最初に宣言して、名前空間プレフィックスをクエリで使用することもできます。 この場合は、 **query()** メソッドと **exist()** メソッドでは、それぞれのプロローグに名前空間の宣言を含める必要はありません。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 XQuery プロローグの明示的な宣言が、WITH 句で定義されている名前空間プレフィックスと既定の要素名前空間をオーバーライドしていることに注意してください。  
  
## <a name="see-also"></a>関連項目  
 [xml データ型メソッド](/sql/t-sql/xml/xml-data-type-methods)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server)   
 [WITH XMLNAMESPACES &#40;Transact-SQL&#41;](/sql/t-sql/xml/with-xmlnamespaces)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
