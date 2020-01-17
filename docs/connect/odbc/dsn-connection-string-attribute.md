---
title: ODBC ドライバーのための DSN と接続文字列のキーワード - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: MightyPen
ms.author: v-jizho2
author: karinazhou
ms.openlocfilehash: c06f6e9f95af02ba6240f9f71ac6a92c25bec755
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71712925"
---
# <a name="dsn-and-connection-string-keywords-and-attributes"></a>DSN と接続文字列のキーワードと属性

このページでは、ODBC Driver for SQL Server で使用可能な、接続文字列と DSN でのキーワード、および SQLSetConnectAttr と SQLGetConnectAttr に対する接続属性の一覧を示します。

## <a name="supported-dsnconnection-string-keywords-and-connection-attributes"></a>サポートされる DSN/接続文字列のキーワードおよび接続属性

次の表では、各プラットフォーム (L: Linux、M: Mac、W: Windows) で使用可能なキーワードと属性の一覧を示します。 キーワードまたは属性をクリックすると、詳細が表示されます。

| DSN / 接続文字列のキーワード | 接続属性 | プラットフォーム |
|-|-|-|
| [Addr](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Address](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [AnsiNPW](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ANSI_NPW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssansinpw) | LMW |
| [APP](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ApplicationIntent](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_APPLICATION_INTENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssapplicationintent) | LMW |
| [AttachDBFileName](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ATTACHDBFILENAME](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssattachdbfilename) | LMW |
| [[認証]](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sql_copt_ss_authentication) | [SQL_COPT_SS_AUTHENTICATION](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sql_copt_ss_authentication) | LMW |
| [AutoTranslate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRANSLATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstranslate) | LMW |
| [ColumnEncryption](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sql_copt_ss_column_encryption) | [SQL_COPT_SS_COLUMN_ENCRYPTION](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sql_copt_ss_column_encryption) | LMW |
| [ConnectRetryCount](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_COUNT](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [ConnectRetryInterval](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_INTERVAL](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [[データベース]](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_ATTR_CURRENT_CATALOG](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| [[説明]](../../connect/odbc/dsn-connection-string-attribute.md#description) | | LMW |
| [[ドライバー]](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [DSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Encrypt](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ENCRYPT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssencrypt) | LMW |
| [Failover_Partner](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssfailoverpartner) | W |
| [FailoverPartnerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | W |
| [FileDSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [KeepAlive](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md) (v 17.4 +、DSN のみ)| | LMW |
| [KeepAliveInterval](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md) (v 17.4 +、DSN のみ) | | LMW |
| [KeystoreAuthentication](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystorePrincipalId](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystoreSecret](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [言語](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [MARS_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MARS_ENABLED](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmarsenabled) | LMW |
| [MultiSubnetFailover](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MULTISUBNET_FAILOVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmultisubnetfailover) | LMW |
| [Net](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Network](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [PWD](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [QueryLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquery) | W |
| [QueryLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquerylog) | W |
| [QueryLogTIme](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_INTERVAL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfqueryinterval) | W |
| [QuotedId](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_QUOTED_IDENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssquotedident) | LMW |
| [Regional](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [SaveFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [[サーバー]](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ServerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_SERVER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| [StatsLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdata) | W |
| [StatsLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalog) | W |
| [TransparentNetworkIPResolution](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sql_copt_ss_tnir) | [SQL_COPT_SS_TNIR](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sql_copt_ss_tnir) | LMW |
| [Trusted_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_INTEGRATED_SECURITY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssintegratedsecurity) | LMW |
| [TrustServerCertificate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRUST_SERVER_CERTIFICATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstrustservercertificate) | LMW |
| [UID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [UseFMTONLY](../../connect/odbc/dsn-connection-string-attribute.md#usefmtonly) | | LMW |
| [WSID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| | [SQL_ATTR_ACCESS_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ACCESS_MODE) | LMW |
| | [SQL_ATTR_ASYNC_DBC_EVENT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCALLBACK](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCONTEXT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_AUTO_IPD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_AUTOCOMMIT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_AUTOCOMMIT) | LMW |
| | [SQL_ATTR_CONNECTION_DEAD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_CONNECTION_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_DBC_INFO_TOKEN](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_LOGIN_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_LOGIN_TIMEOUT) | LMW |
| | [SQL_ATTR_METADATA_ID](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_ODBC_CURSORS](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ODBC_CURSORS) | LMW |
| | [SQL_ATTR_PACKET_SIZE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_PACKET_SIZE) | LMW |
| | [SQL_ATTR_QUIET_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_QUIET_MODE) | LMW |
| | [SQL_ATTR_RESET_CONNECTION](../../odbc/reference/develop-driver/upgrading-a-3-5-driver-to-a-3-8-driver.md#connection-pooling) <br> (SQL_COPT_SS_RESET_CONNECTION) | LMW |  
| | [SQL_ATTR_TRACE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACE) | LMW |
| | [SQL_ATTR_TRACEFILE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACEFILE) | LMW |
| | [SQL_ATTR_TRANSLATE_LIB](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_DLL) | LMW |
| | [SQL_ATTR_TRANSLATE_OPTION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_OPTION) | LMW |
| | [SQL_ATTR_TXN_ISOLATION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TXN_ISOLATION) | LMW |
| | [SQL_COPT_SS_ACCESS_TOKEN](dsn-connection-string-attribute.md#sql_copt_ss_access_token) | LMW |
| | [SQL_COPT_SS_ANSI_OEM](dsn-connection-string-attribute.md#sql_copt_ss_ansi_oem)| W |
| | [SQL_COPT_SS_BCP](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbcp) | LMW |
| | [SQL_COPT_SS_BROWSE_CACHE_DATA](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) | LMW |
| | [SQL_COPT_SS_BROWSE_CONNECT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseconnect) | LMW |
| | [SQL_COPT_SS_BROWSE_SERVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseserver) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREDATA](dsn-connection-string-attribute.md#sql_copt_ss_cekeystoredata) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREPROVIDER](dsn-connection-string-attribute.md#sql_copt_ss_cekeystoreprovider) | LMW |
| | [SQL_COPT_SS_CLIENT_CONNECTION_ID](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) | LMW |
| | [SQL_COPT_SS_CONCAT_NULL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconcatnull) | LMW |
| | [SQL_COPT_SS_CONNECTION_DEAD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconnectiondead) | LMW |
| | [SQL_COPT_SS_ENLIST_IN_DTC](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistindtc) | W |
| | [SQL_COPT_SS_ENLIST_IN_XA](dsn-connection-string-attribute.md#sql_copt_ss_enlist_in_xa) | LMW |
| | [SQL_COPT_SS_FALLBACK_CONNECT](dsn-connection-string-attribute.md#sql_copt_ss_fallback_connect) | LMW |
| | [SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_MUTUALLY_AUTHENTICATED](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_OLDPWD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssoldpwd) | LMW |
| | [SQL_COPT_SS_PERF_DATA_LOG_NOW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalognow) | W |
| | [SQL_COPT_SS_PRESERVE_CURSORS](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsspreservecursors) | LMW |
| | [SQL_COPT_SS_TXN_ISOLATION](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstxnisolation) | LMW |
| | [SQL_COPT_SS_USER_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssuserdata) | LMW |
| | [SQL_COPT_SS_WARN_ON_CP_ERROR](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsswarnoncperror) | LMW |
| [ClientCertificate](../../connect/odbc/dsn-connection-string-attribute.md#clientcertificate) | | LMW | 
| [ClientKey](../../connect/odbc/dsn-connection-string-attribute.md#clientkey) | | LMW | 


以下では、「[SQL Server Native Client での接続文字列キーワードの使用](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」、「[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)」、「[SQLSetConnectAttr 関数](../../odbc/reference/syntax/sqlsetconnectattr-function.md)」に記載されていないいくつかの接続文字列キーワードと接続属性を示します。

### <a name="description"></a>[説明]

データ ソースの説明に使用されます。

### <a name="sql_copt_ss_ansi_oem"></a>SQL_COPT_SS_ANSI_OEM

データの ANSI から OEM への変換を制御します。 

| 属性値 | [説明] |
|-|-|
| SQL_AO_OFF | (既定値) 変換は行われません。 |
| SQL_AO_ON | 変換は行われます。 |

### <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT

SQL Server のフォールバック接続の使用を制御します。 これはサポートされなくなりました。

| 属性値 | [説明] |
|-|-|
| SQL_FB_OFF | (既定値) フォールバック接続は無効です。 |
| SQL_FB_ON | フォールバック接続は有効です。 |



## <a name="new-connection-string-keywords-and-connection-attributes"></a>新しい接続文字列のキーワードおよび接続属性

###  <a name="authentication---sql_copt_ss_authentication"></a>認証 - SQL_COPT_SS_AUTHENTICATION

SQL Server に接続するときに使用する認証モードを設定します。 詳しくは、「[Azure Active Directory の使用](using-azure-active-directory.md)」をご覧ください。

| キーワードの値 | 属性値 | [説明] |
|-|-|-|
| |SQL_AU_NONE|(既定値) 設定されていません。 認証モードは、他の属性の組み合わせによって決まります。|
|SqlPassword|SQL_AU_PASSWORD|ユーザー名とパスワードを使用する SQL Server 認証。|
|ActiveDirectoryIntegrated|SQL_AU_AD_INTEGRATED|Azure Active Directory 統合認証。|
|ActiveDirectoryPassword|SQL_AU_AD_PASSWORD|Azure Active Directory パスワード認証。|
|ActiveDirectoryInteractive|SQL_AU_AD_INTERACTIVE|Azure Active Directory 対話型認証。|
|ActiveDirectoryMsi|SQL_AU_AD_MSI|Azure Active Directory マネージド サービス ID 認証。 ユーザー割り当て ID の場合、UID はユーザー ID のオブジェクト ID に設定されます。 |
| |SQL_AU_RESET|未設定。 すべての DSN または接続文字列の設定をオーバーライドします。|

> [!NOTE]
> `Authentication` キーワードまたは属性を使用するときは、接続文字列/DSN/接続属性で必要な値に対する `Encrypt` の設定を明示的に指定します。 詳しくは、「[Using Connection String Keywords with SQL Server Native Client (SQL Server Native Client での接続文字列キーワードの使用)](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」をご覧ください。

### <a name="columnencryption---sql_copt_ss_column_encryption"></a>ColumnEncryption - SQL_COPT_SS_COLUMN_ENCRYPTION

透過的な列の暗号化を制御します (Always Encrypted)。 詳しくは、「[Using Always Encrypted (ODBC) (Always Encrypted の使用 (ODBC))](using-always-encrypted-with-the-odbc-driver.md)」をご覧ください。

| キーワードの値 | 属性値 | [説明] |
|-|-|-|
|有効|SQL_CE_ENABLED|Always Encrypted を有効にします。|
|Disabled|SQL_CE_DISABLED|(既定値) Always Encrypted を無効にします。|
| |SQL_CE_RESULTSETONLY|解読のみを有効にします (結果と戻り値)。|

### <a name="transparentnetworkipresolution---sql_copt_ss_tnir"></a>TransparentNetworkIPResolution - SQL_COPT_SS_TNIR

透過的ネットワーク IP 解決機能を制御します。この機能は、MultiSubnetFailover と対話して、より速い再接続の試行を可能にします。 詳しくは、「[透過的なネットワーク IP の解決の使用](using-transparent-network-ip-resolution.md)」をご覧ください。

| キーワードの値 | 属性値| [説明] |
|-|-|-|
|はい|SQL_IS_ON|(既定値) 透過的なネットワーク IP の解決を有効にします。|
|いいえ|SQL_IS_OFF|透過的なネットワーク IP の解決を無効にします。|

### <a name="usefmtonly"></a>UseFMTONLY

SQL Server 2012 以降に接続するときの、メタデータに対する SET FMTONLY の使用を制御します。

| キーワードの値 | [説明] |
|-|-|
|いいえ|(既定値) 使用可能な場合は、メタデータに sp_describe_first_result_set を使用します。 |
|はい| メタデータに SET FMTONLY を使用します。 |


## <a name="clientcertificate"></a>ClientCertificate

認証に使用する証明書を指定します。 使用可能なオプションは次のとおりです。 

| オプション値 | [説明] |
|-|-|
| sha1:`<hash_value>` | ODBC ドライバーは SHA1 ハッシュを使用して Windows 証明書ストア内の証明書を検索します。 |
| subject:`<subject>` | ODBC ドライバーは、サブジェクトを使用して Windows 証明書ストアで証明書を検索します。 |
| ファイル: `<file_location>` [、パスワード: `<password>`] | ODBC ドライバーは、証明書ファイルを使用します。 |

証明書が PFX 形式であり、PFX 証明書内の秘密キーがパスワードで保護されている場合は、password キーワードが必要です。 PEM および DER 形式の証明書の場合、ClientKey 属性が必要です


## <a name="clientkey"></a>ClientKey

ClientCertificate 属性によって指定された PEM または DER 証明書の秘密キーのファイルの場所を指定します。 形式: 

| オプション値 | [説明] |
|-|-|
| ファイル: `<file_location>` [、パスワード: `<password>`] | 秘密キーファイルの場所を指定します。 |

秘密キーファイルがパスワードで保護されている場合は、password キーワードが必要です。 パスワードに "," 文字が含まれている場合は、その後に "," という文字が追加されます。 たとえば、パスワードが "a, b, c" の場合、接続文字列に含まれるエスケープされたパスワードは "a,, b,, c" になります。 
    

### <a name="sql_copt_ss_access_token"></a>SQL_COPT_SS_ACCESS_TOKEN

認証のための Azure Active Directory のアクセス トークンの使用を許可します。 詳しくは、「[Azure Active Directory の使用](using-azure-active-directory.md)」をご覧ください。

| 属性値 | [説明] |
|-|-|
| NULL | (既定値) アクセス トークンが提供されていません。 |
| ACCESSTOKEN* | アクセス トークンへのポインター。 |

### <a name="sql_copt_ss_cekeystoredata"></a>SQL_COPT_SS_CEKEYSTOREDATA

読み込まれたキーストア プロバイダー ライブラリと通信します。 透過的な列の暗号化を制御します (Always Encrypted)。 この属性には既定値はありません。 詳しくは、「[カスタム キーストア プロバイダー](custom-keystore-providers.md)」をご覧ください。

| 属性値 | [説明] |
|-|-|
| CEKEYSTOREDATA * | キーストア プロバイダー ライブラリ用の通信データ構造 |

### <a name="sql_copt_ss_cekeystoreprovider"></a>SQL_COPT_SS_CEKEYSTOREPROVIDER

Always Encrypted 用のキーストア プロバイダー ライブラリを読み込むか、または読み込まれたキーストア プロバイダー ライブラリの名前を取得します。 詳しくは、「[カスタム キーストア プロバイダー](custom-keystore-providers.md)」をご覧ください。 この属性には既定値はありません。

| 属性値 | [説明] |
|-|-|
| char * | キーストア プロバイダー ライブラリへのパス |

### <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA

XA 準拠トランザクション プロセッサ (TP) での XA トランザクションを有効にするには、アプリケーションで SQL_COPT_SS_ENLIST_IN_XA および `XACALLPARAM` オブジェクトへのポインターを指定して **SQLSetConnectAttr** を呼び出す必要があります。 このオプションは、Windows、(17.3 以降) Linux、Mac でサポートされています。
```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, param, SQL_IS_POINTER);  // XACALLPARAM *param
``` 
 XA トランザクションを ODBC 接続のみと関連付けるには、**SQLSetConnectAttr** を呼び出すときに、ポインターではなく、SQL_COPT_SS_ENLIST_IN_XA で TRUE または FALSE を指定します。 これは Windows でのみ有効であり、クライアント アプリケーションで XA 操作を指定するために使用することはできません。 
 ```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, (SQLPOINTER)TRUE, 0);
``` 

|[値]|[説明]|プラットフォーム|  
|-----------|-----------------|-----------------|  
|XACALLPARAM object*|`XACALLPARAM` オブジェクトを指すポインター。|Windows、Linux、Mac|
|TRUE|XA トランザクションを ODBC 接続に関連付けます。 関連するすべてのデータベース アクティビティは、XA トランザクションの保護下で実行されます。|Windows|  
|FALSE|トランザクションと ODBC 接続の関連付けを解除します。|Windows|

 XA トランザクションについて詳しくは、「[XA トランザクションの使用](../../connect/odbc/use-xa-with-dtc.md)」をご覧ください。
