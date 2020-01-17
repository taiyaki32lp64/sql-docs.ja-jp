---
title: ドライバー操作のトレース |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18bfd63a8cf3255a62b6aef5c4c31573c60e76b0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027594"
---
# <a name="tracing-driver-operation"></a>ドライバー操作のトレース
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] をアプリケーションで使用すると、トレース (またはログ記録) を使用して JDBC Driver で発生した問題の解決に役立てることができます。 トレースを有効にするため、JDBC Driver では java.util.logging でログ記録 API を使用しています。この API には、Logger および LogRecord オブジェクトを作成するための一連のクラスが用意されています。  
  
> [!NOTE]  
>  JDBC Driver に含まれているネイティブのコンポーネント sqljdbc_xa.dll については、Built-In Diagnostics (BID) フレームワークを使用してトレースを有効にしています。 BID の詳細については、[SQL Server でのデータ アクセスのトレース](https://go.microsoft.com/fwlink/?LinkId=70042)に関するページを参照してください。  
  
 アプリケーションを開発する際に、Logger オブジェクトへの呼び出しを行うことができます。次に、このオブジェクトは LogRecord オブジェクトを作成し、処理のために Handler オブジェクトに渡します。 Logger オブジェクトと Handler オブジェクトはどちらもログレベルを使用し、必要に応じてログフィルターを使用して、どのログレコードを処理するかを制御します。 ログの記録が完了すると、Handler オブジェクトは、Formatter オブジェクトを使用してオプションでログ情報を公開することができます。  
  
 既定では、java.util.logging フレームワークは出力をファイルに書き込みます。 この出力ログ ファイルは、JDBC Driver が動作しているコンテキストについて書き込みアクセス許可を持つ必要があります。  
  
> [!NOTE]  
>  プログラムをトレースするためのさまざまなログ記録オブジェクトの使用の詳細については、Sun Microsystems の Web サイトで Java ログ記録 API についてのドキュメント (英語ページの可能性があります) を参照してください。  
  
 次のセクションでは、ログ記録のレベルおよびログ記録可能なカテゴリについて説明し、アプリケーションでトレースを有効にする方法についての情報を提供します。  
  
## <a name="logging-levels"></a>ログ記録のレベル  
 作成されるすべてのログ メッセージは、ログ記録のレベルと関連付けられています。 ログ記録のレベルはログ メッセージの重要度を決定し、java.util.logging の **Level** クラスで定義されます。 あるレベルでログ記録を有効にすると、それより上のすべてのレベルでログ記録が有効になります。 このセクションでは、ログ記録のパブリックなカテゴリと内部的なカテゴリの両方を対象に、ログ記録のレベルについて説明します。 ログ記録カテゴリの詳細については、この記事の「ログ記録のカテゴリ」を参照してください。  
  
 次の表では、パブリックなログ記録のカテゴリで利用可能なログ記録の各レベルについて説明します。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|SEVERE|重大なエラーを示す、最高レベルのログ記録です。 JDBC Driver では、このレベルはエラーや例外の報告に使用されます。|  
|WARNING|問題が発生する可能性があることを示します。|  
|INFO|情報としてのメッセージを提供します。|  
|CONFIG|構成に関するメッセージを提供します。 ただし、現時点では JDBC Driver から構成メッセージは一切提供されません。|  
|FINE|パブリック メソッドによってスローされるすべての例外を含め、基本的なトレース情報を提供します。|  
|FINER|パブリック メソッドのすべての開始ポイントと終了ポイント、関連するパラメーターのデータ型、パブリック クラスのすべてのパブリック プロパティなど、詳細なトレース情報を提供します。 入力パラメーター、出力パラメーター、メソッドの戻り値も含まれますが、CLOB、BLOB、NCLOB、Reader、\<stream> の戻り値の型は除きます。|  
|FINEST|より詳細なトレース情報を提供します。 これは最低レベルのログ記録です。|  
|OFF|ログ記録をオフにします。|  
|ALL|すべてのメッセージのログ記録を有効にします。|  
  
 次の表では、内部的なログ記録のカテゴリで利用可能なログ記録の各レベルについて説明します。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|SEVERE|重大なエラーを示す、最高レベルのログ記録です。 JDBC Driver では、このレベルはエラーや例外の報告に使用されます。|  
|WARNING|問題が発生する可能性があることを示します。|  
|INFO|情報としてのメッセージを提供します。|  
|FINE|基本的なオブジェクトの作成と破棄など、各種のトレース情報を提供します。 パブリック メソッドによってスローされるすべての例外も含まれます。|  
|FINER|パブリック メソッドのすべての開始ポイントと終了ポイント、関連するパラメーターのデータ型、パブリック クラスのすべてのパブリック プロパティなど、詳細なトレース情報を提供します。 入力パラメーター、出力パラメーター、メソッドの戻り値も含まれますが、CLOB、BLOB、NCLOB、Reader、\<stream> の戻り値の型は除きます。<br /><br /> バージョン 1.2 の JDBC Driver には、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、XA、[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) の各ログ記録カテゴリが存在し、いずれも FINE のログ記録レベルが割り当てられていました。 これらは、バージョン 2.0 リリース以降で FINER レベルにアップグレードされています。|  
|FINEST|より詳細なトレース情報を提供します。 これは最低レベルのログ記録です。<br /><br /> バージョン 1.2 の JDBC Driver には、TDS.DATA および TDS.TOKEN というログ記録カテゴリが存在し、いずれも FINEST のログ記録レベルが割り当てられていました。 バージョン 2.0 リリース以降でも、ログ記録レベルは FINEST から変更されていません。|  
|OFF|ログ記録をオフにします。|  
|ALL|すべてのメッセージのログ記録を有効にします。|  
  
## <a name="logging-categories"></a>ログ記録のカテゴリ  
 Logger オブジェクトを作成するときは、どの名前付きエンティティまたはカテゴリからログ情報を取得するのかをそのオブジェクトに知らせる必要があります。 JDBC Driver は、パブリックなログ記録のカテゴリとして、次のカテゴリをサポートします。いずれも com.microsoft.sqlserver.jdbc ドライバー パッケージで定義されています。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|接続|[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINER として設定できます。|  
|ステートメントから削除してください。|[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINER として設定できます。|  
|DataSource|[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|ResultSet|[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINER として設定できます。|  
|Driver|[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINER として設定できます。|  
  
 Microsoft JDBC Driver Version 2.0 以降では、さらに com.microsoft.sqlserver.jdbc.internals パッケージが用意されており、内部的なログ記録のカテゴリとして、次のカテゴリがサポートされています。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|AuthenticationJNI|Windows 統合認証の問題に関するメッセージをログに記録します ( **Authenticationscheme**接続プロパティが暗黙的 **** または明示的にに設定されている場合)。<br /><br /> アプリケーションは、ログ記録レベルを FINEST および FINE として設定できます。|  
|SQLServerConnection|[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE および FINER として設定できます。|  
|SQLServerDataSource|[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)、[SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)、および [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md) クラスのメッセージを記録します。<br /><br /> アプリケーションは、ログ記録レベルを FINER として設定できます。|  
|InputStream|java.io.InputStream、java.io.Reader のほか、max 指定子を持つデータ型 (varchar、nvarchar、varbinary など) に関するメッセージを記録します。<br /><br /> アプリケーションは、ログ記録レベルを FINER として設定できます。|  
|SQLServerException|[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerResultSet|[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE、FINER、および FINEST として設定できます。|  
|SQLServerStatement|[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE、FINER、および FINEST として設定できます。|  
|XA|[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) クラスのすべての XA トランザクションについてメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE および FINER として設定できます。|  
|KerbAuthentication|種類4の Kerberos 認証に関するメッセージをログに記録します ( **Authenticationscheme**接続プロパティが**JavaKerberos**に設定されている場合)。 アプリケーションは、ログ記録レベルを FINE または FINER として設定できます。|  
|TDS.DATA|ドライバーと SQL Server の間で交わされる TDS プロトコル レベルのメッセージ交換を含んだメッセージを記録します。 送受信される各 TDS パケットの詳細な内容が ASCII および 16 進形式で記録されます。 ログイン資格情報 (ユーザー名とパスワード) は記録されません。 それ以外のすべてのデータが記録されます。<br /><br /> このカテゴリは非常に冗長で詳細なメッセージを作成します。ログ記録のレベルを FINEST に設定したときにのみ有効になります。|  
|TDS.Channel|SQL Server との TCP 通信チャネルのアクションをトレースします。 記録されるメッセージには、読み取りや書き込みのほか、ソケットの開閉が含まれます。 SQL Server との SSL (Secure Sockets Layer) 接続の確立に関連したメッセージもトレースされます。<br /><br /> このカテゴリは、ログ記録レベルを FINE、FINER、または FINEST に設定したときにのみ有効になります。|  
|TDS.Writer|TDS チャネルへの書き込みをトレースします。 トレースされるのは書き込みの長さのみです。書き込みの内容がトレースされるわけではありません。 このカテゴリでは、アテンション シグナルがサーバーに送信され、ステートメントの実行がキャンセルされた場合にも、問題がトレースされます。<br /><br /> このカテゴリは、ログ記録レベルを FINEST に設定したときにのみ有効になります。|  
|TDS.Reader|TDS チャネルからの特定の読み取り操作を FINEST レベルでトレースします。 FINEST レベルのトレースは冗長になる場合があります。 WARNING レベルや SEVERE レベルでは、ドライバーが接続を閉じる前に SQL Server から無効な TDS プロトコルを受信した場合にトレースが行われます。<br /><br /> このカテゴリは、ログ記録レベルを FINER または FINEST に設定したときにのみ有効になります。|  
|TDS.Command|低レベルの状態遷移や、TDS コマンドの実行に関連したその他の情報 ([!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行、ResultSet カーソルのフェッチ、コミットなど) をトレースします。<br /><br /> このカテゴリは、ログ記録レベルを FINEST に設定したときにのみ有効になります。|  
|TDS.TOKEN|このカテゴリは、TDS パケット内のトークンのみを記録しますが、TDS.DATA カテゴリほど冗長ではありません。 ログ記録レベルを FINEST に設定したときにのみ有効になります。<br /><br /> FINEST レベルでは、応答で処理される TDS トークンがトレースされます。 SEVERE レベルでは、無効な TDS トークンが検出された場合にトレースが実行されます。|  
|SQLServerDatabaseMetaData|[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerResultSetMetaData|[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerParameterMetaData|[SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerBlob|[SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerClob|[SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerSQLXML|内部 SQLServerSQLXML クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerDriver|[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
|SQLServerNClob|[SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md) クラスのメッセージを記録します。 アプリケーションは、ログ記録レベルを FINE として設定できます。|  
  
## <a name="enabling-tracing-programmatically"></a>プログラムによるトレースの有効化  
 トレースは、Logger オブジェクトを作成し、ログ記録するカテゴリを指定することにより、プログラムで有効にすることができます。 たとえば、次のコードは SQL ステートメントのログ記録を有効にする方法を示しています。  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 コードの中でログ記録を無効にするには、次のようにします。  
  
```java
logger.setLevel(Level.OFF);  
```  
  
 利用可能なすべてのカテゴリをログ記録するには、次のようにします。  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 特定のカテゴリのログ記録を無効にするには、次のようにします。  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>logging.properties ファイルを使用してトレースを有効にする  
 `logging.properties` ファイルを使用してトレースを有効にすることもできます。このファイルは、Java ランタイム環境 (JRE) のインストール ディレクトリ `lib` にあります。 このファイルを使用すると、トレースが有効になったときに使用されるロガーやハンドラーに既定値を設定することができます。  
  
 次は、`logging.properties` ファイルで行うことができる設定の一例です。  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  java.util.logging に含まれる LogManager オブジェクトを使用して、`logging.properties` ファイルでプロパティを設定することができます。  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーに関する問題の診断](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
