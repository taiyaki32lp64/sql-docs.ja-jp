---
title: XML インデックスの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d8162a8eef652a14993f67e4e3931be7362e6f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929665"
---
# <a name="drop-xml-indexes"></a>XML インデックスの削除
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用すると、XML インデックスと XML 以外のインデックスの両方を含め、既存のプライマリ インデックスまたはセカンダリ インデックスを削除できます。 ただし、DROP INDEX のオプションは XML インデックスに適用されません。 プライマリ XML インデックスを削除すると、存在するセカンダリ XML インデックスもすべて削除されます。  
  
 *TableName.IndexName* を指定する DROP 構文は廃止されるので、XML インデックスではサポートされません。  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>例: プライマリ XML インデックスの作成とドロップ  
 次の例では、 **xml** 型の列に XML インデックスを作成します。  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 テーブルを削除すると、テーブルのすべての XML インデックスも自動的に削除されます。 ただし、XML 列に XML インデックスが存在する場合、その XML 列はテーブルから削除できません。  
  
 次の例では、 **xml** 型の列に XML インデックスを作成します。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 これで次のように、 `Co12`にプライマリ XML インデックスを作成できます。  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-dropexisting-index-option"></a>例: DROP_EXISTING インデックス オプションを使用した XML インデックスの作成  
 次の例では、列 (`XmlColx`) に XML インデックスを作成しています。 次に、同じ名前を使用して異なる列 (`XmlColy`) に別の XML インデックスを作成します。 `DROP_EXISTING` を指定しているので、列 (`XmlColx)` の既存の XML インデックスが削除されて、列 (`XmlColy`) に新しい XML インデックスが作成されます。  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 このクエリからは、指定した XML インデックスを作成する対象の列名が返されます。  
  
## <a name="see-also"></a>参照  
 [XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
