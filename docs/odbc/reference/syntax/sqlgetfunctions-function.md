---
title: SQLGetFunctions 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edb58ebff212e494b84aed12397def2876d3728d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345605"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqlgetfunctions**は、ドライバーが特定の ODBC 関数をサポートしているかどうかに関する情報を返します。 この関数は、ドライバーマネージャーで実装されています。また、ドライバーで実装することもできます。 ドライバーが**Sqlgetfunctions**を実装している場合、ドライバーマネージャーはドライバーで関数を呼び出します。 それ以外の場合は、関数自体を実行します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *FunctionId*  
 代入対象の ODBC 関数を識別する **#define**値です。**SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**。 **SQL_API_ODBC3_ALL_FUNCTIONS**は odbc*3.x アプリケーションに*よって使用され、odbc*3.x およびそれ*以前の関数のサポートを決定します。 **SQL_API_ALL_FUNCTIONS**は、odbc*2.X アプリケーションが*odbc*2.x とそれ*以前の関数のサポートを確認するために使用します。  
  
 ODBC 関数を識別する **#define**値の一覧については、「コメント」の表を参照してください。  
  
 *SupportedPtr*  
 Output *FunctionId*が単一の ODBC 関数を識別する場合、 *supportedptr*は、指定された関数がドライバーによってサポートされている場合は SQL_TRUE の単一の sqlus悪意のある値を指し、サポートされていない場合は SQL_FALSE を指します。  
  
 *FunctionId*が SQL_API_ODBC3_ALL_FUNCTIONS の場合、 *SUPPORTEDPTR*は、SQL_API_ODBC3_ALL_FUNCTIONS_SIZE と等しい数の要素を持つ sqlsmallint 配列を指します。 この配列は、ドライバーマネージャーによって、4000ビットのビットマップとして扱われます。このビットマップを使用して、ODBC 3.x 以前の機能がサポートされているかどうかを判断できます。 関数のサポートを決定するために、SQL_FUNC_EXISTS マクロが呼び出されます。 (「コメント」を参照してください)。ODBC*3.x アプリケーションは*、odbc*2.X または*odbc*2.x ドライバーの*いずれかに対して、SQL_API_ODBC3_ALL_FUNCTIONS を使用して**sqlgetfunctions**を呼び出すことができます。  
  
 *FunctionId*が SQL_API_ALL_FUNCTIONS の場合、 *supportedptr*は100要素の sqlus悪意のある配列を指します。 配列には、各 ODBC 関数を識別するために、 *FunctionId*によって使用される **#define**値によってインデックスが付けられます。配列の一部の要素は使用されておらず、将来使用するために予約されています。 ドライバーでサポートされている ODBC*2.x または*それ以前の関数を識別する場合、要素は SQL_TRUE です。 ドライバーでサポートされていない ODBC 関数が識別された場合、または ODBC 関数が識別されない場合は、SQL_FALSE になります。  
  
 **Supportedptr*で返される配列は、0から始まるインデックスを使用します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlgetfunctions**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、SQL_HANDLE_DBC の*Handletype*および*connectionhandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます。 次の表に、 **Sqlgetfunctions**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------|-----|-----------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) **Sqlgetfunctions**は、 **SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**の前に呼び出されました。<br /><br /> (DM) **SQLBrowseConnect**が*connectionhandle*に対して呼び出され、SQL_NEED_DATA が返されました。 **SQLBrowseConnect**が SQL_SUCCESS_WITH_INFO または SQL_SUCCESS を返す前に、この関数が呼び出されました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が*CONNECTIONHANDLE*に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY095|関数の型が有効範囲にありません|(DM) 無効な*FunctionId*値が指定されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
  
## <a name="comments"></a>コメント  
 **Sqlgetfunctions**は、 **sqlgetfunctions**、 **Sqlデータソース**、および**sqldrivers**がサポートされていることを常に返します。 これらの関数はドライバーマネージャーに実装されるため、これが行われます。 Unicode 関数が存在する場合、ドライバーマネージャーは対応する Unicode 関数に ANSI 関数をマップし、ANSI 関数が存在する場合は、対応する ANSI 関数に Unicode 関数をマップします。 アプリケーションで**Sqlgetfunctions**を使用する方法については、「[インターフェイスの準拠レベル](../../../odbc/reference/develop-app/interface-conformance-levels.md)」を参照してください。  
  
 次に示すのは、ISO 92 標準準拠レベルに準拠している関数の*FunctionId*の有効な値の一覧です。  
  
|FunctionId 値|FunctionId 値|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 オープングループ標準準拠レベルに準拠している*関数の場合*、次のような値が使用されます。  
  
|FunctionId 値|FunctionId 値|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 ODBC 標準のコンプライアンスレベルに準拠している*関数の場合*、次のような値が使用されます。  
  
|FunctionId 値|FunctionId 値|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] ODBC*2.x ドライバーを*使用する場合、 **sqlbulkoperations**はサポート対象として返されます。これは、次の両方が当てはまる場合に限ります。 Odbc*2.x ドライバーは* **SQLSETPOS**をサポートし、情報型 SQL_POS_OPERATIONS はを返します。設定されている SQL_POS_ADD ビット。  
  
 ODBC 3.8 以降で導入された関数の*FunctionId*の有効な値の一覧を次に示します。  
  
|FunctionId 値|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **Sqlcancelhandle**は、ドライバーが**SQLCancel**と**sqlcancelhandle**の両方をサポートしている場合にのみ、サポート対象として返されます。 **SQLCancel**がサポートされているが**sqlcancelhandle**がサポートされていない場合でも、アプリケーションはステートメントハンドルで**sqlcancelhandle**を呼び出すことができます。これは、 **SQLCancel**にマップされるためです。  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS マクロ  
 SQL_FUNC_EXISTS (*Supportedptr*, *FunctionID*) マクロは、 **Sqlgetfunctions**が SQL_API_ODBC3_ALL_ の*FunctionID*引数を使用して呼び出された後の ODBC 3.x またはそれ以前の関数のサポートを判別するために使用され*ます。* 関数. アプリケーションは、SQL_FUNC_EXISTS を呼び出します。*この引数は*、 *sqlgetfunctions*で渡された*supportedptr*に設定され、 *FunctionID*引数が関数の **#define**に設定されています。 SQL_FUNC_EXISTS は、関数がサポートされている場合は SQL_TRUE を返し、それ以外の場合は SQL_FALSE を返します。  
  
> [!NOTE]
>  ODBC*2.x ドライバーを*使用する場合は、 **SQLAllocHandle**が**sqlfreehandle**、sqlfreehandle にマップされるため、odbc 3.X ドライバーマネージャーは**SQLAllocHandle**と**sqlfreehandle**の SQL_TRUE を返します *。* 、、 **Sqlallocstmt**、および**Sqlallocstmt**が**Sqlallocstmt**、 **SQLFreeConnect**、または**SQLFreeStmt**にマップされていることが原因です。 SQL_HANDLE_DESC の*Handletype*引数を持つ**SQLAllocHandle**または**sqlfreehandle**はサポートされていませんが、関数に対して SQL_TRUE が返されます。ただし、この場合、にマップする ODBC*2.x 関数が*ないためです。  
  
## <a name="code-example"></a>コード例  
 次の3つの例は、アプリケーションが**Sqlgetfunctions**を使用して、ドライバーが**sqltables**、 **Sqlcolumns**、および**sqlstatistics**をサポートしているかどうかを判断する方法を示しています。 ドライバーがこれらの機能をサポートしていない場合、アプリケーションはドライバーから切断されます。 最初の例では、関数ごとに1回**Sqlgetfunctions**を呼び出します。  
  
```cpp  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 2番目の例では、ODBC 3. x アプリケーションは**Sqlgetfunctions**を呼び出し、 **SQLGETFUNCTIONS**が odbc 3. x 以前のすべての関数に関する情報を返す配列を渡します。  
  
```cpp  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 3番目の例は、ODBC 2.x アプリケーションが**Sqlgetfunctions**を呼び出し、それに100要素の配列を渡します。これにより、 **sqlgetfunctions**は、すべての ODBC 2.x およびそれ以前の関数に関する情報を返します。  
  
```cpp  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|ドライバーまたはデータソースに関する情報を返す|[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|ステートメント属性の設定を返す|[SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
