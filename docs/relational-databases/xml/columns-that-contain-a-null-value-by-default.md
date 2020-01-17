---
title: NULL 値が含まれる列の既定動作 | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0fb8b86daedb73f62396e1dc13a06a5a4e2a7bb3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113075"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>NULL 値が含まれる列の既定動作

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

既定で、列内の NULL 値は、属性、ノード、または要素がない状態にマップされます。 この既定の動作は、ELEMENTS XSINIL キーワード句を使用してオーバーライドできます。 この句では、要素中心の XML が要求されます。 これは、返される結果で null 値が明示的に示されることを意味します。 これらの要素には、値はありません。

次の Transact-SQL の SELECT の例では、ELEMENTS XSINIL 句を示します。

```sql
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
  AND  E.EmployeeID=1
FOR XML PATH, ELEMENTS XSINIL;
```  
  
 結果を次に示します。 XSINIL を指定しないと、<`Middle`> 要素は出力されません。  
  
```xml
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>参照  
 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
