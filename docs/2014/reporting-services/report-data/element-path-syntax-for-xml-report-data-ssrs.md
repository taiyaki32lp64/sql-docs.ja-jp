---
title: XML レポート データの要素パス構文 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9981a3ebeb1b67bda67509e2a08995fadb195abb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107299"
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>XML レポート データの要素パス構文 (SSRS)
  レポート デザイナーでは、大文字と小文字が区別される要素パスを定義して、レポートに使用するデータを XML データ ソースから指定します。 要素パスとは、XML データ ソースにおける XML 階層のノードとその属性の走査方法を指定するものです。 データセット クエリを空にするか、XML `ElementPath` の XML `Query` を空にした場合、既定の要素パスが使用されます。 XML データ ソースからデータが取得されると、テキスト値を持つ要素ノードおよび要素ノードの属性が、結果セットにおける列になります。 クエリを実行すると、これらのノードと属性の値が、行データになります。 [レポート データ] ペインでは、列がデータセット フィールド コレクションとして表示されます。 このトピックでは、要素パス構文について説明します。  
  
> [!NOTE]  
>  要素パス構文は、名前空間に依存しません。 要素パスで名前空間を使用する XML を含む XML クエリ構文を使用して、`ElementPath`要素[XML レポート データの XML クエリ構文&#40;SSRS&#41;](report-data-ssrs.md)します。  
  
 次の表に、要素パスを定義する際の表記規則を示します。  
  
|表記|使用目的|  
|----------------|--------------|  
|**太字**|記載されているとおりに入力する必要があるテキストを示します。|  
|(& a) #124 です。(縦棒)|構文項目に複数の選択肢があることを示します。 選択できる項目は 1 つだけです。|  
|`[ ] (brackets)`|省略可能な構文項目。 角かっこは入力しません。|  
|**{ }** (中かっこ)|構文項目のパラメーターを区切ります。|  
|[**,**...*n*]|先行する項目を *n* 回繰り返せることを示します。 項目はコンマで区切ります。|  
  
## <a name="syntax"></a>構文  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>コメント  
 次の表は、要素パス関連の用語をまとめたものです。 サンプル XML ドキュメントである Customers.xml (このトピックの「例」を参照) を使って説明しています。  
  
> [!NOTE]  
>  XML タグでは大文字と小文字が区別されます。 要素パスに ElementNode を指定する場合は、データ ソース内の XML タグと完全に一致させる必要があります。  
  
|項目|定義|  
|----------|----------------|  
|Element path|XML ドキュメント内のノードのシーケンス、つまり、どのようにノードをたどっていけば、XML データ ソースからデータセットのフィールド データを取得できるかを定義します。|  
|`ElementNode`|XML ドキュメント内の XML ノードです。 各ノードは他のノードと階層的な関係にあり、タグによって指定されます。 たとえば、\<Customers> は、ルート要素ノードです。 \<Customer> は、\<Customers> のサブ要素です。|  
|`XMLName`|ノードの名前。 たとえば、Customers ノードの名前は Customers です。 すべてのノード名を一意に識別できるように、`XMLName` の先頭には名前空間識別子を付けることができます。|  
|`Encoding`|この要素の `Value` はエンコードされた XML であり、この要素のサブ要素としてデコードおよび追加する必要があることを示します。|  
|`FieldList`|データの取得に使用する一連の要素と属性を定義します。<br /><br /> 指定しなかった場合は、すべての属性およびサブ要素がフィールドとして使用されます。 空のフィールド リストが指定されている場合 (**{}**)、このノードのフィールドは使用されません。<br /><br /> `FieldList` には、`Value` や `Element`、`ElementNode` は含まれません。|  
|`Field`|データセットのフィールドとして取得するデータを指定します。|  
|`Attribute`|`ElementNode` 内に指定される名前と値のペアです。 たとえば、要素ノードで\<Customer ID =「1」>、`ID`属性と`@ID(Integer)`、対応するデータ フィールドは整数型として「1」を返します`ID`。|  
|`Value`|要素の値です。 `Value` は、要素パス内で最後の `ElementNode` でのみ使用できます。 たとえば、ため\<返す > の値を要素パスの末尾に追加した場合、リーフ ノードは、`Return {@}`は`Chair`します。|  
|`Element`|指定されたサブ要素の値です。 たとえば、Customers {}/Customer {}/LastName とすると、LastName 要素についてのみ値が取得されます。|  
|`Type`|この要素から作成されたフィールドに使用するデータ型 (省略可) です。|  
|`NamespacePrefix`|`NamespacePrefix` は XML Query 要素で定義されます。 XML Query 要素が存在しない場合、XML `ElementPath` の名前空間は無視されます。 XML Query 要素が存在する場合は、XML `ElementPath` に属性 `IgnoreNamespaces` を使用できます (省略可)。 IgnoreNamespaces が場合`true`、xml 名前空間`ElementPath`XML ドキュメントは無視されます。 詳細については、「[XML レポート データの XML クエリ構文 &#40;SSRS&#41;](report-data-ssrs.md)」を参照してください。|  
  
## <a name="example---no-namespaces"></a>例 - 名前空間なし  
 データ ソースとして、XML ドキュメント (Customers.xml) を使用した例を次に示します。 要素パスの構文を示しながら、データセットを定義するクエリでその要素パスを使用した場合にどのような結果が得られるかを説明しています。  
  
 要素パスが空の場合、クエリが既定の要素パスを使用ことに注意してください。 リーフ ノードのコレクションに最初のパス。 1 つ目は要素パスを空にする例です。/Customers/Customer/Orders/Order という要素パスを指定した場合と同じ結果になります。 このパス上に存在するすべてのノードの値と属性が結果セットに返され、ノード名と属性名がデータセットのフィールドとして表示されます。  
  
-   *空*  
  
    |[オーダー]|Qty|ID|FirstName|LastName|Customer.ID|xmlns|  
    |-----------|---------|--------|---------------|--------------|-----------------|-----------|  
    |Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
    |テーブル|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
    |Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
    |EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
-   `Customers {}/Customer`  
  
    |FirstName|LastName|ID|  
    |---------------|--------------|--------|  
    |Bobby|Moore|11|  
    |Crystal|Hu|20|  
    |Wyatt|Diaz|33|  
  
-   `Customers {}/Customer {}/LastName`  
  
    |LastName|  
    |--------------|  
    |Moore|  
    |Hu|  
    |Diaz|  
  
-   `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
    |[オーダー]|Qty|  
    |-----------|---------|  
    |Chair|6|  
    |テーブル|1|  
    |Sofa|2|  
    |EndTables|2|  
  
-   `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
    |Order.ID|FirstName|LastName|ID|  
    |--------------|---------------|--------------|--------|  
    |1|Bobby|Moore|11|  
    |2|Bobby|Moore|11|  
    |8|Crystal|Hu|20|  
    |15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>XML ドキュメント:Customers.xml  
 前のセクションの要素パスの例を試すには、この XML をコピーして、レポート デザイナーからアクセス可能な URL に保存した後、この XML ドキュメントを XML データ ソースとして使用します (例: `http://localhost/Customers.xml`)。  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 または、次のプロシージャを使用して、接続文字列のない XML データ ソースを作成し、クエリに Customers.XML を埋め込むこともできます。  
  
###### <a name="to-embed-customersxml-in-a-query"></a>クエリに Customers.XML を埋め込むには  
  
1.  空白の接続文字列を使用して、XML データ ソースを作成します。  
  
2.  XML データ ソースに新しいデータセットを作成します。  
  
3.  **[データセットのプロパティ]** ダイアログ ボックスの **[クエリ デザイナー]** をクリックします。 テキスト ベースのクエリ デザイナー ダイアログ ボックスが表示されます。  
  
4.  クエリ ペインに次の 2 行を入力します。  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  Customers.XML をコピーし、クエリ ペインで、 `<XmlData>`の後にそのテキストを貼り付けます。  
  
6.  クエリ ペインで、Customers.XML からコピーした最初の行を削除します。 `<?xml version="1.0"?>`  
  
7.  クエリの最後に次の 2 行を追加します。  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  **[クエリの実行]** (!) をクリックします。  
  
     `xmlns`、 `Customer.ID`、 `FirstName`、 `LastName`、 `ID`、 `Qty`、 `Order`という列を含む 4 行のデータが結果セットに表示されます。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [XML の接続の種類 (SSRS)](xml-connection-type-ssrs.md)   
 [Reporting Services チュートリアル &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
