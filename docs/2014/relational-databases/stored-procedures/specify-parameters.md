---
title: パラメーターの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f936853c284196b05b6da6369f4410bed2297d4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736365"
---
# <a name="specify-parameters"></a>パラメーターの指定
  プロシージャのパラメーターを指定することで、呼び出し元のプログラムからプロシージャの本体に値を渡すことができます。 これらの値は、プロシージャの実行中にさまざまな目的で使用できます。 プロシージャ パラメーターも、パラメーターが OUTPUT パラメーターとしてマークされている場合は、呼び出し元のプログラムに値を返すことができます。  
  
 プロシージャには最大 2,100 個のパラメーターを指定できます。各パラメーターには、名前、データ型、および方向が割り当てられます。 パラメーターには、必要に応じて既定値を割り当てることもできます。  
  
 次のセクションでは、パラメーターに値を渡す処理と、プロシージャ呼び出しで各パラメーター属性を使用する方法について説明します。  
  
## <a name="passing-values-into-parameters"></a>パラメーターに値を渡す処理  
 プロシージャ呼び出しで指定されるパラメーター値は、定数か変数である必要があります。関数名をパラメーター値として使用することはできません。 変数には、ユーザー定義変数や \@\@spid などのシステム変数を使用できます。  
  
 次の例は、パラメーター値をプロシージャ `uspGetWhereUsedProductID`に渡す方法を示しています。 この例では、定数および変数としてパラメーターを渡す方法のほか、変数を使用して関数の値を渡す方法も示しています。  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>パラメーター名の指定  
 プロシージャを作成してパラメーター名を宣言する際には、パラメーター名の先頭を 1 つの \@ 文字にし、そのプロシージャのスコープ内でパラメーター名が一意になるようにする必要があります。  
  
 パラメーターに明示的に名前を付け、プロシージャ呼び出しで各パラメーターに適切な値を代入することで、パラメーターを任意の順序で指定できます。 たとえば、**my_proc** というプロシージャが **\@first**、 **\@second**、および **\@third** という 3 つのパラメーターを必要とする場合、プロシージャに渡される値は、`EXECUTE my_proc @second = 2, @first = 1, @third = 3;` ようにパラメーター名に代入できます。  
  
> [!NOTE]
>  1 つのパラメーター値を **\@parameter =** _value_ の形式で指定した場合は、後続のパラメーターもすべてこの形式で指定する必要があります。 パラメーター値を **\@parameter =** _value_ の形式で渡さない場合は、CREATE PROCEDURE ステートメント内のパラメーターと同じ順序 (左から右) で値を指定する必要があります。  
> 
> [!WARNING]
>  **\@parameter =** _value_ の形式で渡すパラメーターのスペルが間違っていると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってエラーが生成され、プロシージャは実行されません。  
  
## <a name="specifying-parameter-data-types"></a>パラメーターのデータ型の指定  
 パラメーターを CREATE PROCEDURE ステートメントで宣言する場合は、パラメーターのデータ型を定義する必要があります。 パラメーターのデータ型により、プロシージャの呼び出し時にパラメーターとして指定できる値の型と範囲が決まります。 たとえば、`tinyint` データ型のパラメーターを定義した場合は、そのパラメーターに渡す値として 0 ～ 255 の範囲の数値だけを指定できます。 指定したデータ型と互換性がない値を使用してプロシージャを実行すると、エラーが返されます。  
  
## <a name="specifying-parameter-default-values"></a>パラメーターの既定値の指定  
 宣言時にパラメーターに既定値が指定されていると、そのパラメーターは省略可能と見なされます。 プロシージャ呼び出しで省略可能なパラメーターに値を指定する必要はありません。  
  
 パラメーターの既定値は次の場合に使用されます。  
  
-   プロシージャ呼び出しでパラメーターの値が指定されていない場合  
  
-   プロシージャ呼び出しで値として DEFAULT キーワードが指定されている場合  
  
> [!NOTE]  
>  既定値が空白または句読点を含む文字列の場合、または数字で始まる場合 (たとえば 6xxx)、単一引用符で囲む必要があります。  
  
 パラメーターに対して既定値として適切に値を指定できない場合は、NULL を既定値として指定してください。 パラメーターの値なしでプロシージャを実行する場合は、プロシージャからカスタマイズされたメッセージが返されるようにすることをお勧めします。  
  
 次の例で、 `usp_GetSalesYTD` という 1 つの入力パラメーターを伴う `@SalesPerson`プロシージャを作成します。 このパラメーターには既定値として NULL が割り当てられています。 `@SalesPerson` パラメーターに値を指定せずにプロシージャを実行した場合にカスタム エラー メッセージを返すエラー処理ステートメントで NULL を使用します。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 次の例では、プロシージャを実行します。 最初のステートメントは、入力値を指定せずにプロシージャを実行します。 その結果、プロシージャのエラー処理ステートメントによってカスタム エラー メッセージが返されます。 2 番目のステートメントでは入力値を渡し、予期した結果セットが返されます。  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.usp_GetSalesYTD N'Blythe';  
GO  
```  
  
 既定値が指定されているパラメーターは省略できますが、パラメーターの一覧を切り捨てることしかできません。 たとえば、プロシージャに 5 つのパラメーターがある場合は、4 番目と 5 番目のパラメーターを両方とも省略できます。 ただし、 **\@parameter =** _value_ の形式でパラメーターを指定しない限り、4 番目のパラメーターを省略して 5 番目のパラメーターを指定することはできません。  
  
## <a name="specifying-parameter-direction"></a>パラメーターの方向の指定  
 パラメーターの方向は、入力または出力です。入力の場合は、値がプロシージャの本体に渡されます。出力の場合は、プロシージャが呼び出し元のプログラムに値を返します。 既定値は入力パラメーターです。  
  
 出力パラメーターを指定するには、CREATE PROCEDURE ステートメントでパラメーターの定義に OUTPUT キーワードを指定する必要があります。 プロシージャは終了時に、呼び出し元のプログラムに現在の出力パラメーターの値を返します。 呼び出し元のプログラムも、そのプログラムで使用できる変数にパラメーターの値を保存するために、プロシージャの実行時に OUTPUT キーワードを使用する必要があります。  
  
 次の例では、指定した価格を超えない製品の一覧を返す `Production.usp`_`GetList` プロシージャを作成します。 ここでは、複数の SELECT ステートメントと複数の OUTPUT パラメーターを使用する例を示しています。 外部プロシージャ、バッチ、または複数の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、OUTPUT パラメーターを使用して、プロシージャの実行中に設定された値にアクセスできます。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 `usp_GetList` を実行し、原価が $700 未満である [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 製品 (自転車) の一覧を返します。 ここではフロー制御言語と共に OUTPUT パラメーターの **\@cost** および **\@compareprices** を使用して、 **[メッセージ]** ウィンドウにメッセージを返します。  
  
> [!NOTE]  
>  プロシージャの作成中にも変数の使用中にも、OUTPUT 変数を定義する必要があります。 パラメーター名と変数名が一致する必要はありません。 ただし、データ型とパラメーターの位置は一致する必要があります ( **\@listprice=** _variable_ が使用されている場合は除きます)。  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 次に結果セットの一部を示します。  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>関連項目  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
