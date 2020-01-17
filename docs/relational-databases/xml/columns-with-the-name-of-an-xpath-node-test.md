---
title: XPath ノード テストの名前が付いた列 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
- XPath node test
ms.assetid: b48adccd-3b6b-486a-b326-20f57170186f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e1b4811e15d9f6927d06a4d4f9ff99466eb164c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112898"
---
# <a name="columns-with-the-name-of-an-xpath-node-test"></a>XPath ノード テストの名前が付いた列
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  XPath ノード テストのいずれかが列名である場合、内容は次の表に示すようにマップされます。 列名がいずれかの XPath ノード テストであれば、対応するノードに内容がマップされます。 列の SQL 型が **xml**の場合は、エラーが返されます。  
  
|列名|動作|  
|-----------------|--------------|  
|text()|text() という名前の列では、列内の文字列値がテキスト ノードとして追加されます。|  
|comment()|comment() という名前の列では、列内の文字列値が XML のコメントとして追加されます。|  
|node()|node() という名前の列では、列名がワイルドカード文字 (*) の場合と同じ結果が返されます。|  
|processing-instruction(name)|処理命令を名前とする列では、列内の文字列値が、処理命令ターゲット名に対応する PI 値として追加されます。|  
  
 次のクエリでは、列名としてノード テストを使用しています。 結果の XML では、テキスト ノードとコメントが追加されます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
        'Example of using node tests such as text(), comment(), processing-instruction()'                as "comment()",  
        'Some PI'                   as "processing-instruction(PI)",  
        'Employee name and address data' as "text()",  
        'middle name is optional'        as "EmpName/text()",  
        FirstName                        as "EmpName/First",   
        MiddleName                       as "EmpName/Middle",   
        LastName                         as "EmpName/Last",  
        AddressLine1                     as "Address/AddrLine1",  
        AddressLine2                     as "Address/AddrLIne2",  
        City                             as "Address/City"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P   
    ON P.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS BAE  
    ON BAE.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BAE.AddressID = A.AddressID  
WHERE  E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 結果を次に示します。  
  
 `<row EmpID="1">`  
  
 `<!--Example of using node tests such as text(), comment(), processing-instruction() -->`  
  
 `<?PI Some PI?>`  
  
 `Employee name and address data`  
  
 `<EmpName>middle name is optional`  
  
 `<First>Ken</First>`  
  
 `<Last>Sánchez</Last>`  
  
 `</EmpName>`  
  
 `<Address>`  
  
 `<AddrLine1>4350 Minute Dr.</AddrLine1>`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</row>`  
  
## <a name="see-also"></a>参照  
 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
