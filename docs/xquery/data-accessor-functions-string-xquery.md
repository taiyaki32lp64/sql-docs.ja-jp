---
title: string 関数 (XQuery) |Microsoft Docs
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
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cb30d81102c17f2c3ce04b31ac7ff2b9689343e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038939"
---
# <a name="data-accessor-functions---string-xquery"></a>データ アクセサー関数 - string (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  値を返します *$arg*を文字列として表されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 ノードまたはアトミック値です。  
  
## <a name="remarks"></a>コメント  
  
-   場合 *$arg*空のシーケンスでは、長さ 0 の文字列が返されます。  
  
-   場合 *$arg*ノードで、関数は、文字列値のアクセサーを使用して取得したノードの文字列値を返します。 これは、W3C XQuery 1.0 and XPath 2.0 データ モデルの仕様で定義されます。  
  
-   場合 *$arg*は、アトミック値としてキャスト式によって返されるのと同じ文字列を返します**xs:string**、 *$arg*、以外の場合、それ以外の場合に注意します。  
  
-   場合の種類 *$arg*は**xs:anyURI**URI は、特殊文字をエスケープせず、文字列に変換されます。  
  
-   この実装では、 **fn:string()** せず、引数は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的にのみ使用できます角かっこ () 内で。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-string-function"></a>A. String 関数の使用  
 次のクエリを取得します <`Features`> の子要素ノード、<`ProductDescription`> 要素。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 結果の一部を次に示します。  
  
```  
<PD:Features xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 指定した場合、 **string()** 関数の場合、指定したノードの文字列値を表示します。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 次に結果の一部を示します。  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. 異なるノードに対する string 関数の使用  
 次の例では、XML インスタンスが xml 型の変数に割り当てられています。 クエリが適用した結果を示すために指定された**string()** さまざまなノードにします。  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 次のクエリでは、ドキュメント ノードの文字列値を取得します。 この値は、そのすべての子孫のテキスト ノードの文字列値を連結して形成されます。  
  
```  
select @x.query('string(/)')  
```  
  
 結果を次に示します。  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 次のクエリは、processing-instruction ノードの文字列値を取得します。 テキスト ノードが含まれていないため、空のシーケンスになります。  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 次のクエリでは、コメント ノードの文字列値を取得し、テキスト ノードを返します。  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 結果を次に示します。  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
