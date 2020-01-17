---
title: Microsoft SQL Server 用 Drivers for PHP のシステム要件 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b601d4fbb02b489aca228acb719cfe8bad834dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992568"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft SQL Server 用 Drivers for PHP のシステム要件
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このドキュメントでは、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]を使用して SQL Server または Azure SQL Database のデータにアクセスするためにシステムにインストールする必要があるコンポーネントの一覧を示します。

SQL Server 用の Microsoft PHP ドライバーのバージョン3.1 以降は正式にサポートされています。 サポートライフサイクルと、以前のバージョンの PHP ドライバーを含む要件の詳細については、[サポートマトリックス](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)を参照してください。

## <a name="php"></a>PHP (PHP)

最新の安定した PHP バイナリをダウンロードし、インストールする方法については、[PHP Web サイト](https://php.net)を参照してください。  Microsoft Drivers for PHP for SQL Server には、次のバージョンの PHP が必要です。

|SQL Server ドライバーバージョン用の PHP&#8594;<br />&#8595; PHP バージョン|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. バージョン7.2.1 以降は Windows でサポートされていますが、バージョン7.2.0 以降は Linux および macOS でサポートされています。

-   ドライバー ファイルのバージョンは、PHP 拡張機能ディレクトリにあります。 さまざまなドライバーファイルの詳細については、「[ドライバーバージョン](#driver-versions)」を参照してください。  ドライバーをダウンロードするには、「[Download the Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md)」 (Microsoft SQL Server 用 Drivers for PHP をダウンロードする) を参照してください。 PHP のドライバーを構成する方法については、「[Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)」 (Microsoft SQL Server 用 Drivers for PHP を読み込む) を参照してください。

-   Web サーバーが必要です。 Web サーバーは、PHP を実行するように構成する必要があります。 IIS を使用して PHP アプリケーションをホストする方法については、 [php の web サイトのチュートリアル](http://docs.php.net/manual/da/install.windows.iis7.php)を参照してください。

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は IIS 10 と FastCGI でテストされています。  

    > [!NOTE]  
    > Microsoft は、IIS のサポートのみを提供しています。  

## <a name="odbc-driver"></a>ODBC ドライバー

PHP が実行されているコンピューターでは、正しいバージョンの Microsoft ODBC Driver for SQL Server が必要です。 サポートされているプラットフォームでサポートされているすべてのバージョンのドライバーを[このページ](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)からダウンロードできます。

64ビット版の Windows でドライバーの Windows バージョンをダウンロードする場合は、ODBC 64 ビットインストーラーによって、32ビットと64ビットの両方の ODBC ドライバーがインストールされます。 Windows の32ビットバージョンを使用する場合は、ODBC x86 インストーラーを使用します。 Windows 以外のプラットフォームでは、64ビットバージョンのドライバーのみを使用できます。

|SQL Server ドライバーバージョン用の PHP&#8594;<br />&#8595; ODBC ドライバーのバージョン|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC ドライバー 17 以降 |Y|Y|Y| | | | |
|ODBC ドライバー 13.1|Y|Y|Y|Y|Y| | |
|ODBC ドライバー 13  | | | | |Y| | |
|ODBC ドライバー 11  |Y|Y|Y|Y|Y|Y|Y|

SQLSRV ドライバーを使用している場合、 [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]によって使用されている Microsoft ODBC Driver for SQL Server のバージョンに関する情報を返します。 PDO_SQLSRV ドライバーを使用している場合、[PDO::getAttribute](../../connect/php/pdo-getattribute.md) を使用して、バージョンを確認できます。  

## <a name="sql-server"></a>SQL Server

Azure SQL データベースがサポートされています。 詳細については、「[Connecting to Microsoft Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md)」 (Microsoft Azure SQL Database への接続) をご覧ください。

|SQL Server ドライバーバージョン用の PHP&#8594;<br />&#8595; SQL Server のバージョン|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL データベース        |Y|Y|Y|Y| | | |
|Azure SQL Managed Instance|Y|Y|Y|Y| | | |
|Azure SQL Data Warehouse  |Y|Y|Y|Y| | | |
|SQL Server 2017           |Y|Y|Y|Y| | | |
|SQL Server 2016           |Y|Y|Y|Y|Y| | |
|SQL Server 2014           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2        |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008           | | | | |Y|Y|Y|

## <a name="operating-systems"></a>オペレーティング システム
ドライバーの各バージョンでサポートされているオペレーティングシステムは次のとおりです。

|SQL Server ドライバーバージョン用の PHP&#8594;<br />&#8595; オペレーティング システム|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |Y  |Y  |Y  |Y  |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2008 R2 SP1          |   |   |   |   |Y  |Y  |Y  |
|Windows Server 2008 SP2             |   |   |   |   |Y  |Y  |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows 8                           |   |   |   |Y  |Y  |Y  |Y  |
|Windows 7 SP1                       |   |   |   |   |Y  |Y  |Y  |
|Windows Vista SP2                   |   |   |   |   |Y  |Y  |Y  |
|Ubuntu 18.10 (64 ビット)               |Y  |   |   |   |   |   |   |
|Ubuntu 18.04 (64 ビット)               |Y  |Y  |   |   |   |   |   |
|Ubuntu 17.10 (64 ビット)               |   |Y  |Y  |   |   |   |   |
|Ubuntu 16.04 (64 ビット)               |Y  |Y  |Y  |Y  |Y  |   |   |
|Ubuntu 15.10 (64 ビット)               |   |   |   |Y  |   |   |   |
|Ubuntu 15.04 (64 ビット)               |   |   |   |   |Y  |   |   |
|Debian 9 (64 ビット)                   |Y  |Y  |Y  |   |   |   |   |
|Debian 8 (64 ビット)                   |Y  |Y  |Y  |Y  |   |   |   |
|Red Hat Enterprise Linux 7 (64 ビット) |Y  |Y  |Y  |Y  |Y  |   |   |
|Suse Enterprise Linux 15 (64 ビット)   |Y  |   |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 ビット)   |Y  |Y  |Y  |   |   |   |   |
|macOS Mojave (64 ビット)               |Y  |   |   |   |   |   |   |
|macOS High シエラレオネ (64 ビット)          |Y  |Y  |   |   |   |   |   |
|macOS Sierra (64 ビット)               |Y  |Y  |Y  |Y  |   |   |   |
|macOS El Capitan (64 ビット)           |   |Y  |Y  |Y  |   |   |   |

## <a name="driver-versions"></a>ドライバー バージョン  
ここでは、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]の各バージョンに含まれるドライバーファイルの一覧を示します。 各インストールパッケージには、スレッド化および非スレッド化されたバリアント形式の SQLSRV および PDO_SQLSRV ドライバーファイルが含まれています。 Windows では、32ビットおよび64ビットのバリアントでも使用できます。 PHP ランタイムで使用するドライバーを構成するには、「 [SQL Server 用 Microsoft Drivers FOR PHP の読み込み](../../connect/php/loading-the-php-sql-driver.md)」のインストール手順に従います。

サポートされている Linux および macOS のバージョンでは、 [linux と macos のインストール手順](../../connect/php/installation-tutorial-linux-mac.md)に従って、PHP の PECL パッケージシステムを使用して適切なドライバーをインストールできます。 または、 [Microsoft Drivers FOR PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github プロジェクトページからプラットフォーム用に事前に作成されたバイナリをダウンロードできます。次の表では、作成済みのバイナリパッケージに含まれるファイルを一覧表示しています。

**Microsoft SQL Server 用 Drivers 5.6 for PHP:**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |32ビット php7|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32ビット php7ts|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |64ビット php7|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64ビット php7ts|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|いいえ |32ビット php7|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32ビット php7ts|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|いいえ |64ビット php7|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64ビット php7ts|  
|32-bit php_sqlsrv_73_nts.dll<br />32-bit php_pdo_sqlsrv_73_nts.dll|7.3|いいえ |32ビット php7|  
|32-bit php_sqlsrv_73_ts.dll <br />32-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|32ビット php7ts|  
|64-bit php_sqlsrv_73_nts.dll<br />64-bit php_pdo_sqlsrv_73_nts.dll|7.3|いいえ |64ビット php7|  
|64-bit php_sqlsrv_73_ts.dll <br />64-bit php_pdo_sqlsrv_73_ts.dll |7.3|はい|64ビット php7ts|  

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|いいえ |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|いいえ |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|いいえ |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|はい|

**Microsoft SQL Server 用 Drivers 5.3 for PHP:**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|いいえ |32ビット php7|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|32ビット php7ts|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|いいえ |64ビット php7|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|64ビット php7ts|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |32ビット php7|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32ビット php7ts|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |64ビット php7|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64ビット php7ts|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|いいえ |32ビット php7|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32ビット php7ts|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|いいえ |64ビット php7|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64ビット php7ts|  

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|いいえ |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|いいえ |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|いいえ |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|

**Microsoft SQL Server 用 Drivers 5.2 for PHP:**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|いいえ |32ビット php7|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|32ビット php7ts|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|いいえ |64ビット php7|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|64ビット php7ts|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |32ビット php7|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32ビット php7ts|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |64ビット php7|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64ビット php7ts|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|いいえ |32ビット php7|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|32ビット php7ts|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|いいえ |64ビット php7|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|はい|64ビット php7ts|  

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|いいえ |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|いいえ |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|いいえ |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|はい|

**Microsoft SQL Server 用 Drivers 4.3 for PHP:**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|いいえ |32ビット php7|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|32ビット php7ts|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|いいえ |64ビット php7|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|はい|64ビット php7ts|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |32ビット php7|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|32ビット php7ts|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|いいえ |64ビット php7|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|はい|64ビット php7ts|   

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|いいえ |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|いいえ |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|はい|  

**Microsoft SQL Server 用 Drivers 4.0 for PHP**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|いいえ|32ビット php7|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|はい|32ビット php7ts|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|いいえ|64ビット php7|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|はい|64ビット php7ts|   

Linux では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|いいえ |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|はい|

**Microsoft SQL Server 用 Drivers 3.2 for PHP**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|いいえ|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|はい|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|いいえ|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|はい|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|いいえ|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|はい|php5ts.dll|  

**Microsoft SQL Server 用 Drivers 3.1 for PHP**  

Windows では、次のバージョンのドライバーが含まれています。

|ドライバー ファイル|PHP バージョン|スレッド セーフですか。|PHP .dll で使用|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|いいえ|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|はい|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|いいえ|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|はい|php5ts.dll|  

## <a name="see-also"></a>参照  
[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV ドライバー API リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)  
