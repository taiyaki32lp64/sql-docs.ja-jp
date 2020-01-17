---
title: SQLDescribeParam 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c1ba115766b820cdcc4f671eeacf9eeec90a894
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345446"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ODBC  
  
 **概要**  
 **SQLDescribeParam**は、準備された SQL ステートメントに関連付けられているパラメーターマーカーの説明を返します。 この情報は、IPD のフィールドでも使用できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ParameterNumber*  
 代入パラメーターの順序を昇順に並べ替え、1から始まるパラメーターマーカー番号。  
  
 *DataTypePtr*  
 Outputパラメーターの SQL データ型を返すバッファーへのポインター。 この値は、IPD の SQL_DESC_CONCISE_TYPE record フィールドから読み取られます。 これは、「付録 D」の「 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)」セクションの値のいずれかになります。データ型、またはドライバー固有の SQL データ型。  
  
 ODBC 3 の場合。*x*、SQL_TYPE_DATE、SQL_TYPE_TIME、または SQL_TYPE_TIMESTAMP は、それぞれ、ODBC 2 で日付、時刻、またはタイムスタンプデータの *\*DataTypePtr*に返されます。*x*、SQL_DATE、SQL_TIME、または SQL_TIMESTAMP が返されます。 ODBC 2 では、ドライバーマネージャーが必要なマッピングを実行します。*x*アプリケーションは ODBC 3 を使用して動作しています。*x*ドライバーまたは ODBC 3 の場合。*x*アプリケーションは ODBC 2 で動作しています。*x*ドライバー。  
  
 *Columnnumber*が 0 (ブックマーク列の場合) の場合、SQL_BINARY は可変長ブックマークの *\*DataTypePtr*で返されます。 (SQL_INTEGER は、ブックマークが ODBC 3 で使用されている場合に返されます。*x*アプリケーションが ODBC 2 で動作する。*x*ドライバーまたは ODBC 2。*x*アプリケーションが ODBC 3 を使用して動作している。*x*ドライバー。)  
  
 詳細については、次を参照してください。 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 D:データ型。 ドライバー固有の SQL データ型の詳細については、ドライバーのドキュメントを参照してください。  
  
 *ParameterSizePtr*  
 Outputデータソースによって定義されている、対応するパラメーターマーカーの列または式のサイズを文字数で返すバッファーへのポインター。 列のサイズの詳細については、「[列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。  
  
 *DecimalDigitsPtr*  
 Outputデータソースによって定義された、対応するパラメーターの列または式の小数点以下桁数を返すバッファーへのポインター。 10進数の詳細については、「[列のサイズ、10進数、転送オクテットの長さ、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)」を参照してください。  
  
 *NullablePtr*  
 Outputパラメーターが NULL 値を許容するかどうかを示す値を返すバッファーへのポインター。 この値は、IPD の SQL_DESC_NULLABLE フィールドから読み取られます。 次のいずれかです。  
  
-   SQL_NO_NULLS:パラメーターでは NULL 値が許可されません (これが既定値です)。  
  
-   SQL_NULLABLE:パラメーターでは NULL 値を使用できます。  
  
-   SQL_NULLABLE_UNKNOWN:ドライバーは、パラメーターで NULL 値が許可されているかどうかを判断できません。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLDescribeParam**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、 *handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **SQLDescribeParam**によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|(DM) 引数*Parameternumber*に指定された値が1未満です。<br /><br /> 引数*Parameternumber*に指定された値が、関連付けられている SQL ステートメントのパラメーターの数を超えています。<br /><br /> パラメーターマーカーは、DML 以外のステートメントの一部でした。<br /><br /> パラメーターマーカーは**選択**リストの一部でした。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|21S01|挿入する値の一覧が列の一覧と一致しません|**INSERT**ステートメント内のパラメーターの数が、ステートメントで指定されたテーブル内の列の数と一致しませんでした。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 関数が呼び出され、実行が完了する前に、 **SQLCancel**または**Sqlcancelhandle**が*StatementHandle*で呼び出されました。 次に、 *StatementHandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlcancelhandle**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) *StatementHandle*の**SQLPrepare**または**SQLExecDirect**を呼び出す前に、関数が呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLDescribeParam**関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が*StatementHandle*に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
 パラメーターマーカーには、SQL ステートメントに表示される順序で、パラメーターの順序が1から始まる昇順で番号が付けられています。  
  
 **SQLDescribeParam**は、SQL ステートメント内のパラメーターの型 (入力、入出力、出力) を返しません。 プロシージャの呼び出しを除き、SQL ステートメントのすべてのパラメーターは入力パラメーターです。 プロシージャの呼び出しで各パラメーターの型を特定するには、アプリケーションが**SQLProcedureColumns**を呼び出します。  
  
 詳細については、「[パラメーターの説明](../../../odbc/reference/develop-app/describing-parameters.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 次の例では、SQL ステートメントの入力をユーザーに求め、そのステートメントを準備します。 次に、 **Sqlnumparams**を呼び出して、ステートメントにパラメーターが含まれているかどうかを確認します。 ステートメントにパラメーターが含まれている場合は、 **SQLDescribeParam**を呼び出してそれらのパラメーターを記述し、 **SQLBindParameter**をバインドします。 最後に、任意のパラメーターの値をユーザーに要求し、ステートメントを実行します。  
  
```cpp  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドする|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|実行するステートメントの準備|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
