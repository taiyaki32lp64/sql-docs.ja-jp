---
title: ストアド プロシージャからデータを返す | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b11f924ce5692378896f1fd7d50186861abf223
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63140445"
---
# <a name="return-data-from-a-stored-procedure"></a>ストアド プロシージャからデータを返す
  結果セットやプロシージャからのデータを呼び出し元のプログラムに返す手段には、出力パラメーターとリターン コードの 2 つがあります。 このトピックでは、両方のアプローチについて説明します。  
  
## <a name="returning-data-using-an-output-parameter"></a>出力パラメーターを使用してデータを返す処理  
 プロシージャの定義でパラメーターに OUTPUT キーワードを指定すると、プロシージャの終了時に、そのパラメーターの現在値を呼び出し元のプログラムに返すことができます。 呼び出し元のプログラムで使用できる変数にパラメーターの値を保存するには、呼び出し元のプログラムがプロシージャを実行する際に OUTPUT キーワードを使用する必要があります。 出力パラメーターとして使用できるデータ型の詳細については、「[CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)」を参照してください。  
  
### <a name="examples-of-output-parameter"></a>出力パラメーターの例  
 次の例では、入力パラメーターと出力パラメーターを使用するプロシージャを示します。 `@SalesPerson` パラメーターは、呼び出し元のプログラムによって指定された入力値を受け取ります。 SELECT ステートメントは、入力パラメーターに渡された値を使用して、適切な `SalesYTD` 値を取得します。 また、SELECT ステートメントは、その値を `@SalesYTD` 出力パラメーターに代入します。これにより、プロシージャの終了時にその値が呼び出し元のプログラムに返されます。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 次の例では、最初の例で作成したプロシージャを呼び出し、そのプロシージャから返された出力値を `@SalesYTD` 変数に保存します。これは、呼び出し元のプログラムに対してローカルです。  
  
```  
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 プロシージャを実行する際に、OUTPUT パラメーターに対する入力値を指定することもできます。 これにより、プロシージャは、呼び出し元のプログラムから値を受け取って、その値を変更するかその値を使用して操作を実行してから、新しい値を呼び出し元のプログラムに返すことができます。 前の例では、プログラムによって `@SalesYTDBySalesPerson` プロシージャが呼び出される前に、 `Sales.uspGetEmployeeSalesYTD` 変数に値を代入できます。 実行ステートメントは、 `@SalesYTDBySalesPerson` 変数の値を `@SalesYTD` OUTPUT パラメーターに渡します。 その後、プロシージャの本体で、新しい値を生成する計算にその値を使用できます。 新しい値は OUTPUT パラメーターを通じてプロシージャから戻され、プロシージャの終了時に `@SalesYTDBySalesPerson` 変数の値が更新されます。 これは通常、パラメーターの "参照渡し機能" と呼ばれます。  
  
 プロシージャを呼び出す際にパラメーターに OUTPUT を指定した場合は、そのパラメーターがプロシージャの定義で OUTPUT を使用して定義されていないと、エラー メッセージが表示されます。 ただし、プロシージャに出力パラメーターを定義しておき、OUTPUT を指定せずにこのプロシージャを実行することも可能です。 エラーは返されませんが、呼び出し側のプログラムで出力値を使用することはできません。  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>OUTPUT パラメーターでの cursor データ型の使用  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] プロシージャが使用できる、`cursor`のみ出力パラメーターのデータ型します。 場合、`cursor`プロシージャの定義でそのパラメーターに対して VARYING と出力の両方のキーワードを指定する必要があります、パラメーターのデータ型が指定されています。 パラメーターは OUTPUT としてしか指定できますが、パラメーターの宣言で VARYING キーワードが指定されている場合、データ型がある必要があります`cursor`と OUTPUT キーワードも指定する必要があります。  
  
> [!NOTE]  
>  `cursor` データ型は OLE DB、ODBC、ADO、DB-Library などのデータベース API からアプリケーション変数にバインドすることができません。 アプリケーションでプロシージャを実行するには OUTPUT パラメーターがバインドされている必要があるので、`cursor` 型の OUTPUT パラメーターを指定したプロシージャはデータベース API から呼び出すことができません。 そのようなプロシージャは、`cursor` 型の OUTPUT 変数を [!INCLUDE[tsql](../../../includes/tsql-md.md)] の `cursor` 型のローカル変数に代入したときのみ、[!INCLUDE[tsql](../../../includes/tsql-md.md)] バッチ、プロシージャ、またはトリガーから呼び出すことができます。  
  
### <a name="rules-for-cursor-output-parameters"></a>cursor 出力パラメーターに関する規則  
 プロシージャの実行時には、次の規則が `cursor` 出力パラメーターに適用されます。  
  
-   順方向専用カーソルの場合、カーソルの結果セットとして返される行は、プロシージャの実行が終了したときにカーソルがあった位置以降の行に限られます。たとえば、次のようになります。  
  
    -   RS という名前の 100 行から構成される結果セットに対するプロシージャ内で、スクロールできないカーソルが開かれます。  
  
    -   プロシージャにより結果セット RS の最初の 5 行がフェッチされます。  
  
    -   プロシージャが呼び出し元に戻ります。  
  
    -   呼び出し元に返される結果セット RS は RS の 6 行目から 100 行目までで構成され、呼び出し元のカーソルは RS の 1 行目の前に置かれます。  
  
-   順方向専用カーソルの場合、プロシージャが終了した時点でカーソルが 1 行目の前にあれば、呼び出し元のバッチ、プロシージャ、またはトリガーには結果セット全体が返されます。 結果セットが返されるとき、カーソル位置は 1 行目の前に設定されます。  
  
-   順方向専用カーソルの場合、プロシージャが終了した時点でカーソルが最後の行の後にあれば、呼び出し元のバッチ、プロシージャ、またはトリガーには空の結果セットが返されます。  
  
    > [!NOTE]  
    >  空の結果セットは、NULL 値と同じではありません。  
  
-   スクロール可能なカーソルの場合、プロシージャが終了した時点で、呼び出し元のバッチ、プロシージャ、またはトリガーに結果セット内のすべての行が返されます。 結果セットが返されるとき、カーソル位置はプロシージャで最後にフェッチを行った位置のままです。  
  
-   カーソルがクローズしている場合は、カーソルの種類にかかわらず、呼び出し元のバッチ、プロシージャ、またはトリガーには null 値が返されます。 カーソルがパラメーターに割り当てられていて、そのカーソルが一度も開かれない場合も、同じ結果になります。  
  
    > [!NOTE]  
    >  カーソルがクローズしているかどうかが問題になるのは、結果セットが返される時点のみです。 たとえば、プロシージャの途中でカーソルを閉じ、その後で再び開いて、そのカーソルの結果セットを呼び出し元のバッチ、プロシージャ、またはトリガーに返すのは有効な操作です。  
  
### <a name="examples-of-cursor-output-parameters"></a>cursor 出力パラメーターの例  
 次の例では、プロシージャが作成、出力パラメーターが指定されている`@currency`_`cursor`を使用して、`cursor`データ型。 作成したプロシージャはバッチで呼び出します。  
  
 まず、Currency テーブルに対してカーソルを宣言し、そのカーソルを開くプロシージャを作成します。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 次に、cursor 型のローカル変数を宣言し、そのローカル変数にカーソルを代入するプロシージャを実行し、代入したカーソルから行をフェッチするというバッチを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>リターン コードを使用してデータを返す処理  
 プロシージャは、リターン コードという整数値を返してプロシージャの実行状態を表すことができます。 プロシージャのリターン コードを指定するには、RETURN ステートメントを使用します。 OUTPUT パラメーターと同様に、呼び出し元のプログラムでリターン コード値を使用するには、プロシージャの実行時にリターン コードを変数に保存する必要があります。 代入変数など、`@result`データ型の`int`プロシージャからリターン コードを格納するために使用`my_proc`など。  
  
```  
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 リターン コードは、可能性のあるエラー状態ごとにリターン コードの値を設定するために、プロシージャのフロー制御ブロックの中でよく使用されます。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントの後で @@ERROR 関数を使用すると、ステートメントの実行中にエラーが発生したかどうかを検出できます。  
  
### <a name="examples-of-return-codes"></a>リターン コードの例  
 次の例では、さまざまなエラーに特別なリターン コード値を設定するエラー処理を含む `usp_GetSalesYTD` プロシージャを示します。 次の表では、可能性のある各エラーに対してプロシージャによって割り当てられる整数値と、各値に相当する意味を示します。  
  
|リターン コードの値|説明|  
|-----------------------|-------------|  
|0|実行に成功しました。|  
|1|必要なパラメーター値が指定されていません。|  
|2|指定されたパラメーター値が無効です。|  
|3|売上高の値を取得中にエラーが発生しました。|  
|4|販売員の売上高の値に NULL 値が検出されました。|  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 次の例では、 `usp_GetSalesYTD` プロシージャから返されるリターン コードを処理するプログラムを作成します。  
  
```  
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'EERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>関連項目  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [PRINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/print-transact-sql)   
 [SET @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-local-variable-transact-sql)   
 [カーソル](../cursors.md)   
 [RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql)   
 [@@ERROR &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-transact-sql)  
  
  
