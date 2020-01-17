---
title: Microsoft Drivers for PHP for SQL Server の Linux および macOS インストール チュートリアル | Microsoft Docs
ms.date: 07/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: 78db7a94e462238b65e90d9b2af035a9906403ac
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632008"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server の Linux および macOS インストール チュートリアル
次の手順では、クリーンな環境を想定し、Ubuntu 16.04、18.04、および 18.10、RedHat 7、Debian 8 および 9、Suse 12 および 15、および macOS 10.12、10.13、および 10.14 に、PHP 7.x、Microsoft ODBC ドライバー、Apache、および Microsoft Drivers for PHP for SQL Server をインストールする方法を説明します。 これらの手順では、PECL を使用してドライバーをインストールするようにアドバイスしていますが、「[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases)」 Github プロジェクト ページからビルド済みのバイナリをダウンロードし、「[Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)」(Microsoft Drivers for PHP for SQL Server の読み込み) の手順に従ってそれらをインストールすることもできます。 拡張機能の読み込みおよび php.ini に拡張機能を追加しない理由の説明については、[ドライバーの読み込み](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)に関するセクションを参照してください。

これらの手順では、既定で PHP 7.3 をインストールします。 サポートされている一部の Linux ディストリビューションでは、SQL Server 用 PHP ドライバーでサポートされていない PHP 7.0 以前に既定で設定されていることに注意してください。各セクションの先頭にある注記を参照して、代わりに PHP 7.1 または 7.2 をインストールしてください。

## <a name="contents-of-this-page"></a>このページの内容:

- [Ubuntu 16.04、18.04、および 18.10 へのドライバーのインストール](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [Red Hat 7 へのドライバーのインストール](#installing-the-drivers-on-red-hat-7)
- [Debian 8 および 9 へのドライバーのインストール](#installing-the-drivers-on-debian-8-and-9)
- [Suse 12 および 15 へのドライバーのインストール](#installing-the-drivers-on-suse-12-and-15)
- [macOS Sierra、High Sierra、および Mojave へのドライバーのインストール](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>Ubuntu 16.04、18.04、および 18.10 へのドライバーのインストール

> [!NOTE]
> PHP 7.1 または 7.2 をインストールするには、次のコマンドで 7.3 を 7.1 または 7.2 に置き換えます。

### <a name="step-1-install-php"></a>手順 1. PHP のインストール
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>手順 2. 必須コンポーネントのインストール
[Linux と macOS のインストールに関するページ](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)の手順に従って、Ubuntu 用 ODBC ドライバーをインストールします。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>手順 3. Microsoft SQL Server 用 PHP ドライバーのインストール
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.3/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.3/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.3 sqlsrv pdo_sqlsrv
```

システムに PHP バージョンが1つしかない場合は、最後の手順をに`phpenmod sqlsrv pdo_sqlsrv`簡略化できます。

### <a name="step-4-install-apache-and-configure-driver-loading"></a>手順 4. Apache のインストールとドライバーの読み込みの構成
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>手順 5. Apache の再起動とサンプル スクリプトのテスト
```
sudo service apache2 restart
```
インストールをテストするには、このドキュメントの最後の「[インストールのテスト](#testing-your-installation)」を参照してください。

## <a name="installing-the-drivers-on-red-hat-7"></a>Red Hat 7 へのドライバーのインストール

> [!NOTE]
> PHP 7.1 または 7.2 をインストールするには、次のコマンドで remi php73 を remi-php71 または remi-php72 にそれぞれ置き換えます。

### <a name="step-1-install-php"></a>手順 1. PHP のインストール

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>手順 2. 必須コンポーネントのインストール
[Linux と macOS のインストールに関するページ](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)の手順に従って、Red Hat 7 用 ODBC ドライバーをインストールします。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>手順 3. Microsoft SQL Server 用 PHP ドライバーのインストール
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```

または [Github プロジェクト ページ](https://github.com/Microsoft/msphpsql/releases)からビルド済みのバイナリをダウンロードするか、または Remi リポジトリからインストールすることができます。
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>手順 4. Apache のインストール
```
sudo yum install httpd
```
SELinux は既定でインストールされ、Enforcing モードで実行します。 Apache が SELinux 経由でデータベースに接続できるようにするには、次のコマンドを実行します。
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>手順 5. Apache の再起動とサンプル スクリプトのテスト
```
sudo apachectl restart
```
インストールをテストするには、このドキュメントの最後の「[インストールのテスト](#testing-your-installation)」を参照してください。

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Debian 8 および 9 へのドライバーのインストール

> [!NOTE]
> PHP 7.1 または 7.2 をインストールするには、次のコマンドで 7.3 を 7.1 または 7.2 に置き換えます。

### <a name="step-1-install-php"></a>手順 1. PHP のインストール
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>手順 2. 必須コンポーネントのインストール
[Linux と macOS のインストールに関するページ](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)の手順に従って、Debian 用 ODBC ドライバーをインストールします。 

また、PHP の出力をブラウザーで正しく表示させるために、正しいロケールを生成する必要がある場合もあります。 たとえば、en_US UTF-8 ロケールの場合、次のコマンドを実行します。
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>手順 3. Microsoft SQL Server 用 PHP ドライバーのインストール
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.3/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.3/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.3 sqlsrv pdo_sqlsrv
```

システムに PHP バージョンが1つしかない場合は、最後の手順をに`phpenmod sqlsrv pdo_sqlsrv`簡略化できます。

### <a name="step-4-install-apache-and-configure-driver-loading"></a>手順 4. Apache のインストールとドライバーの読み込みの構成
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>手順 5. Apache の再起動とサンプル スクリプトのテスト
```
sudo service apache2 restart
```
インストールをテストするには、このドキュメントの最後の「[インストールのテスト](#testing-your-installation)」を参照してください。

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Suse 12 および 15 へのドライバーのインストール

> [!NOTE]
> 次の手順で、<SuseVersion> を使用している Suse のバージョンで置き換えます。Suse Enterprise Linux 15 を使用している場合は、SLE_15 または SLE_15_SP1 になります。 Suse 12 の場合は、SLE_12_SP4 (該当する場合は上記以上) を使用します。 Suse Linux のすべてのバージョンで、PHP のすべてのバージョンが利用できるわけではありません。`http://download.opensuse.org/repositories/devel:/languages:/php` を参照して、Suse のどのバージョンで既定のバージョンの PHP を使用できるか確認するか、または `http://download.opensuse.org/repositories/devel:/languages:/php:/` を参照して、PHP のその他のどのバージョンが Suse のどのバージョンで使用できるかを確認してください。

> [!NOTE]
> PHP 7.3 のパッケージは、Suse 12 で使用できません。 PHP 7.1 をインストールするには、下記のリポジトリの URL を URL `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo` で置き換えます。
> PHP 7.2 をインストールするには、下記のリポジトリの URL を URL `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo` で置き換えます。

### <a name="step-1-install-php"></a>手順 1. PHP のインストール
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>手順 2. 必須コンポーネントのインストール
[Linux と macOS のインストールに関するページ](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)の手順に従って、Suse 用 ODBC ドライバーをインストールします。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>手順 3. Microsoft SQL Server 用 PHP ドライバーのインストール
> [!NOTE]
> `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"` というエラー メッセージが表示された場合、/usr/bin/pecl にある pecl スクリプトを編集し、最後の行の `-n` スイッチを削除します。 このスイッチによって、PHP が呼び出されたときに、PECL の ini ファイルの読み込みが妨げられ、それによって、OpenSSL 拡張機能の読み込みが妨げられます。

```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>手順 4. Apache のインストールとドライバーの読み込みの構成
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>手順 5. Apache の再起動とサンプル スクリプトのテスト
```
sudo systemctl restart apache2
```
インストールをテストするには、このドキュメントの最後の「[インストールのテスト](#testing-your-installation)」を参照してください。

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>macOS Sierra、High Sierra、および Mojave へのドライバーのインストール

brew がまだない場合は、次のようにそれをインストールします。
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> PHP 7.1 または 7.2 をインストールするには、次のコマンドで php@7.3 を php@7.1 または php@7.2 にそれぞれ置き換えます。

### <a name="step-1-install-php"></a>手順 1. PHP のインストール

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
PHP がパスに含まれるようになったはずです。`php -v` を実行して、正しいバージョンの PHP が実行されていることを確認します。 PHP がパスにないか、または正しいバージョンでない場合は、次を実行します。
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>手順 2. 必須コンポーネントのインストール
[Linux と macOS のインストールに関するページ](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)の手順に従って、macOS 用 ODBC ドライバーをインストールします。 

さらに、GNU make ツールをインストールする必要がある場合があります。
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>手順 3. Microsoft SQL Server 用 PHP ドライバーのインストール
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>手順 4. Apache のインストールとドライバーの読み込みの構成
```
brew install apache2
```
Apache インストールの Apache 構成ファイルを検索するには、 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
次のコマンドの `httpd.conf` のパスを置き換えて実行します。
```
echo "LoadModule php7_module /usr/local/opt/php@7.3/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>手順 5. Apache の再起動とサンプル スクリプトのテスト
```
sudo apachectl restart
```
インストールをテストするには、このドキュメントの最後の「[インストールのテスト](#testing-your-installation)」を参照してください。

## <a name="testing-your-installation"></a>インストールのテスト

このサンプル スクリプトをテストするには、システムのドキュメント ルートに testsql.php というファイルを作成します。 これは Ubuntu、Debian、および Redhat では `/var/www/html/`、SUSE では `/srv/www/htdocs`、または macOS では `/usr/local/var/www` です。 次のスクリプトをそれにコピーし、該当する場合にサーバー、データベース、ユーザー名、およびパスワードを置き換えます。
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
ブラウザーで https://localhost/testsql.php (macOS では https://localhost:8080/testsql.php ) をポイントします。 SQL Server または Azure SQL データベースに接続できるようになったはずです。

## <a name="see-also"></a>参照  
[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft SQL Server 用 Drivers for PHP を読み込む](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft SQL Server 用 Drivers for PHP のシステム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)
