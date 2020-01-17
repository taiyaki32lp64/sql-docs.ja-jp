---
title: '例 : PATH モードの使用 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, examples
ms.assetid: 3564e13b-9b97-49ef-8cf9-6a78677b09a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd4b9487f6a185b76b5f4ee52d7a39f349906d46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943378"
---
# <a name="examples-using-path-mode"></a>例 :PATH モードの使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  次の例では、PATH モードで SELECT クエリから XML を生成する方法を示します。 これらのクエリの多くは、ProductModel テーブルの Instructions 列に格納されている、自転車製造手順の XML ドキュメントに対して指定されています。  
  
## <a name="specifying-a-simple-path-mode-query"></a>PATH モードの単純なクエリの指定  
 次のクエリには FOR XML PATH モードが指定されています。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   
       ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH;  
GO  
```  
  
 次の結果は、要素中心の XML です。結果の行セットの列値は、それぞれ 1 つの要素に格納されています。 `SELECT` 句に列の別名が指定されていないので、生成される子要素の名前は `SELECT` 句の対応する列名と同じになっています。 行セットの各行には <`row`> タグが追加されます。  
  
 ```
<row>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</row>  
<row>  
  <ProductModelID>119</ProductModelID>
  <Name>Bike Wash</Name>
</row>
```
  
 次の結果は、`RAW` オプションを指定した `ELEMENTS` モードのクエリと同じです。 返される結果は、結果セットの各行に既定の <`row`> 要素が追加された要素中心の XML です。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML RAW, ELEMENTS;  
```  
  
 必要に応じて、行要素の名前を指定して既定の <`row`> を上書きできます。 たとえば、次のクエリは行セットの行ごとに <`ProductModel`> 要素を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModel');  
GO  
```  
  
 結果の XML には指定した行要素名が使用されます。  
  
```
<ProductModel>
  <ProductModelID>122</ProductModelID>
  <Name>All-Purpose Bike Stand</Name>
</ProductModel>
<ProductModel>
  <ProductModelID>119</ProductModelID>
  <Name>Bike Wash</Name>
</ProductModel>
```
  
 長さがゼロの文字列を指定すると、囲み要素は生成されません。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('');  
GO  
```  
  
 結果を次に示します。  
  
```
<ProductModelID>122</ProductModelID>
<Name>All-Purpose Bike Stand</Name>
<ProductModelID>119</ProductModelID>
<Name>Bike Wash</Name>
```
  
## <a name="specifying-xpath-like-column-names"></a>XPath 形式の列名の指定  
 次のクエリでは、`ProductModelID` 列に指定した名前が '\@' で始まり、スラッシュ ('/') を含んでいません。 したがって、結果の XML では、<`row`> 要素の属性が生成され、対応する列値が設定されます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('ProductModelData');  
GO  
```  
  
 結果を次に示します。  
  
```
<ProductModelData id="122">
  <Name>All-Purpose Bike Stand</Name>
</ProductModelData>
<ProductModelData id="119">
  <Name>Bike Wash</Name>
</ProductModelData>
```
  
 `root` で `FOR XML`オプションを指定すると、単一の最上位要素を追加できます。  
  
```  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 階層を生成するには、PATH 形式の構文を使用できます。 たとえば、 `Name` 列の列名を "SomeChild/ModelName" に変更すると、次に示すように階層を伴う XML が返されます。  
  
```
<Root>
  <ProductModelData id="122">
    <SomeChild>
      <ModelName>All-Purpose Bike Stand</ModelName>
    </SomeChild>
  </ProductModelData>
  <ProductModelData id="119">
    <SomeChild>
      <ModelName>Bike Wash</ModelName>
    </SomeChild>
  </ProductModelData>
</Root>
```
  
 次のクエリは、指定した製品モデルの ID および名前以外に、その製品モデルに対応する製造手順書の場所を返します。 Instructions 列が **xml** 型なので、 **xml** データ型の **query()** メソッドを指定して場所を取得します。  
  
```  
SELECT ProductModelID AS "@id",  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') AS ManuInstr  
FROM Production.ProductModel  
WHERE ProductModelID = 7  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 次に結果の一部を示します。 列名として ManuInstr が指定されているので、**query()** メソッドが返す XML は、次に示すように <`ManuInstr`> タグで囲まれています。  

```
<Root>
  <ProductModelData id="7">
    <Name>HL Touring Frame</Name>
    <ManuInstr>
      <MI:Location xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"
        <MI:step>...</MI:step>...
      </MI:Location>
      ...
    </ManuInstr>
  </ProductModelData>
</Root> 
```

上記の FOR XML クエリで、<`Root`> 要素と <`ProductModelData`> 要素に対応する名前空間を含めることができます。 そのためには、WITH XMLNAMESPACES で名前空間のバインドのためのプレフィックスを定義しておき、FOR XML クエリで使用します。 詳細については、「 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)」を参照してください。  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES (  
   'uri1' AS ns1,    
   'uri2' AS ns2,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' as MI)  
SELECT ProductModelID AS "ns1:ProductModelID",  
       Name           AS "ns1:Name",  
       Instructions.query('  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ('ns2:ProductInfo'), root('ns1:root');  
GO  
```  
  
 `MI` では `WITH XMLNAMESPACES`プレフィックスも定義されています。 従って、指定された **xml** 型の **query()** メソッドにおいて、クエリ プロローグでこのプレフィックスは定義されていません。 結果を次に示します。  
  
```
<ns1:root xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">
  <ns2:ProductInfo>
    <ns1:ProductModelID>7</ns1:ProductModelID>
    <ns1:Name>HL Touring Frame</ns1:Name>
    <MI:Location xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" LaborHours="2.5" LotSize="100" MachineHours="3" SetupHours="0.5" LocationID="10" xmlns="">
    <MI:step>
      Insert <MI:material>aluminum sheet MS-2341</MI:material> into the <MI:tool>T-85A framing tool</MI:tool>.
    </MI:step>
    ...
    </MI:Location>
    ...
  </ns2:ProductInfo>
</ns1:root>
```
  
## <a name="generating-a-value-list-using-path-mode"></a>PATH モードを使用した値リストの生成  
 次のクエリは、製品モデルごとに製品 ID の値リストを生成します。 また、次の XML フラグメントで示すように製品 ID ごとに <`ProductName`> 子要素が生成されます。  

```
<ProductModelData ProductModelID="7" ProductModelName="..." ProductIDs="product id list in the product model">
  <ProductName>...</ProductName>
  <ProductName>...</ProductName>
  ...
</ProductModelData>
```
  
 求める XML を生成するクエリを次に示します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID     AS "@ProductModelID",  
       Name               AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')) AS "@ProductIDs",  
       (SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
        FOR XML PATH ('')) AS "ProductNames"  
FROM   Production.ProductModel  
WHERE  ProductModelID= 7 or ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   最初の `SELECT` サブクエリは、列名として `data()` を使用することで ProductID の一覧を返しています。 `FOR XML PATH`の行要素名として空文字列が指定されているので、要素は生成されません。 代わりに、値リストが `ProductID` 属性に割り当てられています。  
  
-   2 番目の `SELECT` サブクエリは、該当する製品モデルに含まれる製品名を取得します。 列名として `ProductNames` を指定しているので、生成した <`ProductName`> 要素は <`ProductNames`> 要素に囲まれた状態で返しています。  
  
 結果の一部を次に示します。  
  
```
<ProductModelData PId="7" ProductModelName="HL Touring Frame" ProductIDs="885 887 ...">
  <ProductNames>
    <ProductName>HL Touring Frame - Yellow, 60</ProductName>
    <ProductName>HL Touring Frame - Yellow, 46</ProductName>
  </ProductNames>
  ...
</ProductModelData>
<ProductModelData PId="9" ProductModelName="LL Road Frame" ProductIDs="722 723 724 ...">
  <ProductNames>
    <ProductName>LL Road Frame - Black, 58</ProductName>
    <ProductName>LL Road Frame - Black, 60</ProductName>
    <ProductName>LL Road Frame - Black, 62</ProductName>
    ...
  </ProductNames>
</ProductModelData>
```
  
 製品名を構成するサブクエリは、結果として返す文字列をエンティティ表記に変換してから XML に追加しています。 TYPE ディレクティブ `FOR XML PATH (''), type`を追加した場合、結果は **xml** 型で返され、エンティティ表記への変換は行われません。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@ProductModelID",  
      Name AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ProductIDs",  
       (  
       SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH (''), type  
       ) AS "ProductNames"  
  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
## <a name="adding-namespaces-in-the-resulting-xml"></a>結果の XML への名前空間の追加  
 「 [WITH XMLNAMESPACES を使用した名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)」で説明したように、WITH XMLNAMESPACES を使用すると PATH モードのクエリに名前空間を含めることができます。 たとえば、SELECT 句で指定する名前に名前空間のプレフィックスを追加できます。 次の `PATH` モードのクエリを実行すると、名前空間を伴った XML が生成されます。  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
GO  
```  
  
 <`English`> 要素に追加されている `@xml:lang` 属性は、定義済みの XML 名前空間で定義されています。  
  
 結果を次に示します。  

```
<Translation>
  <English xml:lang="en">food</English>
  <German xml:lang="ger">Essen</German>
</Translation>
```
  
 次のクエリは例 C と似ていますが、結果の XML に名前空間を含めるために `WITH XMLNAMESPACES` を使用している点が異なります。 詳細については、「 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)」を参照してください。  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES ('uri1' AS ns1,  DEFAULT 'uri2')  
SELECT ProductModelID AS "@ns1:ProductModelID",  
      Name AS "@ns1:ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ns1:ProductIDs",  
       (  
       SELECT ProductID AS "@ns1:ProductID",   
              Name AS "@ns1:ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH , type   
       ) AS "ns1:ProductNames"  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData'), root('root');  
```  
  
 結果を次に示します。  
  
```
<root xmlns="uri2" 
  xmlns:ns1="uri1">
  <ProductModelData ns1:ProductModelID="7" ns1:ProductModelName="HL Touring Frame" ns1:ProductIDs="885 887 888 889 890 891 892 893">
    <ns1:ProductNames>
      <row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="885" ns1:ProductName="HL Touring Frame - Yellow, 60" />
      <row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="887" ns1:ProductName="HL Touring Frame - Yellow, 46" />
      ...
    </ns1:ProductNames>
  </ProductModelData>
  <ProductModelData ns1:ProductModelID="9" ns1:ProductModelName="LL Road Frame" ns1:ProductIDs="722 723 724 725 726 727 728 729 730 736 737 738">
    <ns1:ProductNames>
      <row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="722" ns1:ProductName="LL Road Frame - Black, 58" />
      ...
    </ns1:ProductNames>
  </ProductModelData>
</root>
```
  
## <a name="see-also"></a>参照  
 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
