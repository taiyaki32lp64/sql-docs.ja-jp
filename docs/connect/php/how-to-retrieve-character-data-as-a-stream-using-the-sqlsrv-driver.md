---
title: SQLSRV ドライバーを使用したストリームとしての文字データの取得 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a character stream
- streaming data
ms.assetid: 3c0dbca4-abfc-4449-b133-66c819681840
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3b4a0fd48809d53cda18f2ceb4eaf1f435210e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936412"
---
# <a name="how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用したストリームとしての文字データの取得
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ストリームとしてのデータの取得は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の SQLSRV ドライバーでのみ使用でき、PDO_SQLSRV ドライバーでは使用できません。  
  
SQLSRV ドライバーは、サーバーから大量のデータの取得に PHP ストリームを利用します。 このトピックの例では、ストリームとして文字データを取得する方法を示します。  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *Production.ProductReview* テーブルから行を取得します。 返された行の *Comments* フィールドはストリームとして取得され、PHP [fpassthru](https://php.net/manual/function.fpassthru.php) 関数を使用して表示されます。  
  
ストリームとしてのデータの取得は、戻り値の型を文字ストリームとして指定した [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) および [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) を使用して行われます。 戻り値の型は、定数 **SQLSRV_PHPTYPE_STREAM** を使用して指定します。 **sqlsrv** 定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。  
  
この例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースはローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT ReviewerName,   
               CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
               Rating,   
               Comments   
         FROM Production.ProductReview   
         WHERE ProductReviewID = ? ";  
  
/* Set the parameter value. */  
$productReviewID = 1;  
$params = array( $productReviewID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first three fields are retrieved  
as strings and the fourth as a stream with character encoding. */  
if(sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
echo "Date: ".sqlsrv_get_field( $stmt, 1 )."\n";  
echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
echo "Comments: ";  
$comments = sqlsrv_get_field( $stmt, 3,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
fpassthru($comments);  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
最初の 3 つのフィールドには PHP の戻り値の型が指定されていないので、各フィールドの既定の PHP の型で返されます。 既定の PHP データ型の詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。 PHP の戻り値の型の指定方法の詳細については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)

[SQLSRV ドライバーを使用してデータをストリームとして取得する](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
