---
title: delete (XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- delete keyword
- delete statement [XML DML]
- deleting nodes
ms.assetid: b22c93a4-b84d-4356-af4c-6013322a4b71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cf804f934a08db335c55b15ab23b9e42a7ee9c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051322"
---
# <a name="delete-xml-dml"></a>delete (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML インスタンスのノードを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
delete Expression  
```  
  
## <a name="arguments"></a>引数  
 *[式]*  
 削除するノードを特定する XQuery 式です。 この式で選択されたすべてのノードと、これらの選択されたノード内にあるすべてのノードまたは値が削除されます。 「[insert (XML DML)](../../t-sql/xml/insert-xml-dml.md)」で説明したように、これはドキュメント内の既存のノードへの参照である必要があります。 構築されたノードは使用できません。 また、この式をルート (/) ノードにすることもできません。 この式で空のシーケンスが返されると、削除が行われず、エラーも返されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-deleting-nodes-from-a-document-stored-in-an-untyped-xml-variable"></a>A. 型指定されていない XML 変数に格納されているドキュメントからノードを削除する  
 次の例では、ドキュメントのさまざまなノードを削除する方法を示します。 まず、XML インスタンスが **xml** 型の変数に代入されます。 その後、これに続く delete XML DML ステートメントにより、ドキュメントの各種ノードを削除しています。  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<?Instructions for=TheWC.exe ?>   
<Root>  
 <!-- instructions for the 1st work center -->  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Some text 1  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
SELECT @myDoc  
  
-- delete an attribute  
SET @myDoc.modify('  
  delete /Root/Location/@MachineHours  
')  
SELECT @myDoc  
  
-- delete an element  
SET @myDoc.modify('  
  delete /Root/Location/step[2]  
')  
SELECT @myDoc  
  
-- delete text node (in <Location>  
SET @myDoc.modify('  
  delete /Root/Location/text()  
')  
SELECT @myDoc  
  
-- delete all processing instructions  
SET @myDoc.modify('  
  delete //processing-instruction()  
')  
SELECT @myDoc  
```  
  
### <a name="b-deleting-nodes-from-a-document-stored-in-an-untyped-xml-column"></a>B. 型指定されていない XML 列に格納されているドキュメントからノードを削除する  
 次の例では、**delete** XML DML ステートメントにより、列に格納されているドキュメントから <`Features`> の 2 番目の子要素を削除します。  
  
```  
CREATE TABLE T (i int, x xml)  
go  
INSERT INTO T VALUES(1,'<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>')  
go  
-- verify the contents before delete  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
-- delete the second feature  
UPDATE T  
SET x.modify('delete /Root/ProductDescription/Features/*[2]')  
-- verify the deletion  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   [modify() メソッド (xml データ型)](../../t-sql/xml/modify-method-xml-data-type.md) を使用して、**delete** XML DML キーワードを指定しています。  
  
-   [query() メソッド (XML データ型)](../../t-sql/xml/query-method-xml-data-type.md) を使用して、ドキュメントに対するクエリを実行しています。  
  
### <a name="c-deleting-nodes-from-a-typed-xml-column"></a>C. 型指定された xml 列からノードを削除する  
 次の例では、型指定された **xml** 列に格納されている、製造手順の XML ドキュメントからノードを削除します。  
  
 この例では、まず、型指定された **xml** 列を含むテーブル (T) を AdventureWorks データベースに作成します。 続いて、ProductModel テーブルの Instructions 列から製造手順の XML インスタンスをテーブル T にコピーし、このコピーされたドキュメントから 1 つ以上のノードを削除します。  
  
```  
use AdventureWorks  
go  
drop table T  
go  
create table T(ProductModelID int primary key,   
Instructions xml (Production.ManuInstructionsSchemaCollection))  
go  
insert  T   
select ProductModelID, Instructions  
from Production.ProductModel  
where ProductModelID=7  
go  
select Instructions  
from T  
--1) insert <Location 1000/>. Note: <Root> must be singleton in the query  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  insert <MI:Location LocationID="1000"  LaborHours="1000" >  
           These are manu steps at location 1000.   
           <MI:step>New step1 instructions</MI:step>  
           Instructions for step 2 are here  
           <MI:step>New step 2 instructions</MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
  
-- delete an attribute  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/@LaborHours)   
')  
go  
select Instructions  
from T  
-- delete text in <location>  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/text())   
')  
go  
select Instructions  
from T  
-- delete 2nd manu step at location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/MI:step[2])   
')  
go  
select Instructions  
from T  
-- cleanup  
drop table T  
go  
```  
  
## <a name="see-also"></a>参照  
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
