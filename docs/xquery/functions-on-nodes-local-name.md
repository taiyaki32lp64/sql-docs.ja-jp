---
title: local-name 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
author: rothja
ms.author: jroth
ms.openlocfilehash: 382bbc9aeedacf37c7fe38abd592bcee7e154f5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038872"
---
# <a name="functions-on-nodes---local-name"></a>ノードの関数 - local-name
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  名前のローカル部分を返します *$arg* xs:string される長さ 0 の文字列になりますか、または形式の名前、xs:NCName する必要があります。 引数が指定されていない場合、既定値は、コンテキスト ノードです。  
  
## <a name="syntax"></a>構文  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 ノード名を持つローカル名部分が取得されます。  
  
## <a name="remarks"></a>コメント  
  
-   SQL Server で**fn:local-name()** せず、引数は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的には、この属性は角かっこ内にのみ使用できます (`[ ]`)。  
  
-   引数を指定し、空のシーケンスには、関数は長さ 0 の文字列を返します。  
  
-   ドキュメント ノード、コメント、またはテキスト ノードであるため、ターゲット ノードの名前はありません、関数は長さ 0 の文字列を返します。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. 特定のノードのローカル名を取得します。  
 型指定されていない XML インスタンスに対しては、次のクエリを指定します。 クエリ式、 `local-name(/ROOT[1])`、指定したノードのローカル名部分を取得します。  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 次のクエリは、ProductModel テーブルの型指定された xml 列である Instructions 列に対して指定します。 式では、 `local-name(/AWMI:root[1]/AWMI:Location[1])`、ローカルの名前を返します`Location`、指定したノードの。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. 述語で引数を指定せずに local-name を使用する  
 次のクエリは型指定された、Instructions 列に対して指定**xml** ProductModel テーブルの列。 式のあるすべての子要素を返します、<`root`> 要素の QName のローカル名部分は「場所」です。 **Local-name()** 関数は、述語で指定し、コンテキスト ノードが、関数で使用される引数を持ちません。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 クエリでは、すべてを返します、<`Location`> の子要素、<`root`> 要素。  
  
## <a name="see-also"></a>関連項目  
 [ノードの関数](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [名前空間 uri 関数&#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
