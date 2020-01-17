---
title: sqlsrv_get_field |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_field
apitype: NA
helpviewer_keywords:
- sqlsrv_get_field
- API Reference, sqlsrv_get_field
- retrieving data, as a single field
ms.assetid: fa17cc56-fb38-433b-a40d-65642f04dc23
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64ddca64f049ba95426dec542d68dc8a84e7d9dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015009"
---
# <a name="sqlsrvgetfield"></a>sqlsrv_get_field
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

現在の行の指定したフィールドからデータを取得します。 フィールドのデータには、順にアクセスする必要があります。 たとえば、2 つ目のフィールドのデータにアクセスした後に、1 つ目のフィールドのデータにアクセスすることはできません。  
  
## <a name="syntax"></a>構文  
  
```  
sqlsrv_get_field( resource $stmt, int $fieldIndex [, int $getAsType])  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: 実行されたステートメントに対応するステートメント リソースです。  
  
*$fieldIndex*: 取得するフィールドのインデックス。 インデックスは 0 から始まります。  
  
*$getAsType* [省略可能]: 返されるデータの PHP データ型を決定する **SQLSRV** 定数 (**SQLSRV_PHPTYPE_&#x2a;** )。 サポートされるデータ型については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。 戻り値の型が指定されていない場合、既定の PHP 型が返されます。 既定の PHP 型の詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。 PHP データ型の指定については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
## <a name="return-value"></a>戻り値  
フィールドのデータ。 *$getAsType* パラメーターを指定して、返されるデータの PHP データ型を指定できます。 戻り値のデータ型が指定されていない場合、既定の PHP データ型が返されます。 既定の PHP 型の詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。 PHP データ型の指定については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
**sqlsrv_fetch** と **sqlsrv_get_field** の組み合わせでは、データに対する順方向専用のアクセスが提供されます。  
  
**sqlsrv_fetch**/**sqlsrv_get_field** の組み合わせでは、結果セット行の 1 フィールドのみがスクリプト メモリに読み込まれ、PHP の戻り値の型を指定できます (PHP の戻り値の型の指定方法については、「[方法: PHP データ型を指定する](../../connect/php/how-to-specify-php-data-types.md)」を参照してください)。また、この関数の組み合わせで、データをストリームとして取得することもできます (ストリームとしてのデータの取得については、「[SQLSRV ドライバーを使用してデータをストリームとして取得する](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)」を参照してください)。  
  
## <a name="example"></a>例  
次の例では、製品のレビューとレビュアー名を含むデータの行を取得します。 結果セットからデータを取得するには、 **sqlsrv_get_field** を使用します。 この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of the SQL Server nvarchar type. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[データの取得](../../connect/php/retrieving-data.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
