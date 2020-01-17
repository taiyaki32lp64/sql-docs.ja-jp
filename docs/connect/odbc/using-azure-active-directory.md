---
title: ODBC Driver | を使用した Azure Active Directory の使用 |SQL Server の Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0f9d73dace4e17d87e1c93da703786fc920b2fb
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176169"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>ODBC ドライバーでの Azure Active Directory の使用
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>用途

バージョン13.1 以降の Microsoft ODBC Driver for SQL Server では、ODBC アプリケーションは、ユーザー名/パスワード、Azure Active Directory アクセストークン、Azure Active を使用して Azure Active Directory のフェデレーション id を使用して SQL Azure のインスタンスに接続できます。ディレクトリ管理対象サービス id、または Windows 統合認証 (_windows ドライバーのみ_)。 ODBC ドライバーバージョン13.1 では、Azure Active Directory アクセストークン認証は_Windows のみ_です。 ODBC ドライバーバージョン17以降では、すべてのプラットフォーム (Windows、Linux、Mac) でこの認証がサポートされています。 ログイン ID を使用した新しい Azure Active Directory 対話型認証は、ODBC Driver version 17.1 for Windows で導入されました。 新しい Azure Active Directory 管理されたサービス id の認証方法が、システムによって割り当てられた id とユーザーが割り当てられた id の両方について、ODBC Driver version 17.3.1.1 に追加されました。 これらはすべて、新しい DSN および接続文字列キーワードと接続属性を使用して実現されます。

> [!NOTE]
> Linux および macOS の ODBC ドライバーでは、Active Directory フェデレーションサービス (AD FS) はサポートされていません。 Linux または macOS クライアントから Azure Active Directory ユーザー名/パスワード認証を使用しており、Active Directory 構成にフェデレーションサービスが含まれている場合、認証が失敗する可能性があります。

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>新規または変更された DSN と接続文字列のキーワード

`Authentication`キーワードは、認証モードを制御するために、DSN または接続文字列を使用して接続するときに使用できます。 接続文字列に設定されている値は、DSN 内で指定されている場合にオーバーライドされます。 `Authentication`設定の_属性前の値_は、接続文字列と DSN の値から計算された値です。

|[オブジェクト名]|値|既定|[説明]|
|-|-|-|-|
|`Authentication`|(設定されていません)、 `SqlPassword`(空`ActiveDirectoryIntegrated`の`ActiveDirectoryInteractive`文字列)、 `ActiveDirectoryPassword`、、、、`ActiveDirectoryMsi` |(未設定)|認証モードを制御します。<table><tr><th>[値]<th>[説明]<tr><td>(未設定)<td>他のキーワードによって決定される認証モード (既存の従来の接続オプション)。<tr><td>(空の文字列)<td>接続文字列のヘルプDSN で設定さ`Authentication`れた値をオーバーライドおよび設定解除します。<tr><td>`SqlPassword`<td>ユーザー名とパスワードを使用して、SQL Server インスタンスに直接認証します。<tr><td>`ActiveDirectoryPassword`<td>ユーザー名とパスワードを使用して Azure Active Directory id で認証します。<tr><td>`ActiveDirectoryIntegrated`<td>_Windows ドライバーのみ_。 統合認証を使用して Azure Active Directory id で認証します。<tr><td>`ActiveDirectoryInteractive`<td>_Windows ドライバーのみ_。 対話型認証を使用して Azure Active Directory id で認証します。<tr><td>`ActiveDirectoryMsi`<td>マネージドサービス id 認証を使用して Azure Active Directory id で認証します。 ユーザー割り当て ID の場合、UID はユーザー ID のオブジェクト ID に設定されます。</table>|
|`Encrypt`|(未設定)、`Yes`、`No`|(説明を参照)|接続の暗号化を制御します。 `Authentication`設定の事前属性値が DSN または接続文字列で_none_でない場合、既定値は`Yes`になります。 それ以外の場合、既定値は `No` です。 属性`SQL_COPT_SS_AUTHENTICATION`がの`Authentication`事前属性値をオーバーライドする場合は、DSN または接続文字列または接続属性で Encryption の値を明示的に設定します。 値が DSN または接続文字列の`Yes`いずれかでに設定さ`Yes`れている場合、暗号化の事前属性値はになります。|

## <a name="new-andor-modified-connection-attributes"></a>新規または変更された接続属性

次の接続前接続属性は、Azure Active Directory 認証をサポートするために導入または変更されています。 接続属性に対応する接続文字列または DSN キーワードがあり、が設定されている場合、接続属性が優先されます。

|属性|型|値|既定|[説明]|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`､`SQL_AU_PASSWORD`、`SQL_AU_AD_INTEGRATED`、`SQL_AU_AD_PASSWORD`、`SQL_AU_AD_INTERACTIVE`、`SQL_AU_AD_MSI`、`SQL_AU_RESET`|(未設定)|上のキーワード`Authentication`の説明を参照してください。 `SQL_AU_NONE`は、dsn または接続文字列`Authentication` `SQL_AU_RESET`の設定値を明示的にオーバーライドするために用意されています。設定されている場合は、属性が解除され、dsn または接続文字列の値が優先されるようになります。|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|または`ACCESSTOKEN` NULL へのポインター|NULL|Null 以外の場合は、使用する AzureAD アクセストークンを指定します。 アクセス`UID`トークンと`PWD` `Authentication` 、、、、または接続文字列キーワードまたは同等の属性を指定すると、エラーになります。 `Trusted_Connection` <br> **注:** ODBC ドライバーバージョン13.1 では、 _Windows_でのみサポートされています。|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(説明を参照)|接続の暗号化を制御します。 `SQL_EN_OFF`暗号化`SQL_EN_ON`を無効にして有効にします。 `Authentication`設定の事前属性値が_none_でない場合、また`SQL_COPT_SS_ACCESS_TOKEN`はが設定されていて`Encrypt` 、DSN または接続文字列でが指定され`SQL_EN_ON`ていない場合、既定値はになります。 それ以外の場合、既定値は `SQL_EN_OFF` です。 接続属性`SQL_COPT_SS_AUTHENTICATION`が _[なし_] に設定されている`SQL_COPT_SS_ENCRYPT`場合は、DSN または接続文字列でが指定されていない場合`Encrypt`は、目的の値に明示的にを設定します。 この属性の有効値は、[接続に暗号化を使用するかどうかを制御します。](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Azure Active Directory ではサポートされていません。 AAD プリンシパルへのパスワード変更は、ODBC 接続を使用して行うことはできません。 <br><br>SQL Server 2005 では、SQL Server 認証におけるパスワードの期限切れが導入されました。 `SQL_COPT_SS_OLDPWD`属性が追加され、クライアントが接続に古いパスワードと新しいパスワードの両方を提供できるようになりました。 この属性が設定されている場合、接続文字列には変更された "古いパスワード" が含まれているので、プロバイダーは最初の接続またはそれ以降の接続で接続プールを使用しません。|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`、`SQL_IS_ON`|`SQL_IS_OFF`|_非推奨_です。代わりに`SQL_COPT_SS_AUTHENTICATION` set を`SQL_AU_AD_INTEGRATED`使用してください。 <br><br>サーバーログインのアクセスを検証するために、Windows 認証 (Linux および macOS では Kerberos) を強制的に使用します。 Windows 認証を使用すると、、 `SQLConnect` `SQLDriverConnect`、またはの処理の一部として指定され`SQLBrowseConnect`たユーザー識別子とパスワードの値は、ドライバーによって無視されます。|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory 用の UI の追加 (Windows ドライバーのみ)

Azure AD で認証を使用するために必要な追加オプションを使用して、ドライバーの DSN セットアップと接続の Ui が強化されました。

### <a name="creating-and-editing-dsns-in-the-ui"></a>UI での Dsn の作成と編集

新しい Azure AD 認証オプションは、ドライバーのセットアップ UI を使用して既存の DSN を作成または編集するときに使用できます。

SQL Azure への Azure Active Directory 統合認証の場合: `Authentication=ActiveDirectoryIntegrated`

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`Azure Active Directory のユーザー名/パスワード認証を SQL Azure にするには

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` SQL Azure に Azure Active Directory 対話型認証

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`SQL Server に対するユーザー名/パスワード認証の場合 (Azure またはそれ以外)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`Windows 従来の SSPI 統合認証の場合

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

5つのオプションは`Trusted_Connection=Yes` 、(既存のレガシ Windows SSPI のみの統合認証`Authentication=` ) `SqlPassword`と`ActiveDirectoryPassword` `ActiveDirectoryIntegrated`、、 `ActiveDirectoryInteractive`、、およびのそれぞれに対応しています。

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect Prompt (Windows ドライバーのみ)

接続を完了するために必要な情報を要求するときに SQLDriverConnect によって表示されるプロンプトダイアログには、Azure AD 認証に関する3つの新しいオプションが含まれています。

![ServerLogin.png](windows/ServerLogin.png)

これらのオプションは、上記の DSN セットアップ UI で使用できるのと同じ5つのオプションに対応しています。

### <a name="example-connection-strings"></a>接続文字列の例
1. SQL Server 認証-レガシ構文。 サーバー証明書は検証されず、暗号化はサーバーで適用される場合にのみ使用されます。 ユーザー名/パスワードは接続文字列で渡されます。
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 認証-新しい構文。 クライアントが暗号化を要求する`Encrypt` (の既定値は)。がに`true`設定されている場合を除き`TrustServerCertificate` 、暗号化の設定に関係なく、サーバー証明書が検証さ`true`れます。 ユーザー名/パスワードは接続文字列で渡されます。
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. SSPI (SQL Server または SQL IaaS) を使用した統合 Windows 認証 (Linux および macOS の Kerberos)-現在の構文。 暗号化を使用しない限り、サーバー証明書は検証されません。 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows ドライバーのみ_)。SSPI を使用した統合 Windows 認証 (ターゲットデータベースが SQL Server または SQL IaaS の場合)-新しい構文。 クライアントが暗号化を要求する`Encrypt` (の既定値は)。がに`true`設定されている場合を除き`TrustServerCertificate` 、暗号化の設定に関係なく、サーバー証明書が検証さ`true`れます。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD のユーザー名/パスワード認証 (ターゲットデータベースが Azure SQL DB 内にある場合)。 サーバー証明書は、暗号化の設定に関係なく検証`TrustServerCertificate`されます`true`(がに設定されている場合を除く)。 ユーザー名/パスワードは接続文字列で渡されます。 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows ドライバーのみ_)。ADAL を使用した統合 Windows 認証。ターゲットデータベースが Azure SQL Database であると仮定して、AAD によって発行されたアクセストークンの Windows アカウント資格情報を引き換えます。 サーバー証明書は、暗号化の設定に関係なく検証`TrustServerCertificate`されます`true`(がに設定されている場合を除く)。 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Windows ドライバーのみ_)。AAD Interactive Authentication は、Azure Multi-factor Authentication テクノロジを使用して接続をセットアップします。 このモードでは、ログイン ID を指定することにより、Azure 認証ダイアログがトリガーされ、ユーザーはパスワードを入力して接続を完了できるようになります。 ユーザー名は接続文字列で渡されます。
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. AAD マネージドサービス ID 認証では、認証のためにシステムによって割り当てられた id またはユーザーが割り当てた id を使用して接続を設定します。 ユーザー割り当て ID の場合、UID はユーザー ID のオブジェクト ID に設定されます。<br>
システムによって割り当てられた ID の場合:<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
オブジェクト ID が myObjectId と等しいユーザー割り当て id の場合、<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- Windows ODBC ドライバーで新しい Active Directory オプションを使用する場合は、 [SQL Server の Active Directory 認証ライブラリ](https://go.microsoft.com/fwlink/?LinkID=513072)がインストールされていることを確認してください。 Linux および macOS ドライバーを使用する場合`libcurl`は、がインストールされていることを確認します。 ドライバーバージョン17.2 以降では、他の認証方法や ODBC 操作には必要ないため、これは明示的な依存関係ではありません。
>- SQL Server アカウントのユーザー名とパスワードを使用して接続するには、 `SqlPassword` [新規] オプションを使用することができます。このオプションは、より安全な接続の既定値を有効にするため、特に SQL Azure に対して推奨されます。
>- Azure Active Directory アカウントのユーザー名とパスワードを使用して`Authentication=ActiveDirectoryPassword`接続するには、接続文字列`PWD`にを指定し、ユーザー名とパスワードを使用してとの`UID`キーワードをそれぞれ指定します。
>- Windows 統合または Active Directory 統合 (windows ドライバーのみ) 認証を使用して`Authentication=ActiveDirectoryIntegrated`接続するには、接続文字列でを指定します。 ドライバーは自動的に適切な認証モードを選択します。 `UID`および`PWD`を指定することはできません。
>- Active Directory Interactive (Windows driver only) 認証を使用して`UID`接続するには、を指定する必要があります。

## <a name="authenticating-with-an-access-token"></a>アクセストークンを使用した認証

`SQL_COPT_SS_ACCESS_TOKEN`事前接続属性を使用すると、ユーザー名とパスワードの代わりに Azure AD から取得したアクセストークンを認証に使用できるようになります。また、ドライバーによるアクセストークンのネゴシエーションと取得もバイパスされます。 アクセストークンを使用するには、 `SQL_COPT_SS_ACCESS_TOKEN`接続属性を`ACCESSTOKEN`構造体へのポインターに設定します。

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

は、4バイトの_長さ_の後にアクセストークンを形成する不透明なデータの_長さ_ (バイト) で構成される可変長構造体です。 `ACCESSTOKEN` SQL Server がアクセストークンを処理する方法により、各バイトの後には、ASCII 文字のみを含む UCS 2 の文字列に似た0個の埋め込みバイトが続くように、 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 応答を介して取得されたものを展開する必要があります。ただし、トークンは不透明な値で、指定された長さ (バイト単位) に null 終端文字を含めることはできません。 この認証方法は、長い長さと形式の制約により、接続属性を介して`SQL_COPT_SS_ACCESS_TOKEN`プログラムでのみ使用できます。対応する DSN または接続文字列のキーワードはありません。 `UID`接続文字列には`PWD` `Trusted_Connection` 、、、、またはキーワードを含めることはできません。 `Authentication`

> [!NOTE]
> ODBC ドライバーバージョン13.1 では、この認証は_Windows_でのみサポートされています。

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 認証サンプル コード

次のサンプルは、Azure Active Directory を接続キーワードと共に使用して SQL Server に接続するために必要なコードを示しています。 アプリケーションコード自体を変更する必要はないことに注意してください。認証に AAD を使用するために必要な変更は、接続文字列、または DSN が使用されている場合は DSN だけです。
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
次のサンプルは、アクセストークン認証で Azure Active Directory を使用して SQL Server に接続するために必要なコードを示しています。 この場合、アクセストークンを処理し、関連付けられている接続属性を設定するようにアプリケーションコードを変更する必要があります。
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~
Azure Active Directory 対話型認証で使用するための接続文字列の例を次に示します。 パスワードが Azure 認証画面を使用して入力されるため、PWD フィールドは含まれていないことに注意してください。
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
Azure Active Directory マネージドサービス ID 認証で使用するための接続文字列の例を次に示します。 ユーザー割り当て ID に対して、UID がユーザー ID のオブジェクト ID に設定されていることに注意してください。
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>参照
[Azure AD auth を使用した Azure SQL DB でのトークンベースの認証のサポート](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

