---
title: '方法: SQLSRV ドライバーを使用してバイナリ データをストリームとして取得する | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a binary stream
- streaming data
ms.assetid: cd8d6382-abe6-48ee-9d10-4e6c52c0cb9a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f77439f2369d7fbf4e27603bcbf8c8a2f8d8399
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993480"
---
# <a name="how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver"></a>方法: SQLSRV ドライバーを使用してバイナリ データをストリームとして取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ストリームとしてのデータの取得は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の SQLSRV ドライバーでのみ使用でき、PDO_SQLSRV ドライバーでは使用できません。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は、サーバーから大量のバイナリ データを取得するために PHP ストリームを利用します。 このトピックでは、バイナリ データをストリームとして取得する方法を説明します。  
  
ストリームを使用して画像などのバイナリ データを取得すると、オブジェクト全体をスクリプト メモリに読み込むのではなく、データのチャンクが取得されるので、大量のスクリプト メモリを使用しなくて済みます。  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *Production.ProductPhoto* テーブルからバイナリ データ (この場合は画像) を取得します。 画像はストリームとして取得されて、ブラウザーに表示されます。  
  
ストリームとしての画像データの取得は、戻り値の型をバイナリ ストリームとして指定した [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) および [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) を使用して行われます。 戻り値の型は、定数 **SQLSRV_PHPTYPE_STREAM** を使用して指定します。 **sqlsrv** 定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 ブラウザーからこの例を実行すると、すべての出力はブラウザーに書き込まれます。  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto   
         WHERE ProductPhotoID = ?";  
  
/* Set the parameter values and put them in an array. */  
$productPhotoID = 70;  
$params = array( $productPhotoID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data.  
The return data is retrieved as a binary stream. */  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0,   
                      SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY));  
   header("Content-Type: image/jpg");  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
この例の戻り値の型の指定では、バイナリ ストリームとして PHP の戻り値の型を指定する方法が示されています。 *LargePhoto* フィールドは SQL Server の varbinary(max) 型であり、既定でバイナリ ストリームとして返されるので、技術的にはこの例で指定する必要はありません。 既定の PHP データ型の詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。 PHP の戻り値の型の指定方法の詳細については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)

[SQLSRV ドライバーを使用してデータをストリームとして取得する](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
