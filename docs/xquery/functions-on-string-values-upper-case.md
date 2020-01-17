---
title: upper-case 関数 (XQuery) |Microsoft Docs
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
- upper-case
- upper-case Function (XQuery)
ms.assetid: 5bd01ad2-7adf-48fb-bf42-41e200419d37
author: rothja
ms.author: jroth
ms.openlocfilehash: 0dcbcbc0cd6c0cf479aee7a7c3fd8c5e53a53d28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004609"
---
# <a name="functions-on-string-values---upper-case"></a>文字列値に使用する関数 - upper-case
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  この関数では、各文字に変換 *$arg*大文字にします。 Unicode コード ポイント用 Microsoft Windows バイナリ大文字/小文字の変換では、文字を大文字に変換する方法を指定します。 この標準は、Unicode 標準のコード ポイントの標準のマッピングよりも異なります。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:upper-case($arg as xs:string?) as xs:string  
```  
  
## <a name="arguments"></a>引数  
  
|||  
|-|-|  
|用語|定義|  
|*$arg*|大文字に変換する文字列値。|  
  
## <a name="remarks"></a>コメント  
 場合の値 *$arg*が空、長さ 0 の文字列が返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-a-string-to-upper-case"></a>A. 文字列を大文字に変更します。  
 次の例では、変更、入力文字列 ' abcDEF!@4' を大文字に変換します。  
  
```  
DECLARE @x xml = N'abcDEF!@4';  
SELECT @x.value('fn:upper-case(/text()[1])', 'nvarchar(10)');  
```  
  
### <a name="b-search-for-a-specific-character-string"></a>B. 特定の文字の文字列の検索  
 この例では、upper-case 関数を使用して、大文字と小文字を区別せずに検索を行う方法を示しています。  
  
```  
USE AdventureWorks  
GO  
--WITH XMLNAMESPACES clause specifies the namespace prefix  
--to use.   
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
--The XQuery contains() function is used to determine whether  
--any of the text nodes below the <Summary> element contain  
--the word 'frame'. The upper-case() function is used to make  
--the search case-insensitive.  
  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
/pd:ProductDescription/pd:Summary//text()[  
          contains(upper-case(.), "FRAME")]')  = 1  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `19     <Prod ProductModelID="19">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike.`  
  
 `Performance-enhancing options include the innovative HL Frame,`  
  
 `super-smooth front suspension, and traction for all terrain.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
 `25     <Prod ProductModelID="25">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">This bike is ridden by race winners. Developed with the`  
  
 `Adventure Works Cycles professional race team, it has a extremely light`  
  
 `heat-treated aluminum frame, and steering that allows precision control.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
