---
title: SQLFreeStmt 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6141f3efe357bfb3f14c04aa2f6760e9470649a6
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345149"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ISO 92  
  
 **まとめ**  
 **SQLFreeStmt**は、特定のステートメントに関連付けられている処理を停止し、ステートメントに関連付けられている開いているカーソルを閉じるか、保留中の結果を破棄します  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル  
  
 *Option*  
 代入次のいずれかのオプションを選択します。  
  
 SQL_ CLOSE:*StatementHandle*に関連付けられているカーソルを閉じ (定義されている場合)、保留中のすべての結果を破棄します。 アプリケーションでは、同じまたは異なるパラメーター値を使用して**SELECT**ステートメントを再実行することにより、後でこのカーソルを再度開くことができます。 カーソルが開いていない場合、このオプションはアプリケーションには影響しません。 カーソルを閉じるには、 **Sqlcloセキュリティー**を呼び出すこともできます。 詳細については、「[カーソルを閉じる](../../../odbc/reference/develop-app/closing-the-cursor.md)」を参照してください。  
  
 SQL_DROP:このオプションは非推奨とされます。 SQL_DROP の*オプション*を指定して**SQLFreeStmt**を呼び出すと、ドライバーマネージャーで[sqlfreehandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)にマップされます。  
  
 SQL_UNBIND:の SQL_DESC_COUNT フィールドを0に設定し、指定した*StatementHandle*の**SQLBindCol**によってバインドされているすべての列バッファーを解放します。 この場合、ブックマーク列はバインド解除されません。これを行うには、[ブックマーク] 列の SQL_DESC_DATA_PTR フィールドを NULL に設定します。 この操作は、複数のステートメントによって共有される明示的に割り当てられた記述子に対して実行される場合、この操作は、記述子を共有するすべてのステートメントのバインドに影響します。 詳細については、「[結果の取得の概要 (基本)](../../../odbc/reference/develop-app/retrieving-results-basic.md)」を参照してください。  
  
 SQL_RESET_PARAMS:APD の SQL_DESC_COUNT フィールドを0に設定し、指定した*StatementHandle*の**SQLBindParameter**によって設定されたすべてのパラメーターバッファーを解放します。 複数のステートメントによって共有される明示的に割り当てられた記述子に対してこの操作を実行すると、この操作は、記述子を共有するすべてのステートメントのバインドに影響します。 詳細については、「[バインドパラメーター](../../../odbc/reference/develop-app/binding-parameters-odbc.md)」を参照してください。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLFreeStmt**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、 *handletype* SQL_HANDLE_STMT と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **SQLFreeStmt**によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **SQLFreeStmt**が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が*STATEMENTHANDLE*に対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータを取得する前に、*オプション*を SQL_RESET_PARAMS に設定して呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が*StatementHandle*に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY092|オプションの型が有効範囲にありません|(DM) 引数*オプション*に指定された値が次の値ではありませんでした:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 SQL_CLOSE オプションを指定して**SQLFreeStmt**を呼び出すことは、 **sqlcloを**呼び出すことと同じです。ただし、ステートメントでカーソルが開かれていない場合、 **SQLFreeStmt** with SQL_CLOSE はアプリケーションに影響しません。 カーソルが開いていない場合は、 **Sqlcloを**呼び出すと SQLSTATE 24000 (無効なカーソル状態) が返されます。  
  
 アプリケーションが解放された後に、ステートメントハンドルを使用することはできません。ドライバーマネージャーは、関数呼び出しのハンドルの有効性を確認しません。  
  
## <a name="example"></a>例  
 ハンドルを解放するのに適したプログラミング手法です。 ただし、わかりやすくするために、次のサンプルには、割り当てられたハンドルを解放するコードは含まれていません。 ハンドルを解放する方法の例については、「 [Sqlfreehandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)」を参照してください。  
  
```cpp  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|ステートメント処理の取り消し|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|カーソルを閉じる|[SQLCloseCursor 関数](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|カーソル名の設定|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
