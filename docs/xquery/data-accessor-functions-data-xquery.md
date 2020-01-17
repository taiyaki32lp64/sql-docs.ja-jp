---
title: data 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
ms.openlocfilehash: 7376c57f809fa97168b27b158678d931a696b5df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038971"
---
# <a name="data-accessor-functions---data-xquery"></a>データ アクセサー関数 - data (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定された各項目の型指定された値を返します *$arg*します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 型指定された値を返す対象となるアイテムのシーケンス。  
  
## <a name="remarks"></a>コメント  
 型指定された値には、次のことが当てはまります。  
  
-   アトミック値の型指定された値は、アトミック値になります。  
  
-   テキスト ノードの型指定された値は、そのテキスト ノードの文字列値になります。  
  
-   コメントの型指定された値は、そのコメントの文字列値になります。  
  
-   処理命令の型指定された値は、その処理命令の内容になります。このとき、処理命令の操作対象名は含まれません。  
  
-   ドキュメント ノードの型指定された値は、その文字列値になります。  
  
 属性ノードと要素ノードには、次のことが当てはまります。  
  
-   属性ノードが XML スキーマ型で型指定されている場合、このノードの型指定された値は XML スキーマ型に応じた型の値になります。  
  
-   インスタンスとして返される文字列値をその型指定された値は属性ノードが型指定された場合は、 **xdt:untypedAtomic**します。  
  
-   インスタンスとして返される文字列値をその型指定された値は、要素ノードが型指定されていない場合**xdt:untypedAtomic**します。  
  
 型指定された要素ノードには、次のことが当てはまります。  
  
-   要素が単純なコンテンツの種類、 **data()** 要素の型指定された値を返します。  
  
-   ノードが、xs:anyType などの複合型の場合**data()** 静的エラーが返されます。  
  
 使用していますが、 **data()** を指定する、次の例に示すように、関数は多くの場合、 **data()** 関数は、クエリの読みやすさを明示的に増加します。 詳細については、次を参照してください。 [XQuery の基礎](../xquery/xquery-basics.md)します。  
  
 指定することはできません**data()** で、次に示すように、XML を構築します。  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. data() XQuery 関数によるノードの型指定された値の抽出  
 次のクエリを示していますが、どのように**data()** 関数を使用して、属性、要素、およびテキスト ノードの値を取得します。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 結果を次に示します。  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 前述のように、 **data()** 属性を作成する場合は、関数は省略可能です。 指定しない場合、 **data()** 関数の場合、暗黙的と見なされます。 次のクエリは、前のクエリと同じ結果を生成します。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 次の例では、インスタンスを**data()** 関数が必要です。  
  
 次のクエリで **$pd/1: specifications/素材**を返します、<`Material`> 要素。 また、**データ ($pd/1: specifications/素材)** ため、xdt:untypedatomic 型のデータの文字を返します <`Material`> は型指定されません。 入力が型指定された場合、結果の**data()** として型指定された**xdt:untypedAtomic**します。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 結果を次に示します。  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 次のクエリで**data($pd/p1:Features/wm:Warranty)** ために、静的なエラーを返します <`Warranty`> は複合型の要素です。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
