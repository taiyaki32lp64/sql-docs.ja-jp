---
title: '[全般] の XQuery のユース ケース |Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e844425f0c512cfe7c15354bf1aeb100d6104e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004523"
---
# <a name="general-xquery-use-cases"></a>XQuery の一般的な使用例
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックでは、XQuery の一般的な例を使用して提供します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. 製品と重量を検索するためのカタログ説明のクエリ  
 次のクエリでは、製品カタログの説明に製品モデル ID と重量が含まれている場合、これらの情報を返します。 クエリは、次の形式の XML を構築します。  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 クエリは次のとおりです。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **名前空間**XQuery プロローグ内のキーワードは、クエリ本文で使用される名前空間プレフィックスを定義します。  
  
-   クエリ本文で、必要な XML が構築されます。  
  
-   WHERE 句で、 **exist()** 製品カタログの説明が含まれている行のみを検索するメソッドを使用します。 XML を含む、<`ProductDescription`> 要素。  
  
 結果を次に示します。  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 次のクエリは、同じ情報を取得、カタログの説明が、製品モデルに対してのみには、重みが含まれていますが、<`Weight`>、仕様内の要素、<`Specifications`> 要素。 この例では、WITH XMLNAMESPACES を使用して pd プレフィックスとその名前空間のバインドを宣言します。 これにより、バインディングに記述されていない両方、 **query()** メソッドと、 **exist()** メソッド。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 前のクエリで、 **exist()** のメソッド、 **xml** WHERE 句があるかどうかをチェックのデータ型の <`Weight`> 内の要素、<`Specifications`> 要素。  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. カタログの説明に正面からの小さな製品写真が含まれる製品モデルの製品モデル ID の検索  
 XML 製品カタログの説明には、製品の写真が含まれています、<`Picture`> 要素。 各写真には、いくつかのプロパティがあります。 以下の画像の角度を <`Angle`> 要素、および、サイズ、<`Size`> 要素。  
  
 カタログの説明に正面からと小さいサイズの写真が含まれる製品モデルのクエリは次の形式の XML を構築します。  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句で、 **exist()** を製品カタログの説明を持つ行のみを取得するメソッドを使用します <`Picture`> 要素。  
  
-   WHERE 句を使用して、 **value()** の値を比較のメソッドを 2 回、<`Size`> と <`Angle`> 要素。  
  
 これは、結果の一部です。  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. 製品のフラットなリストにで囲まれた各ペアのモデルの名前と機能のペアを作成、\<機能 > 要素  
 製品モデル カタログの説明では、XML には、いくつかの製品の機能が含まれています。 含まれるこれらの機能はすべて、<`Features`> 要素。 クエリを使用して[XML の構築 (XQuery)](../xquery/xml-construction-xquery.md)必要な XML を構築します。 中かっこで式が結果によって置き換えられます。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   $pd/$pd/p/1: features/* のノードの子要素だけを返します <`Features`> が $pd/1: features/node() はすべてのノードを返します。 返されるノードには、要素ノード、テキスト ノード、処理命令、コメントがあります。  
  
-   FOR ループの 2 つは、元の製品名、および個々 の特徴が返されるデカルト積を生成します。  
  
-   **ProductName**属性です。 このクエリで構築された XML では、この属性を要素として返します。  
  
 これは、結果の一部です。  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. 製品の一覧から製品モデルのカタログの説明、名前、モデルの ID をモデル化し、内の機能にグループ化、\<製品 > 要素  
 製品モデル カタログの説明に格納されている情報を使用して、次のクエリは、製品モデルの名前、モデルの ID を一覧表示し、内の機能にグループ化、\<製品 > 要素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 これは、結果の一部です。  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. 製品モデルの特徴の説明の取得  
 次のクエリに XML を構築、<`Product`> 要素を持つ**ProducModelID**、 **ProductModelName**属性、および最初の 2 つの製品の機能です。 具体的には、最初の 2 つの製品機能では、最初の 2 つの子要素、<`Features`> 要素。 多くの機能がある場合、空を返します <`There-is-more/`> 要素。  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   FOR ... RETURN ループ部分では、最初の 2 つの製品の特徴を取得します。 **Position()** 関数を使用して、シーケンス内の要素の位置を確認します。  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. 製品カタログの説明からの "ons" で終わる要素名の検索  
 次のクエリは、カタログの説明を検索し、内のすべての要素を返します、<`ProductDescription`>"ons"で終わる名前を持つ要素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 これは、結果の一部です。  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. "Aerodynamic という"単語を含む概要説明を検索します。  
 次のクエリでは、カタログの説明の概要説明に "Aerodynamic" という語を含む製品モデルを取得します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 SELECT クエリを指定する注**query()** と**value()** のメソッド、 **xml**データ型。 このため、2 つの異なるクエリ プロローグ内でそれぞれ名前空間の宣言を繰り返す手間を省き、クエリ内で使用されるプレフィックス pd を WITH XMLNAMESPACES を使用して一度だけ定義しています。  
  
 上のクエリに関して、次の点に注意してください。  
  
-   カタログの説明が"aerodynamic という"単語を含む行のみを取得する WHERE 句を使用します <`Summary`> 要素。  
  
-   **Contains()** 関数を使用して、テキストの単語が含まれているかどうかを参照してください。  
  
-   **Value()** のメソッド、 **xml**データ型によって返される値を比較する**contains()** を 1 にします。  
  
 結果を次に示します。  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. カタログの説明に製品モデルの写真が含まれていません製品モデルを検索します。  
 次のクエリを含めるれない製品モデル カタログの説明が操作を実行しているの Productmodelid を取得する <`Picture`> 要素。  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   場合、 **exist()** WHERE 句が False (0) を返すメソッド、製品モデル ID が返されます。 それ以外の場合は返されません。  
  
-   すべての製品の説明が含まれるため、<`Picture`> 要素を結果セットは空ここでします。  
  
## <a name="see-also"></a>関連項目  
 [階層に関連する XQueries](../xquery/xqueries-involving-hierarchy.md)   
 [注文に関連する XQueries](../xquery/xqueries-involving-order.md)   
 [XQueries リレーショナル データを処理](../xquery/xqueries-handling-relational-data.md)   
 [XQuery での文字列検索](../xquery/string-search-in-xquery.md)   
 [XQuery での名前空間の処理](../xquery/handling-namespaces-in-xquery.md)   
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
