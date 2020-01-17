---
title: 初期化プロパティと承認プロパティ |Microsoft Docs
description: 初期化プロパティと承認プロパティ
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- authorization [OLE DB]
- properties [OLE DB]
- OLE DB Driver for SQL Server, initialization properties
- OLE DB Driver for SQL Server, authorization properties
- initialization properties [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 28923ccb78e3edfa4de7b7e780195a643ec9914e
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381874"
---
# <a name="initialization-and-authorization-properties"></a>初期化プロパティと承認プロパティ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server の OLE DB ドライバーは OLE DB 初期化と承認のプロパティを次のように解釈します。  
  
|プロパティ ID|[説明]|  
|-----------------|-----------------|  
|DBPROP_AUTH_CACHE_AUTHINFO|SQL Server の OLE DB ドライバーでは、認証情報はキャッシュされません。<br /><br /> OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_AUTH_ENCRYPT_PASSWORD|SQL Server 用の OLE DB ドライバーは、標準の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティ機構を使用してパスワードを隠します。<br /><br /> OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_AUTH_INTEGRATED|DBPROP_AUTH_INTEGRATED に NULL ポインター、NULL 文字列、または 'SSPI' VT_BSTR 値を設定すると、OLE DB Driver for SQL Server は、Windows 認証モードを使用して、DBPROP_INIT_DATASOURCE プロパティと DBPROP_INIT_CATALOG プロパティで指定されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへのユーザー アクセスを承認します。<br /><br /> VT_EMPTY (既定値) に設定すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティが使用されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインとパスワードは、DBPROP_AUTH_USERID プロパティと DBPROP_AUTH_PASSWORD プロパティで指定されます。|  
|DBPROP_AUTH_MASK_PASSWORD|SQL Server 用の OLE DB ドライバーは、標準の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セキュリティ機構を使用してパスワードを隠します。<br /><br /> OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインに割り当てられたパスワードです。 このプロパティは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへのアクセスの承認に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が選択された場合に使用されます。|  
|DBPROP_AUTH_PERSIST_ENCRYPTED|SQL Server の OLE DB ドライバーは、永続化されるときに認証情報を暗号化しません。<br /><br /> OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|OLE DB Driver for SQL Server は、認証値を保存するよう要求された場合に、パスワードのイメージを含めて、この値を保存します。 暗号化は行われません。|  
|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインです。 このプロパティは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへのアクセスの承認に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証が選択された場合に使用されます。|  
|DBPROP_INIT_ASYNCH|SQL Server の OLE DB ドライバーは、非同期開始をサポートしています。<br /><br /> DBPROPVAL_ASYNCH_INITIALIZE ビットを DBPROP_INIT_ASYNCH プロパティに設定すると、**IDBInitialize::Initialize** は非ブロッキング呼び出しになります。 詳細については、「[非同期操作の実行](../../oledb/features/performing-asynchronous-operations.md)」を参照してください。|  
|DBPROP_INIT_CATALOG|接続先の既存の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベース名です。|  
|DBPROP_INIT_DATASOURCE|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスを実行するサーバーのネットワーク名。 コンピューター上で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の複数のインスタンスが実行されている場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の特定のインスタンスに接続するために、DBPROP_INIT_DATASOURCE の値が *\\\ServerName\InstanceName* として指定されます。 エスケープ シーケンスの \\\ は、円記号を表すために使用されます。|  
|DBPROP_INIT_GENERALTIMEOUT|データ ソースの初期化とコマンドの実行以外の要求がタイムアウトになるまでの秒数を示します。値 0 は、タイムアウトしないことを表します。プロバイダーがネットワーク接続経由で動作している場合、または分散シナリオやトランザクション シナリオで実行されている場合、このプロパティをサポートすることで、実行時間の長い要求が発生した際に、参加しているコンポーネントに対してタイムアウトするよう指示できます。 データ ソースの初期化とコマンド実行のタイムアウトについては、それぞれ DBPROP_INIT_TIMEOUT と DBPROP_COMMANDTIMEOUT で指定されます。<br /><br /> DBPROP_INIT_GENERALTIMEOUT は読み取り専用です。値の設定が試みられると、DBPROPSTATUS_NOTSETTABLE の *dwstatus* エラーが返されます。|  
|DBPROP_INIT_HWND|呼び出し元アプリケーションのウィンドウ ハンドルです。 初期化プロパティに入力要求が許可されている場合は、初期化ダイアログ ボックスを表示するために、有効なウィンドウ ハンドルが必要です。|  
|DBPROP_INIT_IMPERSONATION_LEVEL|SQL Server の OLE DB ドライバーは、偽装レベルの調整をサポートしていません。<br /><br /> OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_INIT_LCID|OLE DB Driver for SQL Server でロケール ID が確認され、ロケール ID がサポートされていないか、クライアントにインストールされていない場合はエラーが返されます。|  
|DBPROP_INIT_LOCATION|OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_INIT_MODE|OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_INIT_PROMPT|OLE DB Driver for SQL Server では、データソースを初期化するためのすべてのプロンプトモードがサポートされています。 SQL Server の OLE DB ドライバーは、プロパティの既定の設定として DBPROMPT_NOPROMPT を使用します。|  
|DBPROP_INIT_PROTECTION_LEVEL|OLE DB Driver for SQL Server は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続で保護レベルをサポートしていません。<br /><br /> OLE DB Driver for SQL Server は、プロパティ値を設定しようとしたときに DB_S_ERRORSOCCURRED を返します。 DBPROP 構造体の *dwStatus* メンバーは、DBPROPSTATUS_NOTSUPPORTED を示します。|  
|DBPROP_INIT_PROVIDERSTRING|このトピックで後述する「OLE DB Driver for SQL Server 文字列」を参照してください。|  
|DBPROP_INIT_TIMEOUT|OLE DB Driver for SQL Server は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続が指定された時間 (秒単位) 内に確立できなかった場合、初期化時にエラーを返します。|  
  
 プロバイダー固有のプロパティ セット DBPROPSET_SQLSERVERDBINIT には、OLE DB Driver for SQL Server により、次の追加の初期化プロパティが定義されます。  
  
|プロパティ ID|[説明]|  
|-----------------|-----------------|  
|SSPROP_AUTH_ACCESS_TOKEN<a href="#table1_1"><sup>**1**</sup></a>|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値 : VT_EMPTY<br /><br /> 説明: Azure Active Directory に対する認証に使用されるアクセストークン。 <br/><br/>**注:** このプロパティを指定すると、`UID`、`PWD`、`Trusted_Connection`、`Authentication` 接続文字列のキーワード、またはそれらに対応する properties/keywords にも、エラーが発生します。|
|SSPROP_AUTH_MODE<a href="#table1_1"><sup>**1**</sup></a>|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値 : VT_EMPTY<br /><br /> 説明: 使用する SQL 認証または Active Directory 認証を指定します。 有効な値は、<br/><ul><li>`(not set)`: 他のキーワードによって決定される認証モード。</li><li>`(empty string)`: 解除認証モードを設定しています。</li><li>Azure Active Directory id を使用した `ActiveDirectoryPassword:`User ID とパスワード認証。</li><li>Azure Active Directory id を使用して統合認証を `ActiveDirectoryIntegrated:` します。</li><br/>**注:** @No__t_1 キーワードは、Windows 認証で SQL Server するためにも使用できます。 これは、`Integrated Security` (または `Trusted_Connection`) 認証キーワードに代わるものです。 @No__t_1 (または `Trusted_Connection`) のキーワードを使用するアプリケーションまたは対応するプロパティを使用して `Authentication` キーワード (または対応するプロパティ) の値を `ActiveDirectoryIntegrated` に設定し、新しい暗号化と証明書の検証動作を有効にすることを**お勧め**します。.<br/><br/><li>Azure Active Directory id を使用した対話型認証を `ActiveDirectoryInteractive:` します。 この方法では、Azure multi-factor authentication (MFA) がサポートされます。 </li><li>[マネージドサービス ID (MSI)](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)認証を `ActiveDirectoryMSI:` します。 ユーザー割り当て id の場合は、ユーザー id のオブジェクト ID にユーザー ID を設定する必要があります。</li><li>ユーザー ID とパスワードを使用して認証を `SqlPassword:` します。</li><br/>**注:** @No__t_2 認証を使用するアプリケーションでは、`Authentication` キーワード (またはそれに対応するプロパティ) の値を `SqlPassword` に設定して、[新しい暗号化と証明書の検証動作](../features/using-azure-active-directory.md#encryption-and-certificate-validation)を有効にすることを**お勧め**します。</ul>|
|SSPROP_AUTH_OLD_PASSWORD|型 : VT_BSTR<br /><br /> R/W: 書き込み<br /><br /> 既定値 : VT_EMPTY<br /><br /> 説明: 現在のパスワードまたは有効期限が切れたパスワードです。 詳細については、「[プログラムによるパスワードの変更](../../oledb/features/changing-passwords-programmatically.md)」を参照してください。|  
|SSPROP_INIT_APPNAME|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: クライアント アプリケーション名です。|  
|SSPROP_INIT_AUTOTRANSLATE|型 : VT_BOOL<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_TRUE<br /><br /> 説明: OEM/ANSI 文字変換です。<br /><br /> VARIANT_TRUE: OLE DB Driver for SQL Server は、クライアントとサーバーの間で送信される ANSI 文字列の変換に Unicode を使用することで、クライアントとサーバーのコード ページ間で拡張文字の対応付けに生じる問題を最小限に抑えます。<br /><br /> クライアントの DBTYPE_STR データを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の **char** 型、**varchar** 型、または **text** 型の変数、パラメーター、列のインスタンスに送信する場合、クライアントの ANSI コード ページ (ACP) に基づいて文字が Unicode に変換され、その後で、サーバーの ACP に基づいて Unicode から文字に変換されます。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の **char** 型、**varchar** 型、または **text** 型のデータをクライアントの DBTYPE_STR 変数に送信する場合は、サーバーの ACP に基づいて文字が Unicode に変換され、その後で、クライアントの ACP に基づいて Unicode から文字に変換されます。<br /><br /> これらの変換は、SQL Server 用の OLE DB ドライバーによってクライアント上で実行されます。 そのため、サーバーで使用しているものと同じ ACP がクライアントでも使用可能になっている必要があります。<br /><br /> 次の設定は、送受信時の変換に影響しません。<br /><br /> サーバーの **char** 型、**varchar** 型、または **text** 型に送信される、Unicode の DBTYPE_WSTR クライアント データ。<br /><br /> クライアントの Unicode の DBTYPE_WSTR 変数に送信される、**char** 型、**varchar** 型、または **text** 型のサーバー データ。<br /><br /> サーバーの Unicode の **nchar** 型、**nvarchar** 型、または **ntext** 型に送信される、ANSI DBTYPE_STR クライアント データ。<br /><br /> クライアントの ANSI DBTYPE_STR 変数に送信される、Unicode の **char** 型、**varchar** 型、または **text** 型のサーバー データ。<br /><br /> VARIANT_FALSE: SQL Server の OLE DB ドライバーは、文字の変換を実行しません。<br /><br /> OLE DB Driver for SQL Server では、サーバーの **char** 型、**varchar** 型、または **text** 型の変数、パラメーター、列のいずれかに送信される、クライアントの ANSI 文字の DBTYPE_STR データは変換されません。 また、サーバーからクライアントの DBTYPE_STR 変数に送信される、**char** 型、**varchar** 型、**text** 型のデータも変換されません。<br /><br /> クライアントと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが使用する ACP が異なる場合、拡張文字の解釈が正しく行われない場合があります。|  
|SSPROP_INIT_CURRENTLANGUAGE|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の言語名です。 システム メッセージの選択や書式設定に使われる言語を示します。 指定された言語が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを実行するコンピューターにインストールされていないと、データ ソースの初期化が失敗します。|  
|SSPROP_INIT_DATATYPECOMPATIBILITY|型: VT_UI2<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値: 0<br /><br /> 説明: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と ActiveX Data Object (ADO) アプリケーション間のデータ型の互換性を確保します。 既定値の 0 が使用されている場合、データ型の処理では、プロバイダーが既定で使用するデータ型が使われます。 値 80 が使用されている場合、データ型の処理では、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] のデータ型しか使われません。 詳細については、「 [USING ADO with OLE DB Driver for SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)」を参照してください。|  
|SSPROP_INIT_ENCRYPT<a href="#table1_1"><sup>**1**</sup></a>|型 : VT_BOOL<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_FALSE<br /><br /> 説明: ネットワーク経由で転送されるデータを暗号化する場合は、SSPROP_INIT_ENCRYPT プロパティを VARIANT_TRUE に設定します。<br /><br /> [プロトコルの暗号化を設定する] がオンになっている場合、SSPROP_INIT_ENCRYPT の設定に関係なく、常に暗号化が行われます。 プロトコルの暗号化が無効な場合でも、SSPROP_INIT_ENCRYPT が VARIANT_TRUE に設定されている場合は、暗号化が行われます。<br /><br /> [プロトコルの暗号化を設定する] がオフになっていて、SSPROP_INIT_ENCRYPT が VARIANT_FALSE に設定されている場合は、暗号化は行われません。|  
|SSPROP_INIT_FAILOVERPARTNER|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: データベース ミラーリングのフェールオーバー パートナーの名前を示します。 これは、初期化プロパティで、初期化前にしか設定できません。 初期化後は、フェールオーバー パートナーが構成されている場合は、プライマリ サーバーから返されたフェールオーバー パートナー名を返します。<br /><br /> これにより、アプリケーションでは最後に判別したバックアップ サーバーをキャッシュできますが、この情報は最初に接続が確立されたとき (接続がプールされている場合はリセットされたとき) にのみ更新されることに注意する必要があります。接続が長期にわたると、この情報は古くなることがあります。<br /><br /> 接続後は、アプリケーションでこの属性をクエリすることにより、フェールオーバー パートナーの ID を判別できます。 プライマリ サーバーのフェールオーバー パートナーが存在しないと、この属性は空文字列を返します。 詳細については、「[データベース ミラーリングの使用](../../oledb/features/using-database-mirroring.md)」を参照してください。|  
|SSPROP_INIT_FILENAME|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: アタッチできるデータベースのプライマリ ファイル名を示します。 このデータベースがアタッチされ、接続の既定のデータベースとして使用されます。 SSPROP_INIT_FILENAME を使用するには、初期化プロパティ DBPROP_INIT_CATALOG の値にデータベース名を指定する必要があります。 指定したデータベース名が存在しない場合は、SSPROP_INIT_FILENAME に指定されているプライマリ ファイル名を確認し、そのデータベースと DBPROP_INIT_CATALOG に指定されている名前とをアタッチします。 データベースが以前にアタッチされていた場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はこれを再アタッチしません。|  
|SSPROP_INIT_MARSCONNECTION|型 : VT_BOOL<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_FALSE<br /><br /> 説明: 複数のアクティブな結果セット (MARS) が接続で有効かどうかを示します。 このオプションは、データベースへの接続が確立される前に、TRUE に設定する必要があります。 詳細については、「[複数のアクティブな結果セット &#40;MARS&#41; の使用](../../oledb/features/using-multiple-active-result-sets-mars.md)」を参照してください。|  
|SSPROP_INIT_NETWORKADDRESS|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: DBPROP_INIT_DATASOURCE プロパティで指定されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを実行するサーバーのネットワーク アドレスです。|  
|SSPROP_INIT_NETWORKLIBRARY|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスとの通信に使われるネットワーク ライブラリ (DLL) の名前です。 この名前には、パスやファイル拡張子 (.dll) は含めません。<br /><br /> 既定値は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クライアント構成ユーティリティを使用してカスタマイズできます。<br /><br /> 注: このプロパティでサポートされるのは、TCP および名前付きパイプのみです。 このプロパティにプレフィックスを使用した場合、プレフィックスが二重になりエラーが発生します。これは、内部でこのプロパティを使用してプレフィックスが生成されるためです。|  
|SSPROP_INIT_PACKETSIZE|型 : VT_I4<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: ネットワーク パケットのバイト単位のサイズです。 このパケット サイズ プロパティの値は 512 ～ 32,767 にする必要があります。 SQL Server ネットワークパケットサイズの既定の OLE DB ドライバーは4096です。|  
|SSPROP_INIT_TAGCOLUMNCOLLATION|型: BOOL<br /><br /> R/W: 書き込み<br /><br /> 既定値: FALSE<br /><br /> 説明: サーバー側カーソルが使用されているとき、データベースの更新中に使用されます。 このプロパティは、クライアントのコード ページではなく、サーバーから取得した照合順序情報を使用してデータにタグを付けます。 現在、このプロパティは、分散クエリ プロセスでしか使われていません。これは、分散クエリ プロセスでは変換先データの照合順序が認識されていて、データが適切に変換されるためです。|  
|SSPROP_INIT_TRUST_SERVER_CERTIFICATE<a href="#table1_1"><sup>**1**</sup></a>|型 : VT_BOOL<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_FALSE<br /><br /> 説明: サーバー証明書の検証の有効化または無効化に使用されます。 このプロパティは読み取り/書き込みですが、接続の確立後にこの値の設定が試みられると、エラーが発生します。<br /><br /> このプロパティは、クライアントが証明書の検証を要求するよう構成されている場合は、無視されます。 ただし、アプリケーションは、このプロパティを SSPROP_INIT_ENCRYPT と共に使用して、クライアントが暗号化を要求するよう構成されておらず、証明書がクライアント側に準備されていない場合でも、アプリケーションとサーバー間の接続が確実に暗号化されるようにすることができます。<br /><br /> クライアント アプリケーションでは、接続を開いた後にこの属性をクエリして、実際に使用されている暗号化と検証の設定を判断できます。<br /><br /> 注: 証明書の検証なしで暗号化を使用する場合、パケット スニッフィングに対してある程度の保護は実現できますが、中間者攻撃に対しては保護できません。 この場合、サーバー証明書を検証せずに、サーバーに送られるログインとデータの暗号化が行われます。<br /><br /> 詳細については、「[検証を伴わない暗号化の使用](../../oledb/features/using-encryption-without-validation.md)」を参照してください。|  
|SSPROP_INIT_USEPROCFORPREP|型 : VT_I4<br /><br /> R/W: 読み取り/書き込み<br /><br /> 既定値: SSPROPVAL_USEPROCFORPREP_ON<br /><br /> 説明: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ストアド プロシージャを使用するかどうか。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の一時ストアド プロシージャを使用して **ICommandPrepare** インターフェイスをサポートすることを定義します。 このプロパティは SQL Server 6.5 に接続するときに限り意味がありました。 これ以降のバージョンでは、このプロパティは無視されます。<br /><br /> SSPROPVAL_USEPROCFORPREP_OFF: コマンドを準備するときには、一時ストアド プロシージャが作成されません。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON: コマンドを準備するときに、一時ストアド プロシージャが作成されます。 セッションが解放されると、作成された一時ストアド プロシージャは削除されます。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON_DROP: コマンドを準備するときに、一時ストアド プロシージャが作成されます。 コマンドが **ICommandPrepare::Unprepare** を使用して準備されていない場合、**ICommandText::SetCommandText** を使用してコマンド オブジェクトに新しいコマンドが指定されたとき、またはコマンドへのアプリケーション参照がすべて解放されたときに、プロシージャは削除されます。|  
|SSPROP_INIT_WSID|型 : VT_BSTR<br /><br /> R/W: 読み取り/書き込み<br /><br /> 説明: ワークステーションを識別する文字列です。|  
  

<b id="table1_1">[1]:</b>セキュリティを強化するために、認証/アクセストークンの初期化プロパティまたはそれに対応する接続文字列キーワードを使用すると、暗号化と証明書の検証の動作が変更されます。 詳細については、「[暗号化と証明書の検証](../features/using-azure-active-directory.md#encryption-and-certificate-validation)」を参照してください。

 プロバイダー固有のプロパティセット DBPROPSET_SQLSERVERDATASOURCEINFO では、SQL Server の OLE DB ドライバーによって追加のプロパティが定義されます。詳細については、「[データソース情報のプロパティ](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)」を参照してください。  
  
## <a name="the-ole-db-driver-for-sql-server-string"></a>OLE DB Driver for SQL Server の文字列  
 OLE DB Driver for SQL Server は、プロバイダー文字列のプロパティ値で ODBC に似た構文を認識します。 プロバイダーの文字列プロパティは、OLE DB データ ソースへの接続が確立される時点で、OLE DB 初期化プロパティ DBPROP_INIT_PROVIDERSTRING の値として提供されます。 このプロパティは、OLE DB データ ソースへの接続の実装に必要な OLE DB プロバイダー固有の接続データを示します。 この文字列内では、要素がセミコロンを使用して区切られます。 文字列の最後の要素には、セミコロンを付けて、終端を示す必要があります。 各要素は、キーワード、等号文字、初期化時に渡される値で構成されます。 例:  
  
```  
Server=MyServer;UID=MyUserName;  
```  
  
 OLE DB Driver for SQL Server では、コンシューマーはプロバイダー文字列プロパティを使用する必要はありません。 コンシューマーは、OLE DB または OLE DB Driver for SQL Server プロバイダー固有の初期化プロパティを使用して、プロバイダー文字列に任意の初期化プロパティを設定できます。  
  
 SQL Server 用の OLE DB ドライバーで使用できるキーワードの一覧については、「 [SQL Server の OLE DB ドライバーでの接続文字列キーワードの使用](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データソースオブジェクト&#40;の OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
