---
title: 非同期実行 (通知方法) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66b806b698164b306eee4dc7d4c48fbe7835adae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077061"
---
# <a name="asynchronous-execution-notification-method"></a>非同期実行 (通知方法)
ODBC では、接続とステートメントの操作の非同期実行を許可します。 アプリケーション スレッドで非同期モードで ODBC 関数を呼び出すことができ、操作が完了すると、その他のタスクを実行するアプリケーションのスレッドを許可する前に、関数が返すことができます。 Windows 7 sdk の非同期ステートメントまたは接続操作では、アプリケーションは、非同期操作が完了のポーリング メソッドを使用して決定されます。 詳細については、次を参照してください。[非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)します。 以降、Windows 8 SDK では、非同期操作が通知メソッドを使用して完全なことを確認できます。  
  
 ポーリング メソッドでは、アプリケーションが操作の状態が必要があるたびに、非同期関数を呼び出す必要があります。 通知方法は、コールバックと ADO.NET での待機に似ています。 ODBC では、通知オブジェクトとしてただし、Win32 イベントを使用します。  
  
 ODBC カーソル ライブラリおよび ODBC 非同期通知を同時に使用できません。 両方の属性を設定すると、SQLSTATE S1119 でエラーが返されます (カーソル ライブラリと非同期の通知を有効にできません同時)。  
  
 参照してください[非同期の関数の完了の通知](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md)ドライバー開発者向けの情報にします。  
  
> [!NOTE]  
>  カーソル ライブラリでは、通知方法はサポートされていません。 アプリケーションと通知方法を有効にすると、SQLSetConnectAttr を使用してカーソル ライブラリを有効にするとエラー メッセージが表示されます。  
  
## <a name="overview"></a>概要  
 非同期モードで ODBC 関数が呼び出されると、コントロールが SQL_STILL_EXECUTING のリターン コードですぐに呼び出し元アプリケーションに返されます。 アプリケーションは、関数を SQL_STILL_EXECUTING 以外に返されるまでポーリング繰り返し必要があります。 ポーリング ループでは、多くの非同期のシナリオでパフォーマンスの低下の原因と、CPU 使用率が向上します。  
  
 通知のモデルを使用すると、常にポーリング モデルが無効です。 アプリケーションでは、元の関数を再度呼び出さないでください。 呼び出す[SQLCompleteAsync 関数](../../../odbc/reference/syntax/sqlcompleteasync-function.md)非同期操作を完了します。 呼び出しで SQL_ERROR SQLSTATE IM017 が返す場合、アプリケーションは、非同期操作が完了する前にもう一度、元の関数を呼び出す、(非同期の通知モードでのポーリングは無効です)。  
  
 通知のモデルを使用する場合、アプリケーションを呼び出すことができます**SQLCancel**または**SQLCancelHandle**ステートメントまたは接続の操作をキャンセルします。 取り消し要求が成功した場合、ODBC は SQL_SUCCESS を返します。 このメッセージは、関数が実際にキャンセルされたことを示していませんこれは、キャンセル要求が処理されたことを示します。 関数が実際に取り消されたかどうかは、ドライバーに依存し、データ ソースに依存します。 操作が取り消されたときに、ドライバー マネージャーは引き続きイベントを通知します。 ドライバー マネージャーは、リターン コードのバッファーで SQL_ERROR を返し、状態が SQLSTATE HY008 (操作が取り消されました) を示す、キャンセルに成功しました。 関数には、通常の処理が完了したら、ドライバー マネージャーは SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返します。  
  
### <a name="downlevel-behavior"></a>ダウンレベルの動作  
 完全にこの通知をサポートしている ODBC ドライバー マネージャーのバージョンでは、ODBC 3.81 です。  
  
|アプリケーションの ODBC のバージョン|ドライバー マネージャーのバージョン|ドライバーのバージョン|動作|  
|------------------------------|----------------------------|--------------------|--------------|  
|任意の ODBC バージョンの新しいアプリケーション|ODBC 3.81|3\.80 の ODBC ドライバー|それ以外の場合、ドライバー マネージャーはエラーになります、ドライバーは、この機能をサポートしている場合、アプリケーションはこの機能を使用できます。|  
|任意の ODBC バージョンの新しいアプリケーション|ODBC 3.81|3\.80 の以前の ODBC ドライバー|ドライバー マネージャー、ドライバーはこの機能をサポートしていないをエラーになります。|  
|任意の ODBC バージョンの新しいアプリケーション|プレ ODBC 3.81|Any|アプリケーションでは、この機能を使用して、古いドライバー マネージャーがドライバー固有の属性として、新しい属性をとらえますドライバーにエラーが発生する必要があります。新しいドライバー マネージャーがドライバーにこれらの属性を渡しません。|  
  
 アプリケーションでは、この機能を使用する前に、ドライバー マネージャーのバージョンを確認する必要があります。 それ以外の場合、不完全ドライバーがエラーではなくは、ドライバー マネージャーのバージョンが以前の ODBC 3.81、動作は定義されません。  
  
## <a name="use-cases"></a>ユース ケース  
 このセクションでは、非同期実行し、ポーリング メカニズムの使用例を示します。  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>複数の ODBC ソースからデータを統合します。  
 データ統合アプリケーションは、複数のデータ ソースから非同期的にデータをフェッチします。 リモート データ ソースからデータの一部は、いくつかのデータはローカル ファイルから. アプリケーションは、非同期操作が完了するまで続行できません。  
  
 完了するための操作を繰り返しポーリングではなく、アプリケーションでイベント オブジェクトを作成および ODBC 接続ハンドルまたは ODBC ステートメント ハンドルに関連付けること。 その後、アプリケーションでは、オペレーティング システムの同期イベントを 1 つ以上の多くのイベント オブジェクト (ODBC のイベントとその他の Windows イベントの両方) 上で待機する Api を呼び出します。 ODBC は、対応する ODBC 非同期操作が完了したときに、イベント オブジェクトに通知します。  
  
 Windows、Win32 イベント オブジェクトが使用され、統一されたプログラミング モデルが提供します。 その他のプラットフォーム上のドライバー マネージャーは、これらのプラットフォームに固有のイベント オブジェクトの実装を使用できます。  
  
 次のコード サンプルでは、接続とステートメントの非同期通知の使用を示しています。  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>ドライバーが非同期通知をサポートしているかを決定します。  
 ODBC アプリケーションが呼び出すことによって、ODBC ドライバーが非同期通知をサポートしているかを判断することができます[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)します。 ODBC ドライバー マネージャーを呼び出す、その結果、 **SQLGetInfo** SQL_ASYNC_NOTIFICATION とドライバーの。  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>ODBC ハンドルを Win32 イベント ハンドルを関連付ける  
 アプリケーションは、対応する Win32 関数を使用して Win32 イベント オブジェクトを作成する責任を負います。 アプリケーションでは、1 つの ODBC 接続ハンドルや ODBC ステートメント ハンドルの 1 つで 1 つの Win32 イベント ハンドルを関連付けることができます。  
  
 接続属性 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE および SQL_ATTR_ASYNC_DBC_EVENT は、ODBC が非同期モードで実行するかどうかと、ODBC 接続ハンドルの通知モードを有効にするかどうかを決定します。 SQL_ATTR_ASYNC_ENABLE と SQL_ATTR_ASYNC_STMT_EVENT ステートメント属性は、ODBC が非同期モードで実行するかどうかと、ODBC ステートメント ハンドルの通知モードを有効にするかどうかを決定します。  
  
|SQL_ATTR_ASYNC_ENABLE または SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT または SQL_ATTR_ASYNC_DBC_EVENT|モード|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|[有効化]|null 以外|非同期通知|  
|[有効化]|null|非同期ポーリング|  
|Disable|any|同期|  
  
 アプリケーションは、非同期の操作モードを無効に一時的にできます。 ODBC では、接続レベルの非同期操作が無効になっている場合、SQL_ATTR_ASYNC_DBC_EVENT の値が無視されます。 ODBC では、ステートメント レベルの非同期操作が無効になっている場合、SQL_ATTR_ASYNC_STMT_EVENT の値が無視されます。  
  
 同期呼び出しの**SQLSetStmtAttr**と**SQLSetConnectAttr**  
 -   **SQLSetConnectAttr**非同期操作の呼び出しでは、 **SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_EVENT を設定するのには同期では常にします。  
  
-   **SQLSetStmtAttr**非同期実行をサポートしていません。  
  
 エラー アウト シナリオ  
 ときに**SQLSetConnectAttr**接続をドライバー マネージャーは使用するドライバーを特定できませんを行う前に呼び出されます。 そのため、ドライバー マネージャーがの成功を返します**SQLSetConnectAttr**が属性が、ドライバーで設定する準備ができていない可能性があります。 ドライバー マネージャーは、アプリケーションが接続関数を呼び出すときにこれらの属性を設定します。 ドライバー マネージャーには、ドライバーでは、非同期操作をサポートしていないため、エラー出力が可能性があります。  
  
 接続属性の継承  
 通常、接続のステートメントは、接続属性を継承します。 ただし、SQL_ATTR_ASYNC_DBC_EVENT 属性は継承できませんし、接続操作にのみ影響します。  
  
 ODBC 接続ハンドルにイベント ハンドルを関連付けるには、ODBC アプリケーションは ODBC API を呼び出します。 **SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_EVENT を属性の値として処理する属性と、イベントを指定します。 新しい ODBC 属性 SQL_ATTR_ASYNC_DBC_EVENT は型 SQL_IS_POINTER です。  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 通常、アプリケーションは、自動リセット イベント オブジェクトを作成します。 ODBC では、イベント オブジェクトはリセットされません。 アプリケーションで必要があります、あるオブジェクトはシグナル状態に非同期 ODBC 関数を呼び出す前に確認します。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT は、ドライバー マネージャー専用の属性で、ドライバーでは設定されません。  
  
 SQL_ATTR_ASYNC_DBC_EVENT の既定値は、NULL です。 取得または設定 SQL_ATTR_ASYNC_DBC_EVENT が SQLSTATE HY092 SQL_ERROR を返します、ドライバーが非同期通知をサポートしていない場合 (無効な属性またはオプション識別子)。  
  
 ODBC 接続ハンドルが NULL でないと、アプリケーション SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE SQL_ASYNC_DBC_ENABLE_ON、任意の ODBC 接続を呼び出すことで属性を設定して非同期モードを有効になっている SQL_ATTR_ASYNC_DBC_EVENT の最後の値の設定の場合非同期モードをサポートしている関数の完了通知が表示されます。 ODBC 接続ハンドルで設定された最後 SQL_ATTR_ASYNC_DBC_EVENT 値が NULL の場合は、ODBC は送信しません、アプリケーション、任意の通知に関係なく非同期モードが有効になっているかどうか。  
  
 アプリケーションは前に、または SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 属性を設定した後、SQL_ATTR_ASYNC_DBC_EVENT を設定できます。  
  
 アプリケーションは接続関数を呼び出す前に ODBC 接続ハンドルの SQL_ATTR_ASYNC_DBC_EVENT 属性を設定することができます (**SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**)。 ODBC ドライバー マネージャーが、アプリケーションで使用する ODBC ドライバーを知らないので、SQL_SUCCESS が返されます。 アプリケーションが接続関数を呼び出すと、ODBC ドライバー マネージャーは、ドライバーが非同期通知をサポートしているかどうかを確認します。 ドライバーが非同期通知をサポートしていない場合、ODBC ドライバー マネージャーは SQLSTATE S1_118 SQL_ERROR を返します (ドライバーは非同期通知をサポートしていません)。 ドライバーは、非同期通知をサポートする場合、ODBC ドライバー マネージャーがドライバーを呼び出すし、SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK と SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT に対応する属性を設定します。  
  
 アプリケーションを呼び出すと同様に、 **SQLSetStmtAttr** ODBC ステートメントで処理し、有効またはステートメント レベルの非同期通知を無効にする SQL_ATTR_ASYNC_STMT_EVENT 属性を指定します。 接続が確立されると、常にステートメントの関数が呼び出されるため**SQLSetStmtAttr** SQLSTATE S1_118 SQL_ERROR が返されます (ドライバーは非同期通知をサポートしていない) 場合にすぐに、対応します。ドライバーは非同期操作をサポートしていないか、ドライバーは、非同期操作をサポートしていますが、非同期通知をサポートしていません。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT で、NULL に設定することができますは、ドライバー マネージャー専用の属性で、ドライバーでは設定されません。  
  
 SQL_ATTR_ASYNC_STMT_EVENT の既定値は、NULL です。 取得または設定 SQL_ATTR_ASYNC_ STMT_EVENT 属性が SQLSTATE HY092 SQL_ERROR を返します、ドライバーが非同期通知をサポートしていない場合 (無効な属性またはオプション識別子)。  
  
 アプリケーションは、ODBC ハンドルの 1 つ以上を同じイベント ハンドルを関連付けないでする必要があります。 それ以外の場合、同じイベント ハンドルを共有する 2 つのハンドルに 2 つの非同期の ODBC 関数呼び出しを完了すると、1 つの通知は失われます。 接続ハンドルから、同じイベント ハンドルを継承する、ステートメント ハンドルを避けるためには、ODBC は、アプリケーションは、接続ハンドルの SQL_ATTR_ASYNC_STMT_EVENT を設定する場合 (接続ハンドルにステートメント属性を設定できません)、SQLSTATE IM016 SQL_ERROR を返します。  
  
### <a name="calling-asynchronous-odbc-functions"></a>非同期の ODBC 関数を呼び出し  
 非同期通知を有効にすると、非同期操作を開始、アプリケーションは、任意の ODBC 関数を呼び出すことができます。 非同期操作をサポートする関数のセットに属する場合、アプリケーションまたは表示されます完了通知、操作が完了したら、関数が失敗したかどうかに関係なくに成功しました。  唯一の例外は、アプリケーションが無効な接続やステートメント ハンドルで ODBC 関数を呼び出します。 この場合は、ODBC がイベント ハンドルを取得しない、およびシグナル状態に設定されます。  
  
 アプリケーションは、対応する ODBC ハンドルでの非同期操作を開始する前に、関連付けられているイベント オブジェクトが、非シグナル状態にことを確認する必要があります。 ODBC では、イベント オブジェクトはリセットされません。  
  
### <a name="getting-notification-from-odbc"></a>ODBC からの通知の取得  
 アプリケーション スレッドを呼び出すことができます**WaitForSingleObject** 1 つのイベントのハンドルまたは呼び出しの待機に**WaitForMultipleObjects**イベント ハンドルの配列を待機し、1 つまたはすべてのイベント オブジェクトまで中断されますシグナル状態になるか、タイムアウト間隔が経過しました。  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
