---
title: IN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IN_TSQL
- IN
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], matching
- NOT IN keyword
- 8623 (Database Engine error)
- matching values in subquery or list [SQL Server]
- IN keyword
- 8632 (Database Engine error)
ms.assetid: 4419de73-96b1-4dfe-8500-f4507915db04
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 99d179218e52801da593eaba6ef9ff5c7dde5ee0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075064"
---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定された値が、サブクエリまたは一覧内の値と一致するかどうかを判断します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>引数  
 *test_expression*  
 任意の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
 *subquery*  
 1 列の結果セットを返すサブクエリです。 この列のデータ型は、*test_expression* と同じデータ型である必要があります。  
  
 *expression*[ **,** ... *n* ]  
 一致するかどうかのテストに使用する式のリストです。 すべての式は、*test_expression* と同じ型である必要があります。  
  
## <a name="result-types"></a>戻り値の型  
 **Boolean**  
  
## <a name="result-value"></a>結果の値  
 *test_expression* の値が *subquery* によって返される値と等しい場合、またはコンマ区切りの一覧内の任意の*式*と等しい場合、結果の値は TRUE です。それ以外の場合、結果の値は FALSE です。  
  
 NOT IN を使用すると、*サブクエリ*値または*式*が否定されます。  
  
> [!CAUTION]  
>  IN または NOT IN を使用して *test_expression* と比較される *subquery* または *expression* で NULL 値が返された場合は、すべて UNKNOWN が返されます。 IN または NOT IN と共に NULL 値を使用すると、予期しない結果が生じる可能性があります。  
  
## <a name="remarks"></a>Remarks  
 かっこで囲んだ極端に多くの値 (コンマで区切られた数千単位の値) を IN 句に明示的に含めると、リソースが消費されてエラー 8623 または 8632 が返される場合があります。 この問題を回避するには、項目をテーブルの IN リストに格納し、IN 句内に SELECT サブクエリを使用します。  
  
 エラー 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 エラー 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>使用例  
  
### <a name="a-comparing-or-and-in"></a>A. OR と IN を比較する  
 次の例では、デザイン エンジニア、ツール デザイナー、またはマーケティング アシスタントのいずれかである従業員の名前の一覧を選択します。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle = 'Design Engineer'   
   OR e.JobTitle = 'Tool Designer'   
   OR e.JobTitle = 'Marketing Assistant';  
GO  
```  
  
 IN を使用しても同じ結果が得られます。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle IN ('Design Engineer', 'Tool Designer', 'Marketing Assistant');  
GO  
```  
  
 次に各クエリの結果セットを示します。  
  
```  
FirstName   LastName      Title  
---------   ---------   ---------------------  
Sharon      Salavaria   Design Engineer                                     
Gail        Erickson    Design Engineer                                     
Jossef      Goldberg    Design Engineer                                     
Janice      Galvin      Tool Designer                                       
Thierry     D'Hers      Tool Designer                                       
Wanida      Benshoof    Marketing Assistant                                 
Kevin       Brown       Marketing Assistant                                 
Mary        Dempsey     Marketing Assistant                                 
  
(8 row(s) affected)  
```  
  
### <a name="b-using-in-with-a-subquery"></a>B. IN とサブクエリを使用する  
 次の例では、年間の販売ノルマが 250,000 ドルを超えるすべての販売員の ID が `SalesPerson` テーブルから検索され、次に、`Employee` テーブルから、`SELECT` サブクエリの結果に一致する `EmployeeID` の従業員の名前がすべて選択されます。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName   LastName                                             
---------   --------   
Tsvi         Reiter                                              
Michael      Blythe                                              
Tete         Mensa-Annan                                         
  
(3 row(s) affected)  
```  
  
### <a name="c-using-not-in-with-a-subquery"></a>C. NOT IN とサブクエリを使用する  
 次の例では、販売ノルマが 250,000 ドル以下の販売員が検索されます。 `NOT IN` は、値の一覧に一致する項目がない販売員を検索します。  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID NOT IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. IN と NOT IN の使用  
 次の例では、`DimSalesReason` テーブルの `SalesReasonKey` 値と一致する `FactInternetSales` テーブルのすべてのエントリを検出します。  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 次の例では、`DimSalesReason` テーブルの `SalesReasonKey` 値と一致しない `FactInternetSalesReason` テーブルのすべてのエントリを検出します。  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. 式リストで IN を使用する  
 次の例は、`DimEmployee` テーブルで、名が `Mike` または `Michael` の従業員について、営業担当者の ID をすべて検出します。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>参照  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  



