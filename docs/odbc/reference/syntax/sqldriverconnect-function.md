---
title: SQLDriverConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9528280514be2eb2424b15a39ded3206aaca112f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104706"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLDriverConnect**に代わる**SQLConnect**します。 3 個の引数よりも多くの接続情報を必要とするデータ ソースがサポートしている**SQLConnect**、すべての接続情報、およびシステムで定義されていないデータ ソースのユーザー入力を求めるダイアログ ボックス情報。  
  
 **SQLDriverConnect**次の接続属性を提供します。  
  
-   データ ソースでデータ ソース名、1 つまたは複数のユーザー Id、1 つまたは複数のパスワード、および必要なその他の情報を含む接続文字列を使用して接続を確立します。  
  
-   部分的な接続文字列または追加情報はありません。 を使用して接続を確立します。この場合、ドライバー マネージャーとドライバー求めることもできますそれぞれの接続情報のユーザー。  
  
-   システム情報で定義されていないデータ ソースへの接続を確立します。 アプリケーションは部分的な接続文字列を提供している場合、ドライバーは接続情報のユーザーを求めることもできます。  
  
-   .Dsn ファイル内の情報から構築された接続文字列を使用してデータ ソースへの接続を確立します。  
  
 接続が確立されると、 **SQLDriverConnect**完全な接続文字列を返します。 アプリケーションでは、後続の接続要求に対して、この文字列を使用できます。 詳細については、次を参照してください。 [SQLDriverConnect による接続](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *WindowHandle*  
 [入力]ウィンドウ ハンドル。 該当する場合、アプリケーションは、親ウィンドウのハンドルを渡すことができますか、どちらの場合は null ポインターのウィンドウ ハンドルは、該当するはまたは**SQLDriverConnect**はダイアログ ボックスが表示されません。  
  
 *InConnectionString*  
 [入力]完全な接続文字列 (「コメント」内の構文を参照)、部分的な接続文字列、または空の文字列。  
  
 *StringLength1*  
 [入力]長さ **InConnectionString*、文字の場合、文字列は ANSI または DBCS 文字列が Unicode、またはバイトの場合。  
  
 *OutConnectionString*  
 [出力]完全な接続文字列を格納するバッファーへのポインター。 ターゲット データ ソースへの接続に成功は、このバッファーには、完全な接続文字列が含まれています。 アプリケーションは、このバッファーには少なくとも 1,024 文字を割り当てる必要があります。  
  
 場合*OutConnectionString*が null の場合、 *StringLength2Ptr*は文字 (文字データの null 終端文字を除く) の合計数を返しますが、バッファーに返される使用可能な指す*OutConnectionString*します。  
  
 *BufferLength*  
 [入力]長さ、**OutConnectionString*文字のバッファー。  
  
 *StringLength2Ptr*  
 [出力]文字 (null 終了文字を除く) の合計数を返すバッファーへのポインターで返される使用可能な\* *OutConnectionString*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength*、内の接続文字列を完了した\* *OutConnectionString*に切り捨てられます*BufferLength* null 終了文字の長さマイナスです。  
  
 *DriverCompletion*  
 [入力]ドライバー マネージャーまたはドライバーの詳細な接続情報を求める必要があるかどうかを示すフラグ。  
  
 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、sql_driver_complete_required の場合、または SQL_DRIVER_NOPROMPT します。  
  
 (詳細については、「コメントです」を参照してください)  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLDriverConnect** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します、関連付けられた SQLSTATE 値を呼び出すことによって取得される可能性があります**SQLGetDiagRec**で、 *fHandleType*sql_handle_dbc としての*hHandle*の*ConnectionHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLDriverConnect** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *OutConnectionString*容量が不足すると、全体の接続文字列を返すため、接続文字列が切り捨てられました。 切り詰められていない接続文字列の長さが返される **StringLength2Ptr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S00|無効な接続文字列の属性|接続文字列で、無効な属性のキーワードが指定された (*InConnectionString*) が、ドライバーがデータ ソースに接続できませんでした。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|ドライバーでは、指定した値によって示されるはサポートされていませんでした、 *ValuePtr*引数**SQLSetConnectAttr**のような値を置き換えるとします。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S08|ファイル DSN の保存エラー|文字列 *\*InConnectionString*に含まれている、 **FILEDSN**キーワードが .dsn ファイルは保存されませんでした。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S09|無効なキーワード|(DM) 内の文字列 *\*InConnectionString*に含まれている、 **SAVEFILE**キーワードがない、**ドライバー**または**FILEDSN**キーワード。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08001|クライアント接続を確立できません。|ドライバーは、データ ソースとの接続を確立できませんでした。|  
|08002|使用されている接続名|(DM)、指定した*ConnectionHandle*データ ソースとの接続を確立するために既に使用されていた接続が開かれたままとします。|  
|08004|サーバー接続を拒否しました|データ ソースには、実装定義上の理由から、接続の確立が拒否されます。|  
|08S01|通信リンク エラー|前に、ドライバーとの接続に、ドライバーをしようとしましたデータ ソース間の通信リンクが失敗しました、 **SQLDriverConnect**関数が完了した処理します。|  
|28000|無効な認証指定|ユーザー id、承認文字列またはその両方の接続文字列で指定されている (*InConnectionString*)、データ ソースで定義されている制約に違反します。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*szMessageText*バッファーは、エラーとその原因について説明します。|  
|HY000|一般的なエラー:無効なファイル dsn|(DM) 内の文字列 **InConnectionString* FILEDSN キーワードが含まれているが、.dsn ファイルの名前が見つかりませんでした。|  
|HY000|一般的なエラー:ファイル バッファーを作成できません。|(DM) 内の文字列 **InConnectionString* FILEDSN キーワードが含まれているが、.dsn ファイルを読み取れませんでした。|  
|HY001|メモリの割り当てエラー|ドライバー マネージャーは実行または完了をサポートするために必要なメモリを割り当てることができませんが、 **SQLDriverConnect**関数。<br /><br /> ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *ConnectionHandle*します。 関数が呼び出された、および実行を完了する前に、 [SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)が呼び出されて、 *ConnectionHandle*をクリックし、 **SQLDriverConnect**関数が再度呼び出されました、 *ConnectionHandle*します。<br /><br /> また、 **SQLDriverConnect**関数が呼び出された、および前に、実行を完了**SQLCancelHandle**が呼び出されて、 *ConnectionHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) 非同期的に実行中の別の関数 (いない**SQLDriverConnect**) に対して呼び出された、 *ConnectionHandle*ときに実行されていると、 **SQLDriverConnect**関数が呼び出されました。|  
|HY013|メモリ管理エラー|**SQLDriverConnect**基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*StringLength1*が 0 未満、SQL_NTS に等しいでした。<br /><br /> 引数に指定された (DM) 値*BufferLength*が 0 未満でした。|  
|HY092|無効な属性またはオプション識別子|(DM)、 *DriverCompletion*引数が SQL_DRIVER_PROMPT、および*WindowHandle*引数が null ポインター。|  
|HY110|ドライバーが正しく完了|引数に指定された値 (DM) *DriverCompletion*が SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、sql_driver_complete_required の場合、または SQL_DRIVER_NOPROMPT と等しくありません。<br /><br /> (DM) 接続プールが有効になっているし、引数に指定された値*DriverCompletion*を SQL_DRIVER_NOPROMPT に等しいでした。|  
|HYC00|省略可能な機能が実装されていません|ドライバーは ODBC の動作をアプリケーションが要求したバージョンをサポートしていません。|  
|HYT00|タイムアウトが発生しました|完了したデータ ソースに接続する前に、ログイン タイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM)、指定されたデータ ソース名に対応するドライバーは、関数をサポートしていません。|  
|IM002|データ ソースが見つかりませんと指定された既定のドライバー|(DM)、データ ソースの接続文字列で指定された名前 (*InConnectionString*)、システム情報には見つかりませんでしたし、既定のドライバーの仕様はありませんでした。<br /><br /> (DM) システム情報 ODBC データ ソースと既定のドライバー情報が見つかりませんでした。|  
|IM003|指定されたドライバーを読み込むことができませんでした。|(DM)、ドライバーは、システムの情報でデータ ソースの仕様に記載またはで指定された、**ドライバー**キーワードが見つからなかったか、何らかの理由でアンロードできませんでした。|  
|IM004|ドライバーの**SQLAllocHandle**を sql_handle_env としてできませんでした|(DM) 中に**SQLDriverConnect**、ドライバー マネージャーという、ドライバーの**SQLAllocHandle**関数と、 *fHandleType* sql_handle_env としてとドライバーの次のように返されます、。エラーがあります。|  
|IM005|ドライバーの**SQLAllocHandle**を sql_handle_dbc としてできませんでした。|(DM) 中に**SQLDriverConnect**、ドライバー マネージャーという、ドライバーの**SQLAllocHandle**関数と、 *fHandleType*ドライバー sql_handle_dbc としての次のように返されます、。エラーがあります。|  
|IM006|ドライバーの**SQLSetConnectAttr**できませんでした|(DM) 中に**SQLDriverConnect**、ドライバー マネージャーという、ドライバーの**SQLSetConnectAttr**関数と、ドライバーにエラーが返されます。|  
|IM007|なしのデータ ソースまたはドライバーを指定します。ダイアログを表示できません。|データ ソースの名前またはドライバーが指定されていない接続文字列と*DriverCompletion* SQL_DRIVER_NOPROMPT でした。|  
|IM008|ダイアログに失敗しました|ドライバーは、そのログイン ダイアログ ボックスを表示しようとし、失敗しました。<br /><br /> *WindowHandle*が null ポインターの場合と*DriverCompletion* SQL_DRIVER_NO_PROMPT でした。|  
|IM009|トランスレーター DLL を読み込むことができません。|ドライバーは、翻訳または接続のデータ ソースの指定された DLL を読み込めませんでした。|  
|IM010|データ ソース名が長すぎます|(DM) DSN キーワードの属性の値は、SQL_MAX_DSN_LENGTH 文字を超えていました。|  
|IM011|ドライバー名が長すぎます|(DM) の場合は、属性値、**ドライバー**キーワードが 255 文字より長かった。|  
|IM012|DRIVER キーワードの構文エラー|(DM) キーワードと値のペア、**ドライバー**キーワードには、構文エラーが含まれています。<br /><br /> (DM) 内の文字列 *\*InConnectionString*に含まれている、 **FILEDSN**キーワードが .dsn ファイルが含まれていない、**ドライバー**キーワードまたは**DSN**キーワード。|  
|IM014|指定された DSN には、ドライバーとアプリケーション間のアーキテクチャの不一致が含まれています。|64 ビット ドライバー; に接続する DSN を使用する (DM) 32 ビット アプリケーションまたはその逆です。|  
|IM015|ドライバーの SQLDriverConnect SQL_HANDLE_DBC_INFO_HANDLE に失敗しました|ドライバーでは、SQL_ERROR が返された場合は、ドライバー マネージャーは、アプリケーションに SQL_ERROR を返し、接続は失敗します。<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN の詳細については、次を参照してください。 [ODBC ドライバーで接続プールの認識を開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)します。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
|S1118|ドライバーが非同期通知をサポートしていません|ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT または SQL_ATTR_ASYNC_DBC_RETCODE_PTR を設定することはできません。|  
  
## <a name="comments"></a>コメント  
 接続文字列では、次の構文があります。  
  
 *接続文字列*:: =*空の文字列*[;]&#124; *属性*[;]&#124; *属性*;*接続文字列*  
  
 *空の文字列*:: =*属性*:: =*属性キーワード*=*属性値*&#124;ドライバー = [{}]*属性値*[}]  
  
 *属性キーワード*:: = DSN &#124; UID &#124; PWD &#124; *ドライバー-定義の属性-キーワード*  
  
 *属性値*:: =*文字の文字列*  
  
 *ドライバーの定義の属性-キーワード*:: =*識別子*  
  
 場所*文字列*0 個以上の文字。*識別子*が 1 つ以上の文字。*属性キーワード*; 大文字小文字を区別することはありません*属性値*可能性があります。 大文字小文字を区別しの値、 **DSN**キーワードは空白ののみで構成されていません。  
  
 接続文字列と初期化ファイルの文法、キーワード、および属性の値の文字が含まれているため **:operator[]{}()、;?\*=! @** で囲まれていない中かっこを避ける必要があります。 値、 **DSN**キーワードが空白ののみで構成されていることはできませんし、先頭の空白を含めることはできません。 によりシステム情報の文章では、キーワード、およびデータ ソース名が円記号を含めることはできません (\\) 文字。  
  
 アプリケーションは後の属性値を囲む中かっこを追加する必要はありません、**ドライバー**キーワード属性にセミコロン (;) が含まれている場合を除き、この場合、中かっこが必要です。 ドライバーが受信した属性の値には、中かっこが含まれている場合、ドライバーは削除せず、返される接続文字列の一部である必要があります。  
  
 DSN または接続文字列値を中かっこで囲む ({}) 文字のいずれかを含む **{}()、;?\*=! @** ドライバーにそのまま渡されます。 ただし、キーワードでこれらの文字を使用して、ドライバー マネージャーはファイル Dsn を使用する場合はエラーを返しますが、通常の接続文字列用のドライバーに接続文字列を渡します。 キーワードの値に埋め込まれた中かっこを使用しないでください。  
  
 接続文字列は、任意の数のドライバー定義のキーワードを含めることができます。 **ドライバー**キーワードは、システム情報の情報を使用していない、ドライバーはドライバーが接続文字列情報のみを使用してデータ ソースに接続できるように十分なキーワードを定義する必要があります。 (詳細については、このセクションの後半の「ドライバー ガイドライン」を参照してください)。ドライバーでは、どのキーワードはデータ ソースに接続するために必要なものを定義します。  
  
 次の表に、属性の値、 **DSN**、 **FILEDSN**、**ドライバー**、 **UID**、 **PWD**、および**SAVEFILE**キーワード。  
  
|Keyword|属性値の説明|  
|-------------|---------------------------------|  
|**DSN**|によって返されるデータ ソースの名前**SQLDataSources**のデータ ソース ダイアログ ボックスまたは**SQLDriverConnect**します。|  
|**FILEDSN**|データ ソースの接続文字列の作成元となる .dsn ファイルの名前。 これらのデータ ソースは、ファイル データ ソースと呼ばれます。|  
|**ドライバー**|によって返されるドライバーの説明、 **SQLDrivers**関数。 たとえば、Rdb または SQL Server。|  
|**UID**|ユーザーの id。|  
|**PWD**|ユーザー ID のパスワードがない場合は、ユーザー ID、または空の文字列に対応するパスワード (PWD =;)。|  
|**SAVEFILE**|現時点では、成功した接続の作成で使用されるキーワードの属性値を保存する必要があります .dsn ファイルのファイル名。|  
  
 アプリケーションがデータ ソースまたはドライバーを選択する方法については、次を参照してください。[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)します。  
  
 接続文字列では、一切のキーワードが繰り返される、ドライバーは、最初に見つかったキーワードの関連付けられた値を使用します。 場合、 **DSN**と**ドライバー**で同じ接続文字列キーワードが含まれている、ドライバー マネージャーとドライバーを使用して最初にどちらのキーワードが表示されます。  
  
 **FILEDSN**と**DSN**キーワードは相互に排他的: どちらのキーワードが最初に表示が使用され、2 番目に表示される 1 つは無視されます。 **FILEDSN**と**ドライバー**キーワード、その一方に相互に排他的です。 接続文字列のいずれかのキーワードが表示された場合**FILEDSN**、.dsn ファイルで同じキーワードの属性値ではなく、接続文字列キーワードの属性値が使用されます。  
  
 場合、 **FILEDSN**キーワードを使用して、.dsn ファイルで指定されたキーワードを使用すると、接続文字列を作成します。 (詳細については、「ファイル データ ソース、」このセクションの後半を参照してください)。**UID**キーワードが省略可能。 .dsn ファイルが作成されるだけ、**ドライバー**キーワード。 **PWD**キーワードは .dsn ファイルに格納されません。 保存と読み込み .dsn ファイルの既定のディレクトリで指定されたパスの組み合わせになります**CommonFileDir** hkey_local_machine \software\microsoft\ です Windows\CurrentVersion と"ODBC\DataSources"。 (CommonFileDir"C:\Program files \common files Files"場合は、既定のディレクトリになります"C:\Program files \common files 場合 Sources"です。)  
  
> [!NOTE]  
>  .Dsn ファイルを呼び出すことによって直接操作できる、 [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)と[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)インストーラー DLL で機能します。  
  
 場合、 **SAVEFILE**キーワードを使用して、現時点では、成功した接続の作成で使用されるキーワードの属性値の属性値の名前を持つ .dsn ファイルとして保存されます、 **SAVEFILE**キーワード。 **SAVEFILE**キーワードを組み合わせて使用する必要があります、**ドライバー** 、キーワード、 **FILEDSN**キーワード、またはその両方で、関数が sql_success_with_info またはSQLSTATE 01S09 (無効なキーワード)。 **SAVEFILE**キーワードを記述する前に、**ドライバー**キーワード、接続文字列、または結果が未定義になります。  
  
## <a name="driver-manager-guidelines"></a>ドライバー マネージャーのガイドライン  
 ドライバー マネージャーがドライバーに渡す接続文字列を構築します、 *InConnectionString*のドライバーの引数**SQLDriverConnect**関数。 ドライバー マネージャーは変更されません、 *InConnectionString*にアプリケーションによって渡される引数。  
  
 ドライバー マネージャーのアクションがの値に基づいて、 *DriverCompletion*引数。  
  
-   SQL_DRIVER_PROMPT:いずれかの接続文字列が含まれない場合、**ドライバー**、 **DSN**、または**FILEDSN**キーワード、ドライバー マネージャーが、データ ソース ダイアログ ボックスが表示されます。 ダイアログ ボックスによって返されるデータ ソース名と、アプリケーションによって渡されたその他のキーワードから接続文字列が構築します。 ドライバー マネージャーが、DSN キーワードと値のペアを指定します ダイアログ ボックスによって返されるデータ ソース名が空の場合は、既定値を = です。 (このダイアログ ボックスは、"Default"という名前のデータ ソースを表示はされません)。  
  
-   SQL_DRIVER_COMPLETE または sql_driver_complete_required の場合:アプリケーションで指定された接続文字列が含まれている場合、 **DSN**キーワード、ドライバー マネージャーが、アプリケーションで指定された接続文字列をコピーします。 ときにと同じ操作を実行、それ以外の場合、 *DriverCompletion* SQL_DRIVER_PROMPT です。  
  
-   SQL_DRIVER_NOPROMPT:ドライバー マネージャーは、アプリケーションで指定された接続文字列をコピーします。  
  
 アプリケーションで指定された接続文字列が含まれている場合、**ドライバー**キーワード、ドライバー マネージャーが、アプリケーションで指定された接続文字列をコピーします。  
  
 作成されますが、接続文字列を使用して、ドライバー マネージャーを使用するドライバーを決定します、ドライバーを接続およびドライバーに構築し、その接続文字列を渡しますドライバー マネージャーとドライバーの相互作用の詳細については、[コメント] セクションを参照してください。 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)します。 接続文字列が含まれていない場合、**ドライバー**キーワード、ドライバー マネージャーは次のように使用するドライバーを決定します。  
  
1.  接続文字列が含まれている場合、 **DSN**キーワード、ドライバー マネージャーは、システム情報のデータ ソースに関連付けられているドライバーを取得します。  
  
2.  接続文字列が含まれていない場合、 **DSN**キーワードまたはデータ ソースが見つからないと、ドライバー マネージャーは、システム情報の既定のデータ ソースに関連付けられているドライバーを取得します。 (詳細については、次を参照してください[サブキーの既定の](../../../odbc/reference/install/default-subkey.md)。)。ドライバー マネージャーの値を変更する、 **DSN** "DEFAULT"への接続文字列のキーワード。  
  
3.  場合、 **DSN**接続文字列キーワードでは、"DEFAULT"に設定されて、ドライバー マネージャーは、システム情報の既定のデータ ソースに関連付けられているドライバーを取得します。  
  
4.  ドライバー マネージャーが SQLSTATE IM002 SQL_ERROR を返します、データ ソースが見つからない場合は、既定のデータ ソースが見つからない場合は、(データ ソースが見つかりませんおよび指定された既定のドライバー)。  
  
## <a name="file-data-sources"></a>[ファイル データ ソース]  
 接続文字列を指定して、アプリケーションへの呼び出しで場合**SQLDriverConnect**が含まれています、 **FILEDSN**キーワード、およびこのキーワードは、いずれかで置き換えられない、 **DSN**または**ドライバー** .dsn ファイルに情報を使用して接続文字列を作成し、キーワード、ドライバー マネージャー、 *InConnectionString*引数。 ドライバー マネージャーは、次のように処理されます。  
  
1.  .Dsn ファイルのファイル名が有効かどうかを確認します。 SQLSTATE IM014 SQL_ERROR が返されたそうでない場合 (ファイル DSN の無効な名前)。 ファイル名が空の文字列である場合 ("") SQL_DRIVER_NOPROMPT がないと、指定された、**ファイルを開く** ダイアログ ボックスが表示されます。 ファイル名には、有効なパスが、ファイル名のない、または、無効なファイル名が含まれているし、SQL_DRIVER_NOPROMPT が指定されていない場合、**ファイルを開く**現在のディレクトリのファイル名で指定されたいずれかに設定 ダイアログ ボックスが表示されます。 ファイル名が空の文字列である場合 ("") またはファイル名には、有効なパスが、ファイル名のない、または、無効なファイル名が含まれていて、SQL_DRIVER_NOPROMPT が指定された、SQLSTATE IM014 と共に SQL_ERROR が返されます (ファイル DSN の無効な名前)。  
  
2.  .Dsn ファイルの [ODBC] セクションでは、すべてのキーワードを読み取ります。 場合、**ドライバー**キーワードが存在しない、SQLSTATE IM012 SQL_ERROR を返します (Driver キーワードの構文のエラー) .dsn ファイルが共有することがないと、したがってのみが含まれますを除く、 **DSN**キーワード。  
  
     ドライバー マネージャーがの値を読み取るファイルのデータ ソースが共有可能でない場合、 **DSN**キーワードし、必要に応じて、共有不能なファイルのデータ ソースが参照するユーザーまたはシステム データ ソースへ接続します。 手順 3. ~ 5. を実行しません。  
  
3.  ドライバーの接続文字列を構築します。 ドライバーの接続文字列は、.dsn ファイルで指定したキーワードと元のアプリケーション接続文字列で指定されているものの和集合です。 キーワードが重なるドライバー接続文字列を構築するための規則は次のとおりです。  
  
    -   場合、**ドライバー**キーワードは、アプリケーションの接続文字列とで指定されたドライバーが存在する、**ドライバー**キーワードは、.dsn ファイルとアプリケーションの接続文字列で同じではありません、.dsn ファイル内のドライバー情報は無視され、アプリケーションの接続文字列内のドライバー情報を使用します。 ドライバーが指定されている場合、**ドライバー** .dsn ファイルとアプリケーションの接続文字列では、同じキーワードより優先順位があるアプリケーションの接続文字列で指定されているすべてのキーワードが重複しています.dsn ファイルで指定します。  
  
    -   新しい接続文字列に、 **FILEDSN**キーワードを削除します。  
  
4.  見つかりましたレジストリ エントリで確認して、ドライバーを読み込みます。INI\\< ドライバー名\>\Driver 場所\<ドライバー名 > で指定された、**ドライバー**キーワード。  
  
5.  ドライバーの新しい接続文字列を渡します。  
  
 .Dsn ファイルの例については、次を参照してください。[を使用してファイル データ ソースの接続](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)します。  
  
## <a name="savefile-keyword"></a>SAVEFILE キーワード  
 アプリケーションで指定された接続文字列が含まれている場合、 **SAVEFILE**キーワード、その後、ドライバー マネージャーは、.dsn ファイルで接続文字列を保存します。 ドライバー マネージャーは、次のように処理されます。  
  
1.  属性値として .dsn ファイルのファイル名が含まれているかどうかを確認します、 **SAVEFILE**キーワードは有効です。 SQLSTATE IM014 SQL_ERROR が返されたそうでない場合 (ファイル DSN の無効な名前)。 ファイル名の有効性は、標準のシステムの名前付け規則によって決定されます。 ファイル名が空の文字列である場合 ("") と*DriverCompletion*引数が SQL_DRIVER_NOPROMPT ではありませんし、ファイル名が無効です。 場合は、ファイル名が既に存在し、場合*DriverCompletion* SQL_DRIVER_NOPROMPT には、ファイルが上書きされます。 場合*DriverCompletion*が SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、または sql_driver_complete_required の場合、ダイアログ ボックスに、ユーザー、ファイルを上書きするかどうかを指定するメッセージが表示されます。 If No を入力したら、次に、**ファイルの保存** ダイアログ ボックスが表示されます。  
  
2.  かどうか、ドライバーは SQL_SUCCESS を返しますとされたファイル名が空の文字列ではありませんし、ドライバー マネージャーで返される接続情報を書き込みます、 *OutConnectionString*で指定された形式で指定したファイルへの引数このセクションで前に、接続文字列 セクション。  
  
3.  場合は、ドライバーは SQL_SUCCESS を返し、ファイル名が空の文字列 ("")、ドライバー マネージャーは呼び出して、**ファイルの保存**でコモン ダイアログ ボックス、 *hwnd*指定し、接続情報を書き込みます返される*OutConnectionString*このセクションで前に、接続文字列 セクションで指定された形式でファイルの保存のコモン ダイアログ ボックスで指定されたファイルにします。  
  
4.  かどうか、ドライバーは SQL_SUCCESS を返しますが返されます、 *OutConnectionString*アプリケーションへの接続文字列が含まれる引数。  
  
5.  ドライバーに SQL_SUCCESS_WITH_INFO または SQL_ERROR が返される場合、ドライバー マネージャーは、アプリケーションに、SQLSTATE を返しますし。  
  
## <a name="driver-guidelines"></a>ドライバーのガイドライン  
 ドライバーがドライバー マネージャーによって渡された接続文字列が含まれているかどうかをチェック、 **DSN**または**ドライバー**キーワード。 接続文字列が含まれている場合、**ドライバー**キーワード、ドライバーはシステム情報からデータ ソースに関する情報を取得することはできません。 接続文字列が含まれている場合、 **DSN**キーワードまたはいずれかを含んでいません、 **DSN**または**ドライバー**キーワード、ドライバーは、データ ソースに関する情報を取得できます次のようにシステム情報: から  
  
1.  接続文字列が含まれている場合、 **DSN**キーワード、ドライバーは、指定したデータ ソースの情報を取得します。  
  
2.  接続文字列が含まれていない場合、 **DSN**キーワードを指定したデータ ソースが見つからない、または**DSN**キーワードは、"DEFAULT"に設定されて、ドライバーは、既定のデータ ソースの情報を取得します.  
  
 ドライバーは接続文字列で渡された情報を強化する、システム情報からを取得、情報を使用します。 システム情報の情報は、接続文字列の情報が重複する場合、ドライバーは、接続文字列に情報を使用します。  
  
 値に基づく*DriverCompletion*ドライバーの接続については、ユーザー ID やパスワードなどのユーザーに求めます、データ ソースに接続します。  
  
-   SQL_DRIVER_PROMPT:ドライバーでは、初期値として (あれば) 接続文字列とシステム情報からの値を使用して、ダイアログ ボックスが表示されます。 ユーザーは、ダイアログ ボックスを終了すると、ドライバーは、データ ソースに接続します。 値からの接続文字列を構築、 **DSN**または**ドライバー**キーワード\* *InConnectionString*から返される情報と、ダイアログ ボックス。 この接続文字列を配置、**OutConnectionString*バッファー。  
  
-   SQL_DRIVER_COMPLETE または sql_driver_complete_required の場合:接続文字列には、十分な情報が含まれていて、その情報が正しい場合、ドライバーは、データ ソースとコピーに接続\* *InConnectionString*に\* *OutConnectionString*. ときに、ドライバーが同じ操作を実行情報が見つからないか正しくない場合は、 *DriverCompletion* SQL_DRIVER_PROMPT は、その場合を除く*DriverCompletion* SQL_DRIVER_COMPLETE_ には必要に応じて、ドライバーには、コントロールしないデータ ソースに接続するために必要な情報が無効にします。  
  
-   SQL_DRIVER_NOPROMPT:接続文字列に十分な情報が含まれている場合、ドライバーは、データ ソースとコピーに接続\* *InConnectionString*に\* *OutConnectionString*します。 ドライバーは SQL_ERROR を返しますそれ以外の場合、 **SQLDriverConnect**します。  
  
 ドライバーのデータ ソースへの接続が成功すると、設定も\* *StringLength2Ptr*で返される使用できる出力の接続文字列の長さ **OutConnectionString*します。  
  
 ユーザーが、ドライバー マネージャー、または、ドライバーによって提示されるダイアログ ボックスを取り消した場合**SQLDriverConnect** sql_no_data が返されます。  
  
 ドライバー マネージャーとドライバーが接続プロセス中にどのように対話する方法については、次を参照してください。 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)します。  
  
 ドライバーをサポートしている場合**SQLDriverConnect**、システム情報、ドライバーのドライバー キーワード セクションを含める必要があります、 **ConnectFunctions**キーワードを 2 番目の文字は"Y"に設定します。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>接続プールが有効になっているときに接続します。  
 接続プールでは既に作成されている接続を再利用するアプリケーション。 ときに**SQLDriverConnect**を呼び出すと、ドライバー マネージャーの接続プールが指定されている環境で接続プールの一部である接続を使用して接続を確立しよう。 接続プールの詳細については、次を参照してください。 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)します。  
  
 アプリケーションでは、プールが有効になっている接続で SQLDisconnect を呼び出す前に、SQL_ATTR_RESET_CONNECTION を設定できます。 詳細については、次を参照してください。 [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)します。  
  
 アプリケーションを呼び出すときに、次の制限が適用**SQLDriverConnect**プールされた接続に接続します。  
  
-   接続プールの処理は行われませんときに、 **SAVEFILE**で接続文字列キーワードを指定します。  
  
-   接続プールが有効になっている場合**SQLDriverConnect**でのみ呼び出すことができます、 *DriverCompletion*引数 SQL_DRIVER_NOPROMPT の場合は**SQLDriverConnect**が呼び出されますその他の*DriverCompletion*、SQLSTATE HY110 (ドライバーが正しく完了) が返されます。  
  
## <a name="connection-attributes"></a>接続属性  
 設定を使用して、SQL_ATTR_LOGIN_TIMEOUT 接続属性**SQLSetConnectAttr**、ログイン要求をアプリケーションに返す前に、ドライバーによって正常に接続を完了するまで待機する秒数を定義します。 ユーザーは、接続文字列を完了するメッセージが表示されたら、ドライバーの接続プロセスの開始時に各ログイン要求の待機期間が開始します。  
  
 ドライバーは、既定では、SQL_MODE_READ_WRITE アクセス モードで接続を開きます。 アクセス モード SQL_MODE_READ_ONLY に設定するアプリケーションを呼び出す必要があります**SQLSetConnectAttr**呼び出す前に SQL_ATTR_ACCESS_MODE 属性を持つ**SQLDriverConnect**します。  
  
 データ ソースのシステム情報の既定のライブラリは翻訳が指定されている場合、ドライバーによって読み込みます。 別の翻訳のライブラリを呼び出すことによって読み込める**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 属性を持つ。 呼び出して変換オプションを指定できます**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION オプションを使用します。  
  
 詳細については、次を参照してください。 [SQLDriverConnect による接続](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)します。  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 参照してください[ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当てください。|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|検出およびデータ ソースに接続するために必要な値を列挙します。|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースへの接続|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|データ ソースからの切断|[SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|ドライバーの説明と属性を返す|[SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
