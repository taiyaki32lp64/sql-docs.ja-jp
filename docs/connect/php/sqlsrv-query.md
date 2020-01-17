---
title: sqlsrv_query | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ce7a12b3964e3e0c2407521978df03af9d88f63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014973"
---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ステートメントを準備して実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>パラメーター  
*$conn*: 準備済みステートメントに関連付けられた接続リソースです。  
  
*$tsql*: 準備済みステートメントに対応する Transact-SQL 式です。  
  
*$params* (省略可能): パラメーター化されたクエリのパラメーターに対応する値の**配列**です。 配列の各要素には、次のいずれかを指定できます。
  
-   リテラル値。  
  
-   PHP 変数。  
  
-   次の構造を持つ **配列** 。  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    次の表で配列の各要素を説明します。  
  
    |要素|[説明]|  
    |-----------|---------------|  
    |*$value*|リテラル値、PHP 変数、または PHP by-reference 変数。|  
    |*$direction*[オプション]|パラメーターの方向を示すために使用する **SQLSRV_PARAM_\*** 定数 (**SQLSRV_PARAM_IN**、**SQLSRV_PARAM_OUT**、**SQLSRV_PARAM_INOUT**) のいずれか。 既定値は **SQLSRV_PARAM_IN** です。<br /><br />PHP 定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。|  
    |*$phpType*[オプション]|戻り値の PHP データ型を指定する **SQLSRV_PHPTYPE_\*** 定数。<br /><br />PHP 定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。|  
    |*$sqlType*[オプション]|入力値の SQL Server データ型を指定する **SQLSRV_SQLTYPE_\*** 定数。<br /><br />PHP 定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。|  
  
*$options* (省略可能): クエリのプロパティを設定する連想配列。 それは、[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md#properties) でサポートされるキーの一覧と同じです。
  
## <a name="return-value"></a>戻り値  
ステートメント リソースです。 ステートメントを作成または実行できない場合、**false** が返されます。  
  
## <a name="remarks"></a>Remarks  
**sqlsrv_query** 関数は 1 回限りのクエリに最適であり、特殊な状況を除き、クエリを実行するための既定の選択となります。 この関数は、最小限のコードでクエリを実行するための簡素化されたメソッドを提供します。 **sqlsrv_query** 関数はステートメントの準備と実行の両方を行い、パラメーター化されたクエリの実行に使用できます。  
  
詳細については、「 [方法: SQLSRV ドライバーを使用して出力パラメーターを取得する](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)」を参照してください。  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *Sales.SalesOrderDetail* テーブルに 1 つの行を挿入します。 この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
> [!NOTE]  
> 次の例では、1 回限りのステートメントの実行に **sqlsrv_query** を使用する方法を示すために INSERT ステートメントを使用していますが、概念は任意の Transact-SQL ステートメントに当てはまります。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt) {  
    echo "Row successfully inserted.\n";  
} else {  
    echo "Row insertion failed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *Sales.SalesOrderDetail* テーブルのフィールドを更新します。 この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = (?)   
         WHERE SalesOrderDetailID = (?)";  
  
/* Assign literal parameter values. */  
$params = array(5, 10);  
  
/* Execute the query. */  
if (sqlsrv_query($conn, $tsql, $params)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Error in statement execution.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> 値を [10 進数列または数値列](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)にバインドするときは、有効桁数と精度を保持するために、入力として文字列を使用することをお勧めします。これは、PHP には[浮動小数点数](https://php.net/manual/en/language.types.float.php)の有効桁数に制限があるためです。 値が[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)の範囲外にある場合は特に、同じことが bigint 列にも適用されます。

## <a name="example"></a>例  
このコード サンプルでは、入力パラメーターとして 10 進数値をバインドする方法を示しています。  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="example"></a>例
このコード例では、[sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) 型のテーブルを作成し、挿入されたデータをフェッチする方法を示しています。

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$options = array("Database"=>$dbName, "UID"=>$uid, "PWD"=>$pwd);
$conn = sqlsrv_connect($server, $options);
if($conn === false) {
    die(print_r(sqlsrv_errors(), true));
}

$tableName = 'testTable';
$query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $query);

if(sqlsrv_fetch($stmt) === false) {
    die(print_r(sqlsrv_errors(), true));
}

$col1 = sqlsrv_get_field($stmt, 0);
echo "First field:  $col1 \n";

$col2 = sqlsrv_get_field($stmt, 1);
echo "Second field:  $col2 \n";

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```

予想される出力は次のようになります。

```
First field:  1
Second field:  test_data
```

## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[方法: パラメーター化クエリを実行する](../../connect/php/how-to-perform-parameterized-queries.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  

[方法: ストリームとしてデータを送信する](../../connect/php/how-to-send-data-as-a-stream.md)  

[方向パラメーターを使用する](../../connect/php/using-directional-parameters.md)  

  
