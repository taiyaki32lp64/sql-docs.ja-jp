---
title: SequenceType 式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
author: rothja
ms.author: jroth
ms.openlocfilehash: e7c3cdf33b0765ba50e5553f3bc31fd5c69312e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946283"
---
# <a name="sequencetype-expressions-xquery"></a>SequenceType 式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery では、値は常にシーケンスです。 値の型をシーケンス型と呼びます。 シーケンスの種類で使用できます、**のインスタンス**XQuery 式です。 XQuery 式で型を参照する必要があるときは、XQuery 仕様に記載されている SequenceType 構文を使用します。  
  
 アトミック型の名前はでも使用できます、**としてキャスト**XQuery 式です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、**のインスタンス**と**としてキャスト**Sequencetype での XQuery 式が部分的にサポートされています。  
  
## <a name="instance-of-operator"></a>instance of 演算子  
 **のインスタンス**動的、または実行時に、指定された式の値が決定する演算子を使用できます。 以下に例を示します。  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 なお、 `instance of` 、演算子、`Occurrence indicator`カーディナリティ、結果として得られるシーケンス内の項目の数を指定します。 この値を指定しないと、カーディナリティは 1 と想定されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、疑問符 () のみ (**でしょうか)。** 出現インジケーターがサポートされています。 **でしょうか。** 出現インジケーターが示す`Expression`0 個または 1 つの項目を返すことができます。 場合、**でしょうか。** 出現インジケーターを指定すると、 `instance of` True が返されます、`Expression`型は、指定された一致`SequenceType`かどうかに関係なく、`Expression`シングルトンまたは空のシーケンスを返します。  
  
 場合、**でしょうか。** 出現インジケーターが指定されていない`sequence of`場合にのみ、True を返します、`Expression`入力と一致する、`Type`指定と`Expression`シングルトンを返します。  
  
 **注**プラス記号 ( **+** ) およびアスタリスク ( **&#42;** ) では、出現インジケーターはサポートされていない[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]します。  
  
 次の例では、使用、**のインスタンス**XQuery 演算子。  
  
### <a name="example-a"></a>例 A  
 次の例では、作成、 **xml**変数を入力し、それに対してクエリを指定します。 このクエリ式では、`instance of` 演算子を指定して、最初のオペランドから返される値の動的な型と 2 つ目のオペランドに指定した型が一致するかどうかを判断します。  
  
 125 という値が指定した型のインスタンスであるために、次のクエリは、True を返します**xs:integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 次のクエリでは、最初のオペランドの式 /a[1] から返される値が要素なので True が返されます。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 同様に、次のクエリでは最初の式に含まれている式の値の型が属性型なので、`instance of` から True が返されます。  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 次の例では、式 `data(/a[1]` から xdt:untypedAtomic に型指定されたアトミック値が返されます。 そのため、 `instance of` True を返します。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 次のクエリでは、式 `data(/a[1]/@attrA` から型指定されていないアトミック値が返されます。 そのため、 `instance of` True を返します。  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>例 B  
 この例では、AdventureWorks サンプル データベース内の、型指定された XML 列に対してクエリを実行しています。 クエリ対象の列に関連付けられた XML スキーマ コレクションにより、型指定情報が提供されます。  
  
 式の**data()** 型が、列に関連付けられたスキーマに従って xs:string ProductModelID 属性の型指定された値を返します。 そのため、 `instance of` True を返します。  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 詳細については、「 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
 次のクエリ usetheBoolean `instance of` LocationID 属性が xs:integer 型かどうかを決定する式。  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 次のクエリは、CatalogDescription 型が指定された XML 列に対して指定されています。 この列に関連付けられた XML スキーマ コレクションにより、型指定情報が提供されます。  
  
 このクエリでは、`element(ElementName, ElementType?)` 式で `instance of` テストを使用して、特定の名前と型の要素ノードが `/PD:ProductDescription[1]` から返されることを確認します。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 クエリから True が返されます。  
  
### <a name="example-c"></a>例 C  
 共用体の型を使用する場合、`instance of`式[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]制限があります。具体的には、要素または属性の型が共用体型が場合`instance of`正確な型が判断されません。 したがって、SequenceType で使用されているアトミック型が、simpleType 階層内にある式の実際の型の最上位の親でない限り、クエリから False が返されます。 つまり、SequenceType に指定したアトミック型は、anySimpleType の直接の子である必要があります。 型階層については、次を参照してください。[型キャストの規則では、XQuery](../xquery/type-casting-rules-in-xquery.md)します。  
  
 次のクエリの例では、以下の操作を実行します。  
  
-   整数型または文字列型などに定義される共用体型を使用して XML スキーマ コレクションを作成します。  
  
-   型指定された宣言**xml** XML スキーマ コレクションを使用して変数。  
  
-   その変数にサンプル XML インスタンスを割り当てます。  
  
-   変数にクエリして、共用体型を処理するときの `instance of` の動作を示します。  
  
 クエリは次のとおりです。  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 次のクエリでは、`instance of` 式に指定している SequenceType が、指定した式の実際の型の最上位の親ではないので  False が返されます。 つまり、<`TestElement`> の値は整数型で、 最上位の親は xs:decimal 型です。 しかし、この型が `instance of` 演算子の 2 つ目のオペランドとして指定されていません。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 xs:integer の最上位の親は xs:decimal なので、クエリを変更し、xs:decimal をクエリの SequenceType に指定すると、クエリから True が返されます。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>例 D  
 この例で最初に XML スキーマ コレクションを作成して使用して入力、 **xml**変数。 型指定された**xml**変数が説明するためにクエリを実行し、`instance of`機能します。  
  
 次の XML スキーマ コレクションでは、単純型 myType と myType 型の要素 <`root`> を定義しています。  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 ここで、型指定された作成**xml**変数しクエリを実行します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 myType 型は制限により、sqltypes スキーマで定義されている varchar 型から派生しているので、`instance of` から True が返されます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>例 E  
 次の例では、式で IDREFS 属性のいずれかの値を取得し、`instance of` を使用して値が IDREF 型かどうかを判断しています。 この例では、次の操作が実行されます。  
  
-   XML スキーマ コレクションを作成、<`Customer`> 要素が、 **OrderList** IDREFS 型属性が、<`Order`> 要素には、 **OrderID** ID 型属性。  
  
-   型指定された作成**xml**変数とサンプル XML インスタンスを割り当てます。  
  
-   変数に対してクエリを指定します。 このクエリ式により、最初の <`Customer`> の OrderList IDRERS 型属性から最初の注文 ID 値が取得されます。 取得される値は IDREF 型です。 したがって、`instance of` から True が返されます。  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Schema-element()** と**schema-attribute()** の比較にシーケンス型はサポートされていません、`instance of`演算子。  
  
-   `(1,2) instance of xs:integer*` などの完全なシーケンスはサポートされません。  
  
-   形式を使用しているときに、 **element()** などの型名を指定する型をシーケンス`element(ElementName, TypeName)`疑問符 (?) で型を修飾する必要があります。 たとえば、`element(Title, xs:string?)` は要素が NULL であることを示します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 実行時に検出をサポートしていません、 **xsi:nil**プロパティを使用して`instance of`します。  
  
-   `Expression` の値が共用体型として型指定された要素または属性の値である場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、派生された型ではなく、値の型の派生元のプリミティブ型しか識別できません。 たとえば、<`e1`> が (xs:integer | xs:string) の静的な型を持つように定義されている場合、次の式では False が返されます。  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     ただし、`data(<e1>123</e1>) instance of xs:decimal` の場合は True が返されます。  
  
-   **Processing-instruction()** と**document-node()** sequence 型、引数を指定しない形式のみが許可されています。 たとえば、`processing-instruction()` は使用できますが、`processing-instruction('abc')` は使用できません。  
  
## <a name="cast-as-operator"></a>cast as 演算子  
 **としてキャスト**値を特定のデータ型に変換する式を使用できます。 以下に例を示します。  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、`AtomicType` の後に疑問符 (?) が必要です。 たとえば、次のクエリに示すとして`"2" cast as xs:integer?`文字列値を整数に変換します。  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 次のクエリで**data()** 文字列型である ProductModelID 属性の型指定された値を返します。 `cast as`演算子、値を xs:integer に変換します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 明示的な使用**data()** このクエリでは必要ありません。 `cast as` 式により、入力式で暗黙のアトミック化が実行されます。  
  
### <a name="constructor-functions"></a>コンストラクター関数  
 アトミック型のコンストラクター関数を使用できます。 使用する代わりに、たとえば、`cast as`演算子、 `"2" cast as xs:integer?`、使用することができます、 **xs:integer()** コンス トラクター関数を次の例。  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 次の例では、2000-01-01Z に等しい xs:date 型の値が返されます。  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 また、ユーザー定義アトミック型のコンストラクターを使用することもできます。 たとえば、XML スキーマ コレクションに関連付けられている XML データ型は 単純な型を定義、 **myType()** をその型の値を返すコンス トラクターを使用できます。  
  
#### <a name="implementation-limitations"></a>実装の制限事項  
  
-   XQuery 式**typeswitch**、**キャスト**、および**扱う**はサポートされていません。  
  
-   **としてキャスト**疑問符 (?) が必要ですアトミック型。  
  
-   **xs:QName**キャストの型としてはサポートされていません。 使用**Expanded-qname**代わりにします。  
  
-   **xs:date**、 **xs:time**、および**xs:datetime**は、Z で示されるタイム ゾーンが必要です。  
  
     タイム ゾーンが指定されていないので、次のクエリは失敗します。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     値に Z タイム ゾーン インジケーターを追加すると、クエリが機能します。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     これは、結果です。  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)   
 [システム入力&#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
