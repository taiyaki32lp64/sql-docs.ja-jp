---
title: NULL 値が含まれる列の既定動作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c98e5cf869b0a4b7e39b640cf4f486ae8f222127
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637752"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>NULL 値が含まれる列の既定動作
  既定で、列内の NULL 値は、属性、ノード、または要素がない状態にマップされます。 この既定動作を変更するには、次のクエリに示すように、ELEMENTS ディレクティブで要素中心の XML を要求し、NULL 値に対しても要素の追加を要求する XSINIL を指定します。  
  
```  
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 結果を次に示します。 XSINIL を指定しないと、<`Middle`> 要素は出力されません。  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>参照  
 [FOR XML での PATH モードの使用](use-path-mode-with-for-xml.md)  
  
  
