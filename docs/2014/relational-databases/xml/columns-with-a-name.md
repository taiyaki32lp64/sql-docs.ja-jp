---
title: 名前のある列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a57f4b1a56c3a23c9be8957f97fa7b352f9674a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638166"
---
# <a name="columns-with-a-name"></a>名前のある列
  行セット内の名前のある列が、大文字と小文字を区別して結果の XML にマップされる条件を次に示します。  
  
-   列名がアット マーク (\@) で始まる場合。  
  
-   列名がアット マーク (\@) で始まらない場合。  
  
-   列名がアット マーク (\@) で始まらず、スラッシュ (/) を含む場合。  
  
-   複数の列に同一のプレフィックスがある場合  
  
-   名前の異なる列がある場合  
  
## <a name="column-name-starts-with-an-at-sign-"></a>列名がアット マーク (\@) で始まる場合  
 列名で始まる場合、アット マーク (\@) にスラッシュ記号 (/) の属性が含まれていないと、<`row`> を対応する列の値を持つ要素が作成されます。 たとえば、次のクエリは 2 列 (\@PmId、Name) の行セットを返します。 結果の XML では、対応する <`row`> 要素に **PmId** 属性が追加され、この属性に ProductModelID の値が設定されます。  
  
```  
  
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
  
```  
  
 結果を次に示します。  
  
```  
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 属性は、同一レベルでは要素ノード、テキスト ノードなどの他の種類のノードよりも前に指定する必要があります。 次のクエリはエラーを返します。  
  
```  
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>列名がアット マーク (\@) で始まらない場合  
 列名が始まっていない場合、アット マーク (\@)、XPath ノード テストのいずれかで、ない場合、スラッシュ記号 (/)、行要素のサブ要素である XML 要素を含まない <`row`> 既定では、作成されます。  
  
 次のクエリでは列名 result が指定されています。 したがって、<`row`> 要素には、<`result`> 子要素が追加されます。  
  
```  
SELECT 2+2 as result  
for xml PATH  
```  
  
 結果を次に示します。  
  
```  
<row>  
  <result>4</result>  
</row>  
```  
  
 次のクエリでは、**xml** 型の Instructions 列に対して指定した XQuery から返される XML に対応する列の名前として、ManuWorkCenterInformation を指定しています。 したがって、<`row`> 要素の子要素として、<`ManuWorkCenterInformation`> 要素が追加されます。  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
 結果を次に示します。  
  
```  
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>列名がアット マーク (\@) で始まらず、スラッシュ (/) を含む場合  
 列名がアット マーク (\@) で始まらず、スラッシュ (/) を含んでいる場合、列名は XML 階層を示します。 たとえば、列名を "Name1/Name2/Name3.../Name***n*** " とすると、Name***i*** は、i = 1 の場合は現在の行要素の入れ子である要素を表し、それ以外の場合は Name***i-1***要素の下にある要素を表します。 Name***n*** が '\@' で始まる場合は、Name***n-1*** 要素の属性にマップされます。  
  
 たとえば次のクエリは、従業員の ID と名前を返します。従業員名は、First、Middle、および Last から構成される複合型の要素 EmpName で表現されます。  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 PATH モードでは、列名は XML を作成する際のパスとして使用されます。 従業員 ID の値を格納している列の名前が始まる '\@'。そのため、属性、 **EmpID**に追加されて、<`row`> 要素。 それ以外のすべての列の列名には、階層を示すスラッシュ ('/') が含まれています。 結果の XML では、<`row`> 要素の下に <`EmpName`> 子要素があり、<`EmpName`> の下に子要素 <`First`>、<`Middle`>、および <`Last`> が生成されます。  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 この従業員のミドル ネームは NULL です。既定では、要素や属性がない状態に NULL 値がマップされます。 値が NULL であっても要素を生成するには、次のクエリのように XSINIL を指定した ELEMENTS ディレクティブを使用します。  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 結果を次に示します。  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 PATH モードの既定では要素中心の XML が生成されます。 したがって、PATH モードのクエリで ELEMENTS ディレクティブを指定しても効力はありません。 ただし、前のクエリで示したように、ELEMENTS ディレクティブを XSINIL と組み合わせると、NULL 値に対して要素を生成する場合に便利です。  
  
 次のクエリでは従業員の ID と名前以外に住所を取得します。 住所列の列名のパスにより、<`row`> 要素に <`Address`> 子要素が追加され、<`Address`> 要素の子要素として詳しい住所が追加されます。  
  
```  
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 結果を次に示します。  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## <a name="several-columns-share-the-same-path-prefix"></a>複数の列に同一のパス プレフィックスがある場合  
 連続した複数の列に同一のパス プレフィックスがある場合、これらの列は 1 つの名前でグループ化されます。 異なる名前空間プレフィックスが使用されている場合は、同一の名前空間にバインドされていても、パスは異なるものと見なされます。 上のクエリで、FirstName 列、MiddleName 列、および LastName 列にはいずれも EmpName プレフィックスがあるので、これらは <`EmpName`> 要素の子として追加されます。 このことは、上記の例の <`Address`> 要素の生成にも該当します。  
  
## <a name="one-column-has-a-different-name"></a>名前の異なる列がある場合  
 変更を加えた次のクエリに示すように、異なる名前の列が間にある場合、グループは分割されます。 上のクエリで示した FirstName、MiddleName、および LastName から構成されるグループは、FirstName 列と MiddleName 列の間に住所列を追加すると分割されます。  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 このクエリの結果、<`EmpName`> 要素が 2 つ作成されます。 最初の <`EmpName`> 要素には <`FirstName`> 子要素が、2 番目の <`EmpName`> 要素には <`MiddleName`> 子要素と <`LastName`> 子要素が含まれます。  
  
 結果を次に示します。  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>関連項目  
 [FOR XML での PATH モードの使用](use-path-mode-with-for-xml.md)  
  
  
