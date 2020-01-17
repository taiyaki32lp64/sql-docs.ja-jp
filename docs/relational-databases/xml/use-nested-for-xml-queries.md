---
title: 入れ子になった FOR XML クエリの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], nested FOR XML
- nested FOR XML queries
ms.assetid: 7604161a-a958-446d-b102-7dee432979d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91ba54ce9141cd0e891e442c5cb89aab02dec1f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001721"
---
# <a name="use-nested-for-xml-queries"></a>入れ子になった FOR XML クエリの使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **xml** データ型と [FOR XML クエリの TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md) を使用すると、FOR XML クエリによって返された XML を、サーバー側およびクライアント側で処理することができます。  
  
## <a name="processing-with-xml-type-variables"></a>xml 型の変数を使用した処理  
 FOR XML クエリの結果を **xml** 型の変数に代入できます。また、XQuery を使用して結果にクエリを実行し、その結果を **xml** 型の変数に代入してからさらに処理を加えることができます。  
  
```  
DECLARE @x xml  
SET @x=(SELECT ProductModelID, Name  
        FROM Production.ProductModel  
        WHERE ProductModelID=122 or ProductModelID=119  
        FOR XML RAW, TYPE)  
SELECT @x  
-- Result  
--<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
--<row ProductModelID="119" Name="Bike Wash" />  
```  
  
 いずれかの `@x`xml **データ型メソッドを使用して、変数** に返された XML にさらに処理を加えることができます。 たとえば、 `ProductModelID` value() メソッド [を使用して、](../../t-sql/xml/value-method-xml-data-type.md)属性の値を取得できます。  
  
```  
DECLARE @i int;  
SET @i = (SELECT @x.value('/row[1]/@ProductModelID[1]', 'int'));  
SELECT @i;  
```  
  
 次の例では、 `FOR XML` 句に **ディレクティブが指定されているので、** クエリの結果が `TYPE` xml `FOR XML` 型で返されます。  
  
```  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=119 or ProductModelID=122  
FOR XML RAW, TYPE,ROOT('myRoot');  
  
```  
  
 結果を次に示します。  
  
```  
<myRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
</myRoot>  
```  
  
 結果は **xml** 型なので、次のクエリのように、この XML に対していずれかの **xml** データ型メソッドを直接指定することができます。 クエリでは、[query() メソッド (xml データ型)](../../t-sql/xml/query-method-xml-data-type.md) が使用され、<`row`> 要素の最初の <`myRoot`> 子要素が取得されます。  
  
```  
SELECT  (SELECT ProductModelID, Name  
         FROM Production.ProductModel  
         WHERE ProductModelID=119 or ProductModelID=122  
         FOR XML RAW, TYPE,ROOT('myRoot')).query('/myRoot[1]/row[1]');  
  
```  
  
 結果を次に示します。  
  
```  
<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
```  
  
## <a name="returning-inner-for-xml-query-results-to-outer-queries-as-xml-type-instances"></a>内側の FOR XML クエリの結果を外側のクエリに xml 型インスタンスとして返す  
 入れ子構造の `FOR XML` クエリを記述して、内側のクエリの結果を **xml** 型で外側のクエリに返すことができます。 例:  
  
```  
SELECT Col1,   
       Col2,   
       ( SELECT Col3, Col4   
        FROM  T2  
        WHERE T2.Col = T1.Col  
        ...  
        FOR XML AUTO, TYPE )  
FROM T1  
WHERE ...  
FOR XML AUTO, TYPE;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   内側の `FOR XML` クエリで生成された XML は、外側の `FOR XML`で生成された XML に追加されます。  
  
-   内側のクエリでは、 `TYPE` ディレクティブが指定されています。 このため、内側のクエリから返される XML データは、 **xml** 型になります。 TYPE ディレクティブを指定しなかった場合、内側の `FOR XML` クエリの結果は **nvarchar(max)** 型として返され、XML データはエンティティ化されます。  
  
## <a name="controlling-the-shape-of-resulting-xml-data"></a>結果の XML データ構造の制御  
 入れ子構造の FOR XML クエリを使用すると、結果の XML データ構造の定義を制御しやすくなります。 入れ子構造の FOR XML クエリを使用して、一部が属性中心で、一部が要素中心の XML を作成できます。  
  
 入れ子構造の FOR XML クエリを使用して属性中心と要素中心の両方の XML を指定する方法の詳細については、「 [FOR XML クエリと入れ子になった FOR XML クエリの比較](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md) 」および「 [入れ子になった FOR XML クエリを使用した XML の構造化](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md)」を参照してください。  
  
 入れ子構造で AUTO モードの FOR XML クエリを指定することで、兄弟を含む XML 階層を生成できます。 詳細については、「 [入れ子になった AUTO モードのクエリを使用した兄弟の生成](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)」を参照してください。  
  
 使用するモードに関係なく、入れ子構造の FOR XML クエリを使用すると、結果の XML の構造の定義を制御しやすくなります。 入れ子構造の FOR XML クエリは、EXPLICIT モードのクエリの代わりに使用できます。  
  
## <a name="examples"></a>使用例  
 ここでは、入れ子になった FOR XML クエリの例を紹介します。  
  
 [FOR XML クエリと入れ子になった FOR XML クエリの比較](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md)  
 単一レベルの FOR XML クエリと入れ子になった FOR XML クエリを比較します。 この例には、属性中心と要素中心の両方の XML をクエリの結果として指定する方法が示されています。  
  
 [入れ子になった AUTO モードのクエリを使用した兄弟の生成](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)  
 入れ子構造で AUTO モードのクエリを使用して兄弟を生成する方法を示します。  
  
 [ASP.NET における入れ子になった FOR XML クエリの使用](../../relational-databases/xml/use-nested-for-xml-queries-in-asp-net.md)  
 ASPX アプリケーションで FOR XML を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]から XML を返す方法を示します。  
  
 [入れ子になった FOR XML クエリを使用した XML の構造化](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md)  
 入れ子になった FOR XML クエリを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって作成される XML ドキュメントの構造を制御する方法を示します。  
  
  
