---
title: サブクエリ
description: SQL Data Warehouse と Parallel Data Warehouse でのサブクエリ
ms.custom: seo-lt-2019
titleSuffix: Azure SQL Data Warehouse
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
author: shkale-msft
ms.author: shkale
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c8f60ee25f00c4b9ba4b7959a6447e11a0f549b1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244831"
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>サブクエリ (Azure SQL Data Warehouse、Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  このトピックでは、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] でサブクエリを使用する例を示します。  
  
 SELECT ステートメントの詳細については、「[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)」を参照してください。  
  
## <a name="contents"></a>内容  
  
-   [基本操作](#Basics)  
  
-   [例:SQL Data Warehouse と Parallel Data Warehouse](#Examples)  
  
##  <a name="Basics"></a> 基本操作  
 サブクエリ  
 サブクエリとは、SELECT、INSERT、UPDATE、または DELETE の各ステートメントの内部、または別のサブクエリの内部で入れ子になっているクエリです。 これは、内側のクエリまたは内側の選択とも呼ばれます。  
  
 外側のクエリ  
 サブクエリを含むステートメント。 これは外側の選択とも呼ばれます。  
  
 相関サブクエリ  
 外側のクエリのテーブルを参照するサブクエリ。  
  
##  <a name="Examples"></a> 例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 ここでは、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] でサポートされるサブクエリの例を挙げます。  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. サブクエリの TOP および ORDER BY  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. HAVING 句と相関サブクエリ  
  
```  
SELECT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
GROUP BY dm.EmployeeKey, dm.FirstName, dm.LastName  
HAVING 5000 <=   
(SELECT sum(OrderQuantity)  
FROM FactResellerSales AS frs  
WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
  
```  
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. 相関サブクエリと分析  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. サブクエリ内の相関 UNION ステートメント  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. サブクエリ内の結合述語  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. サブクエリ内の相関する結合述語  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. データ ソースとして相関するサブ選択  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. 集計で使用されるデータ値の相関サブクエリ  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. 相関サブクエリで IN を使用する  
 次の例では、相関または繰り返しサブクエリ内で `IN` を使用しています。 これは、外側のクエリによって値が決まるクエリです。 内側のクエリは、外側のクエリが選択する行に対して 1 回ずつ、繰り返し実行されます。 このクエリは、`FactResellerSales` テーブルの `OrderQuantity` が `5` で、従業員の ID 番号が `DimEmployee` テーブルと `FactResellerSales` テーブルで一致する各従業員の `EmployeeKey` と姓名のインスタンスを 1 つ取得します。  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. サブクエリで EXISTS を使用する場合と IN を使用する場合  
 次の例では、`EXISTS` キーワードと `IN` キーワードを使用した意味的に等しいクエリと、それらの違いを示します。 両方とも、製品のサブカテゴリが `Road Bikes` である各製品名の 1 つのインスタンスを取得するサブクエリの例です。 `ProductSubcategoryKey` は `DimProduct` テーブルと `DimProductSubcategory` テーブルの間で一致します。  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE EXISTS  
    (SELECT *  
     FROM DimProductSubcategory AS dps   
     WHERE dp.ProductSubcategoryKey = dps.ProductSubcategoryKey  
           AND dps.EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
 または  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE dp.ProductSubcategoryKey IN  
    (SELECT ProductSubcategoryKey  
     FROM DimProductSubcategory   
     WHERE EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
### <a name="k-using-multiple-correlated-subqueries"></a>K. 複数の相関サブクエリを使用する  
 この例では、2 つの相関サブクエリを使って、特定の製品を販売した従業員の名前を検索します。  
  
```  
SELECT DISTINCT LastName, FirstName, e.EmployeeKey  
FROM DimEmployee e JOIN FactResellerSales s ON e.EmployeeKey = s.EmployeeKey  
WHERE ProductKey IN  
(SELECT ProductKey FROM DimProduct WHERE ProductSubcategoryKey IN  
(SELECT ProductSubcategoryKey FROM DimProductSubcategory   
 WHERE EnglishProductSubcategoryName LIKE '%Bikes'))  
ORDER BY LastName  
;  
  
```  
  
  
