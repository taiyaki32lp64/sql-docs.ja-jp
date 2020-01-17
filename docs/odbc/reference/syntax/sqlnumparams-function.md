---
title: SQLNumParams 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumParams
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLNumParams
helpviewer_keywords:
- SQLNumParams function [ODBC]
ms.assetid: dbf2da44-253b-4094-bd6b-29bafc23c7a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 171c40ad53f62abc8541bf449e368fd22419644e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343496"
---
# <a name="sqlnumparams-function"></a>SQLNumParams 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:ISO 92  
  
 **まとめ**  
 **Sqlnumparams**は、SQL ステートメント内のパラメーターの数を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLNumParams(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ParameterCountPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 代入ステートメントハンドル。  
  
 *ParameterCountPtr*  
 Outputステートメント内のパラメーターの数を返すバッファーへのポインター。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlnumparams**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、SQL_HANDLE_STMT の*Handletype*と*StatementHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます。 次の表に、 **Sqlnumparams**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*StatementHandle*に対して非同期処理が有効になりました。 **Sqlnumparams**関数が呼び出され、実行が完了する前に、 **SQLCancel**または**sqlnumparams**が*StatementHandle*で呼び出されました。その後、 *StatementHandle*で**sqlnumparams**関数が再度呼び出されました。<br /><br /> または、 **Sqlnumparams**関数が呼び出され、実行が完了する前に、マルチスレッドアプリケーションの別のスレッドの*StatementHandle*で**SQLCancel**または**sqlnumparams**が呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 関数は、 *StatementHandle*の**SQLPrepare**または**SQLExecDirect**を呼び出す前に呼び出されました。<br /><br /> (DM) 非同期的に実行する関数が、 *StatementHandle*に関連付けられている接続ハンドルに対して呼び出されました。 この非同期関数は、 **Sqlnumparams**関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が*StatementHandle*に対して呼び出され、この関数が呼び出されたときにまだ実行されています。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が*StatementHandle*に対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *StatementHandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
 **Sqlnumparams**は、 **SQLPrepare**が呼び出された後にのみ呼び出すことができます。  
  
 *StatementHandle*に関連付けられたステートメントにパラメーターが含まれていない場合、 **sqlnumparams**は **parametercountptr*を0に設定します。  
  
 **Sqlnumparams**によって返されるパラメーターの数は、IPD の SQL_DESC_COUNT フィールドと同じ値になります。  
  
 詳細については、「[パラメーターの説明](../../../odbc/reference/develop-app/describing-parameters.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドする|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメント内のパラメーターに関する情報を返す|[SQLDescribeParam 関数](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
