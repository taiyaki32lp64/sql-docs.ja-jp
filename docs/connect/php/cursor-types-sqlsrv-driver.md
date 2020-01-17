---
title: カーソルの種類 (SQLSRV ドライバー) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac090ad8831397bf31c0911ab8a8db21486528db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015113"
---
# <a name="cursor-types-sqlsrv-driver"></a>カーソルの種類 (SQLSRV ドライバー)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV ドライバーでは、カーソルの種類に基づき、任意の順番で行にアクセスできる結果セットを作成できます。  このトピックでは、クライアント側 (バッファー) とサーバー側 (バッファーなし) カーソルについて説明します。  
  
## <a name="cursor-types"></a>カーソルの種類  
[Sqlsrv_query](../../connect/php/sqlsrv-query.md)または with [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)を使用して結果セットを作成する場合は、カーソルの種類を指定できます。 既定では、順方向専用カーソルが使用されます。これにより、結果セットの末尾に達するまで、結果セットの最初の行から開始して一度に1行ずつ移動できます。  
  
スクロール可能なカーソルを使用して結果セットを作成すると、結果セット内の任意の行に任意の順序でアクセスできます。 次の表は、sqlsrv_query または sqlsrv_prepare において **Scrollable** オプションに渡すことができる値を示しています。  
  
|オプション|[説明]|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|を使用すると、結果セットの最初の行から開始するまで、一度に1行ずつ移動できます。<br /><br />これは、既定のカーソルの種類です。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)は、このカーソルの種類で作成された結果セットに対してエラーを返します。<br /><br />**forward**は SQLSRV_CURSOR_FORWARD の省略形です。|  
|SQLSRV_CURSOR_STATIC|では、任意の順序で行にアクセスできますが、データベースの変更は反映されません。<br /><br />**static**は、SQLSRV_CURSOR_STATIC の省略形です。|  
|SQLSRV_CURSOR_DYNAMIC|では、任意の順序で行にアクセスでき、データベースの変更が反映されます。<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)は、このカーソルの種類で作成された結果セットに対してエラーを返します。<br /><br />**dynamic**は、SQLSRV_CURSOR_DYNAMIC の省略形です。|  
|SQLSRV_CURSOR_KEYSET|では、任意の順序で行にアクセスできます。 ただし、行がテーブルから削除される場合 (削除された行は、値なしで返されます)、キーセット カーソルは行の数を更新しません。<br /><br />**keyset**は、SQLSRV_CURSOR_KEYSET の省略形です。|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|では、任意の順序で行にアクセスできます。 クライアント側のカーソルクエリを作成します。<br /><br />**バッファー**は SQLSRV_CURSOR_CLIENT_BUFFERED の省略形です。|  
  
クエリで複数の結果セットが生成される場合、**スクロール**可能なオプションはすべての結果セットに適用されます。  
  
## <a name="selecting-rows-in-a-result-set"></a>結果セット内の行の選択  
結果セットを作成したら、 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)、 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)、または[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)を使用して行を指定できます。  
  
次の表では、 *row*パラメーターで指定できる値について説明します。  
  
|パラメーター|[説明]|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|次の行を指定します。 これは、スクロール可能な結果セットの*行*パラメーターを指定しない場合の既定値です。|  
|SQLSRV_SCROLL_PRIOR|現在の行の前に行を指定します。|  
|SQLSRV_SCROLL_FIRST|結果セットの最初の行を指定します。|  
|SQLSRV_SCROLL_LAST|結果セットの最後の行を指定します。|  
|SQLSRV_SCROLL_ABSOLUTE|*Offset*パラメーターで指定された行を指定します。|  
|SQLSRV_SCROLL_RELATIVE|現在の行から*オフセット*パラメーターを使用して指定された行を指定します。|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>サーバー側カーソルと SQLSRV ドライバー  
次の例は、さまざまなカーソルの効果を示しています。 例の33行目では、異なるカーソルを指定する3つのクエリステートメントのうち、最初のステートメントが表示されます。  2つのクエリステートメントがコメント化されます。 プログラムを実行するたびに、別の種類のカーソルを使用して、47行目のデータベースの更新の効果を確認します。  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>クライアント側カーソルと SQLSRV ドライバー  
クライアント側カーソルは、のバージョン3.0 で追加された[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]機能で、結果セット全体をメモリにキャッシュすることができます。 クライアント側カーソルを使用すると、クエリが実行された後に、行数を使用できます。  
  
クライアント側のカーソルは、小規模から中規模の結果セットに対して使用する必要があります。 大きな結果セットには、サーバー側のカーソルを使用します。  
  
クエリは、バッファーが結果セット全体を格納するのに十分な大きさでない場合、false を返します。 バッファーのサイズは PHP メモリの上限まで増やすことができます。  
  
SQLSRV ドライバーを使用すると、 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)の ClientBufferMaxKBSize 設定を使用して、結果セットを保持するバッファーのサイズを構成できます。 [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)は、ClientBufferMaxKBSize の値を返します。 Php.ini ファイルの最大バッファーサイズを sqlsrv で設定することもできます。ClientBufferMaxKBSize (例、sqlsrv)。ClientBufferMaxKBSize = 1024)。  
  
次の例は、を示しています。  
  
-   クライアント側カーソルでは、常に行数が使用できます。  
  
-   クライアント側のカーソルとバッチステートメントの使用。  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
次のサンプルは、 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)を使用したクライアント側のカーソルと、別のクライアントバッファーサイズを示しています。
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>参照  
[カーソルの種類を指定し、行を選択する](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
