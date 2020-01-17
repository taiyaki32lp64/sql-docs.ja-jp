---
title: xml データ型に対する FOR XML サポート | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa53478ba653961d255ee3a03038d44fcbd15f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943258"
---
# <a name="for-xml-support-for-the-xml-data-type"></a>xml データ型に対する FOR XML サポート
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML クエリによって SELECT 句で **xml** 型の列が指定された場合、ELEMENTS ディレクティブを指定したかどうかにかかわらず、返された XML では列の値が要素としてマップされます。 **xml** 型の列内の XML 宣言はシリアル化されません。  
  
 たとえば、次のクエリは、 `BusinessEntityID`、 `FirstName`、および `LastName` 列、および `AdditionalContactInfo` xml **型の** 列からの電話番号など、顧客の連絡先の情報を取得します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 クエリでは ELEMENTS ディレクティブが指定されていないため、 **xml** 型の列から取得された追加の連絡先の情報の値を除き、列の値が属性として返されます。 これらは要素として返されます。  
  
 結果の一部を次に示します。  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</PhoneNumber>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</PhoneNumber>`  
  
```  
</Person.Person>  
...  
```  
  
 XQuery によって生成された XML 列に対して列の別名を指定した場合、その別名は XQuery によって生成された XML にラッパー要素を追加する際に使用されます。 たとえば、次のクエリでは、列の別名として `MorePhoneNumbers` を指定しています。  
  
```  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 XQuery によって返された XML は、次の結果の一部で示すように、<`MorePhoneNumbers`> 要素でラップされます。  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</MorePhoneNumbers>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</MorePhoneNumbers>`  
  
```  
</Person.Person>  
...  
```  
  
 クエリで ELEMENTS ディレクティブを指定した場合、結果の XML では、BusinessEntityID、LastName、および FirstName が要素として返されます。  
  
 次に、 **xml** 型の列の XML データでは、FOR XML の処理ロジックによって XML 宣言がシリアル化されない例を示します。  
  
```  
create table t(i int, x xml)  
go  
insert into t values(1, '<?xml version="1.0" encoding="UTF-8" ?>  
                             <Root SomeID="10" />')  
select i, x  
from   t  
for xml auto;  
```  
  
 結果は次のとおりです。 結果の XML では、XML 宣言 <`?xml version="1.0" encoding="UTF-8" ?`> はシリアル化されません。  
  
```  
<root>  
  <t i="1">  
    <x>  
      <Root SomeID="10" />  
    </x>  
  </t>  
</root>  
```  
  
## <a name="returning-xml-from-a-user-defined-function"></a>ユーザー定義関数から XML を返す  
 FOR XML クエリを使用して、次のいずれかを返すユーザー定義関数から XML を返すことができます。  
  
-   1 つの **xml** 型の列を持つテーブル  
  
-   **xml** 型のインスタンス  
  
 たとえば、次のユーザー定義関数は、 **xml**型の 1 つの列を持つテーブルを返します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.MyUDF (@ProudctModelID int)  
RETURNS @T TABLE  
  (  
     ProductDescription xml  
  )  
AS  
BEGIN  
  INSERT @T  
     SELECT CatalogDescription.query('  
declare namespace PD="https://www.adventure-works.com/schemas/products/description";  
                    //PD:ProductDescription  ')  
     FROM Production.ProductModel  
     WHERE ProductModelID = @ProudctModelID  
  RETURN  
END;  
```  
  
 ユーザー定義関数を実行して、その関数から返されたテーブルにクエリを実行することができます。 この例では、そのテーブルのクエリの結果として返された XML が、 **xml** 型の変数に代入されます。  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 次に、別のユーザー定義関数の例を示します。 このユーザー定義関数は、 **xml** 型のインスタンスを返します。 この例では、スキーマの名前空間が指定されているため、ユーザー定義関数は型指定された XML インスタンスを返します。  
  
```  
DROP FUNCTION dbo.MyUDF;  
GO  
CREATE FUNCTION MyUDF (@ProductModelID int)   
RETURNS xml ([Production].[ProductDescriptionSchemaCollection])  
AS  
BEGIN  
  declare @x xml  
  set @x =   ( SELECT CatalogDescription  
          FROM Production.ProductModel  
          WHERE ProductModelID = @ProductModelID )  
  return @x  
END;  
```  
  
 ユーザー定義関数から返された XML は、次のように **xml** 型の変数に代入できます。  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>参照  
 [各種 SQL Server データ型の FOR XML サポート](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
