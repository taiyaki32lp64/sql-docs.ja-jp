---
title: Kerberos 統合認証による SQL Server への接続 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2215e9f6b6c8cd0e19c220d16ebc7a1520550a42
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026190"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Kerberos 統合認証による SQL Server への接続

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 以降、アプリケーションは、**authenticationScheme** 接続プロパティを使用して、タイプ 4 の Kerberos 統合認証を使用してデータベースに接続することを示すことができます。 接続プロパティの詳細について[は、「接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。 Kerberos の詳細については、「 [Microsoft kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)」を参照してください。

Java **Krb5LoginModule** で統合認証を使用する場合、[Krb5LoginModule クラス](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)を使用してモジュールを構成できます。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、IBM Java VM 用に次のプロパティが設定されます。

- **useDefaultCcache = true**
- **moduleBanner = false**

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、他のすべての Java VM 用に次のプロパティが設定されます。

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Remarks

より前[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]のアプリケーションでは、統合認証 (使用可能なものに応じて Kerberos または NTLM を使用 **** します) を指定できます。そのためには、sqljdbc_auth を参照して**ください。** 「[接続 URL を作成する](../../connect/jdbc/building-the-connection-url.md)」を参照してください。

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 以降、アプリケーションは、**authenticationScheme** 接続プロパティを使用して、ピュア Java Kerberos 実装を使用した Kerberos 統合認証を使用してデータベースに接続することを示すことができます。

- **Krb5LoginModule**を使用して統合認証を使用する場合は、引き続き、Integrated **atedsecurity = true**接続プロパティを指定する必要があります。 次に、 **Authenticationscheme = JavaKerberos**接続プロパティも指定します。

- **Sqljdbc_auth**で統合認証を引き続き使用するには、[Integrated **atedsecurity = true** ] 接続プロパティ (および必要に応じて**authenticationscheme = [認証**]) を指定するだけです。

- **Authenticationscheme = JavaKerberos**を指定しても、を **** 指定しない場合、ドライバーは**authenticationscheme**接続プロパティを無視し、ユーザー名とパスワードが求められます。接続文字列の資格情報。

データソースを使用して接続を作成する場合、**setAuthenticationScheme** を使用して認証スキームをプログラムで設定できます。また、(必要に応じて) **setServerSpn** を使用して Kerberos 接続用の SPN を設定できます。

Kerberos 認証をサポートするために、新しいロガー com.microsoft.sqlserver.jdbc.internals.KerbAuthentication が追加されました。 詳細については、「[ドライバー操作のトレース](../../connect/jdbc/tracing-driver-operation.md)」をご覧ください。

Kerberos を構成する場合は、次のガイドラインに従ってください。

1. Windows のレジストリで**AllowTgtSessionKey**を1に設定します。 詳しくは、「[Kerberos protocol registry entries and KDC configuration keys in Windows Server 2003](https://support.microsoft.com/kb/837361)」(Windows Server 2003 における Kerberos プロトコルのレジストリ エントリおよび KDC 構成キー) をご覧ください。
2. Kerberos 構成 (UNIX 環境の krb5.conf) で環境の適切な領域および KDC が指定されていることを確認します。
3. kinit を使用するかまたはドメインにログインして、TGT キャッシュを初期化します。
4. **authenticationScheme=JavaKerberos** を使用するアプリケーションを Windows Vista または Windows 7 オペレーティング システムで実行する場合は、標準ユーザー アカウントを使用する必要があります。 ただし、管理者のアカウントでアプリケーションを実行する場合は、アプリケーションを管理者権限で実行する必要があります。

> [!NOTE]  
> serverSpn 接続属性は、Microsoft JDBC Driver 4.2 以降でのみサポートされています。

## <a name="service-principal-names"></a>サービス プリンシパル名

サービス プリンシパル名 (SPN) は、クライアントがサービスのインスタンスを一意に識別するための名前です。

**serverSpn** 接続プロパティを使用して SPN を指定できますが、ドライバーで自動的に作成することもできます (既定)。 このプロパティの形式は "MSSQLSvc/fqdn:port\@REALM" です。ここで、fqdn は完全修飾ドメイン名、port はポート番号、REALM は大文字で表記された SQL Server の Kerberos 領域です。 Kerberos 構成の既定の領域が、サーバーと同じ領域であり、既定で含まれていない場合には、このプロパティの領域部分は省略可能です。 ここで、Kerberos 構成で既定の領域がサーバーの領域とは異なる領域であり、その領域間の認証のシナリオをサポートする場合には、serverSpn プロパティを使用して SPN を設定する必要があります。

たとえば、SPN は次のようになります。 "MSSQLSvc/some-ZZZZ: 1433\@" のようになります。コーポレーション.CONTOSO.COM "

サービス プリンシパル名 (SPN) の詳細については、以下を参照してください。

- [SQL Server で Kerberos 認証を使用する方法](https://support.microsoft.com/kb/319723)

- [SQL Server での Kerberos の使用](https://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> JDBC driver の6.2 リリースより前のバージョンでは、クロス領域 Kerberos を適切に使用するために、 **Serverspn**を明示的に設定する必要があります。
>
> 6\.2 リリースの時点で、クロス領域 Kerberos を使用している場合でも、ドライバーは既定で**Serverspn**を構築できます。 **Serverspn**を明示的に使用することもできます。

## <a name="creating-a-login-module-configuration-file"></a>ログイン モジュール構成ファイルの作成

オプションで Kerberos 構成ファイルを指定できます。 構成ファイルを指定しない場合、次の設定が有効になります。

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

ログイン モジュール構成ファイルを作成する場合は、次の形式に従ってファイルを作成する必要があります。

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

ログイン構成ファイルは、特定の 1 つまたは複数のアプリケーションに使用する基底の認証テクノロジを指定する 1 つ以上のエントリから構成されます。 例を次に示します。

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

このように、それぞれのログイン モジュール構成ファイル エントリは、名前と、それに続く、(それぞれがセミコロンで終了し、グループ全体が中かっこで囲まれた) 1 つまたは複数のログイン モジュール固有のエントリから構成されます。 それぞれの構成ファイル エントリはセミコロンで終了します。

ドライバーは、ログイン モジュール構成ファイルに指定された設定を使用して Kerberos 資格情報を取得できることに加え、既存の資格情報を使用できます。 これは、アプリケーションでユーザーの資格情報を複数使用して接続を作成する必要がある場合に便利です。

ドライバーは、指定されたログイン モジュールを使用してログインを試行する前に、既存の資格情報を使用できる場合はそれを使用します。 したがって、特定のコンテキストで `Subject.doAs` メソッドを使用してコードを実行した場合、`Subject.doAs` 呼び出しに渡された資格情報を使用して接続が作成されます。

詳しくは、「[JAAS Login Configuration File](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html)」(JAAS ログイン構成ファイル) および「[Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)」(Krb5LoginModule クラス) をご覧ください。

Microsoft JDBC Driver 6.2 以降では、必要に応じて、接続プロパティ`jaasConfigurationName`を使用してログインモジュール構成ファイルの名前を渡すことができます。これにより、各接続が独自のログイン構成を持つことができます。

## <a name="creating-a-kerberos-configuration-file"></a>Kerberos 構成ファイルの作成

Kerberos の構成ファイルについて詳しくは、「[Kerberos Requirements](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)」(Kerberos の要件) をご覧ください。

サンプル ドメイン構成ファイルの例を次に示します。ここで、YYYY および ZZZZ は、ドメイン名です。

```ini
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  

[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  

[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  

        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  

```

## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>ドメイン構成ファイルおよびログイン モジュール構成ファイルの有効化

ドメイン構成ファイルを有効にするには、-Djava.security.krb5.conf を使用します。 **-Djava. auth. .config**を使用して、ログインモジュール構成ファイルを有効にすることができます。

たとえば、次のコマンドを使用してアプリケーションを起動できます。

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Kerberos を介して SQL Server にアクセスできることを確認する

SQL Server Management Studio で次のクエリを実行します。

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

このクエリを実行するために必要な権限があることを確認してください。

## <a name="constrained-delegation"></a>制約付き委任

Microsoft JDBC Driver 6.2 以降では、このドライバーは Kerberos の制約付き委任をサポートしています。 委任された資格情報は、GSSCredential オブジェクトとして渡すことができます。これらの資格情報は、接続を確立するためにドライバーによって使用されます。

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>プリンシパル名とパスワードを使用した Kerberos 接続

Microsoft JDBC Driver 6.2 以降では、ドライバーは接続文字列で渡されたプリンシパル名とパスワードを使用して Kerberos 接続を確立できます。

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

ユーザーが krb5.conf ファイルの default_realm セットに属している場合、username プロパティには領域は必要ありません。 `userName` `integratedSecurity=true;`とがおよびプロパティと共に設定されている場合、接続は、指定されたパスワードと共に、Kerberosプリンシパルとしてのユーザー名の値を使用して確立されます。`password` `authenticationScheme=JavaKerberos;`

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>同じドメインの Unix マシンからの Kerberos 認証の使用

このガイドは、動作中の Kerberos セットアップが既に存在することを前提としています。 Kerberos 認証を使用して Windows コンピューターで次のコードを実行し、前述のが true であるかどうかを確認します。 成功した場合、コードは "認証方式: KERBEROS" をコンソールに出力します。 追加の実行時フラグ、依存関係、またはドライバー設定は、提供されたもの以外には必要ありません。 同じコードブロックを Linux で実行して、接続が成功したかどうかを確認できます。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. ドメインクライアントコンピューターをサーバーと同じドメインに参加させます。
2. Optional既定の Kerberos チケットの場所を設定します。 これは、環境変数を設定する`KRB5CCNAME`ことによって最も簡単に行うことができます。
3. 新しい kerberos チケットを生成するか、または既存のものを既定の Kerberos チケットの場所に配置することによって、Kerberos チケットを取得します。 チケットを生成するには、単にターミナルを使用して`kinit USER@DOMAIN.AD` 、"USER" と "DOMAIN" でチケットを初期化します。AD "は、それぞれプリンシパルとドメインです。 例: `kinit SQL_SERVER_USER03@MICROSOFT.COM`。 チケットは、既定のチケットの場所、または設定さ`KRB5CCNAME`れている場合はパスに生成されます。
4. ターミナルでパスワードの入力を求められたら、パスワードを入力します。
5. で`klist`チケットの資格情報を確認し、資格情報が認証に使用するものであることを確認します。
6. 上記のサンプルコードを実行し、Kerberos 認証が成功したことを確認します。

## <a name="see-also"></a>参照

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
