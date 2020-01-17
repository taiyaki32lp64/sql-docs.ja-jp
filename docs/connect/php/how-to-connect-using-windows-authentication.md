---
title: '方法: Windows 認証を使用して接続する |Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84707c67491d4f02be41e6506fb233ee7afef9fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936506"
---
# <a name="how-to-connect-using-windows-authentication"></a>方法: Windows 認証を使用して接続する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の既定では、Windows 認証を使用して SQL Server に接続します。 つまり、サーバーに接続するときに、ほとんどのシナリオでエンドユーザーの ID ではなく、Web サーバーのプロセス ID またはスレッド ID (Web サーバーが権限の借用を使用している場合) が使用されるという点が重要です。  
  
Windows 認証を使用して SQL Server に接続する場合は、次の点を考慮する必要があります。  
  
-   接続を確立するには、Web サーバーのプロセス (またはスレッド) を実行する資格情報と、有効な SQL Server ログインが対応付けられている必要があります。  
  
-   SQL Server と Web サーバーが別のコンピューター上にある場合、リモート接続を有効にするように SQL Server を構成する必要があります。  
  
> [!NOTE]  
> 接続を確立するときに、 *Database* や *ConnectionPooling* などの接続属性を設定できます。 サポートされている接続属性の一覧については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  
  
次の理由のために可能な場合は、SQL Server への接続に Windows 認証を使用する必要があります。  
  
-   認証時にネットワーク経由で資格情報が渡されることはありません。ユーザー名とパスワードはデータベース接続文字列に埋め込まれません。 これは、悪意のあるユーザーや攻撃者が、ネットワークを監視したり、構成ファイル内の接続文字列を表示したりして、資格情報を取得できないことを意味します。  
  
-   ユーザーは、アカウントを一元管理されます。また、パスワードの有効期限、パスワードの最小の長さ、および複数の無効なログイン要求後のアカウント ロックアウトなど、セキュリティ ポリシーが強制されます。  
  
Windows 認証を使用できない場合、「 [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)」を参照してください。  
  
## <a name="example"></a>例  
次の例では、Windows 認証で [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]の SQLSRV ドライバーを使用して、SQL Server のローカル インスタンスに接続します。 接続が確立すると、サーバーに対して、データベースにアクセスしているユーザーのログインが照会されます。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 ブラウザーからこの例を実行すると、すべての出力はブラウザーに書き込まれます。  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>例  
次の例では、PDO_SQLSRV ドライバーを使用して前のサンプルと同じタスクを実行します。  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>参照  
[方法: SQL Server 認証を使用して接続する](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)

[SQL Server ログインを作成する方法](../../relational-databases/security/authentication-access/create-a-login.md)

[データベース ユーザーを作成する方法](../../relational-databases/security/authentication-access/create-a-database-user.md)

[ユーザー、ロール、およびログインの管理](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[ユーザーとスキーマの分離](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[GRANT (オブジェクトの権限の許可) (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
