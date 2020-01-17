---
title: sqlsrv_connect |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11da2b4eca130eafe93a01315aaa1f6d9919632c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015041"
---
# <a name="sqlsrvconnect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

接続リソースを作成し、接続を開きます。 既定では、Windows 認証を使用して接続は試行されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>パラメーター  
*$serverName*: 接続が確立されるサーバー名を指定する文字列です。 この文字列の一部には、インスタンス名 (たとえば、"myserver \instancename") またはポート番号 (たとえば、"myServer, 1521") を含めることができます。 このパラメーターに使用できるオプションの詳細については、「[SQL Native Client での接続文字列キーワードの使用](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」の「ODBC ドライバー接続文字列キーワード」の Server キーワードの説明を参照してください。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 3.0 以降では、 `"(localdb)\instancename"`で LocalDB インスタンスを指定することもできます。 詳細については、「 [LocalDB のサポート](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)」を参照してください。  
  
また、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 3.0 以降では、AlwaysOn 可用性グループへの接続に仮想ネットワーク名を指定することもできます。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]サポートの詳細については、「[高可用性、ディザスターリカバリーのサポート](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)」を参照してください。  
  
*$connectionInfo* [省略可能]: 接続属性を含む連想 **array** です (たとえば、**array**("Database" => "AdventureWorks"))。 配列でサポートしているキーの一覧については、「 [Connection Options](../../connect/php/connection-options.md) 」を参照してください。  
  
## <a name="return-value"></a>戻り値  
PHP 接続リソースです。 接続を正常に作成して開くことができない場合、 **false** が返されます。  
  
## <a name="remarks"></a>Remarks  
*UID* キーおよび *PWD* キーの値がオプションの *$connectionInfo* パラメーターで指定されていない場合、Windows 認証を使用して接続は試行されます。 サーバーに接続する方法の詳細については、「 [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) 」および「 [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)」を参照してください。  
  
## <a name="example"></a>例  
次の例では、Windows 認証を使用して接続を作成して開きます。 この例では、SQL Server および [AdventureWorks](https://www.codeplex.com/SqlServerSamples) データベースはローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[Connecting to the Server](../../connect/php/connecting-to-the-server.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
