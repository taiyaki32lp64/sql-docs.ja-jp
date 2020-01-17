---
title: sql:variable() 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 56a8c53a22fefec7fbda4c2ac7476ae46d664199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946007"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery Extension Functions - sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SQL リレーショナル値を含む変数を XQuery 式内部に公開します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>コメント  
 トピックの説明に従って[XML 内リレーショナル データのバインド](../t-sql/xml/binding-relational-data-inside-xml-data.md)を使用する場合は、この関数を使用することができます[XML データ型のメソッド](../t-sql/xml/xml-data-type-methods.md)XQuery 内部にリレーショナル値を公開します。  
  
 たとえば、 [query() メソッド](../t-sql/xml/query-method-xml-data-type.md)に格納されている XML インスタンスに対してクエリを指定するために使用する**xml**データ型の変数または列。 また、場合によっては、リレーショナル データと XML データを一緒にするために、[!INCLUDE[tsql](../includes/tsql-md.md)] 変数の値 (パラメーター) をクエリで使用することもできます。 これを行うには、使用する、 **sql:variable**関数。  
  
 SQL 値は、対応する XQuery 値にマップされ、その型は、対応する SQL 型に相当する XQuery 基本データ型になります。  
  
 のみを参照することができます、 **xml**インスタンス コンテキスト、ソースの式の XML DML 挿入ステートメントで、それ以外の場合は型の値を参照することはできません**xml**または共通言語ランタイム (CLR)ユーザー定義型です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. TRANSACT-SQL 変数の値を XML にするのに sql:variable() 関数の使用  
 次の例では、次の構成されている XML インスタンスを構築します。  
  
-   XML 以外の列の値 (`ProductID`)。 [Sql:column() 関数](../xquery/xquery-extension-functions-sql-column.md)XML にこの値をバインドするために使用します。  
  
-   他のテーブルの XML 以外の列の値 (`ListPrice`)。 ここでも、 `sql:column()` XML にこの値をバインドするために使用します。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 変数の値 (`DiscountPrice`)。 `sql:variable()` XML にこの値をバインドするメソッドを使用します。  
  
-   値 (`ProductModelName`) から、 **xml**型の列で、クエリをさらに興味深いにするようにします。  
  
 クエリは次のとおりです。  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   内の XQuery、`query()`メソッドは、XML を構築します。  
  
-   `namespace`で名前空間プレフィックスを定義するキーワードが使用される、 [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)します。 これは、`ProductModelName`から属性値を取得、`CatalogDescription xml`型の列に関連付けられているスキーマがあります。  
  
 結果を次に示します。  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server XQuery 拡張関数します。](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML データのインスタンスの作成](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
