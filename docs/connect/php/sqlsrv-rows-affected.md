---
title: sqlsrv_rows_affected |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_rows_affected
apitype: NA
helpviewer_keywords:
- sqlsrv_rows_affected
- API Reference, sqlsrv_rows_affected
ms.assetid: 6f43fbfc-fc92-449b-82d0-33fa780e8f09
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93c7ec396d3388a2de6c0d6518fc516de7156f35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014954"
---
# <a name="sqlsrvrowsaffected"></a>sqlsrv_rows_affected
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

直前に実行されたステートメントで変更された行数を返します。 この関数は、SELECT ステートメントによって返される行数を返しません。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_rows_affected( resource $stmt)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: 実行されたステートメントに対応するステートメント リソースです。  
  
## <a name="return-value"></a>戻り値  
直前に実行されたステートメントによって変更された行数を示す整数です。 変更された行がない場合は、ゼロ (0) が返されます。 変更された行数に関する情報が使用できない場合は、マイナス 1 (-1) が返されます。 変更された行数の取得中にエラーが発生した場合は、 **false** が返されます。  
  
## <a name="example"></a>例  
次の例では、UPDATE ステートメントによって変更された行の数が表示されます。 この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
  
/* Set up Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET SpecialOfferID = ?   
         WHERE ProductID = ?";  
  
/* Set parameter values. */  
$params = array(2, 709);  
  
/* Execute the statement. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
  
/* Get the number of rows affected and display appropriate message.*/  
$rows_affected = sqlsrv_rows_affected( $stmt);  
if( $rows_affected === false)  
{  
     echo "Error in calling sqlsrv_rows_affected.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
elseif( $rows_affected == -1)  
{  
      echo "No information available.\n";  
}  
else  
{  
      echo $rows_affected." rows were updated.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  

[データの更新 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  

  
