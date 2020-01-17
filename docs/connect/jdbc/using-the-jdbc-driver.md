---
title: JDBC ドライバーの使用 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 828f58249f525a7c694b15eb85f051d80ba2211a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025771"
---
# <a name="using-the-jdbc-driver"></a>JDBC ドライバーの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

このセクションでは、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへのシンプルな接続を作成する方法について簡単に説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続する前に、まず [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をローカル コンピューターまたはサーバーのどちらかにインストールし、JDBC ドライバーをローカル コンピューターにインストールする必要があります。  
  
## <a name="choosing-the-right-jar-file"></a>適切な JAR ファイルの選択

Microsoft JDBC Driver には、次の Java Runtime Environment (JRE) 設定との通信で使用される複数の Jar が用意されています。

Microsoft JDBC Driver 7.4 for SQL Server では、**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar**、**mssql-jdbc-7.4.1.jre12.jar** の各クラス ライブラリ ファイルが提供されます。

Microsoft JDBC Driver 7.2 for SQL Server には、**mssql-jdbc-7.2.2.jre8.jar** および **mssql-jdbc-7.2.2.jre11.jar** クラス ライブラリ ファイルが提供されます。

Microsoft JDBC Driver 7.0 for SQL Server には、**mssql-jdbc-7.0.0.jre8.jar** および **mssql-jdbc-7.0.0.jre10.jar** クラス ライブラリ ファイルが提供されます。

Microsoft JDBC Driver 6.4 for SQL Server には、**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar**、および **mssql-jdbc-6.4.0.jre9.jar** クラス ライブラリ ファイルが提供されます。

Microsoft JDBC Driver 6.2 for SQL Server には、**mssql-jdbc-6.2.2.jre7.jar**および **mssql-jdbc-6.2.2.jre8.jar** クラス ライブラリ ファイルが提供されます。
  
Microsoft JDBC Driver 6.0 および 4.2 SQL Server には、**sqljdbc41.jar**、および **sqljdbc42.jar** クラス ライブラリ ファイルが提供されます。
  
Microsoft JDBC Driver 4.1 SQL Server には、**sqljdbc41.jar** クラス ライブラリ ファイルが提供されます。

また、選択した JAR ファイルによって、使用可能な機能が決定します。 選択する JAR ファイルの詳細については、「[JDBC Driver のシステム要件](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)」を参照してください。  
  
## <a name="setting-the-classpath"></a>クラスパスの設定

Microsoft JDBC Driver の jar は Java SDK の一部ではないため、ユーザー アプリケーションのクラスパスに含める必要があります。

JDBC Driver 4.1 または 4.2 を使用する場合は、該当するドライバーのダウンロードから **sqljdbc41.jar** または **sqljdbc42.jar** ファイルを含むようにクラスパスを設定します。

JDBC Driver 6.2 を使用する場合は、**mssql-jdbc-6.2.2.jre7.jar** または **mssql-jdbc-6.2.2.jre8.jar** を含むようにクラスパスを設定します。

JDBC Driver 6.4 を使用する場合は、**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar**、または **mssql-jdbc-6.4.0.jre9.jar** が含まれるようにクラスパスを設定します。

JDBC Driver 7.0 を使用する場合は、**mssql-jdbc-7.0.0.jre8.jar** または **mssql-jdbc-7.0.0.jre10.ja**r を含むようにクラスパスを設定します。

JDBC Driver 7.2 を使用する場合は、**mssql-jdbc-7.2.2.jre8.jar** または **mssql-jdbc-7.2.2.jre11.jar**を含むようにクラスパスを設定します。

JDBC Driver 7.4 を使用する場合は、**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar**、または **mssql-jdbc-7.4.1.jre12.jar** が含まれるようにクラスパスを設定します。

クラスパスに適切な Jar ファイルのエントリがない場合、アプリケーションでは `Class not found` という一般的な例外がスローされます。  

### <a name="for-microsoft-jdbc-driver-74"></a>Microsoft JDBC Driver 7.4 の場合

**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar**、または **mssql-jdbc-7.4.1.jre12.jar** ファイルが次の場所にインストールされます。

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre11.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre12.jar
```

次のスニペットは、Windows アプリケーションで使用される CLASSPATH ステートメントの例です。

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.4 for SQL Server\sqljdbc_7.4\enu\mssql-jdbc-7.4.1.jre11.jar`

次のスニペットは、Unix/Linux アプリケーションで使用される CLASSPATH ステートメントの例です。

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.4/enu/mssql-jdbc-7.4.1.jre11.jar`

CLASSPATH ステートメントに [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] が 1 つだけ含まれていることを確認します (**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar**、**mssql-jdbc-7.4.1.jre12.jar** など)。

### <a name="for-microsoft-jdbc-driver-72"></a>Microsoft JDBC driver 7.2 の場合

**Mssql-jdbc-7.2.2.jre8.jar** または **mssql-jdbc-7.2.2.jre11.jar** ファイルが次の場所にインストールされます。

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.2.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.2.jre11.jar
```

次のスニペットは、Windows アプリケーションで使用される CLASSPATH ステートメントの例です。

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.2 for SQL Server\sqljdbc_7.2\enu\mssql-jdbc-7.2.2.jre11.jar`

次のスニペットは、Unix/Linux アプリケーションで使用される CLASSPATH ステートメントの例です。

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.2/enu/mssql-jdbc-7.2.2.jre11.jar`

CLASSPATH ステートメントには 1 つの [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] (**mssql-jdbc-7.2.2.jre8.jar** または **mssql-jdbc-7.2.2.jre11.jar** のいずれか) のみが含まれていることを確認してください。
  
### <a name="for-microsoft-jdbc-driver-70"></a>Microsoft JDBC Driver 7.0 の場合

**mssql-jdbc-7.0.0.jre8.jar** または **mssql-jdbc-7.0.0.jre10.jar** ファイルが次の場所にインストールされます。

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre10.jar
```

次のスニペットは、Windows アプリケーションで使用される CLASSPATH ステートメントの例です。  

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.0 for SQL Server\sqljdbc_7.0\enu\mssql-jdbc-7.0.0.jre10.jar`  
  
次のスニペットは、Unix/Linux アプリケーションで使用される CLASSPATH ステートメントの例です。  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.0/enu/mssql-jdbc-7.0.0.jre10.jar`  
  
CLASSPATH ステートメントには 1 つの [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] (**mssql-jdbc-7.0.0.jre8.jar** または **mssql-jdbc-7.0.0.jre10.jar** のいずれか) のみが含まれていることを確認してください。

### <a name="for-microsoft-jdbc-driver-64"></a>Microsoft JDBC Driver 6.4 の場合

**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar、または **mssql-jdbc-6.4.0.jre9.jar** ファイルが次の場所にインストールされます。  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre9.jar
```

次のスニペットは、Windows アプリケーションで使用される CLASSPATH ステートメントの例です。  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
次のスニペットは、Unix/Linux アプリケーションで使用される CLASSPATH ステートメントの例です。  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
CLASSPATH ステートメントには 1 つの [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] (**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar、または **mssql-jdbc-6.4.0.jre9.jar** のいずれか) のみが含まれていることを確認してください。

### <a name="for-microsoft-jdbc-driver-62"></a>Microsoft JDBC Driver 6.2 の場合

**mssql-jdbc-6.2.2.jre7.jar** または **mssql-jdbc-6.2.2.jre8.jar** ファイルが次の場所にインストールされます。

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre8.jar
```

次のスニペットは、Windows アプリケーションで使用される CLASSPATH ステートメントの例です。  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.2.jre8.jar`  
  
次のスニペットは、Unix/Linux アプリケーションで使用される CLASSPATH ステートメントの例です。  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.2.jre8.jar`  
  
CLASSPATH ステートメントには 1 つの [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] (mssql-jdbc-6.2.2.jre7.jar または mssql-jdbc-6.2.2.jre8.jar のいずれか) のみが含まれていることを確認してください。  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Microsoft JDBC Driver 4.1、4.2、および 6.0 の場合

sqljdbc.jar ファイル、sqljdbc4.jar ファイル、sqljdbc41.jar ファイル、または sqljdbc42.jar ファイルは次の場所にインストールします。  

```bash
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc4.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc41.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc42.jar  
```

次のスニペットは、Windows アプリケーションで使用される CLASSPATH ステートメントの例です。  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
次のスニペットは、Unix/Linux アプリケーションで使用される CLASSPATH ステートメントの例です。  

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
CLASSPATH ステートメントに含まれている [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] が、sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar、または sqljdbc42.jar のいずれか 1 つであることを確認してください。  
  
> [!NOTE]  
> Windows システムでは、ディレクトリ名が 8.3 ファイル名規則より長い場合、またはフォルダー名にスペースが含まれている場合、クラスパスに問題が生じることがあります。 この種の問題が疑われる場合、sqljdbc.jar ファイル、sqljdbc4.jar ファイル、または sqljdbc41.jar ファイルを一時的に `C:\Temp` のようなシンプルな名前のディレクトリへ移動し、クラスパスを変更して問題が解決するかどうかを判断する必要があります。  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>コマンド プロンプトで直接実行されるアプリケーション

クラスパスは、オペレーティング システムにおいて構成されます。 sqljdbc.jar、sqljdbc4.jar、または sqljdbc41.jar をシステムのクラスパスに追加します。 または、`java -classpath` オプションを使用して、アプリケーションを実行するクラスパスを Java コマンド ラインで指定することもできます。  
  
### <a name="applications-that-run-in-an-ide"></a>IDE で実行されるアプリケーション  

各 IDE ベンダーでは、クラスパスを自社の IDE に設定するためのさまざまな方法を用意しています。 クラスパスをオペレーティング システムに設定するだけでは動作しません。 sqljdbc.jar、sqljdbc4.jar、または sqljdbc41.jar を IDE クラスパスに追加する必要があります。  
  
### <a name="servlets-and-jsps"></a>サーブレットおよび JSP  

サーブレットや JSP は、Tomcat のようなサーブレット/JSP エンジンで実行されます。 クラスパスは、サーブレット/JSP エンジンのドキュメントに従って設定する必要があります。 クラスパスをオペレーティング システムに設定するだけでは動作しません。 一部のサーブレット/JSP エンジンでは、エンジンのクラスパスを設定するために使用できるセットアップ画面が用意されています。 この場合、正しい JDBC ドライバー用 JAR ファイルを既存のエンジン クラスパスに追加し、エンジンを再起動する必要があります。 この他の場合は、エンジンをインストールするときに lib のような特定のディレクトリに sqljdbc.jar、sqljdbc4.jar、または sqljdbc41.jar をコピーしてドライバーを配置することができます。 エンジン ドライバーのクラスパスは、エンジン固有の構成ファイルで指定することもできます。  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  

Enterprise Java Beans (EJB) は、EJB コンテナーで実行されます。 EJB コンテナーは、さまざまなベンダーから供給されています。 Java アプレットはブラウザー上で動作しますが、Web サーバーからダウンロードされます。 sqljdbc.jar、sqljdbc4.jar、または sqljdbc41.jar を Web サーバーのルートにコピーし、アプレットの [HTML archive] タブで JAR ファイル名を指定します。たとえば、`<applet ... archive=mssql-jdbc-***.jar>` のようになります。  
  
## <a name="making-a-simple-connection-to-a-database"></a>データベースへの単純な接続を行う

sqljdbc.jar クラス ライブラリを使用するアプリケーションでは、まず次のようにしてドライバーを登録する必要があります。  
  
`Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  

ドライバーが読み込まれたら、接続 URL と、DriverManager クラスの getConnection メソッドを使用して接続を確立できます。

```java
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```

JDBC API 4.0 以降、JDBC ドライバーが自動的に読み込まれるように、`DriverManager.getConnection()` メソッドが改良されました。 したがって、ドライバーの Jar ライブラリを使用する場合は、アプリケーションから `Class.forName` メソッドを呼び出してドライバーの登録や読み込みを行う必要はありません。  
  
DriverManager クラスの getConnection メソッドが呼び出されると、登録されている一連の JDBC ドライバーから適切なドライバーが検出されます。 sqljdbc4.jar、sqljdbc41.jar、または sqljdbc42.jar ファイルには "META-INF/services/java.sql.Driver" ファイルが含まれています。これには、**com.microsoft.sqlserver.jdbc.SQLServerDriver** が登録済みのドライバーとして含まれています。 現在 Class.forName メソッドを使用してドライバーを読み込む仕様になっている既存のアプリケーションも正常に動作します。特に修正の必要はありません。  
  
> [!NOTE]  
> sqljdbc4.jar、sqljdbc41.jar、または sqljdbc42.jar のクラス ライブラリは、以前のバージョンの Java Runtime Environment (JRE) では使用できません。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によってサポートされている JRE バージョンの一覧については、「[JDBC Driver のシステム要件](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)」を参照してください。  

データ ソースの接続方法と接続 URL の使用方法の詳細については、「[接続 URL の構築](../../connect/jdbc/building-the-connection-url.md)」と「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
## <a name="see-also"></a>参照  

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
