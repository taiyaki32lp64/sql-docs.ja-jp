---
title: 例:ELEMENT ディレクティブの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENT directive
ms.assetid: 80dd5d1f-fa90-4f97-a186-8fa3f460a7f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5fd255c763ca516bce53832884ae57c6c3dd8b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287164"
---
# <a name="example-specifying-the-element-directive"></a>例:ELEMENT ディレクティブの指定
  この例では、次に示すように従業員情報を取得し、要素中心の XML を生成します。  
  
```  
<Employee EmpID=...>  
  <Name>  
    <FName>...</FName>  
    <LName>...</LName>  
  </Name>  
</Employee>  
```  
  
 クエリも似ていますが、列名に `ELEMENT` ディレクティブを指定する点が異なります。 そのため、<`Name`> 要素には、属性ではなく、<`FName`> 子要素と <`LName`> 子要素が追加されます。 `Employee!1!EmpID` 列では `ELEMENT` ディレクティブが指定されていないので、`EmpID` は <`Employee`> 要素の属性として追加されます。  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName!ELEMENT],  
       NULL       as [Name!2!LName!ELEMENT]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName!ELEMENT]  
FOR XML EXPLICIT;  
```  
  
 次に結果の一部を示します。  
  
 `<Employee EmpID="1">`  
  
 `<Name>`  
  
 `<FName>Ken</FName>`  
  
 `<LName>S??nchez</LName>`  
  
 `</Name>`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name>`  
  
 `<FName>Terri</FName>`  
  
 `<LName>Duffy</LName>`  
  
 `</Name>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>参照  
 [FOR XML での EXPLICIT モードの使用](use-explicit-mode-with-for-xml.md)  
  
  
