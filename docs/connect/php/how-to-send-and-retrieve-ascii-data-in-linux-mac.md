---
title: '方法: Linux および macOS で ASCII データを送信および取得する (SQL) |Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 9edd73f5ef01d1d3f22db78400cc3c204efe1379
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251901"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>方法: Linux および macOS での ASCII データの送信と取得 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

この記事では、Linux または macOS システムで ASCII (UTF-8 以外の) ロケールが生成またはインストールされていることを前提としています。 

サーバーに対して ASCII 文字セットを送信または取得するには、次のようにします。  

1.  目的のロケールがシステム環境で既定値でない場合は、最初の接続`setlocale(LC_ALL, $locale)`を作成する前にを呼び出すようにしてください。 PHP setlocale () 関数は、現在のスクリプトのロケールのみを変更します。最初の接続を行った後に呼び出された場合は、無視されることがあります。
 
2.  SQLSRV ドライバーを使用する場合は、を`'CharacterSet' => SQLSRV_ENC_CHAR`接続オプションとして指定できますが、この手順は省略可能です。これは既定のエンコーディングであるためです。

3.  PDO_SQLSRV ドライバーを使用する場合、2つの方法があります。 まず、接続を確立するときに`PDO::SQLSRV_ATTR_ENCODING`を`PDO::SQLSRV_ENCODING_SYSTEM`に設定します (接続オプションを設定する例については、「 [PDO:: __ コンストラクト](../../connect/php/pdo-construct.md)」を参照してください)。 または、正常に接続した後、次の行を追加します。`$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
接続リソース (SQLSRV 内) または接続オブジェクト (PDO_SQLSRV) のエンコーディングを指定すると、ドライバーは、他の接続オプション文字列が同じエンコードを使用することを前提としています。 サーバー名およびクエリ文字列も同じ文字セットを使用すると見なします。  
  
SQLSRV ドライバーとは異なり、PDO_SQLSRV ドライバーの既定のエンコーディングは UTF-8 (PDO:: SQLSRV_ENCODING_UTF8) です。 これらの定数の詳細については、「[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)」を参照してください。 
  
## <a name="example"></a>例  
次の例では、接続を作成する前に特定のロケールを指定することによって、SQL Server 用の PHP ドライバーを使用して ASCII データを送受信する方法を示します。 さまざまな Linux プラットフォームのロケールは、macOS の同じロケールとは異なる名前にすることができます。 たとえば、米国 ISO-8859-1 (ラテン 1) ロケールは Linux で`en_US.ISO-8859-1`は、macOS ではという`en_US.ISO8859-1`名前です。
  
この例では[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、がサーバーにインストールされていることを前提としています。 ブラウザーからこの例を実行すると、すべての出力はブラウザーに書き込まれます。  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)  
[Utf-8 データ](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[更新データ&#40;の使用 Microsoft Drivers for PHP for SQL Server&#41; ](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[サンプル アプリケーション &#40;SQLSRV ドライバー&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
