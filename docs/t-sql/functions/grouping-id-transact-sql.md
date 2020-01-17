---
title: GROUPING_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING_ID_TSQL
- GROUPING_ID
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, GROUPING_ID
- GROUPING_ID function
ms.assetid: c1050658-b19f-42ee-9a05-ecd6a73b896c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 13680aea1d34b83d76647d39d0f40b84609b2e8c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910653"
---
# <a name="groupingid-transact-sql"></a>GROUPING_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  グループ化のレベルを計算する関数です。 GROUPING_ID は、GROUP BY が指定されている場合に、SELECT \<select> リスト、HAVING 句、または ORDER BY 句でのみ使用できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GROUPING_ID ( <column_expression>[ ,...n ] )  
```  
  
## <a name="arguments"></a>引数  
 \<column_expression>  
 [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 句の *column_expression* です。  
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 GROUPING_ID \<column_expression> は、GROUP BY リストの式と正確に一致させる必要があります。 たとえば、DATEPART (yyyy, \<*列名*>) でグループ化する場合は GROUPING_ID (DATEPART (yyyy, \<*列名*>)) を使用し、\<*列名* でグループ化する場合は GROUPING_ID (\<*列名*>) を使用します。  
  
## <a name="comparing-groupingid--to-grouping-"></a>GROUPING_ID () と GROUPING () の比較  
 GROUPING_ID (\<列式> [ **,** ...*n* ]) は、列リストの各列に関して返される GROUPING (\<列式>) に相当する値を、0 と 1 の文字列として各出力行に入力します。 GROUPING_ID は、その文字列を基数 2 の数値として解釈し、同等の整数を返します。 たとえば、`SELECT a, b, c, SUM(d),``GROUPING_ID(a,b,c)``FROM T GROUP BY <group by list>` というステートメントがあるものとします。 GROUPING_ID () の入力値と出力値を次の表に示します。  
  
|集計列|GROUPING_ID (a, b, c) の入力 = GROUPING(a) + GROUPING(b) + GROUPING(c)|GROUPING_ID () の出力|  
|------------------------|---------------------------------------------------------------------------------------|------------------------------|  
|`a`|`100`|`4`|  
|`b`|`010`|`2`|  
|`c`|`001`|`1`|  
|`ab`|`110`|`6`|  
|`ac`|`101`|`5`|  
|`bc`|`011`|`3`|  
|`abc`|`111`|`7`|  
  
## <a name="technical-definition-of-groupingid-"></a>GROUPING_ID () の技術的な定義  
 各 GROUPING_ID 引数は、GROUP BY リストの要素でなければなりません。 GROUPING_ID () は、最下位 N ビットが点灯する場合がある **integer** ビットマップを返します。 点灯した **bit** は、対応する引数が特定の出力行に対するグループ列でないことを示します。 最も順位が低い **bit** は引数 N に対応し、N-1<sup> </sup>番目に順位が低い **bit** は引数 1 に対応します。  
  
## <a name="groupingid--equivalents"></a>GROUPING_ID () の対応  
 単一グループ クエリの場合、GROUPING (\<列式>) は GROUPING_ID (\<列式>) に対応し、いずれも 0 を返します。  
  
 たとえば、次のステートメントは互いに対応しています。  
  
 ステートメント A:  
  
```  
SELECT GROUPING_ID(A,B)  
FROM T   
GROUP BY CUBE(A,B)   
```  
  
 ステートメント B:  
  
```  
SELECT 3 FROM T GROUP BY ()  
UNION ALL  
SELECT 1 FROM T GROUP BY A  
UNION ALL  
SELECT 2 FROM T GROUP BY B  
UNION ALL  
SELECT 0 FROM T GROUP BY A,B  
```  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-groupingid-to-identify-grouping-levels"></a>A. GROUPING_ID を使用してグループ化レベルを識別する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `Name` と `Title` ごとの従業員数、`Name,` ごとの従業員数、および会社の合計従業員数が返されます。 `GROUPING_ID()` は、集計レベルを示す `Title` 列の各行に対する値を作成するために使われます。  
  
```  
SELECT D.Name  
    ,CASE   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 0 THEN E.JobTitle  
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 1 THEN N'Total: ' + D.Name   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 3 THEN N'Company Total:'  
        ELSE N'Unknown'  
    END AS N'Job Title'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle);  
```  
  
### <a name="b-using-groupingid-to-filter-a-result-set"></a>B. GROUPING_ID を使用して結果セットをフィルター処理する  
  
#### <a name="simple-example"></a>簡単な例  
 役職ごとの従業員数が含まれた行のみを返すには、次のコードの [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `HAVING GROUPING_ID(D.Name, E.JobTitle); = 0` からコメント文字を削除します。 部門ごとの従業員数が含まれた行のみを返すには、`HAVING GROUPING_ID(D.Name, E.JobTitle) = 1;` からコメント文字を削除します。  
  
```  
SELECT D.Name  
    ,E.JobTitle  
    ,GROUPING_ID(D.Name, E.JobTitle) AS 'Grouping Level'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee AS E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department AS D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle)  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 0; --All titles  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 1; --Group by Name;  
```  
  
 フィルター処理していない結果セットは、次のようになります。  
  
|[オブジェクト名]|[タイトル]|グループ化のレベル|従業員数|[オブジェクト名]|  
|----------|-----------|--------------------|--------------------|----------|  
|文書コントロール|コントロール スペシャリスト|0|2|文書コントロール|  
|文書コントロール|文書コントロール アシスタント|0|2|文書コントロール|  
|文書コントロール|文書コントロール マネージャー|0|1|文書コントロール|  
|文書コントロール|NULL|1|5|文書コントロール|  
|設備およびメンテナンス|設備管理アシスタント|0|1|設備およびメンテナンス|  
|設備およびメンテナンス|設備マネージャー|0|1|設備およびメンテナンス|  
|設備およびメンテナンス|管理人|0|4|設備およびメンテナンス|  
|設備およびメンテナンス|メンテナンス スーパーバイザー|0|1|設備およびメンテナンス|  
|設備およびメンテナンス|NULL|1|7|設備およびメンテナンス|  
|NULL|NULL|3|12|NULL|  
  
#### <a name="complex-example"></a>複雑な例  
 次の例では、`GROUPING_ID()` を使用して、複数のグループ化レベルが含まれた結果セットをグループ化レベルでフィルター処理します。 これと同様のコードを使用すると、複数のグループ化レベルがあるビューとストアド プロシージャを作成できます。このストアド プロシージャは、ビューをグループ化レベルでフィルター処理するパラメーターを渡すことによって、ビューを呼び出します。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```  
DECLARE @Grouping nvarchar(50);  
DECLARE @GroupingLevel smallint;  
SET @Grouping = N'CountryRegionCode Total';  
  
SELECT @GroupingLevel = (  
    CASE @Grouping  
        WHEN N'Grand Total'             THEN 15  
        WHEN N'SalesPerson Total'       THEN 14  
        WHEN N'Store Total'             THEN 13  
        WHEN N'Store SalesPerson Total' THEN 12  
        WHEN N'CountryRegionCode Total' THEN 11  
        WHEN N'Group Total'             THEN 7  
        ELSE N'Unknown'  
    END);  
  
SELECT   
    T.[Group]  
    ,T.CountryRegionCode  
    ,S.Name AS N'Store'  
    ,(SELECT P.FirstName + ' ' + P.LastName   
        FROM Person.Person AS P   
        WHERE P.BusinessEntityID = H.SalesPersonID)  
        AS N'Sales Person'  
    ,SUM(TotalDue)AS N'TotalSold'  
    ,CAST(GROUPING(T.[Group])AS char(1)) +   
        CAST(GROUPING(T.CountryRegionCode)AS char(1)) +   
        CAST(GROUPING(S.Name)AS char(1)) +   
        CAST(GROUPING(H.SalesPersonID)AS char(1))   
        AS N'GROUPING base-2'  
    ,GROUPING_ID((T.[Group])  
        ,(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
        ) AS N'GROUPING_ID'  
    ,CASE   
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 15 THEN N'Grand Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 14 THEN N'SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 13 THEN N'Store Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 12 THEN N'Store SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 11 THEN N'CountryRegionCode Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) =  7 THEN N'Group Total'  
        ELSE N'Error'  
        END AS N'Level'  
FROM Sales.Customer AS C  
    INNER JOIN Sales.Store AS S  
        ON C.StoreID  = S.BusinessEntityID   
    INNER JOIN Sales.SalesTerritory AS T  
        ON C.TerritoryID  = T.TerritoryID   
    INNER JOIN Sales.SalesOrderHeader AS H  
        ON C.CustomerID = H.CustomerID  
GROUP BY GROUPING SETS ((S.Name,H.SalesPersonID)  
    ,(H.SalesPersonID),(S.Name)  
    ,(T.[Group]),(T.CountryRegionCode),()  
    )  
HAVING GROUPING_ID(  
    (T.[Group]),(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
    ) = @GroupingLevel  
ORDER BY   
    GROUPING_ID(S.Name,H.SalesPersonID),GROUPING_ID((T.[Group])  
    ,(T.CountryRegionCode)  
    ,(S.Name)  
    ,(H.SalesPersonID))ASC;  
```  
  
### <a name="c-using-groupingid--with-rollup-and-cube-to-identify-grouping-levels"></a>C. GROUPING_ID () を ROLLUP および CUBE と共に使用してグループ化レベルを識別する  
 以下は、`GROUPING()` を使用して `Bit Vector(base-2)` 列を計算するコードの例です。 `GROUPING_ID()` は、対応する `Integer Equivalent` 列を計算するために使用されます。 `GROUPING_ID()` 関数の列順序は、`GROUPING()` 関数によって連結された列の列順序の逆になります。  
  
 これらの例では、グループ化レベルを示すための値を `Grouping Level` 列の各行に対して作成するために、`GROUPING_ID()` が使用されます。 グループ化レベルは、1 で始まる整数の連番リスト (0, 1, 2,...*n*) になるとは限りません。  
  
> [!NOTE]  
>  GROUPING と GROUPING_ID は、結果セットをフィルター処理するために HAVING 句で使用できます。  
  
#### <a name="rollup-example"></a>ROLLUP の例  
 この例では、すべてのグループ化レベルが次の CUBE 例の場合と同様に表示されるわけではありません。 `ROLLUP` リストの列の順序が変更された場合は、`Grouping Level` 列のレベル値も変更する必要があります。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
     AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY ROLLUP(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(mm,OrderDate)  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 次に結果セットの一部を示します。  
  
|年|Month|日|精算額|ビット ベクター (基数 2)|等価の整数|グループ化のレベル|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|年月日|  
|2007|1|2|21772.3494|000|0|年月日|  
|2007|2|1|2705653.5913|000|0|年月日|  
|2007|2|2|21684.4068|000|0|年月日|  
|2008|1|1|1908122.0967|000|0|年月日|  
|2008|1|2|46458.0691|000|0|年月日|  
|2008|2|1|3108771.9729|000|0|年月日|  
|2008|2|2|54598.5488|000|0|年月日|  
|2007|1|NULL|1519224.956|100|1|年月|  
|2007|2|NULL|2727337.9981|100|1|年月|  
|2008|1|NULL|1954580.1658|100|1|年月|  
|2008|2|NULL|3163370.5217|100|1|年月|  
|2007|NULL|NULL|4246562.9541|110|3|年|  
|2008|NULL|NULL|5117950.6875|110|3|年|  
|NULL|NULL|NULL|9364513.6416|111|7|総計|  
  
#### <a name="cube-example"></a>CUBE の例  
 この例では、`GROUPING_ID()` 関数を使用して、グループ化レベルを識別する値を `Grouping Level` 列の各行に対して作成します。  
  
 前の例の `ROLLUP` と異なり、`CUBE` ではすべてのグループ化レベルが出力されます。 `CUBE` リストの列の順序が変更された場合は、`Grouping Level` 列のレベル値も変更する必要があります。 この例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを使用します。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
        AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'Year Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY CUBE(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 次に結果セットの一部を示します。  
  
|年|Month|日|精算額|ビット ベクター (基数 2)|等価の整数|グループ化のレベル|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|年月日|  
|2007|1|2|21772.3494|000|0|年月日|  
|2007|2|1|2705653.5913|000|0|年月日|  
|2007|2|2|21684.4068|000|0|年月日|  
|2008|1|1|1908122.0967|000|0|年月日|  
|2008|1|2|46458.0691|000|0|年月日|  
|2008|2|1|3108771.9729|000|0|年月日|  
|2008|2|2|54598.5488|000|0|年月日|  
|2007|1|NULL|1519224.956|100|1|年月|  
|2007|2|NULL|2727337.9981|100|1|年月|  
|2008|1|NULL|1954580.1658|100|1|年月|  
|2008|2|NULL|3163370.5217|100|1|年月|  
|2007|NULL|1|4203106.1979|010|2|年日|  
|2007|NULL|2|43456.7562|010|2|年日|  
|2008|NULL|1|5016894.0696|010|2|年日|  
|2008|NULL|2|101056.6179|010|2|年日|  
|2007|NULL|NULL|4246562.9541|110|3|年|  
|2008|NULL|NULL|5117950.6875|110|3|年|  
|NULL|1|1|3405574.7033|001|4|月日|  
|NULL|1|2|68230.4185|001|4|月日|  
|NULL|2|1|5814425.5642|001|4|月日|  
|NULL|2|2|76282.9556|001|4|月日|  
|NULL|1|NULL|3473805.1218|101|5|Month|  
|NULL|2|NULL|5890708.5198|101|5|Month|  
|NULL|NULL|1|9220000.2675|011|6|日|  
|NULL|NULL|2|144513.3741|011|6|日|  
|NULL|NULL|NULL|9364513.6416|111|7|総計|  
  
## <a name="see-also"></a>参照  
 [GROUPING &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
