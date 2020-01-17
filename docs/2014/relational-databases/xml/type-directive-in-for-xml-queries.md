---
title: FOR XML クエリの TYPE ディレクティブ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21ff73c95bb85167dfba64d434ed7b6c42051c07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193287"
---
# <a name="type-directive-in-for-xml-queries"></a>FOR XML クエリの TYPE ディレクティブ
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サポート、 [xml &#40;TRANSACT-SQL&#41; ](/sql/t-sql/xml/xml-transact-sql) FOR XML クエリの結果として返す要求オプションには、 `xml` TYPE ディレクティブを指定することによってデータ型。 これにより、サーバーで FOR XML クエリの結果を処理できるようになります。 たとえば、それに対して XQuery を指定に結果を割り当てる、`xml`変数、または書き込み[入れ子になった FOR XML クエリ](use-nested-for-xml-queries.md)します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、TYPE ディレクティブを使用した FOR XML クエリなど、サーバーでのさまざまな構成の結果として、または SQL テーブルの列および出力パラメーターの XML インスタンス データ値を返すために `xml` データ型が使用された場合に、XML データ型のインスタンス データをクライアントに返します。 クライアント アプリケーション コードでは、ADO.NET プロバイダーが、この XML データ型の情報をサーバーからバイナリ エンコードで送信するように要求します。 ただし、TYPE ディレクティブを指定せずに FOR XML を使用した場合、この XML データは文字列型として返されます。 どんな場合でも、クライアント プロバイダーは常にいずれかの形式の XML を処理できます。 TYPE ディレクティブを指定していない最上位レベルでの FOR XML 句は、カーソルと共に使用できません。  
  
## <a name="examples"></a>使用例  
 次の例は、FOR XML クエリでの TYPE ディレクトリの使用方法を示しています。  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>FOR XML クエリの結果の xml 型としての取得  
 次のクエリでは、 `Contacts` テーブルから顧客の連絡先に関する情報を取得します。 `TYPE` に `FOR XML` ディレクティブが指定されているので、結果は `xml` 型として返されます。  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 結果の一部を次に示します。  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>FOR XML クエリ結果の xml 型の変数への代入  
 次の例では、FOR XML の結果が `xml` 型の変数 `@x` に代入されます。 クエリなど、連絡先情報を取得します、 `BusinessEntityID`、 `FirstName`、 `LastName`、およびその他からの電話番号、`AdditionalContactInfo`の列`xml``TYPE`します。 `FOR XML` 句に `TYPE` ディレクティブを指定するので、この XML は `xml` 型として返され、変数に代入されます。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>FOR XML クエリの結果のクエリ  
 FOR XML クエリにより、XML が返されます。 したがって、FOR XML クエリにより返された XML 結果には、`xml` や `query()` などの `value()` 型のメソッドを適用できます。  
  
 次のクエリでは、`xml` データ型の `query()` メソッドを使用して、`FOR XML` クエリの結果にクエリします。 詳細については、「[クエリ&#40;&#41; メソッド &#40;xml データ型&#41;](/sql/t-sql/xml/query-method-xml-data-type)」を参照してください。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 内側の `SELECT ... FOR XML` クエリにより `xml` 型の結果が返され、外側の `SELECT` によりその `xml` 型の結果に `query()` メソッドが適用されます。 `TYPE` ディレクティブが指定されていることに注意してください。  
  
 結果を次に示します。  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 次のクエリでは、`xml` データ型の `value()` メソッドを使用して、`SELECT...FOR XML` クエリにより返された XML 結果から値を取得します。 詳細については、「[value&#40;&#41; メソッド &#40;xml データ型&#41;](/sql/t-sql/xml/value-method-xml-data-type)」を参照してください。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 `value()` メソッドの XQuery パス式により、 `BusinessEntityID` が `1`の顧客の連絡先から 1 つ目の電話番号が取得されます。  
  
> [!NOTE]  
>  TYPE ディレクティブを指定しなかった場合、この FOR XML クエリの結果は `nvarchar(max)` 型として返されます。  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>INSERT、UPDATE、および DELETE (Transact-SQL DML) での FOR XML クエリの結果の使用  
 次の例では、FOR XML クエリをデータ操作言語 (DML) ステートメントで使用する方法について説明します。 この例では、`FOR XML` により `xml` 型のインスタンスが返されます。 また、 `INSERT` ステートメントによりこの XML がテーブルに挿入されます。  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
