---
title: SQLCopyDesc 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aec6dc776f5fdd84932be089e9503f0083a49c2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345487"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqlcopydesc**は、記述子ハンドルから別の記述子ハンドルに記述子情報をコピーします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>引数  
 *SourceDescHandle*  
 代入ソース記述子ハンドル。  
  
 *TargetDescHandle*  
 代入ターゲット記述子ハンドル。 *TargetDescHandle*引数には、アプリケーション記述子または IPD へのハンドルを指定できます。 *TargetDescHandle*を IRD へのハンドルに設定することはできません。また、 **SQLCOPYDESC**は SQLSTATE HY016 を返します (実装行記述子を変更することはできません)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcopydesc**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、SQL_HANDLE_DESC の*Handletype*と*TargetDescHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます。 呼び出しで無効な*SourceDescHandle*が渡された場合、SQL_INVALID_HANDLE が返されますが、SQLSTATE は返されません。 次の表に、 **Sqlcopydesc**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
 エラーが返されると、 **Sqlcopydesc**への呼び出しはすぐに中止され、 *TargetDescHandle*記述子のフィールドの内容は未定義になります。  
  
 **Sqlcopydesc**は**SQLGetDescField**と**SQLSetDescField**を呼び出すことによって実装される可能性があるため、 **SQLGetDescField**または**SQLSetDescField**によって返される sqlstates を**sqlcopydesc**が返す可能性があります。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY007|関連付けられたステートメントは準備されていません|*SourceDescHandle*が IRD に関連付けられており、関連付けられているステートメントハンドルが準備状態または実行済み状態ではありませんでした。|  
|HY010|関数のシーケンスエラー|(DM) *SourceDescHandle*または*TargetDescHandle*の記述子ハンドルは、非同期的に実行される関数 (この関数ではない) が呼び出され、この関数が実行されたときにまだ実行されていた*StatementHandle*に関連付けられていました。と呼ばれる。<br /><br /> (DM) *SourceDescHandle*または*TargetDescHandle*の記述子ハンドルは、 **sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または**SQLSetPos**がある*StatementHandle*に関連付けられていました。を呼び出し、SQL_NEED_DATA を返しました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が、 *SourceDescHandle*または*TargetDescHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlcopydesc**関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が、 *SourceDescHandle*または*TargetDescHandle*に関連付けられたいずれかのステートメントハンドルに対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY016|実装行記述子を変更できません|*TargetDescHandle*は IRD に関連付けられました。|  
|HY021|不整合な記述子情報|整合性チェック中にチェックされた記述子情報が一致しませんでした。 詳細については、「 **SQLSetDescField**」の「整合性チェック」を参照してください。|  
|HY092|属性またはオプションの識別子が無効です|**Sqlcopydesc**を呼び出すと、 **SQLSetDescField**の呼び出しが要求されましたが *\*、valueptr*は*TargetDescHandle*の*FieldIdentifier*引数に対して無効です。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *SourceDescHandle*または*TargetDescHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 **Sqlcopydesc**を呼び出すと、ソース記述子ハンドルのフィールドがターゲット記述子ハンドルにコピーされます。 フィールドはアプリケーション記述子または IPD にのみコピーできますが、IRD にはコピーできません。 フィールドは、アプリケーションまたは実装記述子からコピーできます。  
  
 ステートメントハンドルが準備状態または実行済み状態の場合にのみ、IRD からフィールドをコピーできます。それ以外の場合、関数は SQLSTATE HY007 (関連付けられたステートメントは準備されていません) を返します。  
  
 ステートメントが準備されているかどうかにかかわらず、IPD からフィールドをコピーできます。 動的パラメーターを持つ SQL ステートメントが準備され、IPD の自動作成がサポートされ、有効になっている場合、IPD はドライバーによって設定されます。 *SourceDescHandle*として IPD を使用して**sqlcopydesc**を呼び出すと、入力されたフィールドがコピーされます。 IPD がドライバーによって設定されていない場合は、IPD の最初のフィールドの内容がコピーされます。  
  
 記述子ハンドルが自動的にまたは明示的に割り当てられたかどうかを指定する SQL_DESC_ALLOC_TYPE を除く、記述子のすべてのフィールドがコピーされます。これは、対象の記述子に対してフィールドが定義されているかどうかによって決まります。 コピーされたフィールドは既存のフィールドを上書きします。  
  
 ドライバーが2つの異なる接続または環境にある場合でも、 *SourceDescHandle*引数と*TargetDescHandle*引数が同じドライバーに関連付けられている場合は、すべての記述子フィールドがコピーされます。 *SourceDescHandle*引数と*TargetDescHandle*引数が異なるドライバーに関連付けられている場合、ドライバーマネージャーは odbc 定義フィールドをコピーしますが、odbc で定義されていないドライバー定義のフィールドやフィールドは、ディスクリプタ.  
  
 エラーが発生すると、 **Sqlcopydesc**への呼び出しは直ちに中止されます。  
  
 SQL_DESC_DATA_PTR フィールドがコピーされると、ターゲット記述子に対して整合性チェックが実行されます。 整合性チェックが失敗した場合は、SQLSTATE HY021 (不整合な記述子情報) が返され、 **Sqlcopydesc**への呼び出しがすぐに中止されます。 整合性チェックの詳細については、「 [SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)」の「整合性チェック」を参照してください。  
  
 接続が異なる環境にある場合でも、記述子ハンドルは接続間でコピーできます。 ソースとターゲット記述子のハンドルが同じ接続に属しておらず、2つの接続が別のドライバーに属していることがドライバーマネージャー によって検出された場合は、を使用し**てフィールドごとのコピーを実行することで、sqlcopydesc が実装されます。SQLGetDescField**と**SQLSetDescField**。  
  
 あるドライバーで*SourceDescHandle*を使用して**sqlcopydesc**が呼び出され、別のドライバーで*TargetDescHandle*が呼び出されると、 *SourceDescHandle*のエラーキューがクリアされます。 このエラーが発生するのは、この場合の**Sqlcopydesc**が**SQLGetDescField**と**SQLSetDescField**の呼び出しによって実装されているためです。  
  
> [!NOTE]  
>  アプリケーションでは、明示的に割り当てられた記述子ハンドルを*StatementHandle*に関連付けることができます。これは、1つの記述子から別の記述子にフィールドをコピーするために**sqlcopydesc**を呼び出すことではありません。 明示的に割り当てられた記述子は、SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC statement 属性を明示的にのハンドルに設定することにより、同じ*Connectionhandle*上の別の*StatementHandle*に関連付けることができます。割り当てられた記述子。 この場合、記述子フィールドの値を1つの記述子から別の記述子にコピーするために、 **Sqlcopydesc**を呼び出す必要はありません。 ただし、記述子ハンドルを別の*Connectionhandle*の*StatementHandle*に関連付けることはできません。異なる*Connectionhandles*の*StatementHandles*で同じ記述子フィールド値を使用するには、 **sqlcopydesc**を呼び出す必要があります。  
  
 記述子ヘッダーまたはレコード内のフィールドの説明については、「 [SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)」を参照してください。 記述子の詳細については、「[記述子](../../../odbc/reference/develop-app/descriptors.md)」を参照してください。  
  
## <a name="copying-rows-between-tables"></a>テーブル間での行のコピー  
 アプリケーションでは、アプリケーションレベルでデータをコピーせずに、あるテーブルから別のテーブルにデータをコピーできます。 これを行うために、アプリケーションは、データをフェッチするステートメントと、データをコピーに挿入するステートメントに、同じデータバッファーと記述子の情報をバインドします。 これを実現するには、アプリケーション記述子を共有する (明示的に割り当てられた記述子を APD ステートメントと別のステートメントの両方にバインドする) か、 **Sqlcopydesc**を使用して、その2つの APD との間のバインドをコピーします。命令. ステートメントが異なる接続にある場合は、 **Sqlcopydesc**を使用する必要があります。 また、 **Sqlcopydesc**を呼び出して、2つのステートメントの IRD と IPD の間のバインドをコピーする必要があります。 同じ接続で複数のステートメントをコピーする場合、この操作を成功させるには、 **SQLGetInfo**の呼び出しのためにドライバーによって返される SQL_ACTIVE_STATEMENTS information 型が1より大きい必要があります。 (これは、複数の接続をコピーする場合には当てはまりません)。  
  
### <a name="code-example"></a>コード例  
 次の例では、記述子操作を使用して、PartsSource テーブルのフィールドを PartsCopy テーブルにコピーします。 PartsSource テーブルの内容は、 *hstmt0*の行セットバッファーにフェッチされます。 これらの値は、 *hstmt1*で INSERT ステートメントのパラメーターとして使用され、PartsCopy テーブルの列を設定します。 これを行うには、 *hstmt0*の IRD のフィールドが*hstmt1*の IPD のフィールドにコピーされ、hstmt0 のフィールドが APD の hstmt1 のフィールドに*コピーされ* *ます。* 出力パラメーターを持つステートメントから入力パラメーターである必要がある IRD フィールドに IPD フィールドをコピーする場合は、 **SQLSetDescField**を使用して IPD の SQL_DESC_PARAMETER_TYPE 属性を SQL_PARAM_INPUT に設定します。  
  
```cpp  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|複数の記述子フィールドの取得|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|1つの記述子フィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|複数の記述子フィールドの設定|[SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
