---
title: SQLSetConnectAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4acd7ce6a33665ce3d32e42328c906aaec3049
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910382"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLSetConnectAttr**接続の側面を制御する属性を設定します。  
  
> [!NOTE]
>  どのようなドライバー マネージャーは、ときに、マッピングするには、この関数、ODBC 3 の詳細については *.x*アプリケーションの操作は、ODBC 2 *.x*ドライバーを参照してください[後方のマッピング置換関数アプリケーションの互換性を](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *属性*  
 [入力]属性を設定すると、「コメントです」記載されています。  
  
 *ValuePtr*  
 [入力]関連付けられる値を指すポインター*属性*します。 値に応じて*属性*、 *ValuePtr*は、符号なし整数値にまたは null で終わる文字列を指します。 整数を入力に注意してください、*属性*引数を修正しない可能性があります、長さの詳細は、コメントのセクションを参照してください。  
  
 *StringLength*  
 [入力]場合*属性*ODBC で定義された属性と*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります **ValuePtr*します。 文字の文字列データでは、この引数は、文字列のバイト数を含める必要があります。  
  
 場合*属性*ODBC で定義された属性と*ValuePtr*整数*StringLength*は無視されます。  
  
 場合*属性*ドライバーの定義済みの属性では、アプリケーションを設定して属性をドライバー マネージャーの性質を示します、 *StringLength*引数。 *StringLength*次の値を持つことができます。  
  
-   場合*ValuePtr*文字の文字列へのポインターは*StringLength* SQL_NTS または文字列の長さです。  
  
-   場合*ValuePtr* 、SQL_LEN_BINARY_ATTR の結果を配置するアプリケーションが、バイナリ バッファーへのポインター (*長さ*) マクロで*StringLength*します。 これにより、負の値で*StringLength*します。  
  
-   場合*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは*StringLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合*ValuePtr* 、固定長の値を含む*StringLength* SQL_IS_INTEGER または SQL_IS_UINTEGER のいずれかを適切なは。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLSetConnectAttr** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_dbc として、*処理*の*ConnectionHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLSetConnectAttr** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
 ドライバーのオプションを設定する結果に関する情報を提供するには、sql_success_with_info が返さを返すことができます。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|ドライバーがで指定された値をサポートしていませんでした*ValuePtr*のような値を置き換えるとします。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08002|使用されている接続名|*属性*引数が SQL_ATTR_ODBC_CURSORS、およびドライバーが既にデータ ソースに接続されています。|  
|08003|接続は開いていません|(DM)、*属性*、開いている接続をするために必要な値が指定されましたが、 *ConnectionHandle*接続状態ではありませんでした。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|*属性*引数が SQL_ATTR_CURRENT_CATALOG、し、結果セットが保留されていました。|  
|25000|ローカル トランザクションの実行中の無効な操作|接続は、接続の SQL_ATTR_ENLIST_IN_DTC 属性を設定して、分散トランザクション (DTC) の接続に参加しているときにローカル トランザクションででした。<br /><br /> 接続は既に、DTC に参加しています。<br /><br /> 接続は分散トランザクションの接続に参加しているが、SQL_ATTR_AUTOCOMMIT を SQL_AUTOCOMMIT_OFF に設定して、ローカル トランザクションが開始します。|  
|3D000|無効なカタログ名|*属性*引数が SQL_CURRENT_CATALOG、および指定されたカタログ名が無効です。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *ConnectionHandle*します。 **SQLSetConnectAttr**関数が呼び出され、実行を完了する前に、 [SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)が呼び出されて、 *ConnectionHandle*をクリックし、**SQLSetConnectAttr**で関数が再度呼び出されました、 *ConnectionHandle*します。<br /><br /> また、 **SQLSetConnectAttr**関数が呼び出された、および前に、実行を完了**SQLCancelHandle**が呼び出されて、 *ConnectionHandle*別のスレッドからマルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|*属性*引数が文字列値を必要とする接続属性を識別し、 *ValuePtr*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された、 *StatementHandle*に関連付けられている、 *ConnectionHandle*ときに実行されていると**SQLSetConnectAttr**が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *ConnectionHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に関連付けられているステートメント ハンドルのいずれかが呼び出された、 *ConnectionHandle* SQL_PARAM_DATA_AVAILABLE が返されます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle*に関連付けられている、 *ConnectionHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。<br /><br /> (DM) **SQLBrowseConnect**に対して呼び出された、 *ConnectionHandle* SQL_NEED_DATA が返されます。 この関数が呼び出されました**SQLBrowseConnect** SQL_SUCCESS_WITH_INFO または SQL_SUCCESS が返されます。|  
|HY011|属性を設定できません。|*属性*引数は、SQL_ATTR_TXN_ISOLATION と、トランザクションが開きます。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY024|無効な属性値|指定した*属性*値、無効な値に指定されました*ValuePtr*します。 (ドライバー マネージャーは、接続とステートメント属性 SQL_ATTR_ACCESS_MODE または SQL_ATTR_ASYNC_ENABLE などの値の個別セットをそのまま使用するには、この SQLSTATE を返します。 ドライバーの他のすべての接続とステートメント属性で指定された値を確認する必要があります*ValuePtr*)。<br /><br /> *属性*引数が SQL_ATTR_TRACEFILE または SQL_ATTR_TRANSLATE_LIB、および*ValuePtr*が空の文字列。|  
|HY090|文字列またはバッファーの長さが無効です。|*(DM) \*ValuePtr*文字の文字列と*StringLength*引数は SQL_NTS が 0 未満でした。|  
|HY092|無効な属性またはオプション識別子|引数に指定された値 (DM)*属性*ODBC ドライバーでサポートされているのバージョンには無効です。<br /><br /> 引数に指定された値 (DM)*属性*読み取り専用属性されました。|  
|HY114|ドライバーは接続レベルの非同期関数の実行をサポートしていません|(DM) アプリケーションは、非同期接続の操作をサポートしていないドライバーの SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE を使用した非同期関数の実行を有効にしようとしました。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HY121|同時に、カーソル ライブラリとドライバー対応のプールが有効にすることはできません。|詳細については、次を参照してください。[ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)します。|  
|HYC00|省略可能な機能が実装されていません|引数が指定された値*属性*が有効な ODBC 接続、または ODBC のバージョンのステートメント属性は、ドライバーによってサポートされていますが、ドライバーによってサポートされていませんでした。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *ConnectionHandle*関数をサポートしていません。|  
|IM009|トランスレーター DLL を読み込むことができません。|ドライバーは、変換の接続に指定された DLL を読み込めませんでした。 このエラーを返すことが場合にのみ*属性*SQL_ATTR_TRANSLATE_LIB です。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
|S1118|ドライバーが非同期通知をサポートしていません|(接続された) 後に、SQL_ATTR_ASYNC_DBC_EVENT が設定されましたが、非同期の通知は、ドライバーによってサポートされていません。|  
  
 ときに*属性*ステートメント属性は、 **SQLSetConnectAttr**によって返される任意の SQLSTATEs を返すことができます**SQLSetStmtAttr**します。  
  
## <a name="comments"></a>コメント  
 接続属性については、次を参照してください。[接続属性](../../../odbc/reference/develop-app/connection-attributes.md)します。  
  
 このセクションの後半の表で現在定義されている属性とが導入されました ODBC のバージョンが表示されます。複数の属性のさまざまなデータ ソースを活用するために定義することが期待されます。 属性の範囲は ODBC; によって予約されていますドライバー開発者向けには、Open Group から個々 のドライバーの使用するための値を予約する必要があります。  
  
> [!NOTE]
>  ステートメント属性を呼び出すことで、接続レベルで設定できる**SQLSetConnectAttr** ODBC 3 では非推奨 *.x*します。 ODBC 3 *.x*アプリケーションは接続レベルでステートメント属性を設定しない必要があります。 ODBC 3 *.x*で、これは、接続属性とステートメント属性の両方を指定できます、SQL_ATTR_METADATA_ID および SQL_ATTR_ASYNC_ENABLE 属性を除く、接続レベルでのステートメント属性を設定することはできません接続レベルまたはステートメント レベルのいずれかに設定します。  
> 
>  ODBC 3 *.x* ODBC 2 協力する場合、ドライバーはこの機能をサポートのみ必要 *.x* ODBC 2 を設定するアプリケーションに *.x*接続レベルでステートメントのオプション。 詳細については、次を参照してください[SQLSetConnectOption のマッピング](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)で付録 g:。旧バージョンとの互換性のためのガイドラインをドライバーです。  
  
 アプリケーションが呼び出すことができます**SQLSetConnectAttr**接続の割り当て、解放までの間、いつでもできます。 まで、接続用にアプリケーションによって設定が正常に接続し、ステートメントのすべての属性が永続化**SQLFreeHandle**が接続で呼び出されます。 たとえば、アプリケーションを呼び出す**SQLSetConnectAttr**をデータ ソースに接続する前に、属性が解決しない場合でも**SQLSetConnectAttr**アプリケーションに接続するときに、ドライバーが失敗した、データ ソース。アプリケーションでは、ドライバー固有の属性を設定、アプリケーションが接続で別のドライバーに接続する場合でも、属性が永続化します。  
  
 接続が確立されています。 前にのみ、接続属性を設定することができます。他のユーザーは、接続が確立した後にのみ設定できます。 次の表では前に、または接続が確立した後に設定する必要があるこれらの接続属性を示します。 *いずれか*前に、または後の接続属性を設定できることを示します。  
  
|属性|接続の前後に設定しますか。|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|接続前/接続後|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|接続前/接続後|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|接続前/接続後|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|接続前/接続後|  
|SQL_ATTR_AUTOCOMMIT|[5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|接続前/接続後|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After|  
|SQL_ATTR_ENLIST_IN_DTC|After|  
|SQL_ATTR_LOGIN_TIMEOUT|[指定日付より前]|  
|SQL_ATTR_METADATA_ID|接続前/接続後|  
|SQL_ATTR_ODBC_CURSORS|[指定日付より前]|  
|SQL_ATTR_PACKET_SIZE|[指定日付より前]|  
|SQL_ATTR_QUIET_MODE|接続前/接続後|  
|SQL_ATTR_TRACE|接続前/接続後|  
|SQL_ATTR_TRACEFILE|接続前/接続後|  
|SQL_ATTR_TRANSLATE_LIB|After|  
|SQL_ATTR_TRANSLATE_OPTION|After|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [前に、または、ドライバーによって、接続した後は、1] SQL_ATTR_ACCESS_MODE と SQL_ATTR_CURRENT_CATALOG を設定できます。 ただし、相互運用可能なアプリケーション設定に接続する前に一部のドライバーが接続した後は、これらの変更をサポートしていないためです。  
  
 [アクティブなステートメントがある前に、2] SQL_ATTR_ASYNC_ENABLE を設定する必要があります。  
  
 [3] SQL_ATTR_TXN_ISOLATION は、接続で開いているトランザクションがない場合にのみ設定できます。 いくつかの接続属性で指定された値をデータ ソースがサポートしていない場合のような値の置換をサポートして\* *ValuePtr*します。 このような場合、ドライバーは SQL_SUCCESS_WITH_INFO と SQLSTATE 01S02 を返します (オプションの値が変更されました)。 たとえば場合、*属性*SQL_ATTR_PACKET_SIZE と\* *ValuePtr*最大パケット サイズを超える場合、ドライバーには、最大サイズが置換されます。 置き換えられた値を決定するアプリケーションを呼び出す**SQLGetConnectAttr**します。  
  
 [呼び出し中にドライバーが読み込まれるときに 4] SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE は接続が開いて前に設定されている場合、ドライバー マネージャーでは、ドライバーの属性を設定は**SQLBrowseConnect**、 **SQLConnect**、または**SQLDriverConnect**します。 呼び出す前に**SQLBrowseConnect**、 **SQLConnect**、または**SQLDriverConnect**、ドライバー マネージャーに接続するには、どのドライバーが把握していないとが把握していないかどうか、ドライバーは、非同期接続の操作をサポートします。 そのため、ドライバー マネージャーでは、常に関係なく SQL_SUCCESS を返します。 ドライバーは、非同期接続操作への呼び出しをサポートしていません場合、が、 **SQLBrowseConnect**、 **SQLConnect**、または**SQLDriverConnect**は失敗します。  
  
 [SQL_ATTR_AUTOCOMMIT は FALSE に設定されているときに 5]、アプリケーションは任意の API にトランザクションの一貫性を確保する SQL_ERROR が返された場合に SQLEndTran(SQL_ROLLBACK) を呼び出す必要があります。  
  
 情報設定の形式、 \* *ValuePtr*バッファーが、指定した依存*属性*します。 **SQLSetConnectAttr**は 2 つの異なる形式のいずれかの属性情報を受け入れます。 null で終わる文字列または整数値。 それぞれの形式は、属性の説明に記録されます。 文字列の指す、 *ValuePtr*の引数**SQLSetConnectAttr**長さ*StringLength*バイト。  
  
 *StringLength*引数は、長さが、属性によって定義されている場合は、ODBC 2 で導入されたすべての属性の場合と同様、無視されます *.x*以前のバージョン。  
  
|*属性*|*ValuePtr*内容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 値。 SQL_MODE_READ_ONLY は、ドライバー、またはデータ ソース、接続を更新する SQL ステートメントをサポートする必要はありませんが、インジケーターとして使用されます。 このモードは、ロック戦略、トランザクションの管理、またはドライバーまたはデータ ソースに適したその他の領域を最適化するために使用できます。 このようなステートメントからデータ ソースに送信されるようにするのには、ドライバーは必要はありません。 データ ソースが読み取り専用、読み取り専用の接続中に SQL ステートメントを処理するように求められたら、ドライバーの動作では、実装定義されます。 SQL_MODE_READ_WRITE では、既定値です。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|イベント ハンドルである SQLPOINTER 値。<br /><br /> 呼び出して非同期関数の完了の通知が有効になっている**SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 属性イベント ハンドルを指定するとします。 **注:** カーソル ライブラリでは、通知方法はサポートされていません。 アプリケーションと通知方法を有効にすると、SQLSetConnectAttr を使用してカーソル ライブラリを有効にするとエラー メッセージが表示されます。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|またはの非同期実行を無効にする SQLUINTEGER 値は、接続ハンドルで関数を選択します。 詳細については、次を参照してください。[非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)します。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 指定した接続に関連する関数の非同期操作を有効にします。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = 指定した接続に関連する関数の非同期操作を (既定値) の無効化します。<br /><br /> 設定 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE は同期では常に (つまり、返さない SQL_STILL_EXECUTING)。<br /><br /> SQL_ATTR_ASYNC_ENABLE では、ステートメントの操作の非同期実行が有効になります。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Context 構造体を指す SQLPOINTER 値。<br /><br /> ドライバー マネージャーがドライバーを呼び出すことができますのみ**SQLSetStmtAttr**この属性を持つ関数です。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Context 構造体を指す SQLPOINTER 値。<br /><br /> ドライバー マネージャーがドライバーを呼び出すことができますのみ**SQLSetStmtAttr**この属性を持つ関数です。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|指定した接続でステートメントを持つ関数が呼び出されたかどうかを示す sqlulen です値は非同期的に実行されます。<br /><br /> SQL_ASYNC_ENABLE_OFF ステートメント操作 (既定値) を無効にする接続レベルの非同期実行のサポートを = です。<br /><br /> SQL_ASYNC_ENABLE_ON = ステートメント操作のための接続レベルの非同期実行のサポートを有効にします。<br /><br /> この属性ができるかどうかを設定**SQLGetInfo** SQL_AM_CONNECTION または SQL_AM_STATEMENT SQL_ASYNC_MODE 情報を使用して型を返します。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|読み取り専用 SQLUINTEGER 値を指定するかどうかを呼び出した後、IPD の自動作成**SQLPrepare**はサポートされています。<br /><br /> SQL_TRUE 呼び出しの後に、IPD の自動作成を = **SQLPrepare**ドライバーでサポートされています。<br /><br /> SQL_FALSE を呼び出した後、IPD の自動作成を = **SQLPrepare**はドライバーによってサポートされていません。 準備されたステートメントをサポートしていないサーバーは、IPD を自動的に設定できません。<br /><br /> SQL_TRUE は SQL_ATTR_AUTO_IPD 接続属性の返された場合、IPD の自動作成を有効または無効にする SQL_ATTR_ENABLE_AUTO_IPD ステートメント属性を設定できます。 SQL_ATTR_AUTO_IPD が SQL_FALSE の場合は、SQL_ATTR_ENABLE_AUTO_IPD が SQL_TRUE に設定できません。 SQL_ATTR_ENABLE_AUTO_IPD の既定値は SQL_ATTR_AUTO_IPD の値にします。<br /><br /> この接続属性によって返される**SQLGetConnectAttr**設定することはできませんが、 **SQLSetConnectAttr**します。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|自動コミット、または手動コミット モードを使用するかどうかを指定する SQLUINTEGER 値:<br /><br /> SQL_AUTOCOMMIT_OFF = ドライバー手動コミット モードを使用して、アプリケーションのコミットまたはとのトランザクションをロールバックする必要があります明示的に**SQLEndTran**します。<br /><br /> Sql_autocommit_on の状態、ドライバーは自動コミット モードを = です。 各ステートメントは、それが実行された直後後に努めています。 既定値です。 手動コミット モードから自動コミット モードに変更する sql_autocommit_on の状態を SQL_ATTR_AUTOCOMMIT に設定、接続で開かれたトランザクションがコミットされます。<br /><br /> 詳細については、次を参照してください。[コミット モード](../../../odbc/reference/develop-app/commit-mode.md)します。 **重要:** 一部のデータ ソース アクセス プランを削除し、接続、ステートメントがコミットされます。 毎回ですべてのステートメントのカーソルを閉じる自動コミット モードには、これを nonquery の各ステートメントが実行された後、またはクエリにカーソルが閉じられたときに発生する可能性があります。 詳細についてで SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類を参照してください。 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)と[カーソルと準備されたステートメントでトランザクションの効果](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)します。 <br /><br /> バッチが自動コミット モードで実行されると、2 つのことが可能です。 バッチ全体を autocommitable 単位として扱うことができます、またはバッチ内の各ステートメントは、autocommitable 単位として扱われます。 特定のデータ ソースは、これら両方の動作をサポートできるし、どちらか一方を選択する方法を提供することがあります。 バッチが autocommitable 単位として扱われるかどうか、またはバッチ内で個々 のステートメント autocommitable ドライバー定義されていることをお勧めします。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|接続の状態を示す読み取り専用 SQLUINTEGER 値。 場合は SQL_CD_TRUE、接続が失われました。 場合は SQL_CD_FALSE、接続は、アクティブなままです。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|アプリケーションに返す前に完了への接続上ですべての要求を待機する秒数に対応する SQLUINTEGER 値。 ドライバーは SQLSTATE HYT00 を返す必要があります (タイムアウトの期限切れ) いつでもクエリの実行またはログインに関連付けられていない状況でタイムアウトすることであること。<br /><br /> 場合*ValuePtr*は 0 (既定値) に等しいか、タイムアウトはありません。|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|データ ソースで使用されるカタログの名前を含む文字列。 たとえば、SQL Server で、カタログは、データベース、ため、ドライバーの送信、**使用**_データベース_ステートメント、データ ソースをどこ*データベース*で指定したデータベース\* *ValuePtr*します。 1 階層のドライバーの場合、カタログがあるディレクトリ、ためドライバーで指定したディレクトリに、現在のディレクトリが変更された **ValuePtr*します。|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|設定するための SQLPOINTER 値戻す、DBC への接続情報トークン時に処理[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)の (\**pRating*) パラメーターは 100 に等しくありません。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN はセット専用です。 使用することはできません**SQLGetConnectAttr**または**SQLGetConnectOption**この値を取得します。 ドライバー マネージャーの**SQLSetConnectAttr**アプリケーションはこの属性を設定する必要がありますいないため、SQL_ATTR_DBC_INFO_TOKEN を受け入れません。<br /><br /> ドライバーは SQL_ERROR を返します SQL_ATTR_DBC_INFO_TOKEN を設定した後、プールから取得した接続が解放されます。 ドライバー マネージャーは、プールから別の接続を取得するから再試行してください。 参照してください[ODBC ドライバーで接続プールの認識を開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)詳細についてはします。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Microsoft コンポーネント サービスによって調整される分散トランザクションで ODBC ドライバーを使用するかどうかを示す SQLPOINTER 値。<br /><br /> DTC OLE トランザクションを指定するオブジェクト、接続の DTC の関連付けを終了するには、SQL Server、または sql_dtc_done を指定してエクスポートするトランザクションを渡します。<br /><br /> クライアントは、MS DTC トランザクションを開始し、トランザクションを表す MS DTC トランザクション オブジェクトを作成する Microsoft 分散トランザクション コーディネーター (MS DTC) OLE itransactiondispenser::begintransaction メソッドを呼び出します。 次に、アプリケーションは、ODBC 接続とトランザクション オブジェクトを関連付ける SQL_ATTR_ENLIST_IN_DTC オプションを使用して SQLSetConnectAttr を呼び出します。 関連のあるすべてのデータベース操作は、MS DTC トランザクションで保護されます。 アプリケーションでは、sql_dtc_done を指定して、接続の DTC の関連付けを終了すると、SQLSetConnectAttr を呼び出します。 詳細については、MS DTC のドキュメントを参照してください。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|ログイン要求をアプリケーションに返す前に完了するまで待機する秒数に対応する SQLUINTEGER 値。 既定ではドライバーによって異なります。 場合*ValuePtr* 0 にも、タイムアウトが無効で、接続試行は無期限に待機します。<br /><br /> ドライバーがその値に置き換えられ、SQLSTATE 01S02 を返します、指定したタイムアウトがデータ ソースの最大ログイン タイムアウトを超えた場合 (オプションの値が変更されました)。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|カタログ関数の文字列引数の処理方法を決定する SQLUINTEGER 値。<br /><br /> 場合は SQL_TRUE、カタログ関数の文字列引数は、識別子として扱われます。 大文字と小文字は大きくありません。 規格文字列の場合、ドライバーは、末尾のスペースを削除および文字列が大文字に折りたたまれません。 区切られた文字列の場合、ドライバーは、先頭または末尾のスペースを削除し、区切り記号の間は文字どおりは。 返しますが SQL_ERROR と SQLSTATE HY009 null ポインターにこれらの引数のいずれかに設定されている場合 (null ポインターの無効な使用)。<br /><br /> 場合は sql_false になります、カタログ関数の文字列引数は、識別子としては扱われません。 大文字と小文字は重要です。 か、含めることができます、文字列の検索パターンまたはそうでない引数に応じて。<br /><br /> 既定値は、sql_false になります。<br /><br /> *TableType*の引数**SQLTables**、この属性を受けませんが、値の一覧を受け取ります。<br /><br /> SQL_ATTR_METADATA_ID をステートメント レベルの設定もできます。 (これは、ステートメント属性になっている唯一の接続属性です)。<br /><br /> 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|ドライバー マネージャーで、ODBC カーソル ライブラリを使用する方法を指定する sqlulen です値:<br /><br /> SQL_CUR_USE_IF_NEEDED 必要な場合にのみ、ODBC カーソル ライブラリで、ドライバー マネージャーの使用を = です。 ドライバーの SQL_FETCH_PRIOR オプションをサポートしている場合**SQLFetchScroll**、ドライバー マネージャーがドライバーのスクロール機能を使用します。 それ以外の場合、ODBC カーソル ライブラリを使用します。<br /><br /> SQL_CUR_USE_ODBC、ドライバー マネージャーは ODBC カーソル ライブラリを = です。<br /><br /> SQL_CUR_USE_DRIVER ドライバーのスクロール機能、ドライバー マネージャーの使用を = です。 これが既定の設定です。<br /><br /> ODBC カーソル ライブラリの詳細については、次を参照してください[付録 f:。ODBC カーソル ライブラリ](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)します。 **警告:** カーソル ライブラリは、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|ネットワーク パケット サイズをバイト単位で示す SQLUINTEGER 値。 **注:** 多くのデータ ソースは、このオプションをサポートしてまたはのみできる戻り値が未設定ネットワーク パケット サイズ。 <br /><br /> ドライバーがその値に置き換えられ、SQLSTATE 01S02 を返します、指定したサイズ、最大パケット サイズを超えていますまたは最小パケットのサイズよりも小さい、(オプションの値が変更されました)。<br /><br /> アプリケーションは、接続が既に確立した後、パケット サイズを設定、ドライバーは SQLSTATE HY011 を返します (属性はここで設定することはできません)。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|ウィンドウ ハンドル (HWND)。<br /><br /> ウィンドウ ハンドルが null ポインターの場合、ドライバーはすべてのダイアログ ボックスが表示されません。<br /><br /> ウィンドウ ハンドルが null ポインターではない場合、アプリケーションの親ウィンドウ ハンドルが必要です。 既定値です。 ドライバーでは、このハンドルを使用して、ダイアログ ボックスを表示します。 **注:** によって表示されるダイアログ ボックスに、SQL_ATTR_QUIET_MODE 接続属性は適用されません**SQLDriverConnect**します。|  
|SQL_ATTR_TRACE (ODBC 1.0)|ドライバー マネージャーは、トレースを実行するかどうかを示す SQLUINTEGER 値:<br /><br /> SQL_OPT_TRACE_OFF off (既定) のトレースを =<br /><br /> SQL_OPT_TRACE_ON でトレースを =<br /><br /> トレースが on の場合は、ドライバー マネージャーは、トレース ファイルに各 ODBC 関数呼び出しを書き込みます。 **注:** トレースが on の場合、ドライバー マネージャーは SQLSTATE IM013 を返すことができます (トレース ファイルのエラー) 任意の関数から。 <br /><br /> アプリケーションでは、SQL_ATTR_TRACEFILE オプションを使用してトレース ファイルを指定します。 ファイルが既に存在する場合、ドライバー マネージャーは、ファイルに追加します。 それ以外の場合、ファイルを作成します。 トレースが有効で、トレース ファイルが指定されていない場合は、ドライバー マネージャーは、SQL ファイルに書き込みます。ルート ディレクトリにログインします。<br /><br /> アプリケーションは、変数を設定できます**ODBCSharedTraceFlag**動的にトレースを有効にします。 現在実行されているすべての ODBC アプリケーションでは、トレースは有効ですし。 場合は、アプリケーションは、トレースをオフに、そのアプリケーションでのみオフにされています。<br /><br /> 場合、**トレース**アプリケーションを呼び出すと、システム情報のキーワードが 1 に設定されて**SQLAllocHandle**で、 *HandleType* sql_handle_env としてのすべてのトレースが有効処理します。 呼び出したアプリケーションに対してのみ有効になっている**SQLAllocHandle**します。<br /><br /> 呼び出す**SQLSetConnectAttr**で、*属性*SQL_ATTR_TRACE のいる必要はありません、 *ConnectionHandle*引数が有効である場合、SQL_ERROR を返しませんが、*ConnectionHandle*は NULL です。 この属性は、すべての接続に適用されます。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|トレース ファイルの名前を含む null で終わる文字列。<br /><br /> SQL_ATTR_TRACEFILE 属性の既定値が指定されています、 **TraceFile**システム情報のキーワード。 詳細については、次を参照してください。 [ODBC サブキー](../../../odbc/reference/install/odbc-subkey.md)します。<br /><br /> 呼び出す**SQLSetConnectAttr**で、*属性*SQL_ATTR TRACEFILE は必要ありません、 *ConnectionHandle*引数を有効にして、SQL_ERROR が返されません場合*ConnectionHandle*が無効です。 この属性は、すべての接続に適用されます。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|関数が含まれるライブラリの名前を含む null で終わる文字列**SQLDriverToDataSource**と**SQLDataSourceToDriver**などのタスクを実行するドライバーにアクセスします。文字セットを変換します。 このオプションがあります、ドライバーがデータ ソースに接続されているかどうかにのみ指定します。 この属性の設定は、接続間で保持されます。 データの翻訳の詳細については、次を参照してください。[翻訳の Dll](../../../odbc/reference/develop-app/translation-dlls.md)と[DLL 関数の参照を翻訳](../../../odbc/reference/syntax/translation-dll-api-reference.md)します。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|トランスレーター DLL に渡される 32 ビット フラグの値。 この属性を指定できます、ドライバーがデータ ソースに接続されているかどうかにのみ指定します。 データを変換する方法の詳細については、次を参照してください。[翻訳の Dll](../../../odbc/reference/develop-app/translation-dlls.md)します。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|現在の接続のトランザクション分離レベルを設定する 32 ビットのビットマスク。 アプリケーションを呼び出す必要があります**SQLEndTran**コミットまたは接続には、呼び出す前にすべての開いているトランザクションをロールバックする**SQLSetConnectAttr**このオプションを使用します。<br /><br /> 有効な値*ValuePtr*呼び出すことによって決まりますできます**SQLGetInfo**で*情報の種類*SQL_TXN_ISOLATION_OPTIONS と等しい。<br /><br /> トランザクション分離レベルについてで SQL_DEFAULT_TXN_ISOLATION 情報の種類の説明を参照してください。 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)と[トランザクション分離レベル](../../../odbc/reference/develop-app/transaction-isolation-levels.md)します。|  
  
 [1] にはこれらの関数は、記述子が、実装の記述子アプリケーション記述子ではない場合にのみ、非同期的に呼び出すことができます。  
  
## <a name="code-example"></a>コード例  
 参照してください[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当てください。|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
