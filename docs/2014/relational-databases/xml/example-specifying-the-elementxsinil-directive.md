---
title: 例:ELEMENTXSINIL ディレクティブの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a23baa7791aea37c4c90077c21391001ddc538a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704808"
---
# <a name="example-specifying-the-elementxsinil-directive"></a>例:ELEMENTXSINIL ディレクティブの指定
  ELEMENT ディレクティブを指定して要素中心の XML を生成する際、列に NULL 値が格納されていると、EXPLICIT モードでは対応する要素が生成されません。 必要に応じて ELEMENTXSINIL ディレクティブを指定し、NULL 値の列に対して要素を生成するように要求することができます。このとき、`xsi:nil` 属性に値 TRUE が設定されます。  
  
 次のクエリは、従業員の住所を含む XML を生成します。 `AddressLine2` 列と `City` 列には、列名に `ELEMENTXSINIL` ディレクティブが指定されています。 この設定により、NULL 値が格納されている `AddressLine2` 列と `City` 列に対して行セットに要素が生成されます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID  as [Employee!1!EmpID],  
       BEA.AddressID as [Employee!1!AddressID],  
       NULL        as [Address!2!AddressID],  
       NULL        as [Address!2!AddressLine1!ELEMENT],  
       NULL        as [Address!2!AddressLine2!ELEMENTXSINIL],  
       NULL        as [Address!2!City!ELEMENTXSINIL]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       BEA.AddressID,  
       A.AddressID,  
       AddressLine1,   
       AddressLine2,  
       City   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BEA.AddressID = A.AddressID  
ORDER BY [Employee!1!EmpID],[Address!2!AddressID]  
FOR XML EXPLICIT;  
```  
  
 結果の一部を次に示します。  
  
 `<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `EmpID="1" AddressID="249">`  
  
 `<Address AddressID="249">`  
  
 `<AddressLine1>4350 Minute Dr.</AddressLine1>`  
  
 `<AddressLine2 xsi:nil="true" />`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>参照  
 [FOR XML での EXPLICIT モードの使用](use-explicit-mode-with-for-xml.md)  
  
  
