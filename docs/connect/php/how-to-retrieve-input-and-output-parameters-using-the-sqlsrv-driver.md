---
title: '方法: SQLSRV ドライバーを使用して I/O パラメーターを取得する | Microsoft Docs'
ms.custom: ''
ms.date: 04/12/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 9a7c5f60-67f9-4968-a3a8-c256ee481da2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27290272b72b27d3bb051da4e7d9a8df202461c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993459"
---
# <a name="how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用して入力/出力パラメーターを取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、SQLSRV ドライバーを使用して 1 つのパラメーターが入力/出力パラメーターとして定義されているストアド プロシージャを呼び出す方法、およびその結果を取得する方法について説明します。 出力パラメーターまたは入出力パラメーターを取得する場合、返されるパラメーター値にアクセスできるようになる前に、ストアド プロシージャによって返されるすべての結果を使用する必要があります。  
  
> [!NOTE]  
> **null**、 **DateTime**、またはストリーム型に初期化または更新される変数は出力パラメーターとして使用できません。  
  
## <a name="example-1"></a>例 1
次の例では、指定された従業員の使用可能な休暇時間から使用済みの休暇時間数を減算するストアド プロシージャを呼び出します。 使用済みの休暇時間数を表す変数 *$vacationHrs*は、入力パラメーターとしてストアド プロシージャに渡されます。 ストアド プロシージャは、使用可能な休暇時間を更新した後、同じパラメーターを使用して残りの休暇時間数を返します。  
  
> [!NOTE]  
> *$vacationHrs* を 4 に初期化すると、返される PHPTYPE が整数に設定されます。 データ型の整合性を確保するため、ストアド プロシージャを呼び出す前に入力/出力パラメーターを初期化するか、目的の PHPTYPE を指定する必要があります。 PHPTYPE の指定については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
ストアド プロシージャは 2 つの結果を返すため、ストアド プロシージャが実行された後に [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md) を呼び出して出力パラメーターの値を使用できるようにする必要があります。 **sqlsrv_next_result** の呼び出しの後、 *$vacationHrs* にはストアド プロシージャによって返される出力パラメーターの値が含まれます。  
  
> [!NOTE]  
> 正規の構文を使用してストアド プロシージャを呼び出すことをお勧めします。 正規の構文の詳細については、「[ストアド プロシージャの呼び出し](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)」を参照してください。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = "CREATE PROCEDURE SubtractVacationHours  
                        @EmployeeID int,  
                        @VacationHrs smallint OUTPUT  
                  AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHrs  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHrs = (SELECT VacationHours  
                                      FROM HumanResources.Employee  
                                      WHERE EmployeeID = @EmployeeID)";  
  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call SubtractVacationHours( ?, ?)}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an INOUT  
parameter. Initializing $vacationHrs to 8 sets the returned PHPTYPE to  
integer. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
  
$employeeId = 4;  
$vacationHrs = 8;  
$params = array(   
                 array($employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $vacationHrs. */  
sqlsrv_next_result($stmt3);  
echo "Remaining vacation hours: ".$vacationHrs;  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> 入力/出力パラメーターを bigint 型にバインドするときに、値が[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)の範囲外になる可能性がある場合は、SQL フィールド型を SQLSRV_SQLTYPE_BIGINT として指定する必要があります。 それ以外の場合は、"範囲外の値" の例外が発生する可能性があります。

## <a name="example-2"></a>例 2
このコードサンプルでは、大きな bigint 値を入力/出力パラメーターとしてバインドする方法を示します。  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"testDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume the stored procedure spTestProcedure exists, which retrieves a bigint value of some large number
// e.g. 9223372036854
$bigintOut = 0;
$outSql = "{CALL spTestProcedure (?)}";
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_INOUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>参照  
[方法: SQLSRV ドライバーを使用してパラメーターの方向を指定する](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[方法: SQLSRV ドライバーを使用して出力パラメーターを取得する](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[データの取得](../../connect/php/retrieving-data.md)  
  
