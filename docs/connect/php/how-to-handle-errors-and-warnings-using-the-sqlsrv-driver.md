---
title: '方法: SQLSRV ドライバーを使用してエラーと警告を処理する | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18e50d7344fb5d3d16c4fc0978137e169ba487ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936492"
---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用してエラーと警告を処理する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

既定で、SQLSRV ドライバーは警告をエラーとして扱います。エラーまたは警告を生成する **sqlsrv** 関数の呼び出しは **false**を返します。 このトピックでは、この既定の動作を無効にする方法と、エラーとは別に警告を処理する方法について説明します。  
  
> [!NOTE]  
> 警告をエラーとして扱う既定の動作にはいくつかの例外があります。 SQLSTATE 値 01000、01001、01003、および 01S02 に対応する警告はエラーとして扱われません。  
  
## <a name="example"></a>例  
以下のコード例では、**DisplayErrors** と **DisplayWarnings** という 2 つのユーザー定義関数を使用して、エラーと警告を処理しています。 この例は、次の手順で警告とエラーを別に処理する方法を示しています。  
  
1.  警告をエラーとして扱う既定の動作を無効にします。  
  
2.  従業員の休暇時間を更新し、出力パラメーターとして残りの休暇時間を返すストアド プロシージャを作成します。 従業員の使用可能な休暇時間が 0 未満の場合、ストアド プロシージャは警告を出力します。  
  
3.  一部の従業員について、従業員ごとにストアド プロシージャを呼び出して休暇時間を更新し、警告とエラーが発生した場合は、それに対応するメッセージを表示します。  
  
4.  各従業員の残りの休暇時間を表示します。  
  
最初の **sqlsrv** 関数の呼び出し ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md)) では、警告はエラーとして扱われています。 警告はエラー コレクションに追加されるので、エラーとは別に警告を確認する必要はありません。 ただし、2 回目以降の **sqlsrv** 関数の呼び出しでは、警告はエラーとして扱われなくなるので、警告とエラーを明示的に確認する必要があります。  
  
また、このコード例では、 **sqlsrv** 関数の各呼び出しの後に、エラーを確認しています。 これは推奨される方法です。  
  
この例では、SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースはローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。 AdventureWorks データベースの新規インストールに対してこの例を実行すると、3 つの警告と 2 つのエラーが生成されます。 最初の 2 つの警告は標準の警告であり、データベースへの接続時に発行されます。 3 つ目の警告は、従業員の使用可能な休暇時間が 0 未満の値に更新された場合に発生します。 エラーは、従業員の使用可能な球形時間が -40 時間未満の値に更新された場合に発生します。-40 は、テーブルの制限に違反している値です。  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to substract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>参照  
[方法: SQLSRV ドライバーを使用してエラーおよび警告処理を構成する](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
  
