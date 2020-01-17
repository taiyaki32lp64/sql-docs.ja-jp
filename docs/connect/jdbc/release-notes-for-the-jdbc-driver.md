---
title: JDBC Driver のリリース ノート | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04a179492b151e664dfe31f4fe4e51c5440fcef5
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027788"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Microsoft JDBC Driver のリリース ノート

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、_Microsoft JDBC Driver for SQL Server_ のリリースを示します。 リリース バージョンごとに、変更された点とそれに関する説明が示されています。
## <a name="741"></a>7.4.1

### <a name="compliance"></a>準拠

2019年8月2日

| コンプライアンスの変更 | 詳細 |
| :---------------- | :------ |
| JDBC Driver 7.4 用の最新の更新のダウンロード。 | &bull; &nbsp; [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=2099962)<br/>&bull; &nbsp; [7.4.1 (GitHub)](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.4.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 仕様 4.2 への完全準拠。 | 7\.4 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。<br/><br/>たとえば、7.4 パッケージの mssql-jdbc-7.4.1.jre11.jar ファイルは、Java 11 で使用する必要があります。 |
| Java Development Kit (JDK) バージョン12.0、11.0、および1.8 と互換性があります。 | Microsoft JDBC Driver 7.4 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 12.0 と互換性を持つようになりました。 |
| &nbsp; | &nbsp; |

### <a name="support-for-jdk-12"></a>JDK 12 のサポート

Microsoft JDBC Driver 7.4 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 12.0 と互換性を持つようになりました。

### <a name="introduces-ntlm-authentication"></a>NTLM 認証について説明します。

| NTLM の変更 | 詳細 |
| :--------- | :------ |
| NTLM 認証モードをサポートします。 | この認証モードでは、windows クライアントと Windows 以外のクライアントの両方が Windows ドメインユーザーを使用して SQL Server に対して認証を行うことができます。 |
| この認証モードを使用するための詳細とサンプル アプリケーション。 | 「 [NTLM 認証を使用](../../connect/jdbc/using-ntlm-authentication-to-connect-to-sql-server.md)した接続」を参照してください。 |
| &nbsp; | &nbsp; |

### <a name="introduces-querying-parametermetadata-via-_usefmtonly_"></a>_UseFmtOnly_を使用した parametermetadata のクエリについて説明します。

| useFmtOnly の変更 | 詳細 |
| :---------- | :------ |
| **useFmtOnly**接続プロパティが追加されました。 | この機能により、ユーザーは必要に応じて`SET FMTONLY ON` 、レガシ API を使用して parametermetadata を照会できます。 これは、が期待どおり`sp_describe_undeclared_parameters`に動作しないシナリオに役立ちます。 |
| 詳細と制限事項についてはこちらを参照してください。 | 「[useFMTOnly の使用](../../connect/jdbc/using-usefmtonly.md)」をご覧ください |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-121"></a>_Microsoft Azure Key Vault SDK for Java_ を更新 (バージョン 1.2.1)

| Key Vault SDK の変更 | 詳細 |
| :------------------- | :------ |
| _Microsoft Azure Key Vault SDK for Java_ の Maven の依存関係がバージョン 1.2.1 に更新されました。 | &nbsp; |
| Maven の依存関係としての _Microsoft Azure SDK for Key Vault WebKey_ が削除されます。 | &nbsp; |
| 追加の詳細。 | 「[Feature dependencies of the Microsoft JDBC Driver for SQL Server (Microsoft JDBC Driver for SQL Server の機能の依存関係)](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :----------- | :------ |
| NTLM 認証を使用するとき。 | 現在、拡張保護と暗号化された接続を同時に有効化することはできません。 |
| useFmtOnly を使用するとき。 | SQL の解析ロジックの欠陥に起因する、いくつかの機能のイシューがあります。 詳細と回避策の提案については、「 [Using useFmtOnly](../../connect/jdbc/using-usefmtonly.md) 」を参照してください。 |
| &nbsp; | &nbsp; |

## <a name="722"></a>7.2.2

### <a name="compliance"></a>準拠

2019 年 4 月 16 日

| コンプライアンスの変更 | 詳細 |
| :---------------- | :------ |
| JDBC Driver 7.2 用の最新の更新のダウンロード。 | &bull; &nbsp; [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [7.2.2 (GitHub)](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 仕様 4.2 への完全準拠。 | 7\.2 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。<br/><br/>たとえば、7.2 パッケージの mssql-jdbc-7.2.2.jre11.jar ファイルは、Java 11 で使用する必要があります。 |
| Java Development Kit (JDK) バージョン 11.0 および JDK 1.8 と互換性があります。 | Microsoft JDBC Driver 7.2 for SQL Server は、JDK 1.8 に加え、Java Development Kit (JDK) バージョン 11.0 と互換性を持つようになりました。 |
| &nbsp; | &nbsp; |

> [!NOTE]
> 2019 年 1 月 31 日にリリースされた JDBC 7.2 Release To Web (RTW) ドライバーで、SQL ステートメントの解析に問題があることがわかりました。 この変更はロールバックされ、2019 年 2 月 11 日に新しい jar (バージョン 7.2.1) がリリースされました。
>
> ドライバーに対して他の更新も行われ、ActivityID が適切に変更されないという問題が修正されました。 新しい jar (バージョン 7.2.2) は、2019 年 4 月 16 日にリリースされました。
> 
> 7\.2.2 リリースの jar を使用するようにプロジェクトを更新することをお勧めします。 詳細については、[7.2.1 (GitHub)](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1) と [7.2.2 (GitHub)](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2) のリリース ノートをご覧ください。

### <a name="active-directory-_managed-service-identity_-msi-authentication"></a>Azure Active Directory "_マネージド サービス ID_" (MSI) 認証

| MSI の変更 | 詳細 |
| :--------- | :------ |
| Azure Active Directory マネージド サービス ID (MSI) 認証モードのサポート。 | この認証モードは、"ID" 機能の有効化がサポートされている Azure リソースに適用できます。<br/><br/>ドライバーによって両方の種類のマネージド システム ID (MSI) がサポートされ、セキュリティで保護された接続を確立するための **accessToken** が取得されます。 |
| この認証モードを使用するための詳細とサンプル アプリケーション。 | 「[Connecting using Azure Active Directory Authentication (Azure Active Directory 認証を利用した接続)](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="introduces-_open-service-gateway-initiative_-osgi-support"></a>"_オープン サービス ゲートウェイ イニシアチブ_" (OSGi) のサポートを導入

| OSGi の変更 | 詳細 |
| :---------- | :------ |
| **DataSourceFactory** の実装の追加。 | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **アクティベーター**の実装の追加。 | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-_sqlservererror_-apis"></a>_SQLServerError_ API を導入

| エラー API の変更 | 詳細 |
| :--------------- | :------ |
| SQLServerError API が導入されました。 | 生成されたエラーの追加の詳細をサーバーから取得する getter API。<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 追加の詳細。 | 「[Handling Errors (エラーの処理)](../../connect/jdbc/handling-errors.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-active-directory-authentication-library-adal4j-for-java_-version-163"></a>"_Microsoft Azure Active Directory 認証ライブラリ (ADAL4J) for Java_" の更新、バージョン 1.6.3

| ADAL4J の変更 | 詳細 |
| :------------ | :------ |
| ADAL4J の Maven の依存関係がバージョン 1.6.3 に更新されました。 | &nbsp; |
| Maven の依存関係として、_Java Client Runtime for AutoRest_ が導入されています (バージョン 1.6.5)。 | &nbsp; |
| 追加の詳細。 | 「[Feature dependencies of the Microsoft JDBC Driver for SQL Server (Microsoft JDBC Driver for SQL Server の機能の依存関係)](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-120"></a>_Microsoft Azure Key Vault SDK for Java_ を更新 (バージョン 1.2.0)

| Key Vault SDK の変更 | 詳細 |
| :------------------- | :------ |
| _Microsoft Azure Key Vault SDK for Java_ の Maven の依存関係がバージョン 1.2.0 に更新されました。 | &nbsp; |
| Maven の依存関係として _Microsoft Azure SDK for Key Vault WebKey_、バージョン 1.2.0 が導入されます。 | &nbsp; |
| 追加の詳細。 | 「[Feature dependencies of the Microsoft JDBC Driver for SQL Server (Microsoft JDBC Driver for SQL Server の機能の依存関係)](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :----------- | :------ |
| クエリがパラメーター化される場合があります。 | この問題に対応するために、7.2.0 バージョンの更新である v7.2.1 が 2019 年 2 月にリリースされました。 |
| ActivityId のクリーンアップ。 | この問題に対応するために、7.2.1 バージョンの更新である v7.2.2 が 2019 年 4 月にリリースされました。 |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

Microsoft JDBC Driver 7.0 for SQL Server は、JDBC API 仕様 4.2 に完全に準拠しています。 7\.0 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされます。 たとえば、7.0 パッケージの mssql-jdbc-7.0.0.jre10.jar ファイルは、Java 10 で使用する必要があります。

### <a name="support-for-jdk-10"></a>JDK 10 のサポート

Microsoft JDBC Driver 7.0 for SQL Server は、JDK 1.8 に加え、Java Development Kit (JDK) バージョン 10.0 と互換性を持つようになりました。 さらに、この更新により、ドライバーの `Automatic-Module-Name` が、MANIFEST ファイルを通して `com.microsoft.sqlserver.jdbc` として公開されます。

### <a name="support-for-spatial-datatypes"></a>空間データ型のサポート

Microsoft JDBC Driver 7.0 for SQL Server で、SQL Server の空間データ型である Geography と Geometry のサポートが提供されるようになりました。 空間データ型の API の詳細とそれらの使用方法については、「[空間データ型の使用](../../connect/jdbc/use-spatial-datatypes.md)」を参照してください。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3 の実装で、java.sql.Connection の API beginRequest() と endRequest() が導入されました。

Microsoft JDBC Driver 7.0 for SQL Server で、`java.sql.Connection` クラスから `beginRequest()` API と `endRequest()` API が実装されるようになりました。 これらの API は、JDBC 4.3 仕様と JDK 9 で導入されました。 ドライバーでのこれらの API の実装の詳細については、「[JDBC Driver の JDBC 4.3 への準拠](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)」を参照してください。

### <a name="support-for-sql-data-discovery-and-classification"></a>SQL データの検出と分類のサポート

Microsoft JDBC Driver 7.0 for SQL Server には、SQL データの検出と分類に関するサポートが、この機能に対応している任意のターゲット データベースに向けて用意されています。 ドライバーで、フェッチされた `ResultSet` からこの情報を抽出するための `SQLServerResultSet.getSensitivityClassification()` API が公開されるようになりました。

JDBC Driver でこの機能を使用する方法の詳細については、「[SQL データの検出と分類](../../connect/jdbc/data-discovery-classification-sample.md)」内の例を参照してください。

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>接続プロパティ useBulkCopyForBatchInsert を追加

Microsoft JDBC Driver 7.0 for SQL Server には、新しい接続プロパティである `useBulkCopyForBatchInsert` が導入されています。 このプロパティは、Azure SQL Data Warehouse に対してのみサポートされます。

このプロパティは、既定では無効になっています。 Azure SQL Data Warehouse に大量のデータをプッシュするときに、それを有効にすることで、ユーザー アプリケーションのパフォーマンスを向上させることができます。 このプロパティを有効にすると、バッチ挿入操作の動作が変更され、ユーザー指定のデータを一括コピーする操作に切り替わります。 このプロパティとその制約については、「[Using Bulk Copy API for batch insert operation (一括挿入操作での Bulk Copy API の使用)](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)」を参照してください。

### <a name="added-connection-property-cancelquerytimeout"></a>接続プロパティ cancelQueryTimeout を追加

Microsoft JDBC Driver 7.0 for SQL Server には、新しい接続プロパティである `cancelQueryTimeout` が導入されています。これは `java.sql.Connection` オブジェクトと `java.sql.Statement` オブジェクトの `queryTimeout` をキャンセルします。

### <a name="added-azure-key-vault-provider-constructors"></a>Azure Key Vault プロバイダー コンストラクターを追加

Microsoft JDBC Driver 7.0 for SQL Server には、以前削除された `SQLServerColumnEncryptionAzureKeyVaultProvider` 用のコンストラクターが再び導入されています。 それは `SQLServerKeyVaultAuthenticationCallback` で実装されたカスタム メソッドを通して認証を行うことを可能にしていました。

新しいコンストラクターには、次の定義が含まれています。

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>"Microsoft Azure Active Directory Authentication Library (ADAL4J) for Java" バージョン: 1.6.0 に更新

Microsoft JDBC Driver 7.0 for SQL Server では、"Java 用 Microsoft Azure Active Directory 認証ライブラリ (ADAL4J)" に関する Maven の依存関係が 1.6.0 に更新されています。 依存関係の詳細については、「[Microsoft JDBC Driver for SQL Server の機能の依存関係](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 6\.4 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。 たとえば、6.4 パッケージの mssql-jdbc-6.4.0.jre8.jar ファイルは、Java 8 で使用する必要があります。

### <a name="support-for-jdk-9"></a>JDK 9 のサポート

ドライバーでは、JDK 8.0 および 7.0 に加えて JDK バージョン 9.0 がサポートされています。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 に準拠

ドライバーでは、Java Database Connectivity API 4.1 および 4.2 に加えて、4.3 の仕様もサポートされます。 JDBC 4.3 API メソッドは追加されていますが、まだ実装されていません。 詳細については、「[JDBC Driver の JDBC 4.3 への準拠](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)」をご覧ください。

### <a name="added-connection-property-sslprotocol"></a>接続プロパティ sslProtocol を追加

新しい接続プロパティを使用して、TLS プロトコルのキーワードを指定できます。 指定できる値は、"TLS"、"TLSv1"、"TLSv1.1"、および "TLSv1.2" です。 詳細については、「[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)」を参照してください。

### <a name="deprecated-connection-property-fipsprovider"></a>非推奨の接続プロパティ fipsProvider

接続プロパティ `fipsProvider` は、指定できる接続プロパティの一覧から削除されています。 詳細については、関連する [GitHub pull request](https://github.com/Microsoft/mssql-jdbc/pull/460) を参照してください。

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>カスタムの TrustManager を指定するための接続プロパティを追加

ドライバーでは、`trustManagerClass` および `trustManagerConstructorArg` 接続プロパティの追加によって、カスタムの TrustManager の指定がサポートされるようになりました。 Java 仮想マシン (JVM) 環境でのグローバル設定の変更なしで、信頼できる一連の証明書を接続ごとに動的に指定できます。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>テーブル値パラメーターでの datetime/smallDatetime 型のサポートを追加

ドライバーでは、テーブル値パラメーター (TVP) を使用している場合に、`datetime` および `smallDatetime` データ型がサポートされるようになりました。

### <a name="added-support-for-the-sql_variant-datatype"></a>sql_variant データ型のサポートを追加

JDBC ドライバーでは、SQL Server で使用する `sql_variant` データ型がサポートされるようになりました。 `sql_variant` データ型は、TVP や一括コピーなどの機能でもサポートされますが、次の制約があります。

* **日付の値の場合**: 

  `sql_variant` 列に `datetime` 値、`smalldatetime` 値、または `date` 値が格納されているテーブルに TVP を使用して入力する場合、結果セットに対する `getDateTime()` メソッド、`getSmallDateTime()` メソッド、または `getDate()` メソッドの呼び出しは機能せず、次の例外がスローされます。

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  回避策として、代わりに `getString()` メソッドまたは `getObject()` メソッドを使用してください。

* **null 値に対して TVP を sql_variant と共に使用する**:
  
  TVP を使用してテーブルに入力しているときに、`sql_variant` 型の列に NULL 値を送信した場合、例外が発生します。 TVPでの `sql_variant` 型の列への NULL 値の挿入は、現在サポートされていません。

### <a name="implemented-prepared-statement-metadata-caching"></a>準備されたステートメントのメタデータのキャッシュを実装

JDBC Driver では、パフォーマンスを向上させるための準備されたステートメントのメタデータのキャッシュが実装されています。 ドライバーでは、準備されたステートメントのメタデータをドライバー内でキャッシュすることがサポートされるようになりました。これには、接続プロパティ `disableStatementPooling` と `statementPoolingCacheSize` が使用されます。 この機能は、既定では無効化されています。 詳細については、「[Prepared statement metadata caching for the JDBC Driver (JDBC Driver での準備されたステートメントのメタデータのキャッシュ)](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)」を参照してください。

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Linux/Mac での Azure AD 統合認証のサポートを追加

JDBC ドライバーでは、サポート対象のすべてのオペレーティング システム (Windows、Linux、Mac) 上で Kerberos を使った Azure Active Directory (Azure AD) 統合認証がサポートされるようになりました。 別の方法として、Windows オペレーティング システムでは sqljdbc_auth.dll を使用して認証できます。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>"Microsoft Azure Active Directory Authentication Library (ADAL4J) for Java" バージョン: 1.4.0 に更新

SQL Server 用 Microsoft JDBC Driver 7.0 では、"Microsoft Azure Active Directory 認証ライブラリ (ADAL4J) for Java" に関する Maven の依存関係が 1.4.0 に更新されています。 依存関係の詳細については、「[Microsoft JDBC Driver for SQL Server の機能の依存関係](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。

## <a name="62"></a>6.2

SQL Server 用 Microsoft JDBC Driver 6.2 は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 6\.2 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。 たとえば、6.2 パッケージの mssql-jdbc-6.2.2.jre8.jar ファイルは、Java 8 で使用することが推奨されています。

> [!NOTE]  
> 2017 年 6 月 29 日にリリースされた JDBC 6.2 RTW で、メタデータのキャッシュの機能強化に問題があることがわかりました。 この機能強化はロールバックされ、2017 年 7 月 17 日に新しい jar (バージョン 6.2.1) がリリースされました。 
>
> 別の機能強化として、Azure Key Vault に依存するライブラリのバージョンが 1.0.0 にアップグレードされ、2017 年 10 月 19 日に新しい jar (バージョン 6.2.2) がリリースされました。
>
> JDBC Driver 6.2 の最新の更新を [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460)、[GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) および [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) からダウンロードしてください。 6\.2.2 リリースの jar を使用するようにプロジェクトを更新してください。 詳細については、[6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) および [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) のリリース ノートをご覧ください。

### <a name="azure-ad-support-for-linux"></a>Linux での Azure AD のサポート

ユーザー名/パスワードとアクセス トークンによる Azure AD 認証を使用して、Linux アプリケーションを Azure SQL Database に接続します。

### <a name="fips-enabled-jvms"></a>FIPS 対応 JVM

米国連邦標準規格を満たす Federal Information Processing Standard (FIPS) 140 準拠モードで実行されている JVM で JDBC Driver を使用できるようになりました。

### <a name="kerberos-authentication-improvements"></a>Kerberos 認証の機能強化

JDBC Driver で、以下がサポートされるようになりました。

- Kerberos 構成を変更できない、または新しいトークンまたは keytab を取得できないアプリケーションでのプリンシパル/パスワードの使用。 Kerberos 認証のみが許可される SQL Server インスタンスへの認証でこの方法を使用できます。
- サーバー SPN の明示的な設定なしで Kerberos 統合認証を使用するレルム間認証。 ドライバーでは、レルムが提供されていない場合でも、自動的にそれを計算するようになりました。
- 偽装されたユーザーの資格情報をデータ ソース経由の GSS 資格情報オブジェクトとして受け入れることによる Kerberos の制約付き委任。 この偽装された資格情報を使用して、Kerberos 接続が確立されます。

### <a name="added-timeouts"></a>タイムアウトを追加

JDBC Driver では、次の構成可能なタイムアウトがサポートされるようになりました。 アプリケーションのニーズに基づいてそれらを変更できます。

- クエリを実行しているときに、タイムアウトが発生する前に待機する秒数を制御するクエリのタイムアウト。
- ソケットの読み取りまたは受け入れで、タイムアウトが発生する前に待機するミリ秒数を指定するソケットのタイムアウト。

## <a name="61"></a>6.1

Microsoft JDBC Driver 6.1 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 これは、JDBC ドライバーの最初のオープン ソースのリリースです。 それには、Java のバージョンの互換性に対応する mssql-jdbc-6.1.0.jre8.jar ファイルと mssql-jdbc-6.1.0.jre7.jar ファイルが含まれています。

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 6\.0 パッケージ内の Jar は、JDBC API のバージョンの準拠に従って名前付けされています。 たとえば、6.0 パッケージの sqljdbc42.jar ファイルは、JDBC API 4.2 準拠です。 同様に、sqljdbc41.jar ファイルは、JDBC API 4.1 準拠です。

適切な sqljdbc42.jar または sqljdbc41.jar ファイルがあることを確認するには、次のコード行を実行します。 出力が "Driver version: 6.0.7507.100" であれば、JDBC Driver 6.0 パッケージがあります。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

ドライバーでは、SQL Server 2016 の Always Encrypted 機能がサポートされます。 この機能により、SQL Server インスタンスで機密データがプレーン テキストで表示されることはないことが保証されます。 Always Encrypted はアプリケーション内のデータを透過的に暗号化することによって動作します。そのため、SQL Server では暗号化データのみが処理され、プレーンテキスト値は処理されません。 SQL Server のインスタンスまたはホスト コンピューターが侵害されたとしても、攻撃者が取得できるものは機密データの暗号化テキストだけになります。 詳細については、「[JDBC ドライバーでの Always Encrypted の使用](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)」をご覧ください。

### <a name="internationalized-domain-names"></a>国際化ドメイン名

ドライバーでは、サーバー名に関する国際化ドメイン名 (IDN) がサポートされます。 詳細については、記事「[International features of the JDBC Driver (JDBC Driver の国際化機能)](../../connect/jdbc/international-features-of-the-jdbc-driver.md)」の「Using International Domain Names (国際化ドメイン名の使用)」を参照してください。

### <a name="parameterized-queries"></a>パラメーター化クエリ

ドライバーで、サブクエリや結合など、複雑なクエリのために準備されたステートメントを使ったパラメーター メタデータの取得がサポートされました。 この機能強化を使用できるのは、SQL Server 2012 以降のバージョンを使用している場合のみであることに注意してください。

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 認証は、Azure AD の ID を使用して Azure SQL Database v12 に接続するメカニズムです。 Azure AD 認証は、データベース ユーザーの ID を一元管理するために、SQL Server 認証の代替として使用します。 

JDBC Driver 6.0 を使用して、Azure AD の資格情報を JDBC 接続文字列内に指定して Azure SQL Database に接続できます。 詳細については、「[Setting the connection properties (接続プロパティの設定)](../../connect/jdbc/setting-the-connection-properties.md)」の認証プロパティを参照してください。

### <a name="table-valued-parameters"></a>テーブル値パラメーター

TVP は、複数行のデータをクライアント アプリケーションから SQL Server に簡単にマーシャリングするための手段です。複数のラウンド トリップや、データ処理用の特別なサーバー側ロジックは必要ありません。 TVP を使用すると、1 つのパラメーター化コマンドで、クライアント アプリケーションで複数行のデータをカプセル化し、そのデータをサーバーに送信できます。 受信データ行はテーブル変数に格納され、Transact-SQL を使用して操作できます。 詳細については、「[テーブル値パラメーターの使用](../../connect/jdbc/using-table-valued-parameters.md)」を参照してください。

### <a name="always-on-availability-groups"></a>Always On 可用性グループ

ドライバーでは、AlwaysOn 可用性グループへの透過的な接続がサポートされるようになりました。 ドライバーによってサーバー インフラストラクチャの現在の Always On トポロジがすばやく検出され、現在アクティブなサーバーに透過的に接続されます。

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 4\.2 パッケージ内の Jar は、JDBC API のバージョンの準拠に従って名前付けされています。 たとえば、4.2 パッケージの sqljdbc42.jar ファイルは、JDBC API 4.2 準拠です。 同様に、sqljdbc41.jar ファイルは、JDBC API 4.1 準拠です。

適切な sqljdbc42.jar または sqljdbc41.jar ファイルがあることを確認するには、次のコード行を実行します。 出力が "Driver version: 4.2.6420.100" であれば、JDBC Driver 4.2 パッケージがあります。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>JDK 8 のサポート

ドライバーでは、JDK 7.0、6.0、および 5.0 に加え、JDK バージョン 8.0 がサポートされています。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 および 4.2 への準拠

ドライバーで、Java Database Connectivity API 4.0 だけでなく、4.1 と 4.2 の仕様もサポートされるようになりました。 詳細については、「[JDBC Driver の JDBC 4.1 への準拠](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)」および「[JDBC Driver の JDBC 4.2 への準拠](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)」を参照してください。

### <a name="bulk-copy"></a>一括コピー

一括コピー機能を使うと、SQL Server データベースのテーブルまたはビューに大量のデータを簡単にコピーできます。 詳細については、「[JDBC ドライバーでの一括コピーの使用](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)」をご覧ください。

### <a name="xa-transaction-rollback-option"></a>XA トランザクション ロールバック オプション

既存の準備解除されたトランザクションの自動ロールバックに向けた、新しいタイムアウト オプションがドライバーに追加されました。 詳細については、「[Understanding XA transactions (XA トランザクションについて)](../../connect/jdbc/understanding-xa-transactions.md)」を参照してください。

### <a name="new-kerberos-principal-connection-property"></a>新しい Kerberos プリンシパル接続プロパティ

Kerberos 接続での柔軟性を強化するために、ドライバーで新しい接続プロパティが使用されます。 詳細については、「[Kerberos 統合認証による SQL Server への接続](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)」をご覧ください。

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>JDK 7 のサポート

ドライバーでは、JDK 6.0 および 5.0 に加え、JDK バージョン 7.0 がサポートされています。

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium では JDBC Driver 6.4、6.0、4.2、4.1 アプリケーションがサポートされない

Microsoft JDBC Drivers 6.4、6.0、4.2、4.1 for SQL Server アプリケーションは、Itanium コンピューター上での実行がサポートされていません。

## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)
