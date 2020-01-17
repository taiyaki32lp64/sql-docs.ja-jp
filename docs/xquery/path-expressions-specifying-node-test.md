---
title: パス式のステップでノード テストの指定 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- node test [XQuery]
ms.assetid: ffe27a4c-fdf3-4c66-94f1-7e955a36cadd
author: rothja
ms.author: jroth
ms.openlocfilehash: 28ac10e211d57fc9e118f47ccb9d506d6cb846e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946431"
---
# <a name="path-expressions---specifying-node-test"></a>パス式 - ノード テストの指定
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パス式の軸ステップには、次のコンポーネントが含まれてます。  
  
-   [軸](../xquery/path-expressions-specifying-axis.md)  
  
-   ノード テスト  
  
-   [(省略可能) 0 個以上のステップ修飾子](../xquery/path-expressions-specifying-predicates.md)  
  
 詳細については、次を参照してください。[パス式&#40;XQuery&#41;](../xquery/path-expressions-xquery.md)します。  
  
 ノード テストとは条件で、パス式の軸ステップの 2 番目のコンポーネントです。 ステップで選択されるすべてのノードは、この条件を満たす必要があります。 パス式 `/child::ProductDescription` の場合、ノード テストは `ProductDescription` です。 このステップでは、ProductDescription という名前の子要素ノードのみが取得されます。  
  
 ノード テストの条件には、次の情報を含めることができます。  
  
-   ノード名。 指定した名前を持つ、主ノード種別に属するノードのみが返されます。  
  
-   ノード型。 指定した型のノードのみが返されます。  
  
> [!NOTE]  
>  XQuery パス式で指定されるノード名には、Transact-SQL クエリと同じ照合順序依存の規則は適用されません。常に大文字と小文字が区別されます。  
  
## <a name="node-name-as-node-test"></a>ノード テストとしてのノード名  
 パス式のステップでノード名をノード テストとして指定する場合は、主ノード種別の概念を理解しておく必要があります。 すべての軸 (child、parent、attribute) には、主ノード種別があります。 以下に例を示します。  
  
-   attribute 軸には、属性のみを含めることができます。 したがって、属性ノードが attribute 軸の主ノード種別になります。  
  
-   その他の軸の場合、軸で選択されるノードに要素ノードを含めることができる場合は、要素がその軸の主ノード種別になります。  
  
 ノード名をノード テストとして指定すると、ステップから次の型のノードが返されます。  
  
-   軸の主ノード種別に属するノード。  
  
-   ノード テストに指定したのと同じ名前のノード。  
  
 たとえば、次のパス式について考えます。  
  
```  
child::ProductDescription   
```  
  
 この 1 ステップの式では、`child` 軸とそのノード名 `ProductDescription` をノード テストとして指定しています。 式は、child 軸の主ノード種別 (つまり要素ノード) に属する、ProductDescription という名前のノードのみを返します。  
  
 パス式 `/child::PD:ProductDescription/child::PD:Features/descendant::*,` には 3 つのステップがあります。 これらのステップでは、child 軸と descendant 軸を指定しています。 各ステップでは、ノード名がノード テストとして指定されています。 3 番目のステップのワイルドカード文字 (`*`) は、descendant 軸の主ノード種別に属するすべてのノードを示しています。 軸の主ノード種別により、選択されるノードの型が決まります。また、ノード名により、選択されるノードがフィルター選択されます。  
  
 その結果、この式が実行されると製品カタログ XML ドキュメントに対して、 **ProductModel**テーブルのすべての要素ノードの子を取得、\<機能 > 子要素ノードの\<ProductDescription > 要素。  
  
 パス式`/child::PD:ProductDescription/attribute::ProductModelID`は 2 つの手順の構成されます。 どちらのステップでも、ノード名をノード テストとして指定しています。 また、2 番目のステップでは attribute 軸を使用します。 したがって、各ステップでは、ノード テストに指定された名前を持つ、その軸の主ノード種別に属するノードが選択されます。 そのため、式を返します**ProductModelID**の属性ノード、 \<ProductDescription > 要素ノード。  
  
 ノード テストにノード名を指定する場合、次の例に示すように、ノードのローカル名やノードの名前空間プレフィックスにワイルドカード文字 (*) を使用することもできます。  
  
```  
declare @x xml  
set @x = '  
<greeting xmlns="ns1">  
   <salutation>hello</salutation>  
</greeting>  
<greeting xmlns="ns2">  
   <salutation>welcome</salutation>  
</greeting>  
<farewell xmlns="ns1" />'  
select @x.query('//*:greeting')  
select @x.query('declare namespace ns="ns1"; /ns:*')  
```  
  
## <a name="node-type-as-node-test"></a>ノード テストとしてのノード型  
 要素ノード以外のノード型を照会するには、ノード型テストを使用します。 次の表に示すように、使用できるノード型テストは 4 つあります。  
  
|ノード型|戻り値|例|  
|---------------|-------------|-------------|  
|`comment()`|コメント ノードの場合に True を返します。|`following::comment()` では、コンテキスト ノードの後にあるすべてのコメント ノードが選択されます。|  
|`node()`|ノードの種類に関係なく True を返します。|`preceding::node()` では、コンテキスト ノードの前にあるすべてのノードが選択されます。|  
|`processing-instruction()`|処理命令ノードの場合は True を返します。|`self::processing instruction()` では、コンテキスト ノード内のすべての処理命令ノードが選択されます。|  
|`text()`|テキスト ノードの場合は True を返します。|`child::text()` では、コンテキスト ノードの子にあたるテキスト ノードが選択されます。|  
  
 text() や comment() などのノード型がノード テストに指定された場合は、軸の主ノード種別にかかわらず、ステップでは指定された種類のノードが返されます。 たとえば、次のパス式は、コンテキスト ノードの子にあたるコメント ノードのみを返します。  
  
```  
child::comment()  
```  
  
 同様に、`/child::ProductDescription/child::Features/child::comment()`コメントの子ノードの取得、\<機能 > 子要素ノードの\<ProductDescription > 要素ノード。  
  
## <a name="examples"></a>使用例  
 次の例では、ノード名とノードの種類を比較します。  
  
### <a name="a-results-of-specifying-the-node-name-and-the-node-type-as-node-tests-in-a-path-expression"></a>A. ノード名とノード型をノード テストとしてパス式に指定した場合の結果  
 次の例では、単純な XML ドキュメントが割り当てられている、 **xml**型の変数。 このドキュメントに対しては、複数のパス式を使用してクエリが実行されます。 その後、結果が比較されます。  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
select @x.query('  
/child::a/child::b/descendant::*  
')  
```  
  
 この式では、`<b>` 要素ノードの子孫にあたる要素ノードが要求されます。  
  
 ノード テストのアスタリスク (`*`) は、ノード名のワイルドカード文字を示しています。 descendant 軸の主ノード種別は要素ノードです。 したがって、この式は、要素ノード `<b>` の子孫にあたるすべての要素ノードを返します。 つまり、次の結果に示すように、要素ノード `<c>` と `<d>` が返されます。  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 次のように、descendant 軸ではなく descendent-or-self 軸を指定すると、コンテキスト ノードとその子孫が返されます。  
  
```  
/child::a/child::b/descendant-or-self::*  
```  
  
 この式は、要素ノード `<b>` とその子孫にあたる要素ノードを返します。 子孫ノードを返すときに、descendant-or-self 軸の主ノード種別 (要素ノード型) により、返されるノードの種類が決まります。  
  
 結果を次に示します。  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 前の式では、ワイルドカード文字をノード名として使用しました。 代わりに、次の式に示すように `node()` 関数を使用できます。  
  
```  
/child::a/child::b/descendant::node()  
```  
  
 `node()`ノードの種類は、descendant 軸のすべてのノードが表示されます。 結果を次に示します。  
  
```  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
 さらに、descendant-or-self 軸と `node()` をノード テストに指定した場合は、すべての子孫、要素、テキスト ノード、およびコンテキスト ノードである `<b>` 要素が返されます。  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
### <a name="b-specifying-a-node-name-in-the-node-test"></a>B. ノード テストでのノード名の指定  
 次の例では、すべてのパス式でノード名をノード テストとして指定します。 結果として、すべての式により、ノード テストに指定したノード名を持つ、軸の主ノード種別に属するノードが返されます。  
  
 次のクエリ式を実行すると、`Production.ProductModel` テーブルに格納されている製品カタログ XML ドキュメントから <`Warranty`> 要素が返されます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:Warranty  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   XQuery プロローグ内の `namespace` キーワードにより、クエリ本文で使用するプレフィックスが定義されています。 XQuery プロローグの詳細については、次を参照してください。 [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)します。  
  
-   パス式の中にある 3 つのすべてのステップで、child 軸とノード テストとしてのノード名が指定されています。  
  
-   軸ステップの省略可能なステップ修飾子の部分は、式のどのステップにも指定されていません。  
  
 このクエリは、<`ProductDescription`> 要素の <`Features`> 子要素の <`Warranty`> 子要素を返します。  
  
 結果を次に示します。  
  
```  
<wm:Warranty xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
  <wm:Description>parts and labor</wm:Description>  
</wm:Warranty>     
```  
  
 次のクエリでは、パス式でノード テストにワイルドカード文字 (`*`) を指定しています。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 ワイルドカード文字は、ノード名に対して指定されています。 したがって、このクエリを実行すると、<`ProductDescription`> 要素ノードの <`Features`> 子要素ノードの子にあたる要素ノードがすべて返されます。  
  
 次のクエリは、ワイルドカード文字と共に名前空間が指定されている点を除けば、前のクエリと同じです。 結果として、その名前空間に含まれるすべての子要素ノードが返されます。 <`Features`> 要素には複数の名前空間の要素を含めることができることに注意してください。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 次のクエリに示すように、ワイルドカード文字を名前空間プレフィックスとして使用できます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*:Maintenance  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 このクエリでは、製品カタログ XML ドキュメントからすべての名前空間の <`Maintenance`> 子要素ノードが返されます。  
  
### <a name="c-specifying-node-kind-in-the-node-test"></a>C. ノード テストでのノードの種類の指定  
 次の例では、すべてのパス式でノードの種類をノード テストとして指定します。 結果として、すべての式がノード テストに指定した種類のノードを返します。  
  
 次のクエリでは、パス式で、3 番目のステップにノードの種類を指定しています。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::text()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 このクエリには、次の指定があります。  
  
-   パス式には、スラッシュ (`/`) で区切られた 3 つのステップがあります。  
  
-   これらの各ステップでは、child 軸を指定しています。  
  
-   最初の 2 つのステップではノード名をノード テストに指定し、3 番目のステップではノードの種類をノード テストに指定しています。  
  
-   この式は、<`ProductDescription`> 要素ノードの <`Features`> 子要素の子にあたるテキスト ノードを返します。  
  
 返されるテキスト ノードは 1 つだけです。 結果を次に示します。  
  
```  
These are the product highlights.   
```  
  
 次のクエリを実行すると、<`ProductDescription`> 要素の子にあたるコメント ノードが返されます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::comment()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   2 番目のステップでは、ノードの種類をノード テストに指定しています。  
  
-   結果として、この式は、<`ProductDescription`> 要素ノードの子にあたるコメント ノードを返します。  
  
 結果を次に示します。  
  
```  
<!-- add one or more of these elements... one for each specific product in this product model -->  
<!-- add any tags in <specifications> -->      
```  
  
 次のクエリを実行すると、最上位の処理命令ノードが取得されます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果を次に示します。  
  
```  
<?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>   
```  
  
 `processing-instruction()` ノード テストには、文字列リテラル パラメーターを渡すことができます。 この場合、クエリは、名前属性の値が引数に指定された文字列リテラルと一致する処理命令を返します。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction("xml-stylesheet")  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 次に、特定の制限事項を示します。  
  
-   拡張された SequenceType ノード テストはサポートされません。  
  
-   processing-instruction(name) はサポートされません。 name は引用符で囲む必要があります。  
  
  
