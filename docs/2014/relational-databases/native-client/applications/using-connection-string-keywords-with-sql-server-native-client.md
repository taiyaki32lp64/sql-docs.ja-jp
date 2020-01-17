---
title: SQL Server Native Client で接続文字列キーワードの使用 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6135c1d2cbf1291465e1346f71010b8befe6f7b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046408"
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>SQL Server Native Client での接続文字列キーワードの使用
  一部の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client API では、接続文字列を使用して接続属性を指定します。 接続文字列はキーワードとそれに関連する値のリストです。各キーワードによって特定の接続属性を識別します。  
  
 **注意してください。** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client により、下位互換性を維持するために、接続文字列のあいまいさ (たとえば、いくつかのキーワードを複数回指定することがあり、位置または優先順位に基づいた解決方法に競合するキーワードを許可されている可能性があります)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の今後のリリースでは、あいまいな接続文字列を使用できなくなる可能性があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用するアプリケーションでは、あいまいな接続文字列を利用しないように変更することをお勧めします。  
  
 次のセクションでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をデータ プロバイダーとして使用するときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー、および ADO (ActiveX Data Objects) と共に使用できるキーワードについて説明します。  
  
## <a name="odbc-driver-connection-string-keywords"></a>ODBC ドライバー接続文字列キーワード  
 ODBC アプリケーションでは、接続文字列を使用するパラメーターとして、 [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)と[SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)関数。  
  
 ODBC で使用される接続文字列の構文を次に示します。  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性値は必要に応じて中かっこで囲むことができます。常に中かっこを使用すると、 属性値に英数字以外の文字が含まれる場合の問題を回避できます。 最初の右中かっこが値の終わりと見なされるため、値に右中かっこを含めることはできません。  
  
 次の表に、ODBC 接続文字列と共に使用できるキーワードを示します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|`Addr`|"Address" のシノニム。|  
|`Address`|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスを実行しているサーバーのネットワーク アドレス。 `Address` には通常、サーバーのネットワーク名を使用しますが、パイプ、IP アドレス、または TCP/IP ポートとソケット アドレスなど他の名前を指定してもかまいません。<br /><br /> IP アドレスを指定する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで TCP/IP または名前付きパイプ プロトコルが有効になっていることを確認します。<br /><br /> `Address` の値は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の使用時に ODBC 接続文字列で `Server` に渡される値よりも優先されます。 `Address=;` の場合は、`Server` キーワードで指定されているサーバーに接続されますが、`Address= ;, Address=.;`、`Address=localhost;`、および `Address=(local);` の場合はすべて、ローカル サーバーに接続されます。<br /><br /> `Address` キーワードの完全な構文は次のとおりです。<br /><br /> [*プロトコル*`:`]*アドレス*[`,`*ポート&#124;\pipe\pipename*]<br /><br /> *プロトコル*できる`tcp`(TCP/IP) `lpc` (共有メモリ)、または`np`(名前付きパイプ)。 プロトコルの詳細については、次を参照してください。 [Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md)します。<br /><br /> どちらの場合*プロトコル*も`Network`キーワードを指定すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client がで指定されたプロトコルの順序を使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *port* は、指定したサーバー上の接続先のポートです。 既定では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はポート 1433 を使用します。|  
|`AnsiNPW`|"yes" の場合、ANSI で定められた動作に従って NULL の比較、文字データの埋め込み、警告、および NULL 連結が処理されます。 "no" の場合、ANSI で定められた動作が公開されません。 ANSI NPW 動作の詳細については、次を参照してください。 [ISO オプションの効果](../../native-client-odbc-queries/executing-statements/effects-of-iso-options.md)します。|  
|`APP`|アプリケーションの呼び出し元の名前[SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) (省略可能)。 この値が格納されている、指定されている場合、 **master.dbo.sysprocesses**列**専用**によって返されると[sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)と[APP_NAME](/sql/t-sql/functions/app-name-transact-sql)関数。|  
|`ApplicationIntent`|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 設定可能な値は `ReadOnly` および `ReadWrite` です。 以下に例を示します。ApplicationIntent=ReadOnly<br /><br /> 既定値は `ReadWrite` です。 詳細については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。|  
|`AttachDBFileName`|アタッチできるデータベースのプライマリ ファイルの名前。 この名前には完全なパス名を指定します。また C 文字列変数を使用する場合は、\ 文字をエスケープしてください。<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> このデータベースがアタッチされ、接続の既定のデータベースとして使用されます。 使用する`AttachDBFileName`いずれかで、データベース名を指定することも必要があります、 [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) DATABASE パラメーターまたは SQL_COPT_CURRENT_CATALOG 接続属性。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|`AutoTranslate`|"yes" の場合、クライアントとサーバーの間で送受信される ANSI 文字列は、いったん Unicode に変換されます。これは、クライアントとサーバーのコード ページ間で拡張文字を照合するときに発生する問題を最小限に抑えるためです。<br /><br /> 送信されるクライアントの SQL_C_CHAR データ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**、 **varchar**、または**テキスト**変数、パラメーター、または列をクライアントを使用して Unicode 文字からに変換されますサーバーの acp に基づいて Unicode から ANSI コード ページ (ACP) が変換されます。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**、 **varchar**、または**テキスト**クライアントの SQL_C_CHAR 変数に送信されるデータが ACP では、サーバーを使用して Unicode 文字から変換し、Unicode に、クライアントから変換されました。ACP します。<br /><br /> この変換は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーによってクライアントで行われます。 また、サーバーで使用しているものと同じ ACP (ANSI コード ページ) がクライアントでも使用可能になっている必要があります。<br /><br /> 次の設定は、送受信時の変換に影響しません。<br /><br /> 送信される Unicode の SQL_C_WCHAR クライアント データ**char**、 **varchar**、または**テキスト**サーバー。<br />-   **char**、 **varchar**、または**テキスト**サーバー データをクライアント上の Unicode の SQL_C_WCHAR 変数に送信します。<br />Unicode に送信される ANSI SQL_C_CHAR クライアント データ**nchar**、 **nvarchar**、または**ntext**サーバー。<br />Unicode **nchar**、 **nvarchar**、または**ntext**サーバー データをクライアントでの ANSI SQL_C_CHAR 変数に送信します。<br /><br /> "no" の場合、文字の変換は行われません。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに送信されるクライアント ANSI 文字の SQL_C_CHAR データに変換されない**char**、 **varchar**、または**テキスト**変数、パラメーター、または、サーバー上の列。 変換は行われません**char**、 **varchar**、または**テキスト**クライアントの SQL_C_CHAR 変数に、サーバーから送信されるデータ。<br /><br /> クライアントと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で使用する ACP が異なる場合、拡張文字の解釈が正しく行われない場合があります。|  
|`Database`|接続に使用する既定の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースの名前。 `Database` を指定していない場合は、ログインに定義されている既定のデータベースが使用されます。 ODBC データ ソースの既定のデータベースは、ログインに定義されている既定のデータベースをオーバーライドします。 `AttachDBFileName` を指定する場合を除き、既存のデータベースを使用する必要があります。 `AttachDBFileName` も指定した場合は、このキーワードが参照するプライマリ ファイルがアタッチされ、`Database` で指定したデータベース名が付けられます。|  
|`Driver`|によって返されるドライバー名[SQLDrivers](../../native-client-odbc-api/sqldrivers.md)します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに対するこのキーワードの値は "{SQL Server Native Client 11.0}" です。 `Server` を指定し、`Driver` を SQL_DRIVER_NOPROMPT に設定している場合は、`DriverCompletion` キーワードが必要です。<br /><br /> ドライバー名の詳細については、次を参照してください。 [SQL Server Native Client ヘッダーとライブラリ ファイルを使用して](using-the-sql-server-native-client-header-and-library-files.md)します。|  
|`DSN`|既存の ODBC ユーザー データ ソースまたはシステム データ ソースの名前。 このキーワードは、`Server`、`Network`、および `Address` の各キーワードに指定されている値をオーバーライドします。|  
|`Encrypt`|データをネットワークに送信する前に暗号化するかどうかを指定します。 有効値は、"yes" および "no" です。 既定値は "no" です。|  
|`Fallback`|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、このキーワードは非推奨とされ、設定は無視されます。|  
|`Failover_Partner`|プライマリ サーバーに接続できない場合に使用するフェールオーバー パートナー サーバーの名前。|  
|`FailoverPartnerSPN`|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はドライバーが生成した SPN を既定値として使用します。|  
|`FileDSN`|既存の ODBC ファイル データ ソースの名前。|  
|`Language`|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語の名前 (省略可)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複数言語のメッセージを格納できる**sysmessages**します。 複数の言語が設定された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続する場合、その接続でどのメッセージのセットを使用するかを `Language` で指定します。|  
|`MARS_Connection`|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします。 認識できる値は "yes" と "no" です。 既定値は"no"です。|  
|`MultiSubnetFailover`|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可用性グループまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの可用性グループ リスナーに接続する際には、必ず `multiSubnetFailover=Yes` を指定してください。 `multiSubnetFailover=Yes` によって、(現在) アクティブなサーバーを迅速に検出し、接続するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client が構成されます。 設定可能な値は `Yes` および `No` です。 以下に例を示します。<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 既定値は `No` です。 詳細については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。|  
|`Net`|"Network" のシノニム。|  
|`Network`|有効な値は**dbnmpntw** (名前付きパイプ) と**dbmssocn** (TCP/IP)。<br /><br /> `Network` キーワードの値と `Server` キーワードのプロトコル プレフィックスの両方を指定すると、エラーになります。|  
|`PWD`|UID パラメーターで指定されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン アカウントのパスワード。 ログインのパスワードが NULL の場合、または Windows 認証 (`Trusted_Connection = yes`) を使用している場合は、`PWD` を指定する必要はありません。|  
|`QueryLog_On`|"yes" の場合、その接続では、実行時間の長いクエリのデータに関するログを記録できます。 "no" の場合、実行時間の長いクエリのデータに関するログは記録されません。|  
|`QueryLogFile`|実行時間の長いクエリのデータをログに記録する場合に使用するファイルの完全なパスとファイル名。|  
|`QueryLogTime`|実行時間の長いクエリをログに記録するためのしきい値 (ミリ秒) を指定する数字文字列。 指定時間内に応答が返ってこないクエリは、実行時間の長いクエリ用のログ ファイルに記録されます。|  
|`QuotedId`|"yes" の場合、その接続の QUOTED_IDENTIFIERS が ON に設定され、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は ISO 規則に従って SQL ステートメントの引用符を処理します。 "no" の場合、その接続の QUOTED_IDENTIFIERS が OFF に設定され、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は従来の [!INCLUDE[tsql](../../../includes/tsql-md.md)] 規則に従って SQL ステートメントの引用符を処理します。 詳細については、次を参照してください。 [ISO オプションの効果](../../native-client-odbc-queries/executing-statements/effects-of-iso-options.md)します。|  
|`Regional`|"yes" の場合、通貨、日付、および時刻データが文字データに変換されるときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーではクライアントの設定が使用されます。 変換は一方向にのみ行われます。INSERT ステートメントや UPDATE ステートメントのパラメーターなどで日付文字列または通貨の値が ODBC 標準以外の形式で指定されている場合、ドライバーでは、これらの値は認識されません。 "no" の場合、文字データに変換される通貨、日付、および時刻データを表現するために ODBC 標準の文字列が使用されます。|  
|`SaveFile`|接続が成功した場合に、現在の接続の属性を保存する ODBC データ ソース ファイルの名前。|  
|`Server`|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前。 ネットワーク上のサーバーの名前、IP アドレス、または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーの別名を指定する必要があります。<br /><br /> `Address` キーワードは、`Server` キーワードをオーバーライドします。<br /><br /> 次のいずれかを指定することで、ローカル サーバー上の既定のインスタンスに接続できます。<br /><br /> -   `Server=;`<br />-   `Server=.;`<br />-   `Server=(local);`<br />-   `Server=(localhost);`<br />-   **Server=(localdb)\\** _instancename_ `;`<br /><br /> LocalDB のサポートの詳細については、次を参照してください。 [SQL Server ネイティブ クライアントのサポート LocalDB](../features/sql-server-native-client-support-for-localdb.md)します。<br /><br /> 名前付きインスタンスを指定する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、追加 **\\** _InstanceName_します。<br /><br /> サーバーを指定しなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続されます。<br /><br /> IP アドレスを指定する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで TCP/IP または名前付きパイプ プロトコルが有効になっていることを確認します。<br /><br /> `Server` キーワードの完全な構文は次のとおりです。<br /><br /> `Server=`[*protocol*`:`]*Server*[`,`*port*]<br /><br /> *プロトコル*できる`tcp`(TCP/IP) `lpc` (共有メモリ)、または`np`(名前付きパイプ)。<br /><br /> 名前付きパイプを指定する例を次に示します。<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> この行では、名前付きパイプのプロトコル、ローカル コンピューター上の名前付きパイプ (`\\.\pipe`)、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前 (`MSSQL$MYINST01`)、および名前付きパイプの既定の名前 (`sql/query`) を指定しています。<br /><br /> どちらの場合、*プロトコル*も`Network`キーワードを指定すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client がで指定されたプロトコルの順序を使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *port* は、指定したサーバー上の接続先のポートです。 既定では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はポート 1433 を使用します。<br /><br /> 渡される値の先頭のスペースは無視されます`Server`ODBC 接続文字列を使用する場合に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client。|  
|`ServerSPN`|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はドライバーが生成した SPN を既定値として使用します。|  
|`StatsLog_On`|"yes" の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのパフォーマンス データをキャプチャできます。 "no" の場合、その接続では [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのパフォーマンス データを取得できません。|  
|`StatsLogFile`|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのパフォーマンス統計を記録するために使用するファイルの完全なパスとファイル名。|  
|`Trusted_Connection`|"yes" の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでログインを検証するときに Windows 認証モードが使用されます。 それ以外の場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでログインを検証するときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のユーザー名とパスワードが使用され、UID キーワードと PWD キーワードの指定が必要になります。|  
|`TrustServerCertificate`|`Encrypt` と共に使用すると、自己署名入りのサーバー証明書による暗号化が有効になります。|  
|`UID`|有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン アカウント。 Windows 認証を使用する場合は UID を指定する必要はありません。|  
|`UseProcForPrepare`|このキーワードは非推奨し、して、設定が無視されます、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー。|  
|`WSID`|ワークステーション ID。 通常は、アプリケーションが実装されているコンピューターのネットワーク名です (省略可)。 この値が格納されている、指定されている場合、 **master.dbo.sysprocesses**列**hostname**によって返されると[sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) 、 [HOST_NAME](/sql/t-sql/functions/host-name-transact-sql)関数。|  
  
 **地域別の変換の設定は、通貨、数値、日付、および時刻のデータ型に適用されます。変換の設定は、出力変換にのみ適用し、通貨、数値、日付、または時刻の値が文字の文字列に変換する場合にのみ表示**します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、現在のユーザーに関するロケールのレジストリ設定が使用されます。 アプリケーション設定、接続後などを呼び出す場合、ドライバーは現在のスレッドのロケールを従いません**SetThreadLocale**します。  
  
 データ ソースの地域別の動作を変更すると、アプリケーション エラーが発生することがあります。 日付文字列を解析し、ODBC の定義に従った形式の日付文字列を受け付けるアプリケーションが、地域別の動作の値を変更することによって、悪影響を受ける可能性があります。  
  
## <a name="ole-db-provider-connection-string-keywords"></a>OLE DB プロバイダーの接続文字列キーワード  
 OLE DB アプリケーションでデータ ソース オブジェクトを初期化する方法は 2 つあります。  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 最初の方法では、DBPROPSET_DBINIT プロパティ セットのプロパティ DBPROP_INIT_PROVIDERSTRING を設定することにより、プロバイダー文字列で接続プロパティを初期化できます。 2 番目の方法では、**IDataInitialize::GetDataSource** メソッドに初期化文字列を渡して、接続プロパティを初期化できます。 いずれの方法でも同一の OLE DB 接続プロパティが初期化されますが、使用されるキーワードのセットは異なります。 **IDataInitialize::GetDataSource** で使用されるキーワードのセットには、少なくとも初期化プロパティ グループ内のプロパティの説明が含まれます。  
  
 対応する OLE DB プロパティを持つプロバイダー文字列の設定は一部の既定値に設定されるか、値に明示的に設定され、OLE DB プロパティ値はプロバイダー文字列の設定をオーバーライドします。  
  
 DBPROP_INIT_PROVIDERSTRING 値によってプロバイダー文字列内で設定されるブール型のプロパティは、値 "yes" と "no" を使用して設定します。 **IDataInitialize::GetDataSource** によって初期化文字列内で設定されるブール型のプロパティは、値 "true" と "false" を使用して設定します。  
  
 **IDataInitialize::GetDataSource** を使用するアプリケーションでは、既定値を持たないプロパティに対してのみ、**IDBInitialize::Initialize** で用いられるキーワードも利用できます。 **IDataInitialize::GetDataSource** キーワードと **IDBInitialize::Initialize** キーワードの両方を初期化文字列で使用すると、**IDataInitialize::GetDataSource** キーワードの設定が利用されます。 今後のリリースではこの動作が維持されない可能性があるので、**IDataInitialize:GetDataSource** 接続文字列では **IDBInitialize::Initialize** キーワードを使用しないことを強くお勧めします。  
  
 **注:****IDataInitialize::GetDataSource** を介して渡される接続文字列は、プロパティに変換され、**IDBProperties::SetProperties** で適用されます。 コンポーネント サービスによって **IDBProperties::GetPropertyInfo** でプロパティ説明が検出された場合、このプロパティはスタンドアロンのプロパティとして適用されます。 それ以外の場合は、DBPROP_PROVIDERSTRING プロパティを介して適用されます。 たとえば、接続文字列を指定する**データ ソース = server1;Server = server2**、`Data Source`をプロパティとして設定されますが、`Server`プロバイダー文字列に変わります。  
  
 同じプロバイダー固有のプロパティのインスタンスを複数指定した場合、最初のプロパティの最初の値が使用されます。  
  
 **IDBInitialize::Initialize** と共に DBPROP_INIT_PROVIDERSTRING を利用する OLE DB アプリケーションで使用される接続文字列の構文は次のとおりです。  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性値は必要に応じて中かっこで囲むことができます。常に中かっこを使用すると、 属性値に英数字以外の文字が含まれる場合の問題を回避できます。 最初の右中かっこが値の終わりと見なされるため、値に右中かっこを含めることはできません。  
  
 接続文字列キーワードの等号 (=) の後のスペース文字は、値を引用符で囲んだ場合でも、リテラルとして解釈されます。  
  
 次の表に、DBPROP_INIT_PROVIDERSTRING と共に使用できるキーワードを示します。  
  
|Keyword|初期化プロパティ|説明|  
|-------------|-----------------------------|-----------------|  
|`Addr`|SSPROP_INIT_NETWORKADDRESS|"Address" のシノニム。|  
|`Address`|SSPROP_INIT_NETWORKADDRESS|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのネットワーク アドレス。<br /><br /> 有効なアドレス構文の詳細については、このトピック内にある `Address` ODBC キーワードに関する説明を参照してください。|  
|`APP`|SSPROP_INIT_APPNAME|アプリケーションを識別する文字列。|  
|`ApplicationIntent`|SSPROP_INIT_APPLICATIONINTENT|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 設定可能な値は `ReadOnly` および `ReadWrite` です。<br /><br /> 既定値は `ReadWrite` です。 詳細については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。|  
|`AttachDBFileName`|SSPROP_INIT_FILENAME|アタッチできるデータベースのプライマリ ファイルの名前 (完全なパス名を含む)。 使用する`AttachDBFileName`、プロバイダー文字列の Database キーワードでデータベース名を指定することも必要があります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|`Auto Translate`|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" のシノニム。|  
|`AutoTranslate`|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 文字の変換を構成します。 認識できる値は "yes" と "no" です。|  
|`Database`|DBPROP_INIT_CATALOG|データベース名です。|  
|`DataTypeCompatibility`|SSPROP_INIT_DATATYPECOMPATIBILITY|データ型を使用する処理モードを指定します。 認識できる値は、プロバイダー データ型を示す "0" および SQL Server 2000 データ型を示す "80" です。|  
|`Encrypt`|SSPROP_INIT_ENCRYPT|データをネットワークに送信する前に暗号化するかどうかを指定します。 有効値は、"yes" および "no" です。 既定値は "no" です。|  
|`FailoverPartner`|SSPROP_INIT_FAILOVERPARTNER|データベース ミラーリングに使用するフェールオーバー サーバーの名前。|  
|`FailoverPartnerSPN`|SSPROP_INIT_FAILOVERPARTNERSPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|`Language`|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語。|  
|`MarsConn`|SSPROP_INIT_MARSCONNECTION|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のサーバーの場合)。 有効値は、"yes" および "no" です。 既定値は "no" です。|  
|`Net`|SSPROP_INIT_NETWORKLIBRARY|"Network" のシノニム。|  
|`Network`|SSPROP_INIT_NETWORKLIBRARY|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立するために使用するネットワーク ライブラリ。|  
|`Network Library`|SSPROP_INIT_NETWORKLIBRARY|"Network" のシノニム。|  
|`PacketSize`|SSPROP_INIT_PACKETSIZE|ネットワーク パケットのサイズ。 既定値は 4096 です。|  
|`PersistSensitive`|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|文字列 "yes" と "no" を値として受け取ります。 "no" の場合、データ ソース オブジェクトには機密の認証情報を保存できません。|  
|`PWD`|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン パスワード。|  
|`Server`|DBPROP_INIT_DATASOURCE|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。<br /><br /> 指定されなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続します。<br /><br /> 有効なアドレス構文の詳細については、の説明を参照して、 `Server` ODBC キーワードは、このトピックの「します。|  
|`ServerSPN`|SSPROP_INIT_SERVERSPN|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|`Timeout`|DBPROP_INIT_TIMEOUT|データ ソースの初期化が完了するのを待機する秒数。|  
|`Trusted_Connection`|DBPROP_AUTH_INTEGRATED|"yes" の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでログインを検証するときに Windows 認証モードが使用されます。 それ以外の場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでログインを検証するときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のユーザー名とパスワードが使用され、UID キーワードと PWD キーワードの指定が必要になります。|  
|`TrustServerCertificate`|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|文字列 "yes" と "no" を値として受け取ります。 既定値は "no" です。これはサーバー証明書が検証されることを示します。|  
|`UID`|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン名。|  
|`UseProcForPrepare`|SSPROP_INIT_USEPROCFORPREP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、このキーワードは非推奨とされ、設定は無視されます。|  
|`WSID`|SSPROP_INIT_WSID|ワークステーションの識別子です。|  
  
 **IDataInitialize::GetDataSource** を利用する OLE DB アプリケーションで使用される接続文字列の構文は次のとおりです。  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 プロパティの使用方法は、プロパティのスコープで許可される構文に従っている必要があります。  たとえば、`WSID`中かっこを使用して (`{}`) 引用符文字と`Application Name`では一重 (`'`) または二重 (`"`) 引用符文字。 引用符で囲むことができるのは、文字列のプロパティのみです。 整数または列挙のプロパティを引用符で囲むと、"接続文字列は OLE DB 仕様に準拠していません" というエラーが発生します。  
  
 属性値は必要に応じて一重引用符または二重引用符で囲むことができます。常にこれらの引用符を使用すると、 値に英数字以外の文字が含まれる場合の問題を回避できます。 二重引用符の場合は、値の中に含めることもできます。  
  
 接続文字列キーワードの等号 (=) の後のスペース文字は、値を引用符で囲んだ場合でも、リテラルとして解釈されます。  
  
 接続文字列に次の表のプロパティが複数含まれている場合は、最後のプロパティの値が使用されます。  
  
 次の表では、**IDataInitialize::GetDataSource** と共に使用できるキーワードについて説明します。  
  
|Keyword|初期化プロパティ|説明|  
|-------------|-----------------------------|-----------------|  
|`Application Name`|SSPROP_INIT_APPNAME|アプリケーションを識別する文字列。|  
|`Application Intent`|SSPROP_INIT_APPLICATIONINTENT|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 設定可能な値は `ReadOnly` および `ReadWrite` です。<br /><br /> 既定値は `ReadWrite` です。 詳細については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。|  
|`Auto Translate`|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" のシノニム。|  
|`AutoTranslate`|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 文字の変換を構成します。 認識できる値は "true" と "false" です。|  
|`Connect Timeout`|DBPROP_INIT_TIMEOUT|データ ソースの初期化が完了するのを待機する秒数。|  
|`Current Language`|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語の名前。|  
|`Data Source`|DBPROP_INIT_DATASOURCE|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。<br /><br /> 指定されなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続します。<br /><br /> 有効なアドレス構文の詳細については、このトピック内にある `Server` ODBC キーワードに関する説明を参照してください。|  
|`DataTypeCompatibility`|SSPROP_INIT_DATATYPECOMPATIBILITY|データ型を使用する処理モードを指定します。 認識できる値は、プロバイダー データ型を示す "0" および [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] データ型を示す "80" です。|  
|`Failover Partner`|SSPROP_INIT_FAILOVERPARTNER|データベース ミラーリングに使用するフェールオーバー サーバーの名前。|  
|`Failover Partner SPN`|SSPROP_INIT_FAILOVERPARTNERSPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|`Initial Catalog`|DBPROP_INIT_CATALOG|データベース名です。|  
|`Initial File Name`|SSPROP_INIT_FILENAME|アタッチできるデータベースのプライマリ ファイルの名前 (完全なパス名を含む)。 `AttachDBFileName` を使用するには、プロバイダー文字列の DATABASE キーワードでデータベース名を指定する必要があります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|`Integrated Security`|DBPROP_AUTH_INTEGRATED|Windows 認証の値 "SSPI" を受け取ります。|  
|`MARS Connection`|SSPROP_INIT_MARSCONNECTION|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします。 認識できる値は "true" と "false" です。 既定値は "false" です。|  
|`Network Address`|SSPROP_INIT_NETWORKADDRESS|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのネットワーク アドレス。<br /><br /> 有効なアドレス構文の詳細については、このトピック内にある `Address` ODBC キーワードに関する説明を参照してください。|  
|`Network Library`|SSPROP_INIT_NETWORKLIBRARY|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立するために使用するネットワーク ライブラリ。|  
|`Packet Size`|SSPROP_INIT_PACKETSIZE|ネットワーク パケットのサイズ。 既定値は 4096 です。|  
|`Password`|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン パスワード。|  
|`Persist Security Info`|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|文字列 "true" と "false" を値として受け取ります。 "false" の場合、データ ソース オブジェクトには機密の認証情報を保存できません|  
|`Provider`||[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の場合は "SQLNCLI11"。|  
|`Server SPN`|SSPROP_INIT_SERVERSPN|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|`Trust Server Certificate`|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|文字列 "true" と "false" を値として受け取ります。 既定値は "false" です。これはサーバー証明書が検証されることを示します。|  
|`Use Encryption for Data`|SSPROP_INIT_ENCRYPT|データをネットワークに送信する前に暗号化するかどうかを指定します。 指定できる値は "true" と "false" です。 既定値は "false" です。|  
|`User ID`|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン名。|  
|`Workstation ID`|SSPROP_INIT_WSID|ワークステーションの識別子です。|  
  
 **注** 接続文字列の "Old Password" プロパティは SSPROP_AUTH_OLD_PASSWORD に設定され、現在の (または期限切れの) パスワードが設定されます。このパスワードをプロバイダー文字列のプロパティ経由で使用することはできません。  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ADO (ActiveX Data Objects) の接続文字列のキーワード  
 ADO アプリケーションでは、**ADODBConnection** オブジェクトの **ConnectionString** プロパティが設定されるか、**ADODBConnection** オブジェクトの **Open** メソッドにパラメーターとして接続文字列が指定されます。  
  
 また、ADO アプリケーションでは、既定値がないプロパティにのみ、OLE DB **IDBInitialize::Initialize** メソッドで使用されるキーワードを利用できます。 アプリケーションにより、初期化文字列で ADO キーワードと **IDBInitialize::Initialize** キーワードが両方とも使われている場合、ADO キーワードの設定が使用されます。 アプリケーションでは ADO 接続文字列のキーワードのみを使用することを強くお勧めします。  
  
 ADO で使用される接続文字列の構文を次に示します。  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性値は必要に応じて二重引用符で囲むことができます。常に二重引用符を使用すると、 値に英数字以外の文字が含まれる場合の問題を回避できます。 属性値に二重引用符を含めることはできません。  
  
 次の表に、ADO 接続文字列と共に使用できるキーワードを示します。  
  
|Keyword|初期化プロパティ|説明|  
|-------------|-----------------------------|-----------------|  
|`Application Intent`|SSPROP_INIT_APPLICATIONINTENT|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 設定可能な値は `ReadOnly` および `ReadWrite` です。<br /><br /> 既定値は `ReadWrite` です。 詳細については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のネイティブ クライアントのサポート[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[SQL Server ネイティブ クライアントをサポートして高可用性、ディザスター リカバリーのため](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。|  
|`Application Name`|SSPROP_INIT_APPNAME|アプリケーションを識別する文字列。|  
|`Auto Translate`|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" のシノニム。|  
|`AutoTranslate`|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 文字の変換を構成します。 認識できる値は "true" と "false" です。|  
|`Connect Timeout`|DBPROP_INIT_TIMEOUT|データ ソースの初期化が完了するのを待機する秒数。|  
|`Current Language`|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語の名前。|  
|`Data Source`|DBPROP_INIT_DATASOURCE|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。<br /><br /> 指定されなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続します。<br /><br /> 有効なアドレス構文の詳細については、の説明を参照して、 `Server` ODBC キーワードは、このトピックの「します。|  
|`DataTypeCompatibility`|SSPROP_INIT_DATATYPECOMPATIBILITY|使用するデータ型処理モードを指定します。 認識できる値は、プロバイダー データ型を示す "0" および SQL Server 2000 データ型を示す "80" です。|  
|`Failover Partner`|SSPROP_INIT_FAILOVERPARTNER|データベース ミラーリングに使用するフェールオーバー サーバーの名前。|  
|`Failover Partner SPN`|SSPROP_INIT_FAILOVERPARTNERSPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|`Initial Catalog`|DBPROP_INIT_CATALOG|データベース名です。|  
|`Initial File Name`|SSPROP_INIT_FILENAME|アタッチできるデータベースのプライマリ ファイルの名前 (完全なパス名を含む)。 `AttachDBFileName` を使用するには、プロバイダー文字列の DATABASE キーワードでデータベース名を指定する必要があります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|`Integrated Security`|DBPROP_AUTH_INTEGRATED|Windows 認証の値 "SSPI" を受け取ります。|  
|`MARS Connection`|SSPROP_INIT_MARSCONNECTION|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のサーバーの場合)。 認識できる値は "true" と "false" です。既定値は "false" です。|  
|`Network Address`|SSPROP_INIT_NETWORKADDRESS|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのネットワーク アドレス。<br /><br /> 有効なアドレス構文の詳細については、の説明を参照して、 `Address` ODBC キーワードは、このトピックの「します。|  
|`Network Library`|SSPROP_INIT_NETWORKLIBRARY|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立するために使用するネットワーク ライブラリ。|  
|`Packet Size`|SSPROP_INIT_PACKETSIZE|ネットワーク パケットのサイズ。 既定値は 4096 です。|  
|`Password`|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン パスワード。|  
|`Persist Security Info`|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|文字列 "true" と "false" を値として受け取ります。 "false" の場合、データ ソース オブジェクトには機密の認証情報を保存できません。|  
|`Provider`||[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の場合は "SQLNCLI11"。|  
|`Server SPN`|SSPROP_INIT_SERVERSPN|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|`Trust Server Certificate`|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|文字列 "true" と "false" を値として受け取ります。 既定値は "false" です。これはサーバー証明書が検証されることを示します。|  
|`Use Encryption for Data`|SSPROP_INIT_ENCRYPT|データをネットワークに送信する前に暗号化するかどうかを指定します。 指定できる値は "true" と "false" です。 既定値は "false" です。|  
|`User ID`|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン名。|  
|`Workstation ID`|SSPROP_INIT_WSID|ワークステーションの識別子です。|  
  
 **注** 接続文字列の "Old Password" プロパティは SSPROP_AUTH_OLD_PASSWORD に設定され、現在の (または期限切れの) パスワードが設定されます。このパスワードをプロバイダー文字列のプロパティ経由で使用することはできません。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションのビルド](building-applications-with-sql-server-native-client.md)  
  
  
