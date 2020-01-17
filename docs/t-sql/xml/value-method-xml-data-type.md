---
title: value() メソッド (xml データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9224e9050ecf01255151e5ec8e11ecaf282d7387
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051217"
---
# <a name="value-method-xml-data-type"></a>value() メソッド (xml データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML に対して XQuery を実行し、SQL 型の値を返します。 このメソッドは、スカラー値を返します。  
  
 このメソッドは、通常、**xml** 型の列、パラメーター、または変数に格納されている XML インスタンスから値を取得するために使用します。 このメソッドを使用すると、XML データと XML 型ではない列のデータを結合したり、比較する SELECT クエリを指定したりすることができます。  
  
## <a name="syntax"></a>構文  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>引数  
 *XQuery*  
 XML インスタンス内のデータを取得する *XQuery* 式 (文字列リテラル) です。 XQuery により、返される値は最大 1 つである必要があります。 それ以外の場合は、エラーが返されます。  
  
 *SQLType*  
 正常な結果として返される SQL 型 (文字列リテラル) です。 このメソッドの戻り値の型は、*SQLType* パラメーターと一致します。 *SQLType* は、**xml** データ型、共通言語ランタイム (CLR) ユーザー定義型、**image**、**text**、**ntext**、または **sql_variant** データ型にすることはできません。 *SQLType* には、SQL ユーザー定義データ型を指定できます。  
  
 **value()** メソッドは、[!INCLUDE[tsql](../../includes/tsql-md.md)] の CONVERT 演算子を暗黙的に使用し、XQuery 式の結果 (シリアル化された文字列形式) を XSD 型から [!INCLUDE[tsql](../../includes/tsql-md.md)] 変換で指定されている対応する SQL 型に変換しようと試みます。 CONVERT の型キャストの規則の詳細については、「[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  パフォーマンス上の理由から、リレーショナル値との比較を行う述語内では **value()** メソッドではなく、**exist()** と **sql:column()** を使用してください。 これは、下の例 D で示しています。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. xml 型の変数に対する value() メソッドの使用  
 次の例では、XML インスタンスが `xml` 型の変数に格納されています。 `value()` メソッドは、XML から `ProductID` 属性の値を取得します。 その後、この値は `int` 変数に代入されます。  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 値 1 が結果として返されます。  
  
 この場合、XML インスタンスに `ProductID` 属性は 1 つしかありませんが、静的な型指定の規則により、パス式がシングルトンを返すことを明示的に指定する必要があります。 このため、パス式の末尾に `[1]` が追加されています。 静的な型指定の詳細については、「[XQuery と静的な型指定](../../xquery/xquery-and-static-typing.md)」を参照してください。  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. value() メソッドを使用した xml 型列の値の取得  
 次のクエリは、`AdventureWorks` データベースの **xml** 型の列 (`CatalogDescription`) に対して指定されています。 このクエリは、この列に格納されている各 XML インスタンスから `ProductModelID` 属性の値を取得します。  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `namespace` キーワードを使用して名前空間プレフィックスが定義されています。  
  
-   静的な型指定の要件により、`[1]` メソッドのパス式の末尾に `value()` を追加して、パス式が単一の値を返すことを明示的に指定しています。  
  
 結果の一部を次に示します。  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. value() メソッドと exist() メソッドを使用した xml 型列の値の取得  
 次の例では、**xml** データ型の `value()` メソッドと [exist() メソッド](../../t-sql/xml/exist-method-xml-data-type.md)の使い方を示しています。 `value()` メソッドは、XML から `ProductModelID` 属性値を取得するために使用されます。 `WHERE` 句の `exist()` メソッドは、テーブルの行をフィルターで選択するために使用されています。  
  
 このクエリは、要素の 1 つとして保証内容 (<`Warranty`> 要素) を含む XML インスタンスから製品モデル ID を取得します。 `WHERE` 句の条件では、`exist()` メソッドを使用して、この条件を満たす行のみを取得しています。  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `CatalogDescription` 列は、型指定された XML 列です。 つまり、この列にはスキーマ コレクションが関連付けられています。 [XQuery プロローグ](../../xquery/modules-and-prologs-xquery-prolog.md)では、名前空間の宣言を使用して、後でクエリ本文で使用するプレフィックスを定義しています。  
  
-   `exist()` メソッドが `1` (True) を返す場合、XML インスタンスには特性の 1 つとして <`Warranty`> 子要素が含まれています。  
  
-   その場合は、`value()` 句の `SELECT` メソッドが、`ProductModelID` 属性の値を整数値として取得します。  
  
 結果の一部を次に示します。  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. value() メソッドの代替としての exist() メソッドの使用  
 パフォーマンス上の理由から、リレーショナル値との比較を行う述語内では `value()` メソッドではなく、`exist()` と `sql:column()` を使用してください。 例:  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 上記のクエリは、次のように記述することもできます。  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>参照  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
