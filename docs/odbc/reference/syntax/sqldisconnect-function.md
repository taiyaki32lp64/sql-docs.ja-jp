---
title: SQLDisconnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 788ca2eb7cf37314eb7d5386a23f17123f9ccaff
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343009"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqldisconnect**は、特定の接続ハンドルに関連付けられている接続を閉じます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **Sqldisconnect**によって SQL_ERROR または SQL_SUCCESS_WITH_INFO が返された場合は、SQL_HANDLE_DBC の*Handletype*および*connectionhandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます。 次の表に、 **Sqldisconnect**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01002|切断エラー|切断中にエラーが発生しました。 ただし、切断は成功しました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続が開かれていません|(DM) 引数*Connectionhandle*に指定された接続が開かれていませんでした。|  
|25000|トランザクション状態が無効|引数*Connectionhandle*によって指定された接続の処理中にトランザクションが発生しました。 トランザクションはアクティブのままです。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*Connectionhandle*に対して非同期処理が有効になりました。 関数が呼び出されました。 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)の実行が、 *connectionhandle*で呼び出されました。 次に、 *Connectionhandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、 **Sqlcancelhandle**の実行が完了する前に、マルチスレッドアプリケーションの別のスレッドからの*connectionhandle*でが呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *Connectionhandle*に関連付けられている*StatementHandle*に対して呼び出されましたが、 **sqldisconnect**が呼び出されたときに実行されていました。<br /><br /> (DM) 非同期的に実行する関数 (この1つではない) が*Connectionhandle*に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が、 *connectionhandle*に関連付けられた*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|接続タイムアウト期間は、データソースが要求に応答する前に期限切れになり、接続はアクティブのままになります。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Connectionhandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLBrowseConnect**が SQL_NEED_DATA を返してから別のリターンコードを返す前に、アプリケーションが**sqldisconnect**を呼び出した場合、ドライバーは接続の参照プロセスをキャンセルし、接続を未接続状態に戻します。  
  
 接続ハンドルに関連付けられた不完全なトランザクションがあるときに、アプリケーションが**Sqldisconnect**を呼び出すと、ドライバーは SQLSTATE 25000 (無効なトランザクションの状態) を返します。これは、トランザクションが変更されず、接続がであることを示します。開き. 不完全なトランザクションとは、 **SQLEndTran**でコミットまたはロールバックされていないトランザクションのことです。  
  
 接続に関連付けられているすべてのステートメントを解放する前に、アプリケーションが**Sqldisconnect**を呼び出した場合、ドライバーは、データソースから正常に切断された後に、それらのステートメントと明示的に割り当てられたすべての記述子を解放します。接続します。 ただし、接続に関連付けられている1つ以上のステートメントがまだ非同期で実行されている場合、 **Sqldisconnect**は SQLSTATE 値が HY010 (関数シーケンスエラー) の SQL_ERROR を返します。 また、接続が中断状態の場合、または**sqldisconnect**がによって **正常に取り消された場合、sqldisconnect は、関連付けられているすべてのステートメントと、接続で明示的に割り当てられたすべての記述子を解放します。SQLCancelHandle**。  
  
 アプリケーションが**Sqldisconnect**を使用する方法の詳細については、「[データソースまたはドライバーからの切断](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)」を参照してください。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>プールされた接続からの切断  
 共有環境に対して接続プールが有効になっていて、アプリケーションがその環境の接続で**Sqldisconnect**を呼び出した場合、接続は接続プールに返され、同じ共有を使用して他のコンポーネントでも使用できます。environment.  
  
## <a name="code-example"></a>コード例  
 「[サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)」、「 [SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)」、および「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|データ ソースへの接続|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|コミットまたはロールバック操作の実行|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|接続ハンドルの解放|[SQLFreeConnect 関数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
