---
title: アイドル状態の接続の回復性
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265170"
---
# <a name="idle-connection-resiliency"></a>アイドル状態の接続の回復性
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[接続の回復性](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)とは、特定の制約内で、切断されたアイドル状態の接続を再確立できることを示します。 Microsoft SQL Server への接続に失敗した場合、接続の回復性によって、クライアントは自動的に接続の再確立を試みることができます。 接続の回復性は、データソースのプロパティです。接続の回復性をサポートするのは、2014以降の SQL Server Azure SQL Database のみです。

接続の回復性は、接続文字列に追加できる2つの接続キーワード**ConnectRetryCount**と**ConnectRetryInterval**によって実装されます。

|Keyword|値|既定|[説明]|
|-|-|-|-|
|**ConnectRetryCount**| 0 から 255 までの整数|1|切断された接続を再確立するための最大試行回数。 既定では、接続が切断されると、接続の再確立が1回試行されます。 値0は再接続が試行されないことを意味します。|
|**ConnectRetryInterval**| 1 から 60 までの整数|1| 接続の再確立を試行するまでの秒単位の時間です。 アプリケーションは、接続が切断されたことを検出した直後に再接続を試み、 **ConnectRetryInterval**秒待機してから再試行します。 **ConnectRetryCount**が0の場合、このキーワードは無視されます。

**ConnectRetryCount**の積が**ConnectRetryInterval**を掛けた**値**よりも大きい場合、 **logintimeout**に達すると、クライアントは接続を停止します。それ以外の場合は、 **ConnectRetryCount**に到達するまで再接続を試行し続けます。

#### <a name="remarks"></a>Remarks

接続がアイドル状態のときは、接続の回復性が適用されます。 たとえば、トランザクションの実行中にエラーが発生した場合、再接続の試行はトリガーされません。それ以外の場合は、失敗します。 次の状況は、回復不可能なセッション状態と呼ばれ、再接続の試行をトリガーしません。

* 一時テーブル
* グローバルカーソルとローカルカーソル
* トランザクションコンテキストとセッションレベルのトランザクションロック
* アプリケーション ロック
* 実行/元に戻すセキュリティコンテキスト
* OLE オートメーションハンドル
* 準備済み XML ハンドル
* トレース フラグ

## <a name="example"></a>例

次のコードは、データベースに接続し、クエリを実行します。 接続は、セッションを強制終了することによって中断され、接続が切断されたときに新しいクエリが試行されます。 この例では、[AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) サンプル データベースを使用します。

この例では、接続を切断する前にバッファーカーソルを指定しています。 バッファーされたカーソルを指定しない場合、接続は再確立されません。これは、アクティブなサーバー側カーソルが存在するため、接続が切断されたときに接続がアイドル状態にならないためです。 ただし、その場合は、sqlsrv_free_stmt () を呼び出して、カーソルを vacate する接続を切断すると、接続が正常に再確立されます。

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
予想される出力:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>参照
[Windows ODBC ドライバーの接続の復元性](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
