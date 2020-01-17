---
title: 接続 URL を作成する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18ed8477e6fc7c276db1842dba4f8856629bd29a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028451"
---
# <a name="building-the-connection-url"></a>接続 URL の構築
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  接続 URL の一般的な書式は次のとおりです。  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 それぞれの文字の説明は次のとおりです。  
  
-   **jdbc:sqlserver://** (必須) は、サブプロトコルであり定数です。  
  
-   **serverName** (省略可能) は、接続先のサーバーのアドレスです。 接続先のサーバーのアドレスには DNS または IP アドレスを指定するか、またはローカル コンピューターを表す localhost あるいは 127.0.0.1 を指定できます。 接続 URL で指定されていない場合、プロパティのコレクションでサーバー名を指定する必要があります。  
  
-   **instanceName** (省略可能) は、serverName 上にある接続先のインスタンスです。 指定しない場合、既定のインスタンスへの接続が確立されます。  
  
-   **portNumber** (省略可能) は、serverName 上にある接続先のポートです。 既定では 1433 です。 既定のポートを使用する場合は、URL でポートおよびその前の ':' を指定する必要はありません。  
  
    > [!NOTE]  
    >  最適な接続パフォーマンスのために、名前付きインスタンスに接続するときは portNumber を設定します。 こうすることにより、ポート番号を決定するためのサーバーへのラウンド トリップが回避されます。 portNumber および instanceName の両方が使用されている場合、portNumber が優先され、instanceName は無視されます。  
  
-   **property** (省略可能) は、1 つ以上の接続プロパティ オプションです。 詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。 リストに含まれる任意のプロパティを指定できます。 プロパティを区切るには必ずセミコロン (';') を使用します。またプロパティを重複して指定することはできません。  
  
> [!CAUTION]  
>  セキュリティ上の理由から、ユーザー入力に基づく接続 URL の作成は避ける必要があります。 URL では、サーバー名とドライバーだけを指定するようにします。 ユーザー名とパスワードの値には、接続プロパティのコレクションを使用します。 JDBC アプリケーションのセキュリティの詳細については、「 [jdbc driver アプリケーション](../../connect/jdbc/securing-jdbc-driver-applications.md)のセキュリティ保護」を参照してください。  
  
## <a name="connection-examples"></a>接続の例  
 ユーザー名とパスワードを使用して、ローカル コンピューター上の既定のデータベースに接続します。  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  前の例では接続文字列でユーザー名とパスワードを使用していますが、より安全な統合セキュリティを使用する必要があります。 詳細については、後の「[Windows 上で統合認証を使用する接続](#Connectingintegrated)」セクションを参照してください。  
  
 次の接続文字列は、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] でサポートされている任意のオペレーティング システム上で実行中のアプリケーションから統合認証および Kerberos を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続する方法の例を示しています。  
  
```java
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 統合認証を使用して、ローカル コンピューター上の既定のデータベースに接続します。  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 リモート サーバー上の名前付きデータベースに接続します。  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 既定のポートでリモート サーバーに接続します。  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 カスタマイズされたアプリケーション名を指定して接続します。  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>名前付きおよび複数の SQL Server インスタンス  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サーバーごとに複数のデータベース インスタンスをインストールできます。 各インスタンスは個別の名前によって識別されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスに接続するには、名前付きインスタンスのポート番号を指定するか (推奨)、またはインスタンス名を JDBC URL プロパティまたは **datasource** プロパティとして指定することができます。 インスタンス名またはポート番号のプロパティを指定しない場合は、既定のインスタンスへの接続が作成されます。 次の例を参照してください。  
  
 ポート番号を使用するには、次のように指定します。  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 JDBC URL プロパティを使用するには、次のように指定します。  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>接続 URL での値のエスケープ  
 スペース、セミコロン、引用符などの特殊文字を挿入するため、接続 URL の値の特定部分のエスケープが必要になる場合があります。 JDBC ドライバーでは、エスケープする文字を中かっこで囲みます。 たとえば、{;} とするとセミコロンがエスケープされます。  
  
 エスケープする値には特殊文字 (特に '='、';'、'[]'、およびスペース) を含めることができますが、中かっこはエスケープできません。 エスケープが必要な値に中かっこが含まれる場合は、プロパティのコレクションに加える必要があります。  
  
> [!NOTE]  
>  中かっこ内の空白はリテラルでありトリミングされません。  
  
##  <a name="Connectingintegrated"></a> Windows 上で統合認証を使用する接続  
 JDBC ドライバーでは、integratedSecurity 接続文字列プロパティを通じて、Windows オペレーティング システム上でのタイプ 2 の統合認証の使用がサポートされています。 統合認証を使用するには、JDBC ドライバーがインストールされているコンピューターの Windows システム パス上のディレクトリに sqljdbc_auth.dll ファイルをコピーします。  
  
 sqljdbc_auth.dll ファイルは次の場所にインストールされています。  
  
 \<"*インストール ディレクトリ*">\sqljdbc_\<"*バージョン*">\\<"*言語*">\auth\  
  
 でサポートされ[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]ているすべてのオペレーティングシステムについては、「 [Kerberos 統合認証を使用して SQL Server に接続する](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)」を参照して、アプリケーションが統合を使用してデータベースに接続できるようにするに[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]追加された機能について説明します。種類が4の Kerberos の認証。  
  
> [!NOTE]  
>  32 ビットの Java 仮想マシン (JVM) を実行している場合は、オペレーティング システムのバージョンが x64 であっても、x86 フォルダーの sqljdbc_auth.dll ファイルを使用してください。 64 ビットの JVM を x64 プロセッサ上で実行している場合は、x64 フォルダーの sqljdbc_auth.dll ファイルを使用してください。  
  
 または、java.library.path システム プロパティを設定して sqljdbc_auth.dll のディレクトリを指定することもできます。 たとえば、JDBC ドライバーが既定のディレクトリにインストールされている場合、Java アプリケーションの起動時に次の仮想マシン (VM) 引数を使用することで、DLL の場所を指定できます。  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>IPv6 アドレスによる接続  
 JDBC ドライバーでは、接続プロパティのコレクション、および serverName 接続文字列プロパティと合わせて IPv6 アドレスを使用できます。 jdbc:*sqlserver*://*serverName* など、serverName の初期値は、接続文字列内の IPv6 アドレスをサポートしていません。 あらゆる接続で、そのままの IPv6 アドレスの代わりに *serverName* の名前を使用できます。 詳細を次の例に示します。  
  
 **serverName プロパティを使用するには**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **プロパティのコレクションを使用するには**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
