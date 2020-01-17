---
title: '方法: PHP データ型を指定する |Microsoft Docs'
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
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae00c01e962da05015a5132608915fc9d70258f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936395"
---
# <a name="how-to-specify-php-data-types"></a>方法: PHP データ型を指定する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV ドライバーを使用する場合、PDOStatement::bindColumn と PDOStatement::bindParam を使用してサーバーからデータを取得するときに PHP データ型を指定できます。 詳細については、「 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) 」および「 [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) 」を参照してください。  
  
次の手順では、SQLSRV ドライバーを使用してサーバーからデータを取得するときに PHP データ型を指定する方法をまとめています。  
  
1.  [sqlsrv_query](../../connect/php/sqlsrv-query.md) または [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md) の組み合わせで Transact-SQL クエリを設定して実行します。  
  
2.  データの行を [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)を使用した読み取りに使用できるようにします。  
  
3.  省略可能な 3 つ目のパラメーターとして指定した目的の PHP データ型の [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) を使用して、返される行のフィールド データを取得します。 省略可能な 3 つ目のパラメーターが指定されていない場合、既定の PHP 型に従ってデータが返されます。 既定の PHP の戻り値の型については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。  
  
    PHP データ型の指定に使用される定数については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」の PHPTYPE のセクションを参照してください。  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *Production.ProductReview* テーブルから行を取得します。 返される各行で、 *ReviewDate* フィールドは文字列として取得され、 *Comments* フィールドはストリームとして取得されます。 ストリーム データを表示するには、PHP の [fpassthru](https://php.net/manual/en/function.fpassthru.php) 関数を使用します。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
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
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
この例では、2 つ目のフィールド (*ReviewDate*) を文字列として取得すると、SQL Server の DATETIME データ型のミリ秒の精度が保持されます。 既定では、SQL Server の DATETIME データ型は PHP DateTime オブジェクトとして取得され、ミリ秒の精度は失われます。  
  
4 つ目のフィールド (*Comments*) をストリームとして取得するのは、例として示すためです。 既定では、SQL Server データ型 nvarchar(3850) は文字列として取得されるので、ほとんどの場合に使用できます。  
  
> [!NOTE]  
> クエリを実行する前に、 [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) 関数を使用して、型情報などのフィールド情報を取得することもできます。  
  
## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)

[方法: SQLSRV ドライバーを使用して出力パラメーターを取得する](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[方法: SQLSRV ドライバーを使用して入力/出力パラメーターを取得する](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
