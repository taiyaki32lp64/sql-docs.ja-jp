---
title: シーケンス型の照合 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
author: rothja
ms.author: jroth
ms.openlocfilehash: 164092d91a6450815662c5022ac6eb62941e3b16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946223"
---
# <a name="type-system---sequence-type-matching"></a>型システム - シーケンス型の照合
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 式の値は必ず 0 個以上のアイテムのシーケンスになります。 項目には、アトミック値またはノードのいずれかを指定できます。 シーケンス型は、特定の種類と、クエリ式によって返されるシーケンス型と一致する機能を指します。 例:  
  
-   式の値がアトミックの場合は、integer、decimal、または文字列型を把握したい場合があります。  
  
-   式の値が XML ノードの場合、その値がコメント ノード、処理命令ノード、またはテキスト ノードであるかどうかを確認できます。  
  
-   XML 要素または属性ノード、特定の名前と型のかどうか、式を返しますを把握したい場合があります。  
  
 使用することができます、`instance of`シーケンス型の照合のブール演算子。 詳細については、`instance of`式を参照してください[SequenceType 式&#40;XQuery&#41;](../xquery/sequencetype-expressions-xquery.md)します。  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>式から返されるアトミック値の型の比較  
 式には、アトミック値のシーケンスが返された場合は、シーケンス内の値の型を確認する必要があります。 次の例は、シーケンス型の構文を使用して式から返されるアトミック値の型を評価する方法を示しています。  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>例:シーケンスが空かどうかを判断します。  
 **Empty()** シーケンスの種類は、指定された式で返されるシーケンスが空のシーケンスであるかどうかを確認するシーケンス型の式で使用できます。  
  
 XML スキーマは、次の例では、<`root`> 要素を nilled します。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 ここでは、型指定された XML インスタンスの値を指定する場合、<`root`> 要素、 `instance of empty()` False を返します。  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 場合、<`root`> 要素は、インスタンスで nilled は、その値は空のシーケンスと`instance of empty()`True を返します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>例:属性値の型を決定します。  
 場合によっては、処理する前に、式によって返されるシーケンス型を評価することがあります。 たとえば、ノードが union 型として定義されている XML スキーマがあります。 次の例では、コレクション内の XML スキーマ定義属性`a`10 進数または文字列の値を持つができる union 型として型。  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 型指定された XML インスタンスを処理する前に、属性 `a` の値の型を確認できます。 次の例では、属性 `a` の値は小数型です。 そのため`, instance of xs:decimal`True を返します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 ここで、属性 `a` の値を文字列型に変更します。 `instance of xs:string`は True を返します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>例:シーケンス式のカーディナリティ  
 この例では、シーケンス式のカーディナリティの効果を示します。 次の XML スキーマ定義を <`root`> 内のバイト型、nillable 要素。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 次のクエリでは、式により単一のバイト型が返されるので、`instance of` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 行った場合、<`root`> 要素 nil、値は空のシーケンス。 つまり、式 `/root[1]` から空のシーケンスが返されます。 そのため、 `instance of xs:byte` False を返します。 この場合の既定のカーディナリティは 1 であることに注意してください。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 出現インジケーター (`?`) を追加してカーディナリティを指定すると、シーケンス式から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 2 つの段階で、シーケンス型の式でのテストが完了したことに注意してください。  
  
1.  最初に、テストを決定式の型が指定した型と一致するかどうか。  
  
2.  その場合、テストは、式によって返される項目の数が指定された出現インジケーターと一致するかどうか決定をします。  
  
 どちらにも該当する場合、`instance of` 式から True が返されます。  
  
### <a name="example-querying-against-an-xml-type-column"></a>例:Xml 型の列に対するクエリを実行します。  
 次の例では、クエリがの Instructions 列に対して指定されて**xml**で入力、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]データベース。 Instructions 列にはスキーマが関連付けられているので、この列は型指定された XML 列です。 XML スキーマで整数型の `LocationID` 属性が定義されます。 そのため、シーケンス式で、 `instance of xs:integer?` True を返します。  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>式によって返されるノードの型の比較  
 式ノードのシーケンスを返す場合は、シーケンス内のノードの型を確認する必要があります。 次の例では、シーケンス型の構文を使用して、式によって返されるノードの種類を評価する方法を示します。 次のシーケンス型を使用できます。  
  
-   **item()** -シーケンス内の任意の項目に一致します。  
  
-   **node()** -シーケンスがノードであるかどうかを決定します。  
  
-   **processing-instruction()** -式が処理命令を返すかどうかを決定します。  
  
-   **comment()** -式がコメントを返すかどうかを決定します。  
  
-   **document-node()** -式がドキュメント ノードを返すかどうかを決定します。  
  
 次の例では、これらのシーケンス型を示します。  
  
### <a name="example-using-sequence-types"></a>例:シーケンス型の使用  
 この例では、いくつかのクエリは、型指定されていない XML 変数に対して実行されます。 これらのクエリでは、シーケンス型の使用について説明します。  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 最初のクエリでは、式は型指定された要素の値を返します。 <`a`>。 2 番目のクエリでは、式は要素を返します。 <`a`>。 どちらもアイテム。 そのため、両方のクエリは、True を返します。  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 次の 3 つのクエリのすべての XQuery 式が要素ノードの子を返す、<`root`> 要素。 そのため、シーケンス型の式 `instance of node()` から True が返され、他の 2 つの式 `instance of text()` と `instance of document-node()` からは False が返されます。  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 次のクエリで、`instance of document-node()`ために、式が True を返しますの親、<`root`> 要素はドキュメント ノードです。  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 次のクエリでは、式は、XML インスタンスから最初のノードを取得します。 このノードは処理命令ノードなので、`instance of processing-instruction()` 式により True が返されます。  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 特定の制限事項を次に示します。  
  
-   **document-node()** コンテンツ タイプの構文はサポートされません。  
  
-   **processing-instruction (name)** 構文がサポートされていません。  
  
## <a name="element-tests"></a>要素のテスト  
 要素のテストを使用して、特定の名前と型を持つ要素ノード、式から返された要素ノードと一致します。 次のような要素のテストを使用できます。  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>属性のテスト  
 属性のテストでは、式から返された属性が属性ノードであるかどうかが判断されます。 これらの属性のテストを使用することができます。  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>テストの例  
 次の例は、要素のテストおよび属性のテストが役立つシナリオを示しています。  
  
### <a name="example-a"></a>例 A  
 次の XML スキーマ定義、`CustomerType`複合型を <`firstName`> と <`lastName`> 要素は省略可能です。 指定された XML インスタンスの場合は、特定の顧客名が存在するかどうかを確認する必要があります。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 次のクエリは、`instance of element (firstName)`を決定する式かどうかの最初の子要素 <`customer`> 名を持つ要素は、<`firstName`>。 この場合、True が返されます。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 削除する場合、<`firstName`> インスタンス要素は、クエリは False を返します。  
  
 また、次を使用することができます。  
  
-   `element(ElementName, ElementType?)`に次のクエリで示すように、型の構文をシーケンス処理します。 この構文では、名前が `firstName` で型が `xs:string` の NULL 要素ノードまたは NULL 以外の要素ノードが照合されます。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   `element(*, type?)`に次のクエリで示すように、型の構文をシーケンス処理します。 型がある場合、要素ノードに一致する`xs:string`の名前に関係なく、します。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>例 B  
 次の例では、式によって返されたノードが特定の名前を持つ要素ノードであるかどうかを確認する方法を示します。 使用して、 **element()** をテストします。  
  
 次の例では、2 つの <`Customer`> の 2 つのさまざまな種類のクエリ対象の XML インスタンス内の要素は`CustomerType`と`SpecialCustomerType`します。 型を認識することを前提としています、<`Customer`> 式によって返される要素。 次の XML スキーマ コレクションでは、`CustomerType` 型と `SpecialCustomerType` 型を定義しています。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 この XML スキーマ コレクションの作成に使用する型指定された**xml**変数。 この変数に割り当てられている XML インスタンスでは、2 つがあります <`customer`> の 2 つの異なる型の要素。 最初の要素は `CustomerType` 型で、2 つ目の要素は `SpecialCustomerType` 型です。  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 次のクエリで、`instance of element (*, x:SpecialCustomerType ?)` 式は False を返します。この式で返されている最初の customer 要素が、`SpecialCustomerType` 型ではないためです。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 以前のクエリの式の変更を 2 つ目を取得するかどうかは <`customer`> 要素 (`/x:customer)[2]`)、`instance of`は True を返します。  
  
### <a name="example-c"></a>例 C  
 この例では、属性のテストを使用します。 次の XML スキーマでは、CustomerID、Age 属性 CustomerType 複合型を定義します。 Age 属性は省略可能です。 特定の XML インスタンスに対して Age 属性に存在するかどうかを判断することがあります、<`customer`> 要素。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 次のクエリでは、クエリ対象の XML インスタンスに `Age` という名前の属性ノードが存在するので、True が返されます。 この式では、`attribute(Age)` 属性のテストを使用しています。 属性の順序が決まっていないので、クエリでは FLWOR 式を使用してすべての属性を取得し、`instance of` 式を使用して各属性をテストします。 例では、最初に、型指定された XML スキーマ コレクションを作成**xml**変数。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 省略可能な `Age` 属性をインスタンスから削除すると、上記のクエリにより False が返されます。  
  
 属性名と型を指定することができます (`attribute(name,type)`) 属性のテスト。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 または、指定することができます、`attribute(*, type)`シーケンス型の構文。 これは、属性の型が名前に関係なく、指定した型と一致する場合で、属性ノードと一致します。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 特定の制限事項を次に示します。  
  
-   要素のテストには、出現インジケーターで、型名を続けて ( **?** )。  
  
-   **element (ElementName, TypeName)** はサポートされていません。  
  
-   **要素 (\*、TypeName)** はサポートされていません。  
  
-   **schema-element()** はサポートされていません。  
  
-   **schema-attribute (attributename)** はサポートされていません。  
  
-   明示的に照会する**xsi:type**または**xsi:nil**はサポートされていません。  
  
## <a name="see-also"></a>関連項目  
 [システム入力&#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
