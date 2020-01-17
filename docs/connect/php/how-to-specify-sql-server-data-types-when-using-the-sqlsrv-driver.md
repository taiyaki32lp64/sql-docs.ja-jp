---
title: '方法: SQLSRV ドライバーを使用する場合に SQL Server データ型を指定する | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b9ddb359c34e929247357713c5c48035a3eed9a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993356"
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用する場合に SQL Server データ型を指定する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、SQLSRV ドライバーを使用して、サーバーに送信されるデータの SQL Server データ型を指定する方法を説明します。 このトピックは、PDO_SQLSRV ドライバーを使用する場合は適用しません。  
  
SQL Server データ型を指定するには、データを挿入または更新するクエリを準備または実行する際に、省略可能な *$params* 配列を使用する必要があります。 *$params* 配列の構造と構文の詳細については、 [sqlsrv_query](../../connect/php/sqlsrv-query.md) または [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)を参照してください。  
  
次の手順は、データをサーバーに送信する際に、SQL Server データ型を指定する方法をまとめています。  
  
> [!NOTE]  
> SQL Server データ型を指定しない場合、既定の型が使用されます。 既定の SQL Server データ型については、「 [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md)」を参照してください。  
  
1.  データを挿入または更新する Transact-SQL クエリを定義します。 クエリでパラメーター値のプレースホルダーとして疑問符 (?) を使用します。  
  
2.  Transact-SQL クエリ内のプレースホルダーに対応する PHP 変数を初期化または更新します。  
  
3.  クエリを準備または実行するときに使用する *$params* 配列を構築します。 SQL Server データ型を指定するときに、 *$params* 配列の各要素も配列にする必要があります。  
  
4.  目的の SQL Server データ型を指定するには、 *$params* 配列の各サブ配列の 4 番目のパラメーターとして、適切な **SQLSRV_SQLTYPE_&#42;** 定数を使用します。 **SQLSRV_SQLTYPE_&#42;** 定数の完全な一覧については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」の SQLTYPE セクションを参照してください。 たとえば、下のコードで、 *$changeDate*、 *$rate*、および *$payFrequency* は、 **$params**配列に、それぞれ SQL Server 型 **datetime**、 **money** 、および *tinyint* として指定されています。 *$employeeId* には SQL Server 型が指定されておらず、整数に初期化されているため、既定の SQL Server 型の **integer** が使用されます。  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *HumanResources.EmployeePayHistory* テーブルにデータを挿入しています。 *$changeDate*、 *$rate*、および *$payFrequency* パラメーターに SQL Server 型が指定されています。 *$employeeId* パラメーターには既定の SQL Server 型が使用されています。 データが正常に挿入されたことを確認するため、同じデータを取得し、表示しています。  
  
この例では、SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースはローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
  
/* Define the query. */  
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)

[方法: PHP データ型を指定する](../../connect/php/how-to-specify-php-data-types.md)

[データ型の変換](../../connect/php/converting-data-types.md)

[方法: 組み込みの UTF-8 サポートを使用した UTF-8 データの送信と取得](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
