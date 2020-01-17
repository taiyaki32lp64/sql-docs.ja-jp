---
title: XML の構築 (XQuery) |Microsoft Docs
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
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
author: rothja
ms.author: jroth
ms.openlocfilehash: 51c1898ddaee1ecf878944a3b43c3d8adbb38590
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946177"
---
# <a name="xml-construction-xquery"></a>XML の構築 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery では、使用することができます、**直接**と**計算**コンス トラクターをクエリ内での XML 構造を構築します。  
  
> [!NOTE]  
>  違いはありません、**直接**と**計算**コンス トラクター。  
  
## <a name="using-direct-constructors"></a>直接コンストラクターの使用  
 直接コンストラクターを使用するときは、XML の構築時に XML 同様の構文を指定します。 次の例では、直接コンストラクターを使用した XML 構築を示しています。  
  
### <a name="constructing-elements"></a>要素の構築  
 XML の表記法を使用して要素を構築できます。 次の例は、直接要素コンス トラクター式を使用し、作成、 \<ProductModel > 要素。 構築される要素には、次の 3 つの子要素があります。  
  
-   テキスト ノード。  
  
-   2 つの要素ノード\<概要 > と\<機能 >。  
  
    -   \<概要 > 要素が 1 つの子テキスト ノード値が"Some description"です。  
  
    -   \<機能 > 要素が 3 つの子の要素ノードでは、\<色 >、\<重み >、および\<保証 >。 これらの各ノードには、子テキスト ノードが 1 つあり、それぞれ "Red"、"25"、"2 years parts and labor" という値を持ちます。  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 作成された XML を次に示します。  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 この例で示しているように、定数式から要素を構築すると便利ですが、XQuery 言語機能の真の威力は、データベースから動的にデータを抽出する XML を構築できる点にあります。 中かっこを使用するとクエリ式を指定できます。 作成される XML では、クエリ式がその式の値に置き換えられます。 たとえば、次のクエリでは子要素 (<`e`>) が 1 つある <`NewRoot`> 要素が構築されます。 要素の値 <`e`> 中かっこ (「{...}」) 内にパス式を指定することによって計算されます。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 中かっこはコンテキスト切り替えトークンとして機能し、XML の構築からクエリの評価へとクエリを切り替えます。 この場合、中かっこ内の XQuery パス式 `/root` が評価されて、その結果がこのパス式と置き換えられます。  
  
 これは、結果です。  
  
```xml
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 次に示すクエリは先ほどのクエリと似ています。 ただし、中かっこで式を指定します、 **data()** のアトミック値を取得する関数を <`root`> 要素を構築済みの要素に割り当てます <`e`>。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 これは、結果です。  
  
```xml
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 コンテキスト切り替えトークンではなく、テキストの一部として中かっこを使用する場合は、次の例に示すように、"}}" や "{{" とすることでエスケープできます。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 これは、結果です。  
  
```xml
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 次のクエリは、直接要素コンストラクターを使用して要素を構築する別の例です。 この例でも、<`FirstLocation`> の値は、中かっこ内の式を実行することにより取得されます。 クエリ式では、Production.ProductModel テーブルの Instructions 列の最初のワーク センターの場所での製造手順が返されます。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 これは、結果です。  
  
```xml
<FirstLocation>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>XML の構築での要素の内容  
 次の例では、直接要素コンストラクターを使用して要素内容を構築する際の式の動作を示しています。 次の例では、直接要素コンストラクターで 1 つの式が指定されています。 この式では、構築される XML に 1 つのテキスト ノードが作成されます。  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 次に示す結果のように、式を評価した結果のアトミック値のシーケンスがテキスト ノードに追加されます。このシーケンスでは隣り合うアトミック値の間に空白が 1 つ追加されます。 構築される要素には子要素が 1 つあります。 結果に表示される値を含んだテキスト ノードを次に示します。  
  
```xml
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 1 つの式ではなく、3 つのテキスト ノードを生成する 3 つの個別の式を指定すると、隣り合ったテキスト ノードが連結されて、作成される XML では 1 つのノードにまとめられます。  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 構築される要素ノードには、1 つの子があります。 結果に表示される値を含んだテキスト ノードを次に示します。  
  
```xml
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>属性の構築  
 直接要素コンストラクターを使用して要素を作成するときに、次の例に示すように、XML 同様の構文を使用して、要素の属性を指定することもできます。  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 作成された XML を次に示します。  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 構築された要素 <`ProductModel`> には、ProductModelID 属性と次に示す子ノードがあります。  
  
-   `This is product model catalog description.` というテキスト ノード。  
  
-   <`Summary`> という要素ノード。 このノードには、`Some description` という子テキスト ノードが 1 つあります。  
  
 属性を構築するときに、中かっこ内で式を使用して属性値を指定できます。 この場合、式の結果が属性値として返されます。  
  
 次の例では、 **data()** 関数は必須ではありません。 式の値は、属性に割り当てているので**data()** が指定された式の型指定された値を取得する暗黙的に適用します。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 これは、結果です。  
  
```xml
<NewRoot attr="5" />  
```  
  
 次に示す別の例では、LocationID 属性と SetupHrs 属性の構築に式を指定しています。 これらの式は、Instruction 列内の XML に対して評価されます。 式の型指定された値が属性に割り当てられます。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 結果の一部を次に示します。  
  
```xml
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step ...   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   文字列や XQuery 式を複数使用したり、混在して使用する属性式はサポートされません。 たとえば、次のクエリに示すように、`Item` が定数で、クエリ式を評価することによって値 `5` が取得される XML を構築するとします。  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
     文字列定数と式 ({/x}) を混在して使用していますが、このような方法はサポートされないので、次のクエリではエラーが返されます。  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     この場合、次の対応方法があります。  
  
    -   2 つのアトミック値を連結して 1 つの属性値を作成します。 この 2 つのアトミック値は、間に空白が挿入されて 1 つの属性値へとシリアル化されます。  
  
        ```sql
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         これは、結果です。  
  
        ```xml
        <a attr="Item 5" />  
        ```  
  
    -   使用して、 [concat 関数](../xquery/functions-on-string-values-concat.md)結果の属性値に、2 つの文字列引数を連結します。  
  
        ```sql
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         この場合、2 つの文字列値の間に空白が追加されません。 2 つの文字列値の間に空白が必要な場合は、明示的に空白を指定する必要があります。  
  
         これは、結果です。  
  
        ```xml
        <a attr="Item5" />  
        ```  
  
-   1 つの属性値としての複数の式はサポートされません。 たとえば、次のクエリではエラーが返されます。  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   異種シーケンスはサポートされません。 次の例に示すように、1 つの属性値として異種シーケンスを割り当てようとすると、エラーが返されます。 この例では、文字列 "Item" と要素 <`x`> で構成された異種シーケンスが属性値として指定されています。  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     適用する場合、 **data()** 関数の場合、このクエリでは、式のアトミック値を取得するため`/x`、これは文字列に連結します。 アトミック値のシーケンスを次に示します。  
  
    ```sql
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     これは、結果です。  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
-   属性ノード順は、静的な型チェック中ではなく、シリアル化中に適用されます。 たとえば、次のクエリは、属性以外のノードの後に属性を追加しようとするため、失敗します。  
  
    ```sql
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     上記のクエリは、次のエラーを返します。  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>名前空間の追加  
 直接コンストラクターを使用して XML を構築するときに、構築される要素と属性の名前を名前空間プレフィックスを使用して修飾できます。 次の方法でプレフィックスを名前空間にバインドできます。  
  
-   名前空間宣言属性を使用する方法。  
  
-   WITH XMLNAMESPACES 句を使用する方法。  
  
-   XQuery プロローグでのバインド。  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>名前空間宣言属性を使用した名前空間の追加  
 次の例では、要素 <`a`> の構築で名前空間宣言属性を使用して、既定の名前空間を宣言しています。 子要素 <`b`> の構築により、親要素で宣言された既定の名前空間宣言が解除されます。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 これは、結果です。  
  
```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 プレフィックスを名前空間に割り当てることができます。 そのプレフィックスは要素 <`a`> の構築で指定されます。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 これは、結果です。  
  
```xml
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 XML の構築で既定の名前空間の宣言を解除できますが、名前空間プレフィックスの宣言を解除することはできません。 次のクエリでは、要素 <`b`> の構築で指定されたプレフィックスの宣言を解除できないので、エラーが返されます。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 新しく構築される名前空間は、クエリ内部で使用できます。 たとえば、次のクエリでは要素 <`FirstLocation`> の構築で名前空間を宣言し、LocationID 属性値と SetupHrs 属性値の式でプレフィックスを指定しています。  
  
```sql
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 この方法で新しい名前空間プレフィックスを作成すると、このプレフィックスの既存の名前空間宣言よりもオーバーライドされることに注意してください。 たとえば、クエリ プロローグ内の名前空間宣言 `AWMI="https://someURI"` は &lt;`FirstLocation`&gt; 要素内の名前空間宣言によってオーバーライドされます。  
  
```sql
SELECT Instructions.query('  
declare namespace AWMI="https://someURI";  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>プロローグを使用した名前空間の追加  
 次の例では、構築される XML にどのように名前空間が追加されるのかを示しています。 既定の名前空間はクエリ プロローグ内で宣言されます。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 要素 <`b`> の構築では、名前空間宣言属性の値が空文字列で指定されていることに注意してください。 これにより、親要素で宣言されている既定の名前空間の宣言が解除されます。  
  

これは、結果です。  

```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>XML の構築と空白文字の処理  
 XML の構築では、要素の内容に空白文字を含めることができます。 空白文字は次のように処理されます。  
  
-   名前空間 Uri 内の空白文字は、XSD 型として扱われます**anyURI**します。 具体的には、空白文字は次のように処理されます。  
  
    -   最初と最後にある空白文字は切り捨てられます。  
  
    -   中間にある複数の空白値は 1 つの空白文字にまとめられます。  
  
-   属性の内容の途中にある改行文字は、空白に置き換えられます。 その他すべての空白文字はそのままです。  
  
-   要素内部の空白文字は保持されます。  
  
 次の例では、XML の構築での空白文字の処理を示しています。  
  
```sql
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   https://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 これは、結果です。  
  
```xml
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>その他の直接 XML コンストラクター  
 処理命令や XML コメントのコンストラクターでは、対応する XML の構築と同じ構文を使用します。 テキスト ノードの計算コンストラクターもサポートされますが、主に、テキスト ノードを構築するために XML DML で使用されます。  
  
 **注**、明示的なテキスト ノード コンス トラクターを使用しての例は、特定の例を参照してください。[挿入&#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md)します。  
  
 次のクエリでは、構築される XML に 1 つの要素、2 つの属性、1 つのコメント、および 1 つの処理命令が含まれます。 シーケンスを作成するので、<`FirstLocation`> の前でコンマを使用していることに注意してください。  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 結果の一部を次に示します。  
  
```xml
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
</FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>計算コンストラクターの使用  
 . このコンストラクターを使用する場合は、構築するノードの種類を特定するキーワードを指定します。 サポートされているキーワードは次の 3 つのみです。  
  
-   element  
  
-   属性 (attribute)  
  
-   text  
  
 要素ノードと属性ノードの場合、これらのキーワードの後にノード名や式を続け、かっこで囲みます。このようにしてノードの内容が生成されます。 この後に示す例では、次の XML を構築しています。  
  
```xml
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 次に示すのは、計算コンストラクターを使用して XML を生成するクエリです。  
  
```sql
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 ノードの内容を生成する式ではクエリ式を指定できます。  
  
```sql
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 XQuery 仕様で定義されているように、要素計算コントラクターおよび属性計算コンストラクターを使用すると、ノード名を計算できることに注意してください。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で直接コンストラクターを使用している場合は、element や attribute などのノード名を定数リテラルとして指定する必要があります。 したがって、要素と属性については、直接コンストラクターと計算コンストラクター間に違いはありません。  
  
 次の例では、構築されたノードのコンテンツがの Instructions 列に格納されている製造手順の XML から取得した、 **xml** ProductModel テーブルのデータ型。  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 結果の一部を次に示します。  
  
```xml
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>実装のその他の制限事項  
 属性計算コンストラクターを使用して新しい名前空間を宣言することはできません。 また、次の計算コンストラクターは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ではサポートされません。  
  
-   ドキュメント ノード計算コンストラクター  
  
-   処理命令計算コンストラクター  
  
-   コメント計算コンストラクター  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
