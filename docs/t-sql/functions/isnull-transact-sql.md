---
title: ISNULL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b49310a633c822f8c57f66cc36951dfebe2c0707
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843644"
---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

NULL 値を、指定された値に置き換えます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>引数  
 *check_expression*  
 NULL かどうかを調べる[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 *check_expression* は任意のデータ型です。  
  
 *replacement_value*  
 *check_expression* が NULL の場合に返される式です。 *replacement_value* は、暗黙的に *check_expression* の型に変換できる型である必要があります。  
  
## <a name="return-types"></a>戻り値の型  
 *check_expression* と同じ型が返されます。 リテラル NULL が *check_expression* として指定されている場合、*replacement_value* のデータ型を返します。 リテラル NULL が *check_expression* として指定されていて *replacement_value* が指定されていない場合、**int** を返します。  
  
## <a name="remarks"></a>Remarks  
 *check_expression* の値が NULL でない場合、その値が返されます。それ以外の場合は、*replacement_value* が返されます。このとき、型どうしが異なる場合は *check_expression* の型に暗黙的に変換されてから返されます。 *replacement_value* は、*replacement_value* が *check_expression* より長い場合は切り捨てられることがあります。  
  
> [!NOTE]  
>  最初の null 以外の値を返すには、[COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md) を使用します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-isnull-with-avg"></a>A. AVG で ISNULL を使用する  
 次の例では、すべての製品の重量の平均を求めます。 `Product` テーブルの `Weight` 列にあるすべての NULL エントリに、値 `50` を代入します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>B. ISNULL を使用する  
 次の例では、`AdventureWorks2012` のすべての特価品について、説明、値引き率、最小数量、および最大数量を選択します。 ある特価品の最大数量が NULL の場合、結果セットに表示される `MaxQty` は `0.00` です。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  [説明]       |  DiscountPct    |   MinQty    |   最大数量       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain-100 Cl   |  0.35           |   0         |   0                  |
|  Sport Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  Sport Helmet Di   |  0.15           |   0         |   0                  |
|  LL Road Frame S   |  0.35           |   0         |   0                  |
|  Touring-3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  Half-Price Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. WHERE 句で NULL をテストする  
 NULL 値の検索に ISNULL を使用しないでください。 代わりに IS NULL を使用します。 次の例では、weight 列が `NULL` の製品をすべて検索しています。 `IS` と `NULL` の間にスペースがあることに注意してください。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. AVG で ISNULL を使用する  
 次の例では、サンプル テーブルのすべての製品の重量の平均を求めます。 `Product` テーブルの `Weight` 列にあるすべての NULL エントリに、値 `50` を代入します。  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. ISNULL を使用する  
 次の例では、ISNULL を使って`MinPaymentAmount` 列が NULL かどうかをテストし、NULL の行には値 `0.00` を表示します。  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 次に結果セットの一部を示します。  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  A Bicycle Association       |     0.0000         |
|  A Bike Store                |     0.0000         |
|  A Cycle Shop                |     0.0000         |
|  A Great Bicycle Company     |     0.0000         |
|  A Typical Bike Shop         |   200.0000         |
|  Acceptable Sales & Service  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. IS NULL を使用して WHERE 句の NULL をテストする  
 次の例では、`Weight` 列が `NULL` の製品をすべて検索しています。 `IS` と `NULL` の間にスペースがあることに注意してください。  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  

