---
title: '例: 従業員情報の取得 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT mode
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3e123a5195d9eb6a5dd489c635cdd687b42f720
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006779"
---
# <a name="example-retrieving-employee-information"></a>例:従業員情報の取得
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  この例では、各従業員の従業員 ID と名前を取得します。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの場合、employeeID は Employee テーブルの BusinessEntityID 列から取得できます。 従業員名は、Person テーブルから取得できます。 これらのテーブルを結合する際には、BusinessEntityID 列を使用します。  
  
 FOR XML EXPLICIT 変換で、次に示す XML を生成するとします。  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 階層は 2 レベルなので、`SELECT` クエリを 2 つ記述して、UNION ALL を適用します。 <`Employee`> 要素とその属性の値を取得する 1 つ目のクエリを次に示します。 <`Employee`> 要素は最上位要素なので、このクエリでは、この要素の `1` 列に値 `Tag` を割り当て、`Parent` 列には NULL を割り当てます。  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 2 つ目のクエリを次に示します。 このクエリでは、<`Name`> 要素の値を取得します。 <`2`> 要素の `Tag` 列に値 `Name` を割り当て、`1` 列には値 `Parent` を割り当てて、親要素が <`Employee`> であることを示します。  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 `UNION AL` を使用してこれらのクエリを結合し、`FOR XML EXPLICIT` を適用して、必要な `ORDER BY` 句を指定します。 行セットは、まず `BusinessEntityID` で並べ替え、次に name で並べ替えます。このように並べ替えると、name に NULL が設定されている行が先に表示されるようになります。 FOR XML 句を指定せずに次のクエリを実行すると、ユニバーサル テーブルが生成されます。  
  
 最終的なクエリは、次のようになります。  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
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
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 結果の一部を次に示します。  
  
```
<Employee EmpID="1">
  <Name FName="Ken" LName="Sánchez" />
</Employee>
<Employee EmpID="2">
  <Name FName="Terri" LName="Duffy" />
</Employee>
...
```
  
 1 つ目の `SELECT` では、結果の行セット内の列名を指定しています。 この名前により、2 つの列グループが形成されます。 `Tag` 列の値が `1` のグループでは、`Employee` が要素であり、`EmpID` が属性であると識別されます。 `Tag` 列の値が `2` のグループでは、<`Name`> が要素であり、`FName` と `LName` が属性であると識別されます。  
  
 次の表に、このクエリを実行した結果として生成される行セットの一部を示します。  
  
タグ | Parent | Employee!1!EmpID | Name!2!FName | Name!2!LName
-|-|-|-|-
1 | NULL | 1 | NULL | NULL 
2 | 1 | 1 | Ken | Sánchez 
1 | NULL | 2 | NULL | NULL 
2 | 1 | 2 | Terri | Duffy 
1 | NULL | 3 | NULL | NULL 
2 | 1 | 3 | Roberto | Tamburello 
[...] | [...] | [...] | [...] | [...]
  
 結果の XML ツリーを生成する際、ユニバーサル テーブル内の行は、次のように処理されます。  
  
 1 行目の `Tag` 列の値は `1`です。 これにより、 `Tag` 列に値 `1` が割り当てられた列グループとして `Employee!1!EmpID`が識別されます。 この列では、`Employee` は要素名として識別されます。 その後、`EmpID` 属性を持つ <`Employee`> 要素が作成されます。 これらの属性には、対応する列の値が割り当てられます。  
  
 2 行目の `Tag` 列の値は `2`です。 これにより、 `Tag` 列に値 `2` が割り当てられた列グループとして `Name!2!FName`、 `Name!2!LName`が識別されます。 これらの列では、`Name` が要素名として識別されます。 <`Name`> 要素の作成時には、`FName` 属性と `LName` 属性が識別されます。 これらの属性には、対応する列の値が割り当てられます。 この行の `1` 列には値 `Parent` が割り当てられています。 したがって、この要素は、1 行目の <`Employee`> 要素に子要素として追加されます。  
  
 この処理が、行セット内の残りの行に対して繰り返されます。 FOR XML EXPLICIT で行セットを順に処理して、必要な XML を生成できるようにするには、ユニバーサル テーブル内の行の並び順が重要になります。  
  
## <a name="see-also"></a>参照  
 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
