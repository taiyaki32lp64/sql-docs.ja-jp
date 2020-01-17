---
title: プログラムによるパスワードの変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: def93c4860a7e1a29a4a721de3aa451f91fd1869
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761498"
---
# <a name="changing-passwords-programmatically"></a>プログラムによるパスワードの変更
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] より前のリリースでは、ユーザーのパスワードの有効期限が切れたとき、そのパスワードをリセットできるのは管理者だけでした。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以降では、native Client は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native client OLE DB プロバイダーと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーの両方、および**SQL Server ログイン**に対する変更を通じて、プログラムによってパスワードの有効期限を処理すること [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をサポートしています。ダイアログボックス。  
  
> [!NOTE]  
>  可能であれば、実行時にユーザーの資格情報を入力し、それらの資格情報を永続的な形式で保存しないように求めるメッセージが表示されます。 資格情報を保持する必要がある場合は、[Win32 Crypto API](https://go.microsoft.com/fwlink/?LinkId=64532) を使用して暗号化してください。 パスワードの使用に関する詳細については、「[強力なパスワード](../../../relational-databases/security/strong-passwords.md)」を参照してください。  
  
## <a name="sql-server-login-error-codes"></a>SQL Server ログイン エラー コード  
 認証の問題により接続できない場合、アプリケーションでは次のいずれかの SQL Server エラー コードを使用して、診断と復旧に役立てることができます。  
  
|SQL Server エラー コード|エラー メッセージ|  
|---------------------------|-------------------|  
|15113|ユーザー '%.*ls' はログインできませんでした。理由: パスワードの検証に失敗しました。 アカウントはロックアウトされています。|  
|18463|ユーザー '%.*ls' はログインできませんでした。 理由: パスワードを変更できませんでした。 この時点ではパスワードを使用できません。|  
|18464|ユーザー '%.*ls' はログインできませんでした。 理由: パスワードを変更できませんでした。 このパスワードは短すぎるので、Windows ポリシーの要件を満たしません。|  
|18465|ユーザー '%.*ls' はログインできませんでした。 理由: パスワードを変更できませんでした。 パスワードは長すぎるため、ポリシー要件を満たしません。|  
|18466|ユーザー '%.*ls' はログインできませんでした。 理由: パスワードを変更できませんでした。 このパスワードはあまり複雑ではないので、Windows のポリシー要件を満たしません。|  
|18467|ユーザー '%.*ls' はログインできませんでした。 理由: パスワードを変更できませんでした。 パスワードがパスワード フィルター DLL の要件を満たしていません。|  
|18468|ユーザー '%.*ls' はログインできませんでした。 理由: パスワードを変更できませんでした。 パスワードの検証で予期しないエラーが発生しました。|  
|18487|ユーザー '%.*ls' はログインできませんでした。 理由: このアカウントのパスワードの有効期限が切れています。|  
|18488|ユーザー '%.*ls' はログインできませんでした。 理由: このアカウントのパスワードを変更する必要があります。|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、ユーザーインターフェイスとプログラムを使ってパスワードの有効期限をサポートします。  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB ユーザー インターフェイスによるパスワード期限切れの処理  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **SQL Server ログイン**ダイアログボックスに対して行われた変更によって、パスワードの有効期限をサポートします。 DBPROP_INIT_PROMPT の値を DBPROMPT_NOPROMPT に設定すると、パスワードの有効期限が切れている場合に、最初の接続試行が失敗します。  
  
 DBPROP_INIT_PROMPT を DBPROMPT_NOPROMPT 以外の値に設定している場合は、パスワードの有効期限が切れているかどうかに関係なく、 **[SQL Server ログイン]** ダイアログ ボックスが表示されます。 ユーザーは、 **[オプション]** をクリックし、 **[パスワードの変更]** チェック ボックスをオンにしてパスワードを変更できます。  
  
 パスワードの有効期限が切れている場合にユーザーが [OK] をクリックすると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] からユーザーに **[パスワードの変更]** ダイアログ ボックスを使用して新しいパスワードを入力し、確認することを要求されます。  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB プロンプトの動作とロックされたアカウント  
 アカウントがロックされていることにより、接続に失敗することがあります。 **[SQL Server ログイン]** ダイアログ ボックスが表示された後にこの現象が発生する場合は、サーバー エラー メッセージが表示され、接続試行が中止されます。 また、 **[パスワードの変更]** ダイアログ ボックスが表示された後にユーザーが古いパスワードに無効な値を入力すると、この現象が発生することもあります。 この場合も同じエラー メッセージが表示され、接続試行が中止されます。  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 接続プーリング、パスワードの期限切れ、およびロックされたアカウント  
 接続プール内で接続がアクティブな状態になっている間に、アカウントがロックされたり、そのアカウントのパスワードの有効期限が切れたりすることがあります。 サーバーでは、期限切れのパスワードとロックされたアカウントを 2 回チェックします。 最初のチェックは、初回接続時に行われます。 2 回目のチェックは、接続のリセット時、接続がプールから取り除かれるときに行われます。  
  
 リセットの試行が失敗すると、その接続はプールから削除され、エラーが返されます。  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB プログラムによるパスワード期限切れの処理  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROPSET_SQLSERVERDBINIT プロパティセットに追加された SSPROP_AUTH_OLD_PASSWORD (型 VT_BSTR) プロパティを追加することによって、パスワードの有効期限をサポートします。  
  
 既存の "Password" プロパティは DBPROP_AUTH_PASSWORD を参照し、新しいパスワードを保存する場合に使用されます。  
  
> [!NOTE]  
>  接続文字列の "Old Password" プロパティは SSPROP_AUTH_OLD_PASSWORD に設定され、現在の (または期限切れの) パスワードが設定されます。このパスワードをプロバイダー文字列のプロパティ経由で使用することはできません。  
  
 プロバイダーでは、このプロパティの値が保存されません。 このプロパティを設定すると新しい接続が行われるので、プロバイダーでは最初の接続に接続プールが使用されません。 パスワード変更が正常に行われた場合でも、現在の接続にはまだ古いパスワードが含まれているので再利用できません。古いパスワードとは、変更後に無効になるパスワードのことです。 また、ログインに成功すると、このプロパティはクリアされます。 クリア後に古いパスワードを取得しようとすると、VT_EMPTY が返されます。  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD は、パスワードの有効期限が切れたときにしか使用されないので、保存しないでください。  
  
 "Old Password" プロパティが設定されると、プロバイダーでは、パスワードの変更が試行されていることが想定されます。ただし、Windows 認証も指定されている場合は除きます。この場合は、常に Windows 認証が優先されるためです。  
  
 Windows 認証を使用している場合、古いパスワードを REQUIRED と指定するか OPTIONAL と指定するかによって、それぞれ DB_E_ERRORSOCCURRED または DB_S_ERRORSOCCURRED のいずれかが返され、*dwStatus* に状態値として DBPROPSTATUS_CONFLICTINGBADVALUE が返されます。 これは、**IDBInitialize::Initialize** を呼び出したときに検出されます。  
  
 パスワード変更の試行が予期せず失敗すると、サーバーからエラー コード 18468 が返されます。 接続試行からは標準の OLE DB エラーが返されます。  
  
 DBPROPSET_SQLSERVERDBINIT プロパティセットの詳細については、「[初期化プロパティと承認プロパティ](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)」を参照してください。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、ユーザーインターフェイスとプログラムを使ってパスワードの有効期限をサポートします。  
  
### <a name="odbc-user-interface-password-expiration"></a>ODBC ユーザー インターフェイスによるパスワード期限切れの処理  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、 **SQL Server ログイン**ダイアログボックスに対して行われた変更によって、パスワードの有効期限がサポートされます。  
  
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)が呼び出され、 **drivercompletion**の値が SQL_DRIVER_NOPROMPT に設定されている場合、パスワードの有効期限が切れていると、最初の接続試行は失敗します。 SQLSTATE 値28000とネイティブエラーコード値18487は、次の**SQLError**または**SQLGetDiagRec**への呼び出しによって返されます。  
  
 **Drivercompletion**がその他の値に設定されている場合、パスワードの有効期限が切れているかどうかにかかわらず、ユーザーには**SQL Server ログイン**ダイアログが表示されます。 ユーザーは、 **[オプション]** をクリックし、 **[パスワードの変更]** チェック ボックスをオンにしてパスワードを変更できます。  
  
 ユーザーが OK] をクリックし、パスワードの有効期限が切れている場合は、 **[SQL Server パスワードの変更]** ダイアログボックスを使用して、新しいパスワードの入力と確認を求めるメッセージが表示され [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>ODBC プロンプトの動作とロックされたアカウント  
 アカウントがロックされていることにより、接続に失敗することがあります。 **[SQL Server ログイン]** ダイアログ ボックスが表示された後にこの現象が発生する場合は、サーバー エラー メッセージが表示され、接続試行が中止されます。 また、 **[パスワードの変更]** ダイアログ ボックスが表示された後にユーザーが古いパスワードに無効な値を入力すると、この現象が発生することもあります。 この場合も同じエラー メッセージが表示され、接続試行が中止されます。  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>ODBC 接続プーリング、パスワードの期限切れ、およびロックされたアカウント  
 接続プール内で接続がアクティブな状態になっている間に、アカウントがロックされたり、そのアカウントのパスワードの有効期限が切れたりすることがあります。 サーバーでは、期限切れのパスワードとロックされたアカウントを 2 回チェックします。 最初のチェックは、初回接続時に行われます。 2 回目のチェックは、接続のリセット時、接続がプールから取り除かれるときに行われます。  
  
 リセットの試行が失敗すると、その接続はプールから削除され、エラーが返されます。  
  
### <a name="odbc-programmatic-password-expiration"></a>ODBC プログラムによるパスワードの有効期限  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)関数を使用してサーバーに接続する前に設定されている SQL_COPT_SS_OLDPWD 属性を追加することによって、パスワードの有効期限をサポートしています。  
  
 接続ハンドルの SQL_COPT_SS_OLDPWD 属性は、期限切れのパスワードを表します。 接続文字列の属性は接続プーリングに影響を与えることになるので、この属性に関する接続文字列属性はありません。 ログインに成功すると、この属性はクリアされます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、パスワードの有効期限、パスワードポリシーの競合、アカウントのロックアウト、および Windows 認証の使用時に古いパスワードプロパティが設定されている場合に、この機能の4つのケースで SQL_ERROR を返します。 [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md)が呼び出されると、ドライバーはユーザーに適切なエラーメッセージを返します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
