---
title: SQLFreeHandle 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e312bcbc6efcb96ff02657b98034f0340ae377dc
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345175"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqlfreehandle**は、特定の環境、接続、ステートメント、または記述子ハンドルに関連付けられているリソースを解放します。  
  
> [!NOTE]
>  この関数は、ハンドルを解放するためのジェネリック関数です。 これは、 **SQLFreeConnect** (接続ハンドルを解放するため) および**sqlfreeenv** (環境ハンドルを解放するため) という ODBC 2.0 関数を置き換えます。 **SQLFreeConnect**と**sqlfreeenv**はどちらも ODBC 3.x で非推奨とさ*れます。* また、 **Sqlfreehandle**は、ステートメントハンドルを解放するために、ODBC 2.0 関数**SQLFreeStmt** (SQL_DROP*オプション*) を置き換えます。 詳細については、「コメント」を参照してください。 Odbc*2.x アプリケーションが*odbc*2.x ドライバーで*動作しているときに、ドライバーマネージャーがこの関数をマップする方法の詳細については、「[アプリケーションの下位互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 代入**Sqlfreehandle**によって解放されるハンドルの型。 次のいずれかの値を指定する必要があります。  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN HANDLE は、ドライバーマネージャーとドライバーによってのみ使用されます。 アプリケーションでは、このハンドルの種類を使用しないでください。 SQL_HANDLE_DBC_INFO_TOKEN の詳細については、「 [ODBC ドライバーでの接続プールの認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)」を参照してください。  
  
 *Handletype*がこれらの値のいずれでもない場合、 **SQLFREEHANDLE**は SQL_INVALID_HANDLE を返します。  
  
 *Handle*  
 代入解放するハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
 **Sqlfreehandle**が SQL_ERROR を返す場合、ハンドルは引き続き有効です。  
  
## <a name="diagnostics"></a>診断  
 **Sqlfreehandle**から SQL_ERROR が返された場合、関連する SQLSTATE 値は、 **sqlfreehandle**が解放しようとしたハンドルの診断データ構造から取得できますが、それ以外の場合はできませんでした。 次の表に、 **Sqlfreehandle**によって通常返される SQLSTATE 値の一覧を示し、この関数のコンテキストでそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) *Handletype*引数は SQL_HANDLE_ENV でしたが、少なくとも1つの接続が割り当てられた状態または接続状態でした。 SQL_HANDLE_DBC の*handletype*を持つ **Sqldisconnect** および**SQLFREEHANDLE**は、SQL_HANDLE_ENV の*Handletype*を使用して**sqlfreehandle**を呼び出す前に、接続ごとに呼び出す必要があります。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_DBC でした。この関数は、接続のために**sqldisconnect**を呼び出す前に呼び出されました。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_DBC でした。 非同期的に実行する関数が*ハンドル*を使用して呼び出されましたが、この関数が呼び出されたときに関数がまだ実行されていました。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_STMT でした。 **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または**SQLSetPos**がステートメントハンドルを使用して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_STMT でした。 非同期的に実行する関数がステートメントハンドルまたは関連付けられた接続ハンドルで呼び出されましたが、この関数が呼び出されたときに関数がまだ実行されていました。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_DESC でした。 関連付けられた接続ハンドルで非同期に実行する関数が呼び出されました。関数は、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlfreehandle**が呼び出される前に、すべての子会社ハンドルとその他のリソースが解放されませんでした。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**sqlmoreresults**が*ハンドル*に関連付けられているいずれかのステートメントハンドルに対して呼び出されました。 *handletype*は SQL_HANDLE_STMT または SQL_HANDLE_DESC に設定されました SQL_PARAM_DATA_ご. この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|*Handletype*引数が SQL_HANDLE_STMT または SQL_HANDLE_DESC でしたが、基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY017|自動的に割り当てられた記述子ハンドルの使い方が正しくありません。|(DM)*ハンドル*引数が、自動的に割り当てられた記述子のハンドルに設定されました。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Handletype*引数は SQL_HANDLE_DESC で、ドライバーは ODBC*2.x ドライバーでし*た。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_STMT で、ドライバーは有効な ODBC ドライバーではありませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlfreehandle**は、次のセクションで説明するように、環境、接続、ステートメント、および記述子のハンドルを解放するために使用されます。 ハンドルに関する一般的な情報については、「[ハンドル](../../../odbc/reference/develop-app/handles.md)」を参照してください。  
  
 アプリケーションが解放された後でハンドルを使用することはできません。ドライバーマネージャーは、関数呼び出しのハンドルの有効性を確認しません。  
  
## <a name="freeing-an-environment-handle"></a>環境ハンドルの解放  
 SQL_HANDLE_ENV の*Handletype*を使用して**sqlfreehandle**を呼び出す前に、アプリケーションは、環境内で割り当てられたすべての接続に対して*handletype* SQL_HANDLE_DBC を指定して**sqlfreehandle**を呼び出す必要があります。 それ以外の場合、 **Sqlfreehandle**を呼び出すと SQL_ERROR が返され、環境とアクティブな接続はすべて有効のままになります。 詳細については、「[環境ハンドル](../../../odbc/reference/develop-app/environment-handles.md)と[環境ハンドルの割り当て](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)」を参照してください。  
  
 環境が共有環境の場合、SQL_HANDLE_ENV の*Handletype*を使用して**sqlfreehandle**を呼び出すアプリケーションは、呼び出し後に環境にアクセスできなくなりますが、環境のリソースは必ずしも解放されません。 **Sqlfreehandle**を呼び出すと、環境の参照カウントが減少します。 参照カウントは、ドライバーマネージャーによって管理されます。 0にならない場合、共有環境は別のコンポーネントによって使用されているため、解放されません。 参照カウントが0になると、共有環境のリソースが解放されます。  
  
## <a name="freeing-a-connection-handle"></a>接続ハンドルの解放  
 SQL_HANDLE_DBC の*Handletype*を使用して**sqlfreehandle**を呼び出す前に、アプリケーションはこのハンドルに接続されている場合、接続に対して**sqldisconnect**を呼び出す必要があり*ます。* それ以外の場合、 **Sqlfreehandle**を呼び出すと SQL_ERROR が返され、接続は有効なままになります。  
  
 詳細については、「[接続ハンドル](../../../odbc/reference/develop-app/connection-handles.md)と[データソースまたはドライバーからの切断](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)」を参照してください。  
  
## <a name="freeing-a-statement-handle"></a>ステートメント ハンドルの解放  
 *Handletype*が SQL_HANDLE_STMT の**sqlfreehandle**を呼び出すと、SQL_HANDLE_STMT の*Handletype*を使用して**SQLAllocHandle**への呼び出しによって割り当てられたすべてのリソースが解放されます。 アプリケーションが**Sqlfreehandle**を呼び出して、保留中の結果を含むステートメントを解放すると、保留中の結果が削除されます。 アプリケーションがステートメントハンドルを解放すると、ドライバーによって自動的に割り当てられた4つの記述子が解放されます。 詳細については[、「ステートメント](../../../odbc/reference/develop-app/statement-handles.md)ハンドルおよび[ステートメントハンドルの解放](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)」を参照してください。  
  
 接続で開かれているステートメントと記述子が**Sqldisconnect**によって自動的に削除されることに注意してください。  
  
## <a name="freeing-a-descriptor-handle"></a>記述子ハンドルの解放  
 SQL_HANDLE_DESC の*Handletype*を使用して**sqlfreehandle**を呼び出すと、*ハンドル*内の記述子ハンドルが解放されます。 **Sqlfreehandle**を呼び出すと、アプリケーションによって割り当てられたメモリが解放されません。これは、の*記述子レコードのポインターフィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR を含む) によって参照される可能性があります。ハンドル*。 ポインターフィールドではないフィールドのドライバーによって割り当てられたメモリは、ハンドルが解放されると解放されます。 ユーザーが割り当てた記述子ハンドルを解放すると、解放されたハンドルに関連付けられていたすべてのステートメントが、自動的に割り当てられた記述子ハンドルに戻されます。  
  
> [!NOTE]
>  ODBC 2.x*ドライバーは*、記述子ハンドルの割り当てをサポートしていないのと同様に、記述子ハンドルの解放をサポートしていません。  
  
 接続で開かれているステートメントと記述子が**Sqldisconnect**によって自動的に削除されることに注意してください。 アプリケーションがステートメントハンドルを解放すると、ドライバーは、そのハンドルに関連付けられている自動的に生成されたすべての記述子を解放します。  
  
 記述子の詳細については、「[記述子](../../../odbc/reference/develop-app/descriptors.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 その他のコードサンプルについては、「 [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) and [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
### <a name="code"></a>コード  
  
```cpp  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|ステートメント処理の取り消し|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|カーソル名の設定|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC のサンプル プログラム](../../../odbc/reference/sample-odbc-program.md)
