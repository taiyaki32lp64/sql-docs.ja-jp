---
title: アクティビティのログ記録 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29c7c1e3b536e237e2c61a8e3303313ec53fe679
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993330"
---
# <a name="logging-activity"></a>アクティビティのログ記録
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

既定では、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] で生成されるエラーと警告はログ記録されません。 このトピックでは、アクティビティのログ記録を構成する方法について説明します。  
  
## <a name="logging-activity-using-the-pdosqlsrv-driver"></a>PDO_SQLSRV ドライバーを使用したアクティビティのログ記録  
PDO_SQLSRV ドライバーで利用可能な構成は、php.ini ファイル内の pdo_sqlsrv.log_severity エントリのみです。  
  
php.ini ファイルの最後に、次を追加します。  
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = <number>  
```  
  
**log_severity** は次のいずれかの値をとります。場所は次の値のいずれかです。  
  
|[値]|Description|  
|---------|---------------|  
|0|ログ記録は無効です (何も定義されていない場合は、これが既定です)。|  
|-1|エラー、警告、および通知をログ記録することを指定します。|  
|1|エラーをログに記録することを指定します。|  
|2|警告をログに記録することを指定します。|  
|4|通知をログに記録することを指定します。|  
  
ログ記録の情報は、phperrors.log ファイルに追加されます。  
  
PHP では、初期化時に構成ファイルを読み取り、データをキャッシュに格納します。また、PHP では、これらの設定を更新してすぐに使用するための API も提供し、構成ファイルに書き込まれます。 この API は、PHP を初期化した後でも、アプリケーションのスクリプトで設定を変更できるようにします。  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>SQLSRV ドライバーを使用したアクティビティのログ記録  
ログ記録をオンにするには、[sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 関数を使用するか、php.ini ファイルを変更することができます。 初期化、接続、ステートメント、またはエラー関数のアクティビティをログ記録できます。 また、エラー、警告、通知、または 3 つすべてをログ記録するかどうかも指定できます。  
  
> [!NOTE]  
> ログ ファイルの場所は php.ini ファイルで構成できます。  
  
### <a name="turning-logging-on"></a>ログ記録をオンにする  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 関数を使用して、**LogSubsystems** 設定の値を指定し、ログ記録をオンにすることができます。 たとえば、次のコードの行は、接続時のアクティビティをログ記録するようにドライバーを構成します。  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN);`  
  
次の表では、 **LogSubsystems** 設定の値として使用できる定数について説明します。  
  
|値 (かっこ内と同等の整数)|[説明]|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|すべてのサブシステムのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_OFF (0)|ログ記録をオフにします。 これは既定値です。|  
|SQLSRV_LOG_SYSTEM_INIT (1)|初期化アクティビティのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_CONN (2)|接続アクティビティのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_STMT (4)|ステートメント アクティビティのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|エラー関数アクティビティ (handle_error や handle_warning など) のログ記録をオンにします。|  
  
論理 OR 演算子 (|) を使用して、**LogSubsystems** の設定に一度に複数の値を設定することができます。 たとえば、次のコードの行は、接続とステートメントの両方のアクティビティのログ記録をオンにします。  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN | SQLSRV_LOG_SYSTEM_STMT);`  
  
また、php.ini ファイルの **LogSubsystems** の設定に整数値を指定して、ログ記録をオンにすることもできます。 たとえば、次の行を php.ini ファイルの `[sqlsrv]` セクションに追加すると、接続アクティビティのログ記録がオンになります。  
  
`sqlsrv.LogSubsystems = 2`  
  
整数値をまとめて追加すると、一度に複数のオプションを指定できます。 たとえば、次の行を php.ini ファイルの `[sqlsrv]` セクションに追加すると、接続とステートメントのアクティビティのログ記録がオンになります。  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>エラー、警告および通知のログ記録  
ログ記録をオンにした後、ログ記録する内容を指定する必要があります。 次の 1 つ以上をログ記録することができます: エラー、警告および通知。 たとえば、次のコードの行では、警告のみをログ記録することを指定します。  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> **LogSeverity** の既定の設定は、**SQLSRV_LOG_SEVERITY_ERROR** です。 ログ記録がオンで、 **LogSeverity** の設定が指定されていない場合、エラーのみがログ記録されます。  
  
次の表では、 **LogSeverity** 設定の値として使用できる定数について説明します。  
  
|値 (かっこ内と同等の整数)|[説明]|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|エラー、警告、および通知をログ記録することを指定します。|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|エラーをログに記録することを指定します。 これは既定値です。|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|警告をログに記録することを指定します。|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|通知をログに記録することを指定します。|  
  
論理 OR 演算子 (|) を使用して、**LogSeverity** の設定に一度に複数の値を設定することができます。 たとえば、次のコードの行では、エラーと警告をログ記録することを指定します。  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> **LogSeverity** の設定の値を指定しても、ログ記録は有効になりません。 **LogSubsystems** の設定の値を指定してログ記録をオンにし、**LogSeverity** の値を設定してログ内容の重大度を指定します。  
  
また、php.ini ファイルの整数値を使用して、 **LogSeverity** 設定の設定を指定することもできます。 たとえば、次の行を php.ini ファイルの `[sqlsrv]` セクションに追加すると、警告のログ記録のみが有効になります。  
  
`sqlsrv.LogSeverity = 2`  
  
整数値をまとめて追加すると、一度に複数のオプションを指定できます。 たとえば、次の行を php.ini ファイルの `[sqlsrv]` セクションに追加すると、エラーと警告のログ記録が有効になります。  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>参照  
[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)

[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
  
