---
title: 非同期実行 (ポーリング メソッド) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97fe8af6f02e9797bc14578edda09c420f8f94e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077049"
---
# <a name="asynchronous-execution-polling-method"></a>非同期実行 (ポーリング メソッド)
ODBC 3.8 と Windows 7 SDK では、前に、非同期操作は、ステートメントの関数でのみ可能でした。 詳細については、次を参照してください。、**ステートメントの操作を非同期に実行**、このトピックで後述します。  
  
 Windows 7 SDK で ODBC 3.8 には、接続関連の操作での非同期実行が導入されました。 詳細については、次を参照してください。、**接続の操作を非同期に実行**セクションで、このトピックで後述します。  
  
 Windows 7 sdk の非同期ステートメントまたは接続操作では、アプリケーションは、非同期操作が完了のポーリング メソッドを使用して決定されます。 以降、Windows 8 SDK では、非同期操作が通知メソッドを使用して完全なことを確認できます。 詳細については、次を参照してください。[非同期実行 (通知方法)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)します。  
  
 既定では、ドライバーの ODBC 関数同期的に実行します。つまり、アプリケーション関数を呼び出し、関数の実行が完了するまで、ドライバーがアプリケーションにコントロールを返すされません。 一部の関数を非同期的に実行できる、つまり、関数を呼び出し、アプリケーションと、ドライバーの 最小限の処理後に、アプリケーションに返しますコントロール。 アプリケーションは、最初の関数がまだ実行中に、他の関数を呼び出すしことができます。  
  
 ほとんどの関数、データ ソースで実行されるほとんどの非同期実行がサポートされている、データをフェッチし、トランザクションのコミットなど、接続の確立、準備、および SQL ステートメントを実行する関数には、メタデータを取得します。 データ ソースで実行されているタスクのログイン プロセスを大規模データベースに対する複雑なクエリなど、時間がかかる場合に便利です。  
  
 アプリケーションでは、ステートメントまたは非同期処理が有効になっている接続を持つ関数を実行するとき、ドライバー (引数のエラーをチェック) などの処理量が最小限、および実行します渡し、処理、データ ソースを返しますSQL_STILL_EXECUTING リターン コードをアプリケーションに制御します。 その後、アプリケーションでは、その他のタスクを実行します。 非同期関数が終了したときを確認するのには、アプリケーションは、最初に使用されるのと同じ引数を使用して、関数を呼び出すことによって、一定の間隔でドライバーをポーリングします。 関数がまだ実行中、; SQL_STILL_EXECUTING が返されます実行が終了する場合は、返さに同期的に実行、SQL_SUCCESS や SQL_ERROR、SQL_NEED_DATA などが、コードを返します。  
  
 特定のドライバーは、同期または非同期かどうか、関数を実行します。 たとえば、ドライバーの結果セットのメタデータがキャッシュされているとします。 実行するほとんどの時間がかかるこの場合、 **SQLDescribeCol**ドライバーする必要があります、関数を実行するだけではなく意図的に実行を遅延とします。 その一方で、ドライバーは、データ ソースからメタデータを取得する必要がある場合が返されますコントロールをアプリケーションにこれを実行中にします。 そのため、アプリケーションは、最初に実行すると関数を非同期的に SQL_STILL_EXECUTING 以外のリターン コードを処理できる必要があります。  
  
## <a name="executing-statement-operations-asynchronously"></a>ステートメントの操作を非同期的に実行  
 次のステートメントの関数は、データ ソースに対して機能し、非同期的に実行できます。  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 非同期のステートメントの実行はステートメントごとまたはデータ ソースによっては、接続ごとのいずれかで制御されます。 つまり、アプリケーションは、特定の関数が非同期に実行することが、特定のステートメントで実行される任意の関数が非同期的に実行すること、しない指定します。 検索するアプリケーションを呼び出すと、どれがサポートされているに[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_ASYNC_MODE のオプション。 (ステートメント ハンドル) の接続レベルの非同期実行がサポートされる場合は、SQL_AM_CONNECTION が返されます。SQL_AM_STATEMENT ステートメント レベルの非同期実行がサポートされている場合。  
  
 関数を実行すると、特定のステートメントがあることを指定する非同期的に実行、アプリケーション呼び出し**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE 属性し、SQL_ASYNC_ENABLE_ON に設定します。 接続レベルの非同期処理がサポートされている場合、SQL_ATTR_ASYNC_ENABLE ステートメント属性は読み取り専用とその値は、ステートメントが割り当てられている接続の接続属性と同じです。 これは、ステートメントの割り当て時、またはそれ以降には、ステートメント属性の値を設定するかどうかドライバー固有です。 SQL_ERROR と SQLSTATE HYC00 戻ります設定しようとしました。 (省略可能な機能が実装されていません)。  
  
 関数を実行すると、特定の接続があることを指定する非同期的に実行、アプリケーション呼び出し**SQLSetConnectAttr** SQL_ATTR_ASYNC_ENABLE 属性し、SQL_ASYNC_ENABLE_ON に設定します。 非同期実行のための接続に割り当てられているすべての将来のステートメント ハンドルを有効になりますドライバー定義されているかどうか既存のステートメント ハンドルは、この操作で有効になります。 SQL_ATTR_ASYNC_ENABLE が SQL_ASYNC_ENABLE_OFF に設定されている場合、接続ですべてのステートメントは同期モードです。 接続でアクティブなステートメントは、非同期実行が有効になっている場合は、エラーが返されます。  
  
 アプリケーションが呼び出す、ドライバーは、特定の接続でサポートできる非同期モードでのアクティブな同時実行ステートメントの最大数を決定する**SQLGetInfo** SQL_MAX_ASYNC_CONCURRENT_STATEMENTS オプションを使用します。  
  
 次のコードでは、ポーリング モデルのしくみを示しています。  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 関数を非同期的に実行するときに、アプリケーションの他のステートメントで関数を呼び出すことができます。 アプリケーションは、非同期のステートメントに関連付けられた 1 つを除く、すべての接続で関数を呼び出すこともできます。 アプリケーションがのみを呼び出しては、元の関数と (ステートメント ハンドルまたは、関連する接続、環境ハンドル) で、次の関数ステートメント操作の後に返します SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (上、ステートメント ハンドル)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 アプリケーションが非同期のステートメントまたはステートメントに関連付けられている接続の他の関数を呼び出す場合、関数は、SQLSTATE HY010 を返します (関数シーケンス エラー) など。  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 アプリケーションかどうかをまだ実行中に非同期に判断する関数を呼び出すときに、元のステートメント ハンドルを使用する必要があります。 これは、非同期実行は、ステートメントごとに追跡されるためです。 アプリケーションは、他の引数の有効な値も指定する必要があります - エラー ドライバー マネージャーでのチェックを通過する - 元の引数が実行されます。 ただし、ドライバーは、ステートメント ハンドルをチェックし、ステートメントが非同期的に実行されているかを決定後、は、その他のすべての引数を無視します。  
  
 関数は非同期的に - 実行中には、SQL_STILL_EXECUTING が返された後、および別のコードに返す前に、アプリケーションをキャンセルできます呼び出して**SQLCancel**または**SQLCancelHandle** 、同じステートメント ハンドルを使用します。 関数の実行をキャンセルします。 これは保証されません。 たとえば、関数を既に完了がある可能性があります。 によって返される、コードのさらに、 **SQLCancel**または**SQLCancelHandle**のみから実際には、関数が取り消されるかどうかない関数をキャンセルの試行が成功すると、かどうかを示します。 関数がキャンセルされたかどうかを確認するのには、アプリケーションは、関数をもう一度呼び出します。 SQLSTATE HY008、SQL_ERROR を返しますが、関数が取り消された場合 (操作が取り消されました)。 関数が取り消されない場合は、SQL_SUCCESS、SQL_STILL_EXECUTING、または別の sqlstate SQL_ERROR などの別のコードを返します。  
  
 ドライバーは、ステートメント レベルの非同期処理、アプリケーション呼び出しをサポートしている場合は、特定のステートメントの非同期実行を無効にする**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE 属性し、sql _ に設定ASYNC_ENABLE_OFF します。 ドライバーは接続レベルの非同期処理をサポートする場合、アプリケーション呼び出し**SQLSetConnectAttr** SQL_ASYNC_ENABLE_OFF で、上のすべてのステートメントの非同期実行を無効にして SQL_ATTR_ASYNC_ENABLE を設定するのには接続します。  
  
 アプリケーションには、元の関数の反復ループ内の診断レコードを処理する必要があります。 場合**SQLGetDiagField**または**SQLGetDiagRec**非同期関数を実行しているときに呼び出される現在の診断レコードの一覧が返されます。 元の関数呼び出しが繰り返されるたびに、前の診断レコードを消去します。  
  
## <a name="executing-connection-operations-asynchronously"></a>接続操作を非同期的に実行します。  
 ODBC 3.8、前にステートメント関連の操作の準備などの非同期実行が許可されました、実行、およびフェッチもカタログ メタデータの操作です。 ODBC 3.8 以降、非同期実行ことも、接続の切断などの接続に関連する操作、commit、およびロールバックのできます。  
  
 ODBC 3.8 の詳細については、次を参照してください。[で ODBC 3.8 新](../../../odbc/reference/what-s-new-in-odbc-3-8.md)します。  
  
 接続操作を非同期的に実行するは、次のシナリオで役立ちます。  
  
-   ときにスレッドの数が少ない多数の非常に高いデータ レートでデバイスを管理します。 応答性とスケーラビリティを最大化するには、すべての操作を非同期にすることをお勧めします。  
  
-   転送の経過時間を短縮する複数の接続経由でデータベース操作が重複する場合。  
  
-   効率的な非同期の ODBC 呼び出しとの接続操作をキャンセルする機能は、ユーザーは、タイムアウトを待機することがなく、低速な操作をキャンセルできるようにアプリケーションを有効にします。  
  
 接続ハンドルの操作には、次の関数が非同期的に実行するようになりましたことができます。  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 アプリケーションを呼び出すドライバーがこれらの関数で、非同期操作をサポートしているかどうかを判断する**SQLGetInfo** SQL_ASYNC_DBC_FUNCTIONS とします。 非同期操作がサポートされている場合は、SQL_ASYNC_DBC_CAPABLE が返されます。 非同期操作がサポートされていない場合は、SQL_ASYNC_DBC_NOT_CAPABLE が返されます。  
  
 関数を実行すると、特定の接続があることを指定する非同期的に実行、アプリケーション呼び出し**SQLSetConnectAttr** SQL_ASYNC_DBC_ENABLE を SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 属性を設定_ON します。 常に接続を確立する前に、接続属性の設定を同期的に実行します。 操作を設定すると、接続属性で SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE のも、 **SQLSetConnectAttr**常に同期的に実行されます。  
  
 アプリケーションは、接続を行う前に非同期操作を有効にできます。 ドライバー マネージャーは、接続を行う前に使用するドライバーを特定できないため、ドライバー マネージャーが常に成功を返します**SQLSetConnectAttr**します。 ただし、ODBC ドライバーは非同期操作をサポートしていない場合に接続することがあります。  
  
 一般があります多くて 1 つの関数を非同期的に実行するか、特定の接続ハンドルまたはステートメント ハンドルに関連付けられています。 ただし、接続ハンドルでは、1 つ以上関連付けられているステートメント ハンドルを持つことができます。 接続ハンドルで実行する非同期操作がない場合、関連付けられているステートメント ハンドルは非同期操作を実行できます。 同様に、関連付けられているステートメント ハンドルのいずれかで進行中の非同期操作がない場合は、接続ハンドルでの非同期操作を設定できます。 現在、非同期操作を実行しているハンドルを使用して非同期操作を実行するとは HY010、「関数のシーケンス エラー」を返します。  
  
 接続操作では、SQL_STILL_EXECUTING が返された場合、アプリケーションのみを呼び出せます、元の関数と、次の関数その接続ハンドル。  
  
-   **SQLCancelHandle** (接続ハンドル)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (ENV/DBC の割り当て)  
  
-   **SQLAllocHandleStd** (ENV/DBC の割り当て)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 アプリケーションには、元の関数の反復ループ内の診断レコードを処理する必要があります。 非同期関数を実行するときに、SQLGetDiagField または SQLGetDiagRec を呼び出すには、診断レコードの現在の一覧を返します。 元の関数呼び出しが繰り返されるたびに、前の診断レコードを消去します。  
  
 接続されている場合、操作が完了しているアプリケーションは SQL_SUCCESS、SQL_SUCCESS_WITH_INFO または元の関数呼び出しで受信すると、開かれたまたは、非同期的に終了しました。  
  
 ODBC 3.8 に新しい関数が追加されました**SQLCancelHandle**します。 この関数は、6 つの接続の機能を取り消します (**SQLBrowseConnect**、 **SQLConnect**、 **SQLDisconnect**、 **SQLDriverConnect**、**SQLEndTran**、および**SQLSetConnectAttr**)。 アプリケーションを呼び出す必要があります**SQLGetFunctions**ドライバーをサポートしているかどうかは**SQLCancelHandle**します。 同様**SQLCancel**場合は、 **SQLCancelHandle**返します成功した場合、操作が取り消されたわけではありません。 アプリケーションは、操作が取り消されたかどうかを判断するには、もう一度、元の関数を呼び出す必要があります。 **SQLCancelHandle**ステートメント ハンドルまたは接続で非同期操作を取り消すことができます。 使用して**SQLCancelHandle**ステートメントで、操作をキャンセルするハンドルは、呼び出した場合と同じ**SQLCancel**します。  
  
 両方をサポートする必要はありません**SQLCancelHandle**と同時に操作を非同期接続します。 ドライバーは、非同期接続の操作をサポートできますが**SQLCancelHandle**、またはその逆です。  
  
 非同期接続の操作と**SQLCancelHandle** ODBC によっても使用できます 3.x と ODBC 2.x アプリケーションの ODBC 3.8 ドライバーと ODBC 3.8 ドライバー マネージャーを使用します。 以降の ODBC バージョンの新機能を使用する古いアプリケーションを有効にする方法については、次を参照してください。[の互換性対応表](../../../odbc/reference/develop-app/compatibility-matrix.md)します。  
  
### <a name="connection-pooling"></a>接続のプール  
 接続を確立するため、非同期操作が最小限でのみサポートされる接続プールが有効になっているときに (で**SQLConnect**と**SQLDriverConnect**) との接続を閉じると**SQLDisconnect**します。 アプリケーションから SQL_STILL_EXECUTING の戻り値を処理できる必要がありますが、 **SQLConnect**、 **SQLDriverConnect**、および**SQLDisconnect**します。  
  
 接続プールを有効にすると、 **SQLEndTran**と**SQLSetConnectAttr**は非同期操作はサポートされています。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例は、使用する方法を示します**SQLSetConnectAttr**接続関連の関数の非同期実行を有効にします。  
  
### <a name="code"></a>コード  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 この例では、非同期コミット操作が表示されます。 ロールバック操作は、このように実行できます。  
  
### <a name="code"></a>コード  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>参照  
 [ステートメントの実行 (ODBC)](../../../odbc/reference/develop-app/executing-statements-odbc.md)
