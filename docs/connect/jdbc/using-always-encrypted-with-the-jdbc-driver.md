---
title: JDBC driver での Always Encrypted の使用 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31f81cb2e12360956d14d1706b119233add94a35
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594090"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>JDBC ドライバーでの Always Encrypted の使用
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

このページでは、 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)と Microsoft JDBC Driver 6.0 (またはそれ以降) を使用して SQL Server の Java アプリケーションを開発する方法について説明します。

Always Encrypted を使用すると、クライアントは SQL Server または Azure SQL データベースにデータまたは暗号化キーを開示することなく、機密データを暗号化することができます。 Microsoft JDBC Driver 6.0 for SQL Server 以降など、Always Encrypted が有効のドライバーは、クライアント アプリケーション内の機密データを透過的に暗号化および暗号化解除することで、この動作を実行します。 ドライバーは、どのクエリパラメーターが Always Encrypted データベースの列に対応しているかを自動的に判断し、それらのパラメーターの値を暗号化して SQL Server または Azure SQL Database に送信します。 同様に、ドライバーは、クエリ結果内の暗号化されたデータベース列から取得されたデータを透過的に暗号化解除します。 詳細については、JDBC driver の[Always Encrypted (データベースエンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)と[Always Encrypted API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)に関する説明を参照してください。

## <a name="prerequisites"></a>Prerequisites
- SQL Server の Microsoft JDBC Driver 6.0 (またはそれ以降) が開発用コンピューターにインストールされていることを確認します。 
- Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files (JCE 管轄ポリシーファイル (無制限強度)) をダウンロードしてインストールします。  インストール手順、および考えられるエクスポート/インポート問題に関する詳細について、zip ファイルに含まれる Readme を必ず読んでください。  

    - mssql-jdbc-X.X.X.jre7.jar または sqljdbc41.jar を使用している場合は、[Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 7 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html) からポリシー ファイルをダウンロードできます。

    - mssql-jdbc-X.X.X.jre8.jar または sqljdbc42.jar を使用している場合は、[Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) からポリシー ファイルをダウンロードできます。

    - Mssql-jdbc-X を使用している場合は、ポリシーファイルをダウンロードする必要はありません。 Java 9 の管轄ポリシーは、既定で無制限の強度の暗号化を行います。

## <a name="working-with-column-master-key-stores"></a>列マスター キー ストアを操作する
暗号化された列のデータを暗号化または暗号化解除するために、SQL Server は列の暗号化キーを保持します。 列暗号化キーは、データベースのメタデータに暗号化された形式で格納されています。 各列暗号化キーには、列暗号化キーの暗号化に使用された対応する列マスター キーが含まれます。 データベースのメタデータには、列のマスターキーが含まれていません。 これらのキーはクライアントによってのみ保持されます。 ただし、データベースのメタデータには、クライアントに対して相対的に列マスターキーが格納されている場所に関する情報が含まれます。 たとえば、データベースのメタデータは、列マスターキーを保持するキーストアが Windows 証明書ストアであり、暗号化と復号化に使用される特定の証明書が Windows 証明書ストア内の特定のパスにあることを示している場合があります。 クライアントが Windows 証明書ストア内の証明書にアクセスできる場合は、証明書を取得できます。 その後、証明書を使用して、列暗号化キーの暗号化を解除できます。 その後、その暗号化キーを使用して、その列暗号化キーを使用する暗号化された列のデータの暗号化解除または暗号化を行うことができます。

Microsoft JDBC Driver for SQL Server は、 **, string,** から派生したクラスのインスタンスである列マスターキーストアプロバイダーを使用してキーストアと通信します。

### <a name="using-built-in-column-master-key-store-providers"></a>組み込み列マスター キー ストア プロバイダーを使用する
Microsoft JDBC Driver for SQL Server には、次の組み込み列マスターキーストアプロバイダーが付属しています。 これらのプロバイダーの一部は、(プロバイダーの検索に使用される) 特定のプロバイダー名に事前登録されています。また、追加の資格情報または明示的な登録が必要なものもあります。

| クラス                                                 | [説明]                                        | プロバイダー (検索) 名  | 事前登録されていますか? |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Azure Key Vault のキーストアのプロバイダー。 | AZURE_KEY_VAULT         | いいえ                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Windows 証明書ストアのプロバイダー。      | MSSQL_CERTIFICATE_STORE | はい                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Java キーストアのプロバイダー                   | MSSQL_JAVA_KEYSTORE     | はい                |

事前登録されたキーストアプロバイダーの場合、これらのプロバイダーを使用するためにアプリケーションコードを変更する必要はありませんが、次の項目に注意してください。

- ユーザー (またはデータベース管理者) は、列マスター キーのメタデータで構成されているプロバイダー名が正しいこと、および列マスター キー パスが、特定のプロバイダーに対して有効なキー パス形式に準拠していることを確認する必要があります。 CREATE COLUMN MASTER KEY (Transact-SQL) ステートメントを発行する際に有効なプロバイダー名とキー パスを自動的に生成する、SQL Server Management Studio などのツールを使用してキーを構成することをお勧めします。
- アプリケーションがキー ストア内のキーにアクセスできることを確認します。 このタスクには、キーストアに応じてキーまたはキー ストアへのアクセスをアプリケーションに許可したり、その他のキー ストア固有の構成手順を行ったりするプロセスが含まれる場合があります。 たとえば、SQLServerColumnEncryptionJavaKeyStoreProvider を使用する場合は、接続プロパティでキーストアの場所とパスワードを指定する必要があります。 

これらのキーストアプロバイダーについては、以降のセクションで詳しく説明します。 Always Encrypted を使用するには、キーストアプロバイダーを1つだけ実装する必要があります。

### <a name="using-azure-key-vault-provider"></a>Azure Key Vault プロバイダーを使用する
Azure Key Vault は、特にアプリケーションが Azure でホストされている場合、Always Encrypted の列マスター キーの格納と管理に便利なオプションです。 Microsoft JDBC Driver for SQL Server には、Azure Key Vault にキーが格納されているアプリケーション用の組み込みプロバイダー SQLServerColumnEncryptionAzureKeyVaultProvider が含まれています。 このプロバイダーの名前は AZURE_KEY_VAULT。 Azure Key Vault ストアプロバイダーを使用するには、アプリケーション開発者が Azure Key Vault でコンテナーとキーを作成し、Azure Active Directory でアプリの登録を作成する必要があります。 登録されたアプリケーションには、Always Encrypted で使用するために作成されたキーコンテナーに対して定義されているアクセスポリシーで、Get、Encrypt、Encrypt、Wrap キー、Wrap キー、および Verify アクセス許可が付与されている必要があります。 キーコンテナーを設定し、列マスターキーを作成する方法の詳細については、「 [Azure Key Vault-](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)ステップバイステップ」と「 [Azure Key Vault での列マスターキーの作成](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)」を参照してください。

このページの例では、SQL Server Management Studio を使用して Azure Key Vault ベースの列マスターキーと列暗号化キーを作成した場合、それらを再作成する T-sql スクリプトは、次の例のように、独自の特定の**KEY_PATH**および**ENCRYPTED_VALUE**を使用して作成することができます。

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

Azure Key Vault を使用するには、クライアントアプリケーションで SQLServerColumnEncryptionAzureKeyVaultProvider をインスタンス化し、ドライバーに登録する必要があります。

SQLServerColumnEncryptionAzureKeyVaultProvider を初期化する例を次に示します。  

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID**は、Azure Active Directory インスタンスのアプリ登録のアプリケーション ID です。 **clientkey**は、そのアプリケーションに登録されているキーパスワードであり、Azure Key Vault への API アクセスを提供します。

アプリケーションで SQLServerColumnEncryptionAzureKeyVaultProvider のインスタンスを作成した後、アプリケーションは SQLServerConnection () メソッドを使用して、インスタンスをドライバーに登録する必要があります。 インスタンスは、既定のルックアップ名 AZURE_KEY_VAULT を使用して登録することを強くお勧めします。この名前は、SQLServerColumnEncryptionAzureKeyVaultProvider () API を呼び出すことによって取得できます。 既定の名前を使用すると、SQL Server Management Studio や PowerShell などのツールを使用して Always Encrypted キーをプロビジョニングして管理することができます (ツールでは、既定の名前を使用してメタデータオブジェクトを列マスターキーに生成します)。 次の例は、Azure Key Vault プロバイダーの登録を示しています。 SQLServerConnection () メソッドの詳細については、「 [JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)」を参照してください。

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Azure Key Vault キーストアプロバイダーを使用する場合、JDBC ドライバーの Azure Key Vault 実装には、アプリケーションに含める必要があるこれらのライブラリ (GitHub から) に依存しています。
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-ライブラリ-java ライブラリ](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> これらの依存関係を Maven プロジェクトに含める方法の例については、「 [Apache Maven を使用した ADAL4J と AKV の依存関係のダウンロード](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)」を参照してください。

### <a name="using-windows-certificate-store-provider"></a>Windows 証明書ストア プロバイダーの使用
SQLServerColumnEncryptionCertificateStoreProvider は、列マスター キーを Windows 証明書ストアに格納するために使用できます。 データベースに列マスターキーと列暗号化キーの定義を作成するには、SQL Server Management Studio (SSMS) Always Encrypted ウィザードまたはその他のサポートされているツールを使用します。 同じウィザードを使用して、Windows 証明書ストアに自己署名証明書を生成し、Always Encrypted データの列マスターキーとして使用することができます。 列マスターキーと列暗号化キーの T-sql 構文の詳細については、「列[マスターキーの作成](../../t-sql/statements/create-column-master-key-transact-sql.md)」および「[列暗号化キーの作成](../../t-sql/statements/create-column-encryption-key-transact-sql.md)」を参照してください。

SQLServerColumnEncryptionCertificateStoreProvider の名前は MSSQL_CERTIFICATE_STORE であり、プロバイダーオブジェクトの getName () API によってクエリを実行できます。 これはドライバーによって自動的に登録され、アプリケーションを変更することなくシームレスに使用できます。

このページの例では、SQL Server Management Studio を使用して Windows 証明書ストアベースの列マスターキーと列暗号化キーを作成した場合、T-sql スクリプトを再作成するには、次の例のように、独自の**KEY_PATH**と**ENCRYPTED_VALUE**を使用します。

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> この記事の他のキーストアプロバイダーは、ドライバーでサポートされているすべてのプラットフォームで利用できますが、JDBC ドライバーの SQLServerColumnEncryptionCertificateStoreProvider 実装は、Windows オペレーティングシステムでのみ使用できます。 このファイルは、ドライバーパッケージで使用可能な sqljdbc_auth に依存しています。 このプロバイダーを使用するには、JDBC ドライバーがインストールされているコンピューターの Windows システム パス上のディレクトリに sqljdbc_auth.dll ファイルをコピーします。 または、java.library.path システム プロパティを設定して sqljdbc_auth.dll のディレクトリを指定することもできます。 32 ビットの Java 仮想マシン (JVM) を実行している場合は、オペレーティング システムのバージョンが x64 であっても、x86 フォルダーの sqljdbc_auth.dll ファイルを使用してください。 64 ビットの JVM を x64 プロセッサ上で実行している場合は、x64 フォルダーの sqljdbc_auth.dll ファイルを使用してください。 たとえば、32 ビットの JVM を使用していて、JDBC ドライバーが既定のディレクトリにインストールされている場合、Java アプリケーションの起動時に次の仮想マシン (VM) 引数を使用することで、DLL の場所を指定できます。`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Java キーストアプロバイダーの使用
JDBC ドライバーには、Java キー ストアの組み込みキー ストア プロバイダー実装が含まれています。 接続文字列に**keyStoreAuthentication**接続文字列プロパティが存在し、それが "JavaKeyStorePassword" に設定されている場合、ドライバーは自動的に Java キーストアのプロバイダーをインスタンス化して登録します。 Java キーストアプロバイダーの名前は MSSQL_JAVA_KEYSTORE。 この名前は、SQLServerColumnEncryptionJavaKeyStoreProvider () API を使用して照会することもできます。 

クライアントアプリケーションが Java キーストアに対する認証に必要な資格情報を指定できる接続文字列プロパティは3つあります。 ドライバーは、接続文字列のこれら3つのプロパティの値に基づいて、プロバイダーを初期化します。

**keyStoreAuthentication:** 使用する Java キーストアを識別します。 SQL Server 用に Microsoft JDBC Driver 6.0 以降を使用している場合は、このプロパティを介してのみ Java キーストアに対して認証を行うことができます。 Java キーストアの場合、このプロパティの値は `JavaKeyStorePassword`である必要があります。

**keyStoreLocation:** 列マスターキーを格納する Java キーストアファイルへのパス。 パスには、キーストアファイル名が含まれます。

**keyStoreSecret:** キーストアとキーの両方に使用するシークレット/パスワード。 Java キーストアを使用する場合、キーストアとキーパスワードは同じである必要があります。

これらの資格情報を接続文字列に指定する例を次に示します。

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

これらの設定は、SQLServerDataSource オブジェクトを使用して取得または設定することもできます。 詳細については、「 [JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)」を参照してください。

これらの資格情報が接続プロパティに存在する場合、JDBC ドライバーは自動的に SQLServerColumnEncryptionJavaKeyStoreProvider をインスタンス化します。

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Java キーストアの列マスターキーを作成する
SQLServerColumnEncryptionJavaKeyStoreProvider は、JKS または PKCS12 キーストアの種類で使用できます。 このプロバイダーで使用するキーを作成またはインポートするには、Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html)ユーティリティを使用します。 キーは、キーストア自体と同じパスワードを持っている必要があります。 Keytool ユーティリティを使用して公開キーとそれに関連付けられている秘密キーを作成する方法の例を次に示します。

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

このコマンドは、公開キーを作成し、x.509 自己署名証明書にラップします。これは、キーストア ' キーストア ' に格納され、関連付けられている秘密キーと共に格納されます。 キーストア内のこのエントリは、エイリアス ' AlwaysEncryptedKey ' によって識別されます。

次に、PKCS12 ストア型を使用した場合の例を示します。

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

キーストアの種類が PKCS12 の場合、keytool ユーティリティはキーのパスワードの入力を要求しません。キーのパスワードは-キーパスワードを指定する必要があります。 SQLServerColumnEncryptionJavaKeyStoreProvider ではキーストアとキーが同じである必要があるためです。入力.

また、.pfx 形式で Windows 証明書ストアから証明書をエクスポートし、それを SQLServerColumnEncryptionJavaKeyStoreProvider と共に使用することもできます。 エクスポートされた証明書は、JKS キーストア型として Java キーストアにインポートすることもできます。

Keytool エントリを作成した後、データベースに列マスターキーのメタデータを作成します。これには、キーストアプロバイダー名とキーパスが必要です。 列マスターキーのメタデータを作成する方法の詳細については、「 [CREATE COLUMN MASTER key](../../t-sql/statements/create-column-master-key-transact-sql.md)」を参照してください。 SQLServerColumnEncryptionJavaKeyStoreProvider の場合、キーのパスはキーのエイリアスにすぎず、SQLServerColumnEncryptionJavaKeyStoreProvider の名前は ' MSSQL_JAVA_KEYSTORE ' になります。 また、SQLServerColumnEncryptionJavaKeyStoreProvider クラスの getName () パブリック API を使用して、この名前を照会することもできます。 

列マスターキーを作成するための T-sql 構文は次のとおりです。

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

上記で作成した ' AlwaysEncryptedKey ' では、列マスターキーの定義は次のようになります。

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> 組み込みの SQL Server management Studio 機能では、Java キーストアの列マスターキー定義を作成することはできません。 T-sql コマンドはプログラムで使用する必要があります。

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Java キーストアの列暗号化キーの作成
SQL Server Management Studio またはその他のツールを使用して、Java キーストアの列マスターキーを使用して列暗号化キーを作成することはできません。 クライアントアプリケーションは、SQLServerColumnEncryptionJavaKeyStoreProvider クラスを使用して、プログラムで列暗号化キーを作成する必要があります。 詳細については、「[プログラムによるキーのプロビジョニングに列マスターキーストアプロバイダーを使用する](#using-column-master-key-store-providers-for-programmatic-key-provisioning)」を参照してください。

### <a name="implementing-a-custom-column-master-key-store-provider"></a>カスタム列マスター キー ストア プロバイダーを実装する
既存のプロバイダーでサポートされていないキー ストアに列マスター キーを格納する場合は、SQLServerColumnEncryptionKeyStoreProvider クラスを拡張し、SQLServerConnection.registerColumnEncryptionKeyStoreProviders() メソッドを使用してプロバイダーを登録して、カスタム プロバイダーを実装できます。

```java
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

プロバイダーを登録します。

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>プログラムによるキーのプロビジョニングに列マスター キー ストア プロバイダーを使用する
Microsoft JDBC Driver for SQL Server は、暗号化された列にアクセスする際に、列暗号化キーを暗号化解除するための適切な列マスター キー ストア プロバイダーを透過的に検索して呼び出します。 一般的に、通常のアプリケーション コードは列マスター キー ストア プロバイダーを直接呼び出しません。 ただし、Always Encrypted キーをプロビジョニングして管理するために、プログラムによってプロバイダーをインスタンス化して呼び出すことができます。 この手順は、暗号化された列暗号化キーを生成し、列のマスターキーのローテーションとして列暗号化キーを復号化するために実行できます。たとえば、のようになります。 詳細については、「 [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Always Encrypted のキー管理の概要)」を参照してください。

カスタム キー ストア プロバイダーを使用する場合、独自のキー管理ツールの実装が必要になることがあります。 Windows 証明書ストアまたは Azure Key Vault に格納されているキーを使用する場合は、SQL Server Management Studio や PowerShell などの既存のツールを使用して、キーの管理とプロビジョニングを行うことができます。 Java キーストアに格納されているキーを使用する場合は、プログラムによってキーをプロビジョニングする必要があります。 次の例は、SQLServerColumnEncryptionJavaKeyStoreProvider クラスを使用して、Java キーストアに格納されているキーを使用してキーを暗号化する方法を示しています。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>アプリケーション クエリで Always Encrypted を有効にする
パラメーターの暗号化と、暗号化された列をターゲットとするクエリ結果の暗号化解除を有効にする最も簡単な方法としては、**columnEncryptionSetting** 接続文字列キーワードの値を **Enabled** に設定します。

次の接続文字列は、JDBC ドライバーで Always Encrypted を有効にする例です。

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

次のコードは、SQLServerDataSource オブジェクトを使用した場合と同等の例です。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

Always Encrypted は、個々のクエリに対しても有効にすることができます。 詳細については、「[Always Encrypted のパフォーマンスの影響を制御する](#controlling-the-performance-impact-of-always-encrypted)」をご覧ください。 暗号化または暗号化解除を正常に行うには、Always Encrypted を有効にするだけでは不十分です。 次のことを確認する必要もあります。
- アプリケーションが、データベース内の Always Encrypted キーに関するメタデータへのアクセスに必要な *VIEW ANY COLUMN MASTER KEY DEFINITION* および *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* データベース権限を持っている。 詳細については、[「Always Encrypted (データベース エンジン)」のページで権限に関するセクション](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)を参照してください。
- アプリケーションが、列暗号化キーを保護する列マスター キーにアクセスでき、クエリされたデータベース列を暗号化する。 Java キーストアプロバイダーを使用するには、接続文字列に追加の資格情報を提供する必要があります。 詳細については、「 [Java キーストアプロバイダーの使用](#using-java-key-store-provider)」を参照してください。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>java.sql.Time の値をサーバーに送信する方法の構成
java.sql.Time 値のサーバーへの送信方法を構成するために、**sendTimeAsDatetime** 接続プロパティを使用します。 False に設定すると、時刻値は SQL Server の時刻型として送信されます。 True に設定すると、時刻値は datetime 型として送信されます。 Time 列が暗号化されている場合、暗号化された列では time から datetime への変換がサポートされていないため、 **sendTimeAsDatetime**プロパティは false に設定する必要があります。 また、このプロパティは既定で true になっているため、暗号化された時刻列を使用する場合は false に設定する必要があります。 それ以外の場合、ドライバーは例外をスローします。 ドライバーのバージョン6.0 以降では、SQLServerConnection クラスには、このプロパティの値をプログラムで構成する2つのメソッドがあります。
 
* public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

このプロパティの詳細については、「 [java の時刻値をサーバーに送信する方法の構成](configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>文字列値をサーバーに送信する方法の構成
**SendStringParametersAsUnicode**接続プロパティは、文字列値を SQL Server に送信する方法を構成するために使用されます。 true に設定されている場合、サーバーには Unicode 形式で文字列パラメーターが送信されます。 False に設定されている場合、文字列パラメーターは Unicode ではなく、ASCII や MBCS などの非 Unicode 形式で送信されます。 このプロパティの既定値は、true です。 Always Encrypted が有効になっていて、char/varchar/varchar (max) 列が暗号化されている場合、 **sendStringParametersAsUnicode**の値を false に設定する必要があります。 このプロパティが true に設定されている場合、Unicode 文字を含む暗号化された char/varchar/varchar (max) 列からデータを復号化するときに、ドライバーは例外をスローします。 このプロパティの詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>暗号化された列のデータを取得および変更する
アプリケーションクエリの Always Encrypted を有効にすると、標準の JDBC Api を使用して、暗号化されたデータベース列のデータを取得または変更できます。 アプリケーションが必要なデータベース権限を持っていて、列マスターキーにアクセスできる場合、ドライバーは暗号化された列を対象とするすべてのクエリパラメーターを暗号化し、暗号化された列から取得されるデータを復号化します。

Always Encrypted が有効でない場合、暗号化された列をターゲットとするパラメーターを含むクエリは失敗します。 暗号化された列をターゲットとするパラメーターがクエリにない場合、クエリでは、暗号化された列からデータを取得できます。 ただし、ドライバーは、暗号化された列から取得された値を暗号化解除しようとせず、アプリケーションは、暗号化されたバイナリ データを (バイト配列として) 受け取ります。

次の表は、Always Encrypted が有効かどうかに応じたクエリの動作をまとめたものです。

| クエリの特性                                                                           | Always Encrypted が有効になっており、アプリケーションがキーとキー メタデータにアクセスできる                                                                                                                        | Always Encrypted が有効になっており、アプリケーションがキーまたはキー メタデータにアクセスできない | Always Encrypted が無効になっている                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| 暗号化された列をターゲットとするパラメーターを含むクエリ。                                           | パラメーター値は透過的に暗号化されます。                                                                                                                                                           | エラー                                                                             | エラー                                                                                                               |
| 暗号化された列をターゲットとするパラメーターを含まず、暗号化された列からデータを取得するクエリ。 | 暗号化された列の結果は透過的に暗号化解除されます。 アプリケーションは、暗号化された列用に構成された SQL Server 型に対応する、JDBC データ型のプレーンテキスト値を受け取ります。 | エラー                                                                             | 暗号化された列の結果は暗号化解除されません。 アプリケーションは、暗号化された値をバイト配列 (byte[]) として受け取ります。 |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>暗号化されたデータの例の挿入と取得

次の例は、暗号化された列のデータを取得および変更する方法を示しています。 この例では、次のスキーマおよび暗号化された SSN 列と誕生日列を含むターゲットテーブルを想定しています。 "MyCMK" という名前の列マスターキーと "Mycmk" という名前の列暗号化キー (前述の「キーストアプロバイダー」セクションで説明) を構成した場合は、次のスクリプトを使用してテーブルを作成できます。

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

各 Java コード例では、メモした場所にキーストア固有のコードを挿入する必要があります。

Azure Key Vault キーストアプロバイダーを使用している場合:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Windows 証明書ストアのキーストアプロバイダーを使用している場合:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Java キーストアのキーストアプロバイダーを使用している場合は、次のようにします。

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>データの挿入の例

この例では、Patients テーブルに列を挿入します。 次の項目に注意してください。

- このサンプル コードの暗号化に固有のものは何もありません。 Microsoft JDBC Driver for SQL Server は、暗号化された列を対象とするパラメーターを自動的に検出して暗号化します。 この動作により、アプリケーションに対して暗号化が透過的に実行されます。
- 暗号化された列を含む、データベースの列に挿入された値は、SQLServerPreparedStatement を使用してパラメーターとして渡されます。 暗号化されていない列に値を送信する場合、パラメーターの使用は省略可能です (ただし、SQL インジェクションを防ぐのに役立つので、強くお勧めします) が、暗号化された列をターゲットとする値に対しては必須です。 暗号化された列に挿入された値がクエリステートメントに埋め込まれているリテラルとして渡された場合、ドライバーはターゲットの暗号化された列の値を特定できず、値を暗号化しないため、クエリは失敗します。 その結果、サーバーはこれらの値を、暗号化された列と互換性がないと見なして拒否します。
- Microsoft JDBC Driver for SQL Server は、暗号化された列から取得されたデータを透過的に暗号化解除するので、プログラムで印刷される値はすべてプレーンテキストになります。
- WHERE 句を使用して検索を実行する場合は、ドライバーがデータベースに送信する前にその値を透過的に暗号化できるように、WHERE 句で使用される値をパラメーターとして渡す必要があります。 次の例では、SSN はパラメーターとして渡されますが、lastname は暗号化されていないので、LastName はリテラルとして渡されます。
- SSN 列をターゲットとするパラメーターに使用される setter メソッドは setString () であり、char/varchar SQL Server データ型にマップされます。 このパラメーターに対して使用されている setter メソッドが setNString () だった場合、nchar/nvarchar にマップされ、クエリは失敗します。これは、暗号化された nchar/nvarchar 値から暗号化された char/varchar 値への変換が Always Encrypted でサポートされていないためです。

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>プレーンテキスト データの取得の例

次の例は、暗号化された値に基づいてデータをフィルター処理し、暗号化された列からプレーンテキスト データを取得する方法を示しています。 次の項目に注意してください。

- SSN 列に対してフィルター処理するために WHERE 句で使用される値は、Microsoft JDBC Driver for SQL Server がデータベースに送信する前に透過的に暗号化できるように、パラメーターとして渡す必要があります。
- Microsoft JDBC Driver for SQL Server は、SSN 列と BirthDate 列から取得されたデータを透過的に暗号化解除するので、プログラムで印刷される値はすべてプレーンテキストになります。

> [!NOTE]
> 決定論的暗号化を使用して列が暗号化される場合、クエリは列に対して等価比較を実行できます。 詳細については、[「Always Encrypted (データベース エンジン)」の「明確な暗号化またはランダム化された暗号化の選択」](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)を参照してください。

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-encrypted-data-example"></a>暗号化されたデータの取得の例

Always Encrypted が有効になっていない場合でも、暗号化された列をターゲットとするパラメーターをクエリが含んでいなければ、クエリでは、暗号化された列からデータを取得できます。

次の例は、暗号化された列から暗号化されたバイナリ データを取得する方法を示しています。 次の項目に注意してください。

- 接続文字列で Always Encrypted が有効になっていないので、クエリは、SSN と BirthDate の暗号化された値をバイト配列として返します (プログラムによって値が文字列に変換されます)。
- Always Encrypted が無効の状態で、暗号化された列からデータを取得するクエリは、暗号化された列をターゲットとするパラメーターがない場合に限り、パラメーターを含むことができます。 次のクエリは、データベースで暗号化されない LastName によってフィルター処理を行います。 クエリが SSN または BirthDate によってフィルター処理を行った場合、クエリは失敗します。

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>暗号化された列をクエリする際の一般的な問題を回避する

ここでは、暗号化された列を Java アプリケーションからクエリする際のエラーの一般的なカテゴリと、その対処方法に関するいくつかのガイドラインを示します。

### <a name="unsupported-data-type-conversion-errors"></a>サポートされていないデータ型の変換エラー

Always Encrypted では、暗号化されたデータ型に対するいくつかの変換がサポートされています。 サポートされている型の変換の詳細な一覧については、「[Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)」を参照してください。 データ型の変換エラーを回避するには、 次のことを確認してください。

- 暗号化された列をターゲットとするパラメーターの値を渡すときは、適切な setter メソッドを使用します。 パラメーターの SQL Server データ型が、ターゲット列の型とまったく同じであること、またはパラメーターの SQL Server データ型を列の対象の型に変換することがサポートされていることを確認してください。 特定の SQL Server データ型に対応するパラメーターを渡すために、API メソッドが SQLServerPreparedStatement、SQLServerCallableStatement、および SQLServerResultSet クラスに追加されました。 たとえば、列が暗号化されていない場合は、setTimestamp () メソッドを使用して、パラメーターを datetime2 または datetime 列に渡すことができます。 ただし、列が暗号化されている場合は、データベース内の列の型を表す正確なメソッドを使用する必要があります。 たとえば、setTimestamp () を使用して、暗号化された datetime2 列に値を渡し、Settimestamp () を使用して、暗号化された datetime 列に値を渡すことができます。 新しい Api の完全な一覧については[、JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)を参照してください。
- 10 進数と数値の SQL Server データ型の列をターゲットとするパラメーターの有効桁数と小数点以下桁数が、ターゲット列に対して構成された有効桁数と小数点と同じである。 API メソッドが SQLServerPreparedStatement、SQLServerCallableStatement、および SQLServerResultSet クラスに追加され、decimal および numeric データ型を表すパラメーターまたは列のデータ値と共に、有効桁数と小数点以下桁数を受け入れるようになりました。 新しい Api とオーバーロードされた Api の完全な一覧については[、「JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)」を参照してください。  
- datetime2、datetimeoffset、または time SQL Server データ型の列をターゲットとするパラメーターの秒の小数部の有効桁数/小数点以下桁数が、ターゲット列の値を変更するクエリで、対象になる列の秒の小数部の有効桁数/小数点以下桁数を超えていません。 API メソッドは、SQLServerPreparedStatement、SQLServerCallableStatement、および SQLServerResultSet クラスに追加され、秒の小数部の有効桁数/小数点以下桁数と、これらのデータ型を表すパラメーターのデータ値を受け入れるようになりました。 新しい/オーバーロードされた Api の完全な一覧については、 [JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)を参照してください。

### <a name="errors-due-to-incorrect-connection-properties"></a>接続プロパティが正しくないために発生するエラー

このセクションでは、Always Encrypted データを使用するように接続設定を適切に構成する方法について説明します。 暗号化されたデータ型は限定的な変換をサポートしているため、暗号化された列を使用する場合、 **sendTimeAsDatetime**と**sendStringParametersAsUnicode**の接続設定で適切な構成が必要になります。 次のことを確認してください。

- [sendTimeAsDatetime](setting-the-connection-properties.md)接続設定は、データを暗号化された時刻列に挿入するときに false に設定されます。 詳細については、「 [java .sql の時刻値をサーバーに送信する方法の構成](configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。
- [sendStringParametersAsUnicode](setting-the-connection-properties.md)接続設定は、暗号化された char/varchar/varchar (max) 列にデータを挿入するときに、true (または既定値のまま) に設定されます。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>暗号化された値の代わりにプレーンテキストを渡すことによるエラー

暗号化された列をターゲットとするすべての値は、アプリケーションの内部で暗号化される必要があります。 暗号化された列でプレーンテキスト値を挿入/変更したり、この値によってフィルター処理を行おうとしたりすると、次のようなエラーになります。

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

このようなエラーを防ぐには、次のことを確認してください。

- Always Encrypted が、暗号化された列をターゲットとするアプリケーション クエリに対して有効になっている (接続文字列または特定のクエリで)。
- 準備されたステートメントとパラメーターを使用して、暗号化された列をターゲットとするデータを送信します。 次の例は、パラメーターとしてリテラルを渡す代わりに、暗号化された列 (SSN) でリテラル/定数によって不正なフィルター処理を行うクエリを示しています。 このクエリは失敗します。

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>入力パラメーターの暗号化を強制する

強制暗号化機能では、Always Encrypted を使用する場合に、パラメーターの暗号化が適用されます。 強制的な暗号化が使用され、パラメーターの暗号化が不要であることが SQL Server からドライバーに通知された場合、このパラメーターを使用するクエリは失敗します。 攻撃を受けた SQL Server がクライアントに不正な暗号化メタデータを提供すると、データ漏えいが引き起こされる可能性がありますが、このプロパティは、そのようなセキュリティ攻撃に対する保護を強化します。 SQLServerPreparedStatement クラスと SQLServerCallableStatement クラスの set * メソッドと SQLServerResultSet クラスの update\* メソッドは、ブール型の引数を受け取り、force encryption 設定を指定するようにオーバーロードされています。 この引数の値が false の場合、ドライバーはパラメーターの暗号化を強制しません。 Force encryption が true に設定されている場合、クエリパラメーターは、送信先列が暗号化され、接続またはステートメントで Always Encrypted が有効になっている場合にのみ送信されます。 このプロパティを使用すると、セキュリティがさらに強化され、暗号化されることが予想される場合に、ドライバーがプレーンテキストとして SQL Server に誤ってデータを送信することがなくなります。

強制暗号化設定でオーバーロードされる SQLServerPreparedStatement メソッドと SQLServerCallableStatement メソッドの詳細については、「 [JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)」を参照してください。  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Always Encrypted のパフォーマンスの影響を制御する

Always Encrypted はクライアント側暗号化テクノロジであるため、ほとんどのパフォーマンス オーバーヘッドは、データベースではなくクライアント側で発生します。 暗号化および暗号化解除の操作のコストとは別に、クライアント側のパフォーマンス オーバーヘッドのその他の原因を次に示します。

- クエリ パラメーターのメタデータを取得するためのデータベースへの追加のラウンド トリップ。
- 列マスター キーにアクセスするための列マスター キー ストアの呼び出し。

このセクションでは、Microsoft JDBC Driver for SQL Server の組み込みのパフォーマンス最適化、および上記の 2 つの要因によるパフォーマンスへの影響を制御する方法について説明します。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>クエリ パラメーターのメタデータを取得するためのラウンド トリップを制御する

既定では、接続に対して Always Encrypted が有効になっている場合、ドライバーは、各パラメーター化クエリに対して [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) を呼び出し、クエリ ステートメント (パラメーター値を除く) を SQL Server に渡します。 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) はクエリ ステートメントを分析して、パラメーターを暗号化する必要があるかどうかを判断し、必要がある場合は、これらの各パラメーターに対して暗号化関連の情報を返します。この情報により、ドライバーはパラメーター値を暗号化できます。 この動作により、クライアント アプリケーションに対する高度な透明性が確保されます。 アプリケーションでパラメーターを使用して、暗号化された列を対象とする値をドライバーに渡す限り、アプリケーション (およびアプリケーション開発者) は、暗号化された列にアクセスするクエリを認識する必要はありません。

### <a name="setting-always-encrypted-at-the-query-level"></a>クエリ レベルで Always Encrypted を設定する

パラメーター化クエリに対して暗号化メタデータを取得することによるパフォーマンスへの影響を制御するには、Always Encrypted を接続に対して設定する代わりに、個々のクエリに対して有効にします。 これにより、暗号化された列をターゲットとするパラメーターを含むことがわかっているクエリに対してのみ、sys.sp_describe_parameter_encryption が呼び出されるように設定できます。 ただし、これにより、暗号化の透明度が損なわれることに注意してください。データベース列の暗号化プロパティを変更する場合は、スキーマの変更に合わせてアプリケーション コードの変更が必要になる可能性があります。

個々のクエリの Always Encrypted 動作を制御するには、列挙型 SQLServerStatementColumnEncryptionSetting を渡すことによって個々のステートメントオブジェクトを構成する必要があります。これは、読み取りと書き込み時のデータの送受信方法を指定します。その特定のステートメントの暗号化された列。 有用なガイドラインを次に示します。

- クライアント アプリケーションがデータベース接続を介して送信するほとんどのクエリが、暗号化された列にアクセスする場合は、次のガイドラインを使用してください。

    - **columnEncryptionSetting** 接続文字列キーワードを **Enabled** に設定します。
    - 暗号化された列にアクセスしない個々のクエリに対して、SQLServerStatementColumnEncryptionSetting.Disabled を設定します。 この設定により、sys.sp_describe_parameter_encryption の呼び出しと、結果セット内の値を暗号化解除しようとする試みの両方が無効になります。
    - 暗号化を必要とするパラメーターを含まないが、暗号化された列からデータを取得する個々のクエリに対して、SQLServerStatementColumnEncryptionSetting.ResultSet を設定します。 この設定により、sys.sp_describe_parameter_encryption の呼び出しと、パラメーター暗号化が無効になります。 クエリは、暗号化列の結果を暗号化解除できます。

- クライアント アプリケーションがデータベース接続を介して送信するほとんどのクエリが、暗号化された列にアクセスしない場合は、次のガイドラインを使用してください。

    - **columnEncryptionSetting** 接続文字列キーワードを **Disabled** に設定します。
    - 暗号化を必要とするパラメーターを含む個々のクエリに対して、SQLServerStatementColumnEncryptionSetting.Enabled を設定します。 この設定により、sys.sp_describe_parameter_encryption の呼び出しと、暗号化された列から取得されたクエリ結果の暗号化解除の両方が有効になります。
    - 暗号化を必要とするパラメーターを含まないが、暗号化された列からデータを取得するクエリに対して、SQLServerStatementColumnEncryptionSetting.ResultSet を設定します。 この設定により、sys.sp_describe_parameter_encryption の呼び出しと、パラメーター暗号化が無効になります。 クエリは、暗号化列の結果を暗号化解除できます。

SQLServerStatementColumnEncryptionSetting 設定を使用して暗号化を回避し、プレーンテキストデータにアクセスすることはできません。 ステートメントで列の暗号化を構成する方法の詳細については、 [JDBC Driver の ALWAYS ENCRYPTED API リファレンス](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)を参照してください。  

次の例では、データベース接続に対して Always Encrypted が無効になっています。 アプリケーションが発行するクエリに、暗号化されていない LastName 列をターゲットとするパラメーターが含まれています。 このクエリは、どちらも暗号化されている SSN 列と BirthDate 列からデータを取得します。 このような場合、暗号化メタデータを取得するために sys.sp_describe_parameter_encryption を呼び出す必要ありません。 ただし、アプリケーションが 2 つの暗号化された列からプレーンテキスト値を受け取ることができるよう、クエリ結果の暗号化解除を有効にする必要があります。 SQLServerStatementColumnEncryptionSetting 設定を使用して、を確認します。

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>;" 
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>" 
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="column-encryption-key-caching"></a>列暗号化キーのキャッシュ

列暗号化キーを暗号化解除するための列マスター キー ストアの呼び出し回数を減らすために、Microsoft JDBC Driver for SQL Server は、プレーンテキストの列暗号化キーをメモリにキャッシュします。 暗号化された列暗号化キー値をデータベース メタデータから受け取った後、ドライバーは、暗号化されたキー値に対応するプレーンテキストの列暗号化キーをまず見つけようとします。 ドライバーは、暗号化された列暗号化キー値がキャッシュ内に見つからない場合にのみ、列マスター キーを含むキー ストアを呼び出します。

SQLServerConnection クラスの setColumnEncryptionKeyCacheTtl () API を使用して、キャッシュ内の列暗号化キーエントリの有効期間の値を構成できます。 キャッシュ内の列暗号化キーエントリの既定の有効期限の値は2時間です。 キャッシュを無効にするには、値0を使用します。 有効期限を設定するには、次の API を使用します。

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

たとえば、有効期限を10分に設定するには、次のように指定します。

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

時間単位としては、日、時、分、または秒のみがサポートされます。  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>SQLServerBulkCopy を使用した暗号化されたデータのコピー

SQLServerBulkCopy を使用して、データの暗号化解除を行うことなく、既に暗号化されて 1 つのテーブルに格納されているデータを別のテーブルにコピーできます。 この手順は次のとおりです。

- ターゲット テーブルの暗号化構成が、ソース テーブルの構成と同じであることを確認します。 具体的には、両方のテーブルで同じ列が暗号化されており、同じ暗号化タイプおよび同じ暗号化キーを使用してこれらの列が暗号化されている必要があります。 いずれかのターゲット列が、対応するソース列と異なる方法で暗号化されている場合、コピー操作の後でターゲット テーブル内のデータを暗号化解除することはできません。 データは破損します。
- Always Encrypted を有効にせずに、ソース テーブルとターゲット テーブルへの両方のデータベース接続を構成します。
- AllowEncryptedValueModifications オプションを設定します。 詳細については、「 [JDBC ドライバーでの一括コピーの使用](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)」を参照してください。

> [!NOTE]
> データベースが破損する可能性があるので、AllowEncryptedValueModifications を指定する際には注意が必要です。このオプションは、データが実際に暗号化されているかどうか、またはターゲット列と同じ暗号化のタイプ、アルゴリズム、およびキーを使用して正しく暗号化されているかどうかを、Microsoft JDBC Driver for SQL Server がチェックしないためです。

## <a name="see-also"></a>参照

[Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
