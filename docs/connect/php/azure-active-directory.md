---
title: Azure Active Directory |Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 8712681a244e969d230b0b7099acd4aa56334f11
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265176"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Azure Active Directory 認証を使用して接続する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)(Azure AD) は、 [SQL Server 認証](../../connect/php/how-to-connect-using-sql-server-authentication.md)の代わりに動作する、中央のユーザー ID 管理テクノロジです。 Azure AD を使用すると、ユーザー名とパスワード、Windows 統合認証、または Azure AD アクセストークンを使用して Azure AD のフェデレーション id で Microsoft Azure SQL Database と SQL Data Warehouse に接続できます。 SQL Server 用の PHP ドライバーは、これらの機能に対して部分的なサポートを提供します。

Azure AD を使用するには、次の表に示すように、 **Authentication**キーワードまたは**AccessToken**キーワードを使用します (これらは相互に排他的です)。 技術的な詳細については、「 [ODBC ドライバーでの Azure Active Directory の使用](../../connect/odbc/using-azure-active-directory.md)」を参照してください。

|Keyword|値|[説明]|
|-|-|-|
|**AccessToken**|未設定 (既定値)|他のキーワードによって決定される認証モード。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。 |
||バイト文字列|OAuth JSON 応答から抽出された Azure AD アクセストークン。 接続文字列には、ユーザー ID、パスワード、または Authentication キーワードを含めることができません (Linux または macOS では、ODBC Driver バージョン17以降が必要です)。 |
|**[認証]**|未設定 (既定値)|他のキーワードによって決定される認証モード。 詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。 |
||`SqlPassword`|ユーザー名とパスワードを使用して、(Azure インスタンスである可能性がある) SQL Server インスタンスに直接認証します。 **UID**キーワードと**PWD**キーワードを使用して、ユーザー名とパスワードを接続文字列に渡す必要があります。 |
||`ActiveDirectoryPassword`|ユーザー名とパスワードを使用して Azure Active Directory id で認証します。 **UID**キーワードと**PWD**キーワードを使用して、ユーザー名とパスワードを接続文字列に渡す必要があります。 |
||`ActiveDirectoryMsi`|システムによって割り当てられたマネージド id またはユーザーが割り当てられたマネージド id を使用して認証します (ODBC ドライバーバージョン17.3.1.1 以上が必要です)。 概要とチュートリアルについては、「 [Azure リソースのマネージド id とは](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)」を参照してください。|

**Authentication**キーワードは、接続のセキュリティ設定に影響します。 接続文字列で設定されている場合は、既定で**Encrypt**キーワードが true に設定されます。これは、クライアントが暗号化を要求することを意味します。 また、 **Trustservercertificate**が true (既定では**false** ) に設定されていない限り、暗号化の設定に関係なくサーバー証明書が検証されます。 この機能は、暗号化が特に接続文字列で要求された場合にのみサーバー証明書が検証される、古い、セキュリティの低いログイン方法と区別されます。

Windows で SQL Server 用の PHP ドライバーで Azure AD を使用する場合は、 [Microsoft Online Services サインインアシスタント](https://www.microsoft.com/download/details.aspx?id=41950)をインストールするように求められることがあります (ODBC 17 以降では不要)。

#### <a name="limitations"></a>制限事項

Windows では、基になる ODBC ドライバーが**Authentication**キーワード**ActiveDirectoryIntegrated**に対してもう1つの値をサポートしていますが、PHP ドライバーは、どのプラットフォームでもこの値をサポートしていません。

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>例-SqlPassword と ActiveDirectoryPassword を使用して接続する

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>例-PDO_SQLSRV ドライバーを使用して接続する

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>例-Azure AD アクセストークンを使用して接続する

### <a name="sqlsrv-driver"></a>SQLSRV ドライバー

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdosqlsrv-driver"></a>PDO_SQLSRV ドライバー

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>例-Azure リソースの管理対象 id を使用して接続する

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>SQLSRV ドライバーでシステム割り当て済みマネージド id を使用する

システム割り当て済みマネージド id を使用して接続する場合は、UID または PWD オプションを使用しないでください。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>PDO_SQLSRV driver でユーザー割り当てのマネージド id を使用する

ユーザー割り当てのマネージド id は、スタンドアロンの Azure リソースとして作成されます。 Azure では、使用中のサブスクリプションによって信頼されている Azure AD テナントに id が作成されます。 Id を作成したら、1つまたは複数の Azure サービスインスタンスに id を割り当てることができます。 この id `Object ID`のをコピーし、接続文字列のユーザー名として設定します。 

そのため、ユーザー割り当てのマネージド id を使用して接続する場合は、ユーザー名としてオブジェクト ID を指定しますが、パスワードは省略します。

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>参照
[ODBC ドライバーでの Azure Active Directory の使用](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[Azure リソースの管理対象 id とは](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
