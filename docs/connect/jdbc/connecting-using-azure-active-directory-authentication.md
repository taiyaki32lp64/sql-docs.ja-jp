---
title: Azure Active Directory 認証を利用した接続 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028120"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Azure Active Directory 認証を利用した接続

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、Microsoft JDBC Driver for SQL Server と共に Azure Active Directory 認証機能を使用する Java アプリケーションを開発する方法について説明します。

Azure Active Directory で id を使用して Azure SQL Database v12 に接続するメカニズムである Azure Active Directory (AAD) 認証を使用できます。 Azure Active Directory 認証は、データベース ユーザーの ID を一元管理するという目的で使用でき、SQL Server 認証に代わる方法となります。 JDBC ドライバーを使用すると、JDBC 接続文字列で Azure Active Directory 資格情報を指定して Azure SQL DB に接続できます。 Azure Active Directory 認証を構成する方法の詳細については[Azure Active Directory 認証を使用した SQL Database への接続](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)」を参照してください。 

Microsoft JDBC Driver for SQL Server での Azure Active Directory 認証をサポートする接続プロパティは次のとおりです。
*   **認証**: このプロパティを使用して、接続に使用する SQL 認証方法を指定します。 有効な値は次のとおりです。 
    * **ActiveDirectoryMSI**
        * ドライバーバージョン version **7.2**以降でサポート`authentication=ActiveDirectoryMSI`されています。これは、"Identity" サポートが有効になっている Azure リソース内から Azure SQL Database/データウェアハウスに接続するために使用できます。 必要に応じて、接続/データソースのプロパティで**msiClientId**を指定することもできます。この認証モードには、確立のために**accessToken**を取得するために使用されるマネージドサービス ID のクライアント ID が含まれている必要があります。接続です。
    * **ActiveDirectoryIntegrated**
        * ドライバーバージョン **v2.0** 以降でサポートさ`authentication=ActiveDirectoryIntegrated`れているは、統合認証を使用して Azure SQL Database/データウェアハウスに接続するために使用できます。 この認証モードを使用するには、オンプレミスの Active Directory フェデレーションサービス (AD FS) (ADFS) をクラウドで Azure Active Directory とフェデレーションする必要があります。 セットアップが完了したら、ネイティブライブラリ "sqljdbc_auth" を Windows OS のアプリケーションクラスパスに追加するか、クロスプラットフォーム認証をサポートするための Kerberos チケットを設定して接続できます。 ドメインに参加しているコンピューターにログインしているときに資格情報の入力を求められることなく、Azure SQL DB/DW にアクセスできるようになります。
    * **ActiveDirectoryPassword**
        * ドライバーバージョン **v2.0** 以降でサポートさ`authentication=ActiveDirectoryPassword`れているは、Azure AD プリンシパル名とパスワードを使用して、Azure SQL Database/データウェアハウスに接続するために使用できます。
    * **SqlPassword**
        * ユーザー `authentication=SqlPassword`名/ユーザーとパスワードのプロパティを使用して SQL Server に接続するには、を使用します。
    * **NotSpecified**
        * これらの認証方法が不要な場合は、既定値のままにしておきます。`authentication=NotSpecified`

*   **accessToken**: この接続プロパティを使用して、アクセストークンを使用して SQL Database に接続します。 accessToken は、DriverManager クラスの getConnection () メソッドの Properties パラメーターを使用してのみ設定できます。 接続 URL では使用できません。  

詳細については、[[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)] ページの [認証] プロパティを参照してください。  


## <a name="client-setup-requirements"></a>クライアントセットアップの要件
**ActiveDirectoryMSI**認証の場合は、次のコンポーネントをクライアントコンピューターにインストールする必要があります。
* Java 8 以上
* SQL Server 用 Microsoft JDBC Driver 7.2 (またはそれ以降)
* クライアント環境は Azure リソースである必要があり、"Id" 機能のサポートが有効になっている必要があります。
* Azure リソースのシステム割り当て済みマネージド Id またはユーザー割り当て済みマネージド Id、または MSI が属しているグループのいずれかを表す包含データベースユーザーは、ターゲットデータベースに存在し、CONNECT 権限を持っている必要があります。

その他の認証モードの場合は、次のコンポーネントをクライアントコンピューターにインストールする必要があります。
* Java 7 以降
* SQL Server 用 Microsoft JDBC Driver 6.0 (またはそれ以降)
* アクセストークンベースの認証モードを使用している場合は、この記事の例を実行するために、 [azure-activedirectory-library-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)とその依存関係が必要です。 詳細については、「**アクセストークンを使用した接続**」を参照してください。
* **ActiveDirectoryPassword**認証モードを使用している場合は、 [java](https://github.com/AzureAD/azure-activedirectory-library-for-java)とその依存関係が必要です。 詳細については、「 **ActiveDirectoryPassword 認証モードを使用した接続**」を参照してください。
* **ActiveDirectoryIntegrated**モードを使用している場合は、java とその依存関係が必要です。 詳細については、「 **ActiveDirectoryIntegrated 認証モードを使用した接続**」を参照してください。

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>ActiveDirectoryMSI 認証モードを使用した接続
次の例では、`authentication=ActiveDirectoryMSI` モードの使用方法を示します。 この例は、Azure リソースの内部から実行するか、Azure の仮想マシン、App Service、または Azure Active Directory とフェデレーションされている Function App を実行します。

この例を実行する前に、次の行のサーバー/データベース名を実際のサーバー名またはデータベース名に置き換えます。

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

ActiveDirectoryMSI 認証モードを使用する例を次に示します。

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Azure 仮想マシンでこの例を実行すると、_システム割り当て済みマネージド id_または_ユーザー割り当て済みマネージド id_からアクセストークンをフェッチし ( **msiClientId**が指定されている場合)、フェッチしたアクセスを使用して接続を確立します。token. 接続が確立されると、次のメッセージが表示されます。

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>ActiveDirectoryIntegrated 認証モードを使用した接続
バージョン6.4 では、Microsoft JDBC Driver によって、複数のプラットフォーム (Windows、Linux、および macOS) で Kerberos チケットを使用した ActiveDirectoryIntegrated 認証のサポートが追加されています。
詳細については、 [Windows、Linux、および Mac での Kerberos チケットの設定](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)に関する詳細を参照してください。 また、Windows では、JDBC ドライバーを使用した ActiveDirectoryIntegrated 認証に sqljdbc_auth を使用することもできます。

> [!NOTE]
>  古いバージョンのドライバーを使用している場合は、この認証モードを使用するために必要な依存関係について、この[リンク](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)を確認してください。 

次の例では、`authentication=ActiveDirectoryIntegrated` モードの使用方法を示します。 Azure Active Directory とフェデレーションされているドメインに参加しているコンピューターで、この例を実行します。 Azure AD プリンシパルを表す包含データベースユーザー、または属しているグループの1つがデータベースに存在し、CONNECT 権限を持っている必要があります。 

この例をビルドして実行する前に、(例を実行する) クライアントコンピューターで、 [azure-activedirectory-ライブラリライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java)とその依存関係をダウンロードし、java ビルドパスに含めます。

この例を実行する前に、次の行のサーバー/データベース名を実際のサーバー名またはデータベース名に置き換えます。

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

ActiveDirectoryIntegrated 認証モードを使用する例を次に示します。
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

クライアントコンピューターでこの例を実行すると、Kerberos チケットが自動的に使用され、パスワードは必要ありません。 接続が確立されると、次のメッセージが表示されます。

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Windows、Linux、Mac で Kerberos チケットを設定する

現在のユーザーを Windows ドメインアカウントにリンクする Kerberos チケットを設定する必要があります。 主要な手順の概要を以下に示します。

#### <a name="windows"></a>Windows
JDK には`kinit`が付属しています。これを使用すると、Azure Active Directory とフェデレーションされているドメインに参加しているコンピューター上のキー配布センター (KDC) から TGT を取得できます。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>手順 1: チケット交付チケットの取得
- **実行**: Windows
- **アクション**:
  - コマンド`kinit username@DOMAIN.COMPANY.COM`を使用して KDC から TGT を取得すると、ドメインパスワードの入力を求めるメッセージが表示されます。
  - 使用`klist`可能なチケットを表示するには、を使用します。 Kinit が正常に実行された場合は、krbtgt/DOMAIN. COMPANY .COM @ DOMAIN.COMPANY.COM のチケットが表示されます。

> [!NOTE]
>  アプリケーションで KDC を検索する`.ini`ために`-Djava.security.krb5.conf` 、でファイルを指定することが必要になる場合があります。

#### <a name="linux-and-mac"></a>Linux と Mac

##### <a name="requirements"></a>必要条件
Kerberos ドメイン コントローラーのクエリを実行するための、Windows ドメインに参加しているコンピューターへのアクセス権。

##### <a name="step-1-find-kerberos-kdc"></a>手順 1: Kerberos KDC を検索する
- データベース参照または接続を選択して**実行**Windows コマンドライン
- **Action**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` ("DOMAIN.COMPANY.COM" がドメインの名前にマップされる)
- **サンプル出力**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **抽出する情報**DC 名 (この場合は)`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>手順 2: krb5.conf で KDC を構成する
- データベース参照または接続を選択して**実行**Linux または Mac
- **アクション**: 任意のエディターで/Etc/krb5.conf を編集します。 次のキーを構成します。
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  次に、krb5.conf ファイルを保存して終了します。

> [!NOTE]
>  ドメインはすべて大文字にする必要があります。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>手順 3: チケット保証チケットの取得をテストする
- データベース参照または接続を選択して**実行**Linux または Mac
- **アクション**:
  - コマンド`kinit username@DOMAIN.COMPANY.COM`を使用して KDC から TGT を取得すると、ドメインパスワードの入力を求めるメッセージが表示されます。
  - 使用`klist`可能なチケットを表示するには、を使用します。 Kinit が正常に実行された場合は、krbtgt/DOMAIN. COMPANY .COM @ DOMAIN.COMPANY.COM のチケットが表示されます。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>ActiveDirectoryPassword 認証モードを使用した接続
次の例では、`authentication=ActiveDirectoryPassword` モードの使用方法を示します。

例をビルドして実行する前に、次のようにします。
1.  (例を実行する) クライアントコンピューターで、 [azure-activedirectory-ライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java)とその依存関係をダウンロードして、java ビルドパスに含めます (例:)。
2.  次のコード行を見つけて、サーバー/データベース名を実際のサーバー名またはデータベース名に置き換えます。
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  次のコード行を見つけて、ユーザー名を、接続する AAD ユーザーの名前に置き換えます。
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

ActiveDirectoryPassword 認証モードを使用する例を次に示します。
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
接続が確立されると、次のメッセージが出力として表示されます。
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含ユーザーデータベースが存在し、指定された Azure AD ユーザーまたはグループの1つを表す包含データベースユーザーが存在する必要があります。また、指定した Azure AD ユーザーが属していて、データベースに存在する必要があり、CONNECT 権限を持っている必要があります (を除き Azure Active Directoryサーバー管理者またはグループ)

## <a name="connecting-using-access-token"></a>アクセストークンを使用した接続
アプリケーション/サービスは、Azure Active Directory からアクセストークンを取得し、それを使用して Azure SQL Database/データウェアハウスに接続できます。

> [!NOTE] 
> **accessToken**は、drivermanager クラスの getconnection () メソッドの Properties パラメーターを使用してのみ設定できます。 接続文字列では使用できません。

次の例には、アクセストークンベースの認証を使用して Azure SQL Database/データウェアハウスに接続する単純な Java アプリケーションが含まれています。 例をビルドして実行する前に、次の手順を実行します。
1.  サービスの Azure Active Directory でアプリケーションアカウントを作成します。
    1. Azure portal にサインインします。
    2. 左側のナビゲーションにある [Azure Active Directory] をクリックします。
    3. [アプリの登録] タブをクリックします。
    4. ドロワーで、[新しいアプリケーションの登録] をクリックします。
    5. アプリケーションのフレンドリ名として「mytokentest」と入力し、[Web アプリ/API] を選択します。
    6. サインオン URL は必要ありません。 何も指定します。 "https://mytokentest" 。
    7. 下部にある [作成] をクリックします。
    9. Azure portal のままで、アプリケーションの [設定] タブをクリックし、[プロパティ] タブを開きます。
    10. "アプリケーション ID" (クライアント ID) の値を探してコピーします。後でアプリケーションを構成するときに必要になります (たとえば、1846943b-ad04-4808-aa13-4702d908b5c1)。 次のスナップショットを参照してください。
    11. [キー] セクションで、[名前] フィールドに入力し、キーの期間を選択して構成を保存することで、キーを作成します (値フィールドは空のままにします)。 保存した後、[値] フィールドを自動的に入力し、生成された値をコピーします。 これがクライアント シークレットです。
    12. 左側のパネルで [Azure Active Directory] をクリックします。 [アプリの登録] の下で、[エンドポイント] タブを見つけます。"OATH 2.0 トークンエンドポイント" の URL をコピーします。これは STS URL です。
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Azure SQL Server のユーザーデータベースに Azure Active Directory 管理者としてサインインし、T-sql コマンドを使用して、アプリケーションプリンシパルの包含データベースユーザーをプロビジョニングします。 詳細については、Azure Active Directory 管理者と包含データベースユーザーを作成する方法の詳細については、「 [Azure Active Directory 認証を使用した SQL Database または SQL Data Warehouse への接続](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)」を参照してください。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  (例を実行する) クライアントコンピューターで、 [azure-activedirectory-ライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java)ライブラリとその依存関係をダウンロードし、それらを java ビルドパスに含めておきます。 この特定の例を実行するために必要なのは、azure-activedirectory-java だけです。 この例では、このライブラリの Api を使用して、Azure AAD からアクセストークンを取得します。 アクセストークンを既に持っている場合は、この手順を省略できます。 また、アクセストークンを取得する例のセクションも削除する必要があることに注意してください。

次の例では、STS URL、クライアント ID、クライアントシークレット、サーバー、データベース名を実際の値に置き換えます。

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

接続に成功すると、次のメッセージが出力として表示されます。

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
