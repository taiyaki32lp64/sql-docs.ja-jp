---
title: 接続の操作 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 267605b6a89f323570cfacfc66517b028ef716a2
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025471"
---
# <a name="working-with-a-connection"></a>接続の操作

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

以下のセクションでは、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] の [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続するさまざまな方法の例を示します。

> [!NOTE]  
> JDBC ドライバーを使用した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続で問題が発生した場合は、「[接続のトラブルシューティング](../../connect/jdbc/troubleshooting-connectivity.md)」で提案されている修正方法を参照してください。

## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>DriverManager クラスを使用した接続の作成

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続を最も効率的に作成するには、JDBC ドライバーを読み込み、次のように DriverManager クラスの getConnection メソッドを呼び出します。

```java
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```

この手法では、渡された URL で正常に接続できるドライバーを示す一覧から、最初の使用可能なドライバーを使用して、データベース接続を作成します。

> [!NOTE]  
> sqljdbc4.jar クラス ライブラリを使用する場合は、アプリケーションから Class.forName メソッドを使用してドライバーの登録または読み込みを明示的に行う必要はありません。 DriverManager クラスの getConnection メソッドが呼び出されると、登録されている一連の JDBC ドライバーから適切なドライバーが検出されます。 詳細については、「JDBC ドライバーの使用」を参照してください。

## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>SQLServerDriver クラスを使用した接続の作成

ドライバーの一覧で DriverManager 用に特定のドライバーを指定する必要がある場合は、次のように [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) クラスの [connect](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) メソッドを使用して、データベース接続を作成できます。

```java
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```

## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>SQLServerDataSource クラスを使用した接続の作成

[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスを使用して接続を作成する必要がある場合は、次のように、クラスのさまざまな setter メソッドを使用してから [getConnection](../../connect/jdbc/reference/getconnection-method.md) メソッドを呼び出すことができます。

```java
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```

## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>限定されたデータ ソースを対象とした接続の作成

限定されたデータ ソースを対象にデータベース接続を作成するには複数の方法があります。 それぞれの方法は、接続 URL を使用して設定するプロパティによって設定されます。

リモート サーバーの既定のインスタンスに接続するには、次の方法を使用します。

```java
String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"
```

サーバーの特定のポートに接続するには、次の方法を使用します。

```java
String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"
```

サーバーの名前付きインスタンスに接続するには、次の方法を使用します。

```java
String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"
```

サーバーの特定のデータベースに接続するには、次の方法を使用します。

```java
String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"
```

接続 URL の例については、「[接続 url を作成する](../../connect/jdbc/building-the-connection-url.md)」を参照してください。

## <a name="creating-a-connection-with-a-custom-login-time-out"></a>カスタムのログイン タイムアウトを持つ接続の作成

サーバーの負荷またはネットワーク トラフィックを調整する必要がある場合は、次のように、特定のログイン タイムアウト値を秒数で指定した接続を作成できます。

```java
String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"
```

## <a name="create-a-connection-with-application-level-identity"></a>アプリケーション レベルの ID を持つ接続の作成

ログとプロファイリングを使用する必要がある場合は、次のように、接続が特定のアプリケーションからのものであることを識別する必要があります。

```java
String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"
```

## <a name="closing-a-connection"></a>接続を閉じる

次のように、SQLServerConnection クラスの [close](../../connect/jdbc/reference/close-method-sqlserverconnection.md) メソッドを呼び出すことで、データベース接続を明示的に閉じることができます。

```java
con.close();
```

これにより、SQLServerConnection オブジェクトが使用しているデータベース リソースが解放されます。また、接続がプールされるシナリオでは、接続が接続プールに戻されます。

> [!NOTE]  
> また、close メソッドを呼び出すと、保留中のトランザクションもすべてロールバックされます。

## <a name="see-also"></a>参照

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
