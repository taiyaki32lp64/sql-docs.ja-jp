---
title: パラメーター | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- user-defined functions [SQL Server], parameters
ms.assetid: c1f9bd93-3271-4098-a23b-7bd7a19ab65b
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9422e6c8b406258210e03262014d04abc1a4d3ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136731"
---
# <a name="parameters"></a>パラメーター
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
パラメーターは、ストアド プロシージャや関数と、それらを呼び出したアプリケーションやツールとの間でデータを交換するために使用されます。 

*  入力パラメーターは、呼び出し側がストアド プロシージャや関数にデータ値を渡すときに使用します。
*  出力パラメーターは、ストアド プロシージャが呼び出し側にデータ値またはカーソル変数を返すときに使用します。 ユーザー定義関数では出力パラメーターを指定できません。
*  ストアド プロシージャはいずれも呼び出し側に整数のリターン コードを返します。 ストアド プロシージャがリターン コードの値を明示的に設定しないと、リターン コードは 0 になります。

次のストアド プロシージャは、入力パラメーター、出力パラメーター、およびリターン コードを使用する例を示しています。
```
-- Create a procedure that takes one input parameter and returns one output parameter and a return code.
CREATE PROCEDURE SampleProcedure @EmployeeIDParm INT,
         @MaxTotal INT OUTPUT
AS
-- Declare and initialize a variable to hold @@ERROR.
DECLARE @ErrorSave INT
SET @ErrorSave = 0

-- Do a SELECT using the input parameter.
SELECT FirstName, LastName, JobTitle
FROM HumanResources.vEmployee
WHERE EmployeeID = @EmployeeIDParm

-- Save any nonzero @@ERROR value.
IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Set a value in the output parameter.
SELECT @MaxTotal = MAX(TotalDue)
FROM Sales.SalesOrderHeader;

IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Returns 0 if neither SELECT statement had an error; otherwise, returns the last error.
RETURN @ErrorSave
GO
```

ストアド プロシージャや関数を実行するときは、入力パラメーターの値に定数を設定することも、変数の値を使用することもできます。 出力パラメーターとリターン コードは、値を変数に代入して返す必要があります。 パラメーターとリターン コードにより、Transact-SQL 変数やアプリケーション変数との間でデータ値を交換できます。

バッチやスクリプトからストアド プロシージャを呼び出す場合、パラメーターとリターン コード値には同じバッチ内で定義された Transact-SQL 変数を使用できます。 次の例は、作成済みのプロシージャを実行するバッチを示しています。 入力パラメーターの値が定数で指定され、出力パラメーターとリターン コードでは Transact-SQL 変数に値が格納されます。
```
-- Declare the variables for the return code and output parameter.
DECLARE @ReturnCode INT
DECLARE @MaxTotalVariable INT

-- Execute the stored procedure and specify which variables
-- are to receive the output parameter and return code values.
EXEC @ReturnCode = SampleProcedure @EmployeeIDParm = 19,
   @MaxTotal = @MaxTotalVariable OUTPUT

-- Show the values returned.
PRINT ' '
PRINT 'Return code = ' + CAST(@ReturnCode AS CHAR(10))
PRINT 'Maximum Quantity = ' + CAST(@MaxTotalVariable AS CHAR(10))
GO
```

アプリケーションはプログラム変数にバインドされたパラメーター マーカーを使用して、アプリケーション変数、パラメーター、およびリターン コード間でデータを交換できます。

## <a name="see-also"></a>参照
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [「パラメーターと実行プランの再利用」セクション](../../relational-databases/query-processing-architecture-guide.md)   
 [変数 (Transact-SQL)](../../t-sql/language-elements/variables-transact-sql.md)
