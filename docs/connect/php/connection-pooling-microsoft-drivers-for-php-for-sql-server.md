---
title: 接続のプール (Microsoft SQL Server 用 Drivers for PHP) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13e1075cd25fa352543837afa31ff2a3d540704f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015120"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>接続のプール (Microsoft SQL Server 用 Drivers for PHP)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]の接続のプールについて重要な点は、次のとおりです。  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] では ODBC 接続プールが使用されます。  
  
-   Windows の既定では、接続プールは有効になっています。 Linux と macOS では、接続プールが ODBC に対して有効になっている場合にのみ、接続がプールされます ([接続プールの有効化/無効化](#enablingdisabling-connection-pooling)に関する参照を参照してください)。 接続プールが有効になっていて、サーバーに接続している場合、ドライバーは新しい接続を作成する前に、プールされた接続を使用しようとします。 プールに同等の接続がない場合、新しい接続が構築され、プールに追加されます。 ドライバーは、接続文字列の比較に基づき、接続が同等かどうかを判断します。  
  
-   プールの接続が使用されると、接続状態がリセットされます。  
  
-   接続を閉じると、接続がプールに返されます。  
  
接続のプールについて詳しくは、「[ドライバー マネージャーの接続プール](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)」をご覧ください。  
  
## <a name="enablingdisabling-connection-pooling"></a>接続プールの有効化/無効化
### <a name="windows"></a>Windows
(接続プールで同等の接続を探す代わりに) 新しい接続を構築するようにドライバーに強制できます。その場合、接続文字列の *ConnectionPooling* 属性を **false** (または 0) に設定します。  
  
接続文字列から *ConnectionPooling* 属性を省略する場合、あるいは **true** (または 1) に設定する場合、同等の接続が接続プールに存在しないときにのみ、ドライバーは新しい接続を構築します。  
  
その他の接続属性の詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  
### <a name="linux-and-macos"></a>Linux と macOS
*Connectionpooling*属性を使用して、接続プールを有効/無効にすることはできません。 

接続プールは、odbcinst .ini 構成ファイルを編集することで有効または無効にすることができます。 変更を有効にするには、ドライバーを再読み込みする必要があります。

を`Pooling`に`Yes`設定し、 `CPTimeout` odbcinst .ini ファイルで正の値を指定すると、接続プールが有効になります。 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
少なくと、odbcinst .ini ファイルは次の例のようになります。

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

Odbcinst `No` .ini ファイルのをに設定`Pooling`すると、ドライバーによって新しい接続が強制的に作成されます。
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Remarks
- Linux または macOS では、odbcinst .ini ファイルでプーリングが有効になっている場合、すべての接続がプールされます。 これは、ConnectionPooling 接続オプションが無効であることを意味します。 プーリングを無効にするには、odbcinst .ini ファイルに Pooling = No を設定し、ドライバーを再読み込みします。
  - unixODBC < = 2.3.4 (Linux および macOS) が、エラーメッセージ、警告、および情報メッセージなどの適切な診断情報を返さない場合がある
  - このため、SQLSRV および PDO_SQLSRV ドライバーは、長いデータ (xml、バイナリなど) を文字列として適切にフェッチできない可能性があります。 回避策として、長いデータをストリームとしてフェッチできます。 SQLSRV については、次の例を参照してください。

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>参照  
[方法: Windows 認証を使用して接続する](../../connect/php/how-to-connect-using-windows-authentication.md)

[方法: SQL Server 認証を使用して接続する](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
