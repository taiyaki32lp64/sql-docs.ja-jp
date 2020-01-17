---
title: Native Client、接続キーワード SQL
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33612f7e4303ad9d02e4c6d3b7980e750e3a594b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258739"
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>SQL Server Native Client での接続文字列キーワードの使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  一部の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client API では、接続文字列を使用して接続属性を指定します。 接続文字列はキーワードとそれに関連する値のリストです。各キーワードによって特定の接続属性を識別します。  

> [!IMPORTANT]
> Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB (SQLNCLI) は非推奨とされます。新しい開発作業には使用しないことをお勧めします。 代わりに、新しい [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) を使用します。これは、最新のサーバー機能で更新されます。    
> 詳細については、「 [SQL Server の OLE DB ドライバーでの接続文字列キーワードの使用](../../../connect/oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)」を参照してください。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client を使用すると、接続文字列のあいまいさを解消して下位互換性を維持することができます (たとえば、いくつかのキーワードを複数回指定でき、競合するキーワードは位置や優先順位に基づいて解決される場合があります)。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用するアプリケーションでは、あいまいな接続文字列を利用しないように変更することをお勧めします。  
  
 次のセクションでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をデータ プロバイダーとして使用するときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー、および ADO (ActiveX Data Objects) と共に使用できるキーワードについて説明します。  
  
## <a name="odbc-driver-connection-string-keywords"></a>ODBC ドライバーの接続文字列キーワード  
 ODBC アプリケーションでは、 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)関数と[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)関数のパラメーターとして接続文字列を使用します。  
  
 ODBC で使用される接続文字列の構文を次に示します。  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性値は必要に応じて中かっこで囲むことができます。常に中かっこを使用すると、 属性値に英数字以外の文字が含まれる場合の問題を回避できます。 最初の右中かっこが値の終わりと見なされるため、値に右中かっこを含めることはできません。  
  
 次の表に、ODBC 接続文字列と共に使用できるキーワードを示します。  
  
|キーワード|説明|  
|-------------|-----------------|  
|**引き**|"Address" のシノニム。|  
|**番地**|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスを実行しているサーバーのネットワーク アドレス。 **アドレス**は通常、サーバーのネットワーク名ですが、パイプ、ip アドレス、tcp/ip ポート、ソケットアドレスなど、他の名前を指定することもできます。<br /><br /> IP アドレスを指定する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで TCP/IP または名前付きパイプ プロトコルが有効になっていることを確認します。<br /><br /> **Address**の値は、Native Client の使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時に ODBC 接続文字列で**サーバー**に渡される値よりも優先されます。 また、は`Address=;` **server**キーワード`Address= ;, Address=.;` `Address=localhost;`に指定されているサーバーに接続しますが、 `Address=(local);` 、、およびはすべて、ローカルサーバーへの接続を引き起こします。<br /><br /> 
  **Address** キーワードの完全な構文は次のとおりです。<br /><br /> [_プロトコル_**:**]*アドレス*[**、**_ポート &#124; \pipe\pipename_]<br /><br /> *プロトコル*には、 **tcp** (tcp/ip)、 **lpc** (共有メモリ)、または**np** (名前付きパイプ) を指定できます。 プロトコルの詳細については、「 [Configure Client プロトコル](../../../database-engine/configure-windows/configure-client-protocols.md)」を参照してください。<br /><br /> *Protocol*も**Network**キーワードも指定されてい[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ない場合、Native Client では Configuration Manager で[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]指定されたプロトコル順が使用されます。<br /><br /> *port*は、指定されたサーバー上の接続先のポートです。 既定では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はポート 1433 を使用します。|  
|**AnsiNPW**|"yes" の場合、ANSI で定められた動作に従って NULL の比較、文字データの埋め込み、警告、および NULL 連結が処理されます。 "no" の場合、ANSI で定められた動作が公開されません。 ANSI NPW の動作の詳細については、「 [ISO オプションの効果](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)」を参照してください。|  
|**アプリケーション**|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)を呼び出すアプリケーションの名前 (省略可能)。 この値が指定されている場合、この値は**program_name** **マスター**列に格納され、 [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)と[APP_NAME](../../../t-sql/functions/app-name-transact-sql.md)関数によって返されます。|  
|**ApplicationIntent**|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 有効値は、**ReadOnly** と **ReadWrite** です。 既定値は**ReadWrite**です。  例:<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるの[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]サポートの詳細については、「[高可用性、ディザスターリカバリーのサポートの SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。|  
|**AttachDBFileName**|アタッチできるデータベースのプライマリ ファイルの名前。 この名前には完全なパス名を指定します。また C 文字列変数を使用する場合は、\ 文字をエスケープしてください。<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> このデータベースがアタッチされ、接続の既定のデータベースとして使用されます。 **AttachDBFileName**を使用するには、 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)データベースパラメーターまたは SQL_COPT_CURRENT_CATALOG 接続属性でもデータベース名を指定する必要があります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|**AutoTranslate**|"yes" の場合、クライアントとサーバーの間で送受信される ANSI 文字列は、いったん Unicode に変換されます。これは、クライアントとサーバーのコード ページ間で拡張文字を照合するときに発生する問題を最小限に抑えるためです。<br /><br /> クライアント SQL_C_CHAR [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **CHAR**、 **varchar**、または**text**変数、パラメーター、または列に送信されるデータは、クライアントの ANSI コードページ (acp) を使用して文字から unicode に変換され、その後、サーバーの acp を使用して unicode から文字に変換されます。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]クライアント SQL_C_CHAR 変数に送信される**char**、 **varchar**、または**text**データは、サーバーの acp を使用して文字から unicode に変換され、その後、クライアントの acp を使用して unicode から文字に変換されます。<br /><br /> この変換は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーによってクライアントで行われます。 また、サーバーで使用しているものと同じ ACP (ANSI コード ページ) がクライアントでも使用可能になっている必要があります。<br /><br /> 次の設定は、送受信時の変換に影響しません。<br /><br /> \*サーバー上の**char**型、 **varchar**型、または**text**型に送信される、Unicode SQL_C_WCHAR クライアントデータ。<br /><br /> クライアント上の Unicode SQL_C_WCHAR 変数に送信される**char**、 **varchar**、または**text** server のデータ &#42; ます。<br /><br /> \*ANSI SQL_C_CHAR サーバー上の Unicode **nchar**、 **nvarchar**、または**ntext**に送信されるクライアントデータ。<br /><br /> \*Unicode **nchar**、 **nvarchar**、または**ntext**サーバーのデータが、クライアントの ANSI SQL_C_CHAR 変数に送信されます。<br /><br /> "no" の場合、文字の変換は行われません。<br /><br /> Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client ODBC ドライバーは、サーバー上の**CHAR**、 **varchar**、または**text**変数、パラメーター、または列に送信される、クライアントの ANSI 文字 SQL_C_CHAR データを変換しません。 サーバーからクライアントの SQL_C_CHAR 変数に送信される**char**、 **varchar**、または**text**型のデータに対しては、変換は実行されません。<br /><br /> クライアントと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で使用する ACP が異なる場合、拡張文字の解釈が正しく行われない場合があります。|  
|**データベース**|接続に使用する既定の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースの名前。 **データベース**が指定されていない場合は、ログイン用に定義された既定のデータベースが使用されます。 ODBC データ ソースの既定のデータベースは、ログインに定義されている既定のデータベースをオーバーライドします。 **AttachDBFileName**も指定しない限り、データベースは既存のデータベースである必要があります。 **AttachDBFileName**も指定した場合、参照先のプライマリファイルがアタッチされ、**データベース**によって指定されたデータベース名が割り当てられます。|  
|**Driver**|[Sqldrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md)によって返されるドライバーの名前。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに対するこのキーワードの値は "{SQL Server Native Client 11.0}" です。 **Driver**が指定され、 **drivercompletion**が SQL_DRIVER_NOPROMPT に設定されている場合は、 **Server**キーワードが必要です。<br /><br /> ドライバー名の詳細については、「 [SQL Server Native Client ヘッダーファイルとライブラリファイルの使用](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md)」を参照してください。|  
|**ソース**|既存の ODBC ユーザー データ ソースまたはシステム データ ソースの名前。 このキーワードは、**サーバー**、**ネットワーク**、および**アドレス**キーワードに指定されている可能性のあるすべての値を上書きします。|  
|**暗号化**|データをネットワークに送信する前に暗号化するかどうかを指定します。 有効値は、"yes" および "no" です。 既定値は "no" です。|  
|**プライ**|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、このキーワードは非推奨とされ、設定は無視されます。|  
|**Failover_Partner**|プライマリ サーバーに接続できない場合に使用するフェールオーバー パートナー サーバーの名前。|  
|**FailoverPartnerSPN**|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はドライバーが生成した SPN を既定値として使用します。|  
|**FileDSN**|既存の ODBC ファイル データ ソースの名前。|  
|**言語**|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語の名前 (省略可)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、複数の言語のメッセージを**sysmessages**に格納できます。 複数の言語[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]でに接続する場合、**言語**では、接続に使用するメッセージのセットを指定します。|  
|**MARS_Connection**|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします。 認識できる値は "yes" と "no" です。 既定値は "no" です。|  
|**MultiSubnetFailover**|可用性グループまたは[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]フェールオーバークラスターインスタンスの可用性グループリスナーに接続する場合は、常に**multiSubnetFailover = Yes**を指定します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **multiSubnetFailover = Yes**を[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]指定すると、Native Client は、(現在) アクティブなサーバーを迅速に検出して接続するように構成されます。 使用可能な値は**Yes**と**No**です。 既定値は **[いいえ]** です。 例:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるの[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]サポートの詳細については、「[高可用性、ディザスターリカバリーのサポートの SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。|  
|**Net**|"Network" のシノニム。|  
|**ネットワーク**|有効な値は、 **dbnmpntw** (名前付きパイプ) と**dbmssocn** (tcp/ip) です。<br /><br /> **Network**キーワードの値と**Server**キーワードのプロトコルプレフィックスの両方を指定すると、エラーになります。|  
|**PWD**|UID パラメーターで指定されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン アカウントのパスワード。 **** ログインに NULL パスワードが含まれている場合、または Windows 認証 (`Trusted_Connection = yes`) を使用している場合は、PWD を指定する必要はありません。|  
|**QueryLog_On**|"yes" の場合、その接続では、実行時間の長いクエリのデータに関するログを記録できます。 "no" の場合、実行時間の長いクエリのデータに関するログは記録されません。|  
|**QueryLogFile**|実行時間の長いクエリのデータをログに記録する場合に使用するファイルの完全なパスとファイル名。|  
|**QueryLogTime**|実行時間の長いクエリをログに記録するためのしきい値 (ミリ秒) を指定する数字文字列。 指定時間内に応答が返ってこないクエリは、実行時間の長いクエリ用のログ ファイルに記録されます。|  
|**QuotedId**|"yes" の場合、その接続の QUOTED_IDENTIFIERS が ON に設定され、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は ISO 規則に従って SQL ステートメントの引用符を処理します。 "no" の場合、その接続の QUOTED_IDENTIFIERS が OFF に設定され、 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は従来の [!INCLUDE[tsql](../../../includes/tsql-md.md)] 規則に従って SQL ステートメントの引用符を処理します。 詳細については、「 [ISO オプションの効果](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)」を参照してください。|  
|**地域**|"yes" の場合、通貨、日付、および時刻データが文字データに変換されるときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーではクライアントの設定が使用されます。 変換は一方向にのみ行われます。INSERT ステートメントや UPDATE ステートメントのパラメーターなどで日付文字列または通貨の値が ODBC 標準以外の形式で指定されている場合、ドライバーでは、これらの値は認識されません。 "no" の場合、文字データに変換される通貨、日付、および時刻データを表現するために ODBC 標準の文字列が使用されます。|  
|**SaveFile**|接続が成功した場合に、現在の接続の属性を保存する ODBC データ ソース ファイルの名前。|  
|**Server**|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前。 ネットワーク上のサーバーの名前、IP アドレス、または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーの別名を指定する必要があります。<br /><br /> **Address**キーワードは**Server**キーワードよりも優先されます。<br /><br /> 次のいずれかを指定することで、ローカル サーバー上の既定のインスタンスに接続できます。<br /><br /> **サーバー =;**<br /><br /> **サーバー =.;**<br /><br /> **Server = (local);**<br /><br /> **Server = (local);**<br /><br /> **Server = (localhost);**<br /><br /> **Server = (localdb)\\ ** _instancename_ **;**<br /><br /> LocalDB のサポートの詳細については、「 [SQL Server Native Client サポート localdb](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)」を参照してください。<br /><br /> の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]名前付きインスタンスを指定するに**\\**は、 _InstanceName_を追加します。<br /><br /> サーバーを指定しなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続されます。<br /><br /> IP アドレスを指定する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで TCP/IP または名前付きパイプ プロトコルが有効になっていることを確認します。<br /><br /> 
  **Server** キーワードの完全な構文は次のとおりです。<br /><br /> **Server =**[_protocol_**:**]*サーバー*[**,**_port_]<br /><br /> *プロトコル*には、 **tcp** (tcp/ip)、 **lpc** (共有メモリ)、または**np** (名前付きパイプ) を指定できます。<br /><br /> 名前付きパイプを指定する例を次に示します。<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> この行では、名前付きパイプのプロトコル、ローカル コンピューター上の名前付きパイプ (`\\.\pipe`)、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前 (`MSSQL$MYINST01`)、および名前付きパイプの既定の名前 (`sql/query`) を指定しています。<br /><br /> *Protocol*も**Network**キーワードも指定されていない[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]場合、Native Client では Configuration Manager で[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]指定されたプロトコル順が使用されます。<br /><br /> *port*は、指定されたサーバー上の接続先のポートです。 既定では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はポート 1433 を使用します。<br /><br /> Native Client を使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]する場合、ODBC 接続文字列内の**サーバー**に渡される値の先頭では、スペースは無視されます。|  
|**ServerSPN**|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はドライバーが生成した SPN を既定値として使用します。|  
|**StatsLog_On**|"yes" の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのパフォーマンス データをキャプチャできます。 "no" の場合、その接続では [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのパフォーマンス データを取得できません。|  
|**StatsLogFile**|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのパフォーマンス統計を記録するために使用するファイルの完全なパスとファイル名。|  
|**Trusted_Connection**|"yes" の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでログインを検証するときに Windows 認証モードが使用されます。 それ以外の場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでログインを検証するときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のユーザー名とパスワードが使用され、UID キーワードと PWD キーワードの指定が必要になります。|  
|**TrustServerCertificate**|**暗号化**と共に使用すると、自己署名サーバー証明書を使用した暗号化が有効になります。|  
|**UID**|有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン アカウント。 Windows 認証を使用する場合は UID を指定する必要はありません。|  
|**UseProcForPrepare**|このキーワードは非推奨とされており、その[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]設定は NATIVE Client ODBC ドライバーによって無視されます。|  
|**WSID**|ワークステーション ID。 通常は、アプリケーションが実装されているコンピューターのネットワーク名です (省略可)。 この値が指定さ**れている**場合、この値は、 [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)と[HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)関数によって返され**ます。**|  
  
> **注:** 地域への変換の設定は、通貨、数値、日付、および時刻のデータ型に適用されます。 変換の設定は、出力変換にのみ適用され、通貨、数値、日付、または時刻の値を文字列に変換する場合にのみ確認することができます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、現在のユーザーに関するロケールのレジストリ設定が使用されます。 アプリケーションが接続後に ( **Setthreadlocale**を呼び出すなど) 設定した場合、ドライバーは現在のスレッドのロケールを優先しません。  
  
 データ ソースの地域別の動作を変更すると、アプリケーション エラーが発生することがあります。 日付文字列を解析し、ODBC の定義に従った形式の日付文字列を受け付けるアプリケーションが、地域別の動作の値を変更することによって、悪影響を受ける可能性があります。  
  
## <a name="ole-db-provider-connection-string-keywords"></a>OLE DB プロバイダーの接続文字列キーワード  
 OLE DB アプリケーションでデータ ソース オブジェクトを初期化する方法は 2 つあります。  
  
-   **IDBInitialize:: Initialize**  
  
-   **IDataInitialize:: GetDataSource**  
  
 最初の方法では、DBPROPSET_DBINIT プロパティ セットのプロパティ DBPROP_INIT_PROVIDERSTRING を設定することにより、プロバイダー文字列で接続プロパティを初期化できます。 2 番目の方法では、**IDataInitialize::GetDataSource** メソッドに初期化文字列を渡して、接続プロパティを初期化できます。 いずれの方法でも同一の OLE DB 接続プロパティが初期化されますが、使用されるキーワードのセットは異なります。 
  **IDataInitialize::GetDataSource** で使用されるキーワードのセットには、少なくとも初期化プロパティ グループ内のプロパティの説明が含まれます。  
  
 対応する OLE DB プロパティを持つプロバイダー文字列の設定は一部の既定値に設定されるか、値に明示的に設定され、OLE DB プロパティ値はプロバイダー文字列の設定をオーバーライドします。  
  
 DBPROP_INIT_PROVIDERSTRING 値によってプロバイダー文字列内で設定されるブール型のプロパティは、値 "yes" と "no" を使用して設定します。 
  **IDataInitialize::GetDataSource** によって初期化文字列内で設定されるブール型のプロパティは、値 "true" と "false" を使用して設定します。  
  
 
  **IDataInitialize::GetDataSource** を使用するアプリケーションでは、既定値を持たないプロパティに対してのみ、**IDBInitialize::Initialize** で用いられるキーワードも利用できます。 
  **IDataInitialize::GetDataSource** キーワードと **IDBInitialize::Initialize** キーワードの両方を初期化文字列で使用すると、**IDataInitialize::GetDataSource** キーワードの設定が利用されます。 今後のリリースではこの動作が維持されない可能性があるので、**IDataInitialize:GetDataSource** 接続文字列では **IDBInitialize::Initialize** キーワードを使用しないことを強くお勧めします。  
  
> [!NOTE]  
>  
  **IDataInitialize::GetDataSource** を介して渡される接続文字列は、プロパティに変換され、**IDBProperties::SetProperties** で適用されます。 コンポーネント サービスによって **IDBProperties::GetPropertyInfo** でプロパティ説明が検出された場合、このプロパティはスタンドアロンのプロパティとして適用されます。 それ以外の場合は、DBPROP_PROVIDERSTRING プロパティを介して適用されます。 たとえば、接続文字列**Data Source = server1; を指定した場合、Server = server2**、**データソース**はプロパティとして設定されますが、**サーバー**はプロバイダー文字列に入ります。  
  
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
  
|キーワード|初期化プロパティ|説明|  
|-------------|-----------------------------|-----------------|  
|**引き**|SSPROP_INIT_NETWORKADDRESS|"Address" のシノニム。|  
|**番地**|SSPROP_INIT_NETWORKADDRESS|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのネットワーク アドレス。<br /><br /> 有効なアドレス構文の詳細については、このトピックの「 **address** ODBC キーワード」の説明を参照してください。|  
|**アプリケーション**|SSPROP_INIT_APPNAME|アプリケーションを識別する文字列。|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 有効値は、**ReadOnly** と **ReadWrite** です。<br /><br /> 既定値は**ReadWrite**です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるの[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]サポートの詳細については、「[高可用性、ディザスターリカバリーのサポートの SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|アタッチできるデータベースのプライマリ ファイルの名前 (完全なパス名を含む)。 
  **AttachDBFileName** を使用するには、プロバイダー文字列の Database キーワードでデータベース名を指定する必要もあります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|**自動翻訳**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" のシノニム。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 文字の変換を構成します。 認識できる値は "yes" と "no" です。|  
|**データベース**|DBPROP_INIT_CATALOG|データベース名です。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|使用するデータ型の処理モードを指定します。 認識できる値は、プロバイダー データ型を示す "0" および SQL Server 2000 データ型を示す "80" です。|  
|**暗号化**|SSPROP_INIT_ENCRYPT|データをネットワークに送信する前に暗号化するかどうかを指定します。 有効値は、"yes" および "no" です。 既定値は "no" です。|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|データベース ミラーリングに使用するフェールオーバー サーバーの名前。|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|**言語**|SSPROPT_INIT_CURRENTLANGUAGE|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語。|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のサーバーの場合)。 有効値は、"yes" および "no" です。 既定値は "no" です。|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|"Network" のシノニム。|  
|**ネットワーク**|SSPROP_INIT_NETWORKLIBRARY|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立するために使用するネットワーク ライブラリ。|  
|**ネットワークライブラリ**|SSPROP_INIT_NETWORKLIBRARY|"Network" のシノニム。|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|ネットワーク パケットのサイズ。 既定値は 4096 です。|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|文字列 "yes" と "no" を値として受け取ります。 "no" の場合、データ ソース オブジェクトには機密の認証情報を保存できません。|  
|**PWD**|DBPROP_AUTH_PASSWORD|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン パスワード。|  
|**Server**|DBPROP_INIT_DATASOURCE|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。<br /><br /> 指定されなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続します。<br /><br /> 有効なアドレス構文の詳細については、このトピックの「 **Server** ODBC キーワードの説明」を参照してください。|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|**タイムアウト**|DBPROP_INIT_TIMEOUT|データ ソースの初期化が完了するのを待機する秒数。|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|"yes" の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでログインを検証するときに Windows 認証モードが使用されます。 それ以外の場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでログインを検証するときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のユーザー名とパスワードが使用され、UID キーワードと PWD キーワードの指定が必要になります。|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|文字列 "yes" と "no" を値として受け取ります。 既定値は "no" です。これはサーバー証明書が検証されることを示します。|  
|**UID**|DBPROP_AUTH_USERID|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン名。|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、このキーワードは非推奨とされ、設定は無視されます。|  
|**WSID**|SSPROP_INIT_WSID|ワークステーション識別子。|  
  
 
  **IDataInitialize::GetDataSource** を利用する OLE DB アプリケーションで使用される接続文字列の構文は次のとおりです。  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 プロパティの使用方法は、プロパティのスコープで許可される構文に従っている必要があります。  たとえば、 **Wsid**では中かっこ (**{}**) 引用符が使用され、**アプリケーション名**には単一 (**'**) または二重引用符 (**"**) の文字が使用されます。 引用符で囲むことができるのは、文字列のプロパティのみです。 整数または列挙のプロパティを引用符で囲むと、"接続文字列は OLE DB 仕様に準拠していません" というエラーが発生します。  
  
 属性値は必要に応じて一重引用符または二重引用符で囲むことができます。常にこれらの引用符を使用すると、 値に英数字以外の文字が含まれる場合の問題を回避できます。 二重引用符の場合は、値の中に含めることもできます。  
  
 接続文字列キーワードの等号 (=) の後のスペース文字は、値を引用符で囲んだ場合でも、リテラルとして解釈されます。  
  
 接続文字列に次の表のプロパティが複数含まれている場合は、最後のプロパティの値が使用されます。  
  
 次の表では、**IDataInitialize::GetDataSource** と共に使用できるキーワードについて説明します。  
  
|キーワード|初期化プロパティ|説明|  
|-------------|-----------------------------|-----------------|  
|**アプリケーション名**|SSPROP_INIT_APPNAME|アプリケーションを識別する文字列。|  
|**アプリケーションの目的**|SSPROP_INIT_APPLICATIONINTENT|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 有効値は、**ReadOnly** と **ReadWrite** です。<br /><br /> 既定値は**ReadWrite**です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるの[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]サポートの詳細については、「[高可用性、ディザスターリカバリーのサポートの SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。|  
|**自動翻訳**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" のシノニム。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 文字の変換を構成します。 認識できる値は "true" と "false" です。|  
|**接続のタイムアウト**|DBPROP_INIT_TIMEOUT|データ ソースの初期化が完了するのを待機する秒数。|  
|**[現在の言語]**|SSPROPT_INIT_CURRENTLANGUAGE|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語の名前。|  
|**データソース**|DBPROP_INIT_DATASOURCE|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。<br /><br /> 指定されなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続します。<br /><br /> 有効なアドレス構文の詳細については、このトピックで後述する「**サーバー** ODBC キーワードの説明」を参照してください。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|使用するデータ型の処理モードを指定します。 認識できる値は、プロバイダー データ型を示す "0" および [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] データ型を示す "80" です。|  
|**フェールオーバーパートナー**|SSPROP_INIT_FAILOVERPARTNER|データベース ミラーリングに使用するフェールオーバー サーバーの名前。|  
|**フェールオーバー パートナー SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|**初期カタログ**|DBPROP_INIT_CATALOG|データベース名です。|  
|**初期ファイル名**|SSPROP_INIT_FILENAME|アタッチできるデータベースのプライマリ ファイルの名前 (完全なパス名を含む)。 **AttachDBFileName**を使用するには、プロバイダー文字列 database キーワードを使用してデータベース名も指定する必要があります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|**統合セキュリティ**|DBPROP_AUTH_INTEGRATED|Windows 認証の値 "SSPI" を受け取ります。|  
|**MARS 接続**|SSPROP_INIT_MARSCONNECTION|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします。 認識できる値は "true" と "false" です。 既定値は "false" です。|  
|**ネットワークアドレス**|SSPROP_INIT_NETWORKADDRESS|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのネットワーク アドレス。<br /><br /> 有効なアドレス構文の詳細については、このトピックの「 **address** ODBC キーワード」の説明を参照してください。|  
|**ネットワークライブラリ**|SSPROP_INIT_NETWORKLIBRARY|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立するために使用するネットワーク ライブラリ。|  
|**パケットサイズ**|SSPROP_INIT_PACKETSIZE|ネットワーク パケットのサイズ。 既定値は 4096 です。|  
|**Password**|DBPROP_AUTH_PASSWORD|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン パスワード。|  
|**セキュリティ情報を保持する**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|文字列 "true" と "false" を値として受け取ります。 "false" の場合、データ ソース オブジェクトには機密の認証情報を保存できません|  
|**Provider**||
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の場合は "SQLNCLI11"。|  
|**サーバー SPN**|SSPROP_INIT_SERVERSPN|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|**サーバー証明書を信頼する**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|文字列 "true" と "false" を値として受け取ります。 既定値は "false" です。これはサーバー証明書が検証されることを示します。|  
|**データの暗号化を使用する**|SSPROP_INIT_ENCRYPT|データをネットワークに送信する前に暗号化するかどうかを指定します。 指定できる値は "true" と "false" です。 既定値は "false" です。|  
|**ユーザー ID**|DBPROP_AUTH_USERID|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン名。|  
|**[ワークステーション ID]**|SSPROP_INIT_WSID|ワークステーション識別子。|  
  
 **メモ**接続文字列では、"Old Password" プロパティによって SSPROP_AUTH_OLD_PASSWORD が設定されます。これは、プロバイダー文字列プロパティでは使用できない、現在の (有効期限切れの) パスワードです。  
  
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
  
|キーワード|初期化プロパティ|説明|  
|-------------|-----------------------------|-----------------|  
|**アプリケーションの目的**|SSPROP_INIT_APPLICATIONINTENT|アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 有効値は、**ReadOnly** と **ReadWrite** です。<br /><br /> 既定値は**ReadWrite**です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるの[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]サポートの詳細については、「[高可用性、ディザスターリカバリーのサポートの SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。|  
|**アプリケーション名**|SSPROP_INIT_APPNAME|アプリケーションを識別する文字列。|  
|**自動翻訳**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" のシノニム。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 文字の変換を構成します。 認識できる値は "true" と "false" です。|  
|**接続のタイムアウト**|DBPROP_INIT_TIMEOUT|データ ソースの初期化が完了するのを待機する秒数。|  
|**[現在の言語]**|SSPROPT_INIT_CURRENTLANGUAGE|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 言語の名前。|  
|**データソース**|DBPROP_INIT_DATASOURCE|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。<br /><br /> 指定されなかった場合は、ローカル コンピューター上にある既定のインスタンスに接続します。<br /><br /> 有効なアドレス構文の詳細については、このトピックの「 **Server** ODBC キーワードの説明」を参照してください。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|使用するデータ型処理モードを指定します。 認識できる値は、プロバイダー データ型を示す "0" および SQL Server 2000 データ型を示す "80" です。|  
|**フェールオーバーパートナー**|SSPROP_INIT_FAILOVERPARTNER|データベース ミラーリングに使用するフェールオーバー サーバーの名前。|  
|**フェールオーバー パートナー SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|フェールオーバー パートナーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|**初期カタログ**|DBPROP_INIT_CATALOG|データベース名です。|  
|**初期ファイル名**|SSPROP_INIT_FILENAME|アタッチできるデータベースのプライマリ ファイルの名前 (完全なパス名を含む)。 **AttachDBFileName**を使用するには、プロバイダー文字列 database キーワードを使用してデータベース名も指定する必要があります。 データベースが以前にアタッチされていた場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] により再アタッチされることはありません (アタッチされたデータベースがその接続の既定のデータベースとして使用されます)。|  
|**統合セキュリティ**|DBPROP_AUTH_INTEGRATED|Windows 認証の値 "SSPI" を受け取ります。|  
|**MARS 接続**|SSPROP_INIT_MARSCONNECTION|その接続で MARS (複数のアクティブな結果セット) を有効または無効にします ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のサーバーの場合)。 認識できる値は "true" と "false" です。既定値は "false" です。|  
|**ネットワークアドレス**|SSPROP_INIT_NETWORKADDRESS|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのネットワーク アドレス。<br /><br /> 有効なアドレス構文の詳細については、このトピックの「 **address** ODBC キーワードの説明」を参照してください。|  
|**ネットワークライブラリ**|SSPROP_INIT_NETWORKLIBRARY|組織内の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続を確立するために使用するネットワーク ライブラリ。|  
|**パケットサイズ**|SSPROP_INIT_PACKETSIZE|ネットワーク パケットのサイズ。 既定値は 4096 です。|  
|**Password**|DBPROP_AUTH_PASSWORD|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン パスワード。|  
|**セキュリティ情報を保持する**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|文字列 "true" と "false" を値として受け取ります。 "false" の場合、データ ソース オブジェクトには機密の認証情報を保存できません。|  
|**Provider**||
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の場合は "SQLNCLI11"。|  
|**サーバー SPN**|SSPROP_INIT_SERVERSPN|サーバーの SPN。 既定値は空の文字列です。 空の文字列の場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はプロバイダーが生成した SPN を既定値として使用します。|  
|**サーバー証明書を信頼する**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|文字列 "true" と "false" を値として受け取ります。 既定値は "false" です。これはサーバー証明書が検証されることを示します。|  
|**データの暗号化を使用する**|SSPROP_INIT_ENCRYPT|データをネットワークに送信する前に暗号化するかどうかを指定します。 指定できる値は "true" と "false" です。 既定値は "false" です。|  
|**ユーザー ID**|DBPROP_AUTH_USERID|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログイン名。|  
|**[ワークステーション ID]**|SSPROP_INIT_WSID|ワークステーション識別子。|  
  
 **メモ**接続文字列では、"Old Password" プロパティによって SSPROP_AUTH_OLD_PASSWORD が設定されます。これは、プロバイダー文字列プロパティでは使用できない、現在の (有効期限切れの) パスワードです。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションの構築](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
