---
title: ユーザー定義関数の作成 (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
- UDF
- TVF
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 62d63c65ce1fae63fa9453a0dc37ddc134a87012
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138750"
---
# <a name="create-user-defined-functions-database-engine"></a>ユーザー定義関数の作成 (データベース エンジン)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してユーザー定義関数 (UDF) を作成する方法について説明します。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ユーザー定義関数は、データベースの状態を変更するアクションの実行に使用することはできません。  
  
-   出力先がテーブルである `OUTPUT INTO` 句をユーザー定義関数に含めることはできません。  
  
-   ユーザー定義関数では複数の結果セットは返せません。 複数の結果セットを返す必要がある場合は、ストアド プロシージャを使用します。  
  
-   エラー処理は、ユーザー定義の関数では制限されます。 UDF では `TRY...CATCH`、`@ERROR`、`RAISERROR` はいずれもサポートされません。  
  
-   ユーザー定義関数はストアド プロシージャを呼び出すことができませんが、拡張ストアド プロシージャを呼び出すことはできます。  
  
-   ユーザー定義関数では、動的 SQL または一時テーブルを利用することはできません。 テーブル変数は使用できます。  
  
-   `SET` ステートメントはユーザー定義関数では使用できません。  
  
-   `FOR XML` 句は使用できません。  
  
-   ユーザー定義関数は入れ子にすることができます。つまり、1 つのユーザー定義関数で、別のユーザー定義関数を呼び出すことができます。 呼び出された関数が実行を開始すると入れ子レベルが 1 つ上がり、呼び出された関数が実行を終了するとレベルが 1 つ下がります。 ユーザー定義関数は、32 レベルまで入れ子にすることができます。 入れ子レベルが最大値を超えると、関数チェーン全体の呼び出しが失敗します。 Transact-SQL ユーザー定義関数からマネージド コードへの参照は、32 レベルの入れ子制限のうちの 1 レベルとカウントします。 マネージド コード内から呼び出されたメソッドは、この制限としてはカウントされません。  
  
-   以下の Service Broker ステートメントは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数の定義に**含めることができません**。  
  
    -   `BEGIN DIALOG CONVERSATION`  
  
    -   `END CONVERSATION`  
  
    -   `GET CONVERSATION GROUP`  
  
    -   `MOVE CONVERSATION`  
  
    -   `RECEIVE`  
  
    -   `SEND`  
  
###  <a name="Security"></a> Permissions 

データベースの `CREATE FUNCTION` 権限と、関数を作成するスキーマの `ALTER` 権限が必要です。 関数でユーザー定義型が指定されている場合は、その型に対する `EXECUTE` 権限が必要です。  
  
##  <a name="Scalar"></a> スカラー関数  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに複数ステートメントの**スカラー関数 (スカラー UDF)** を作成します。 この関数は、1 つの入力値 `ProductID`を受け取り、単一のデータ値 (在庫品目中の指定された製品に関する集計量) を返します。  
  
```sql  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END; 
```  
  
 次に、 `ufnGetInventoryStock` 関数を使用して、 `ProductModelID` が 75 ～ 80 の製品の現在の在庫量を返す例を示します。  
  
```sql  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
```  

> [!NOTE]  
> スカラー関数の詳細および例については、「[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)」を参照してください。 

##  <a name="TVF"></a> テーブル値関数  
次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに**インライン テーブル値関数 (TVF)** を作成します。 この関数は、入力パラメーターとして 1 つの顧客 (商店) ID を受け取り、 `ProductID`列と `Name`列、および過去 1 年間の集計である `YTD Total` を商店に販売した製品ごとに返します。  
  
```sql  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
```  
  
次の例では、この関数を呼び出して顧客 ID 602 を指定します。  
  
```sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに**複数ステートメント テーブル値関数 (MSTVF)** を作成します。 この関数は、単一の入力パラメーター `EmployeeID` を受け取り、指定された従業員の直接または間接の部下であるすべての従業員の一覧を返します。 関数が呼び出され、従業員 ID 109 を指定します。  
  
```sql  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
```  
  
次の例では、この関数を呼び出して顧客 ID 1 を指定します。  
  
```sql  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
```  

> [!NOTE]  
> インライン テーブル値関数 (インライン TVF) および複数ステートメント テーブル値関数 (MSTVF) の詳細および例については、「[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)」を参照してください。 

## <a name="best-practices"></a>ベスト プラクティス  
ユーザー定義関数 (UDF) の作成時に `SCHEMABINDING` 句を使用しないと、基になるオブジェクトに加えられた変更が関数の定義に影響して、関数が呼び出されたときに予期しない結果が生じる可能性があります。 基になるオブジェクトに対する変更によって関数が古くならないように、次のいずれかの操作を行うことをお勧めします。  
  
-   UDF を作成するときには、`WITH SCHEMABINDING` 句を指定します。 これにより、関数定義で参照されているオブジェクトは、一緒に関数も変更しない限り変更できなくなります。  
  
-   UDF の定義で指定されているオブジェクトを変更した後に [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) ストアド プロシージャを実行します。  

データにアクセスしない UDF を作成する場合は、`SCHEMABINDING` オプションを指定します。 これにより、これらの UDF を必要とするクエリ プランにおいてクエリ オプティマイザーが不要なスプール演算子を作成するのを防止できます。 スプールの詳細については、「[プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)」を参照してください。 スキーマ バインド関数の作成の詳細については、「[スキーマ バインド関数](../../relational-databases/user-defined-functions/user-defined-functions.md#SchemaBound)」を参照してください。

`FROM` 句内で MSTVF に結合することは可能ですが、その結果パフォーマンスが低下する可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、MSTVF に含まれることがある一部のステートメントに対して、すべての最適化技法を使用できるわけではありません。そのため、最適化されていないクエリ プランになる場合があります。 パフォーマンスをできるだけ高くするには、可能な限り、関数間ではなくベース テーブル間の結合を使用してください。  

> [!IMPORTANT]
> MSTVF の固定のカーディナリティの推定は、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降のバージョンでは 100、それより前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンでは 1 となります。    
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降、MSTVF を使用する実行プランの最適化ではインターリーブ実行を活用できます。それを活用すると、上記のヒューリスティックではなく実際のカーディナリティが使用されます。     
> 詳細については、「[複数ステートメントのテーブル値関数のインターリーブ実行](../../relational-databases/performance/intelligent-query-processing.md#interleaved-execution-for-mstvfs)」を参照してください。

> [!NOTE]  
> ストアド プロシージャまたはユーザー定義関数でパラメーターを渡すとき、あるいはバッチ ステートメントで変数を宣言して設定するときには、ANSI_WARNINGS が無視されます。 たとえば、変数を **char(3)** と定義し、これに 4 文字以上の値を設定すると、データが定義されたサイズに合わせて切り捨てられてから、`INSERT` または `UPDATE` ステートメントが成功します。

## <a name="see-also"></a>参照  
 [ユーザー定義関数](../../relational-databases/user-defined-functions/user-defined-functions.md)     
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)    
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../tools/sql-server-profiler/start-sql-server-profiler.md)    
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../tools/sql-server-profiler/start-sql-server-profiler.md)     
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)    
 [コミュニティ](https://www.bing.com/search?q=user%20defined%20function%20%22sql%20server%202016%22%20examples&qs=n&form=QBRE&pq=user%20defined%20function%20%22sql%20server%202016%22%20examples&sc=0-48&sp=-1&sk=&cvid=C3AD337125A840AD9EEFA3AAC36A3712)のその他の例   
  
