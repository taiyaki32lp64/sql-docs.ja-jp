---
title: SQLCancel 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 94f823cdefe4b3e5a62beb62062356dad3a88a03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036117"
---
# <a name="sqlcancel-function"></a>SQLCancel 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLCancel**ステートメントで処理を取り消します。  
  
 使用して、接続やステートメントの処理をキャンセルする[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLCancel** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLCancel** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)引数 *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLCancel**関数が呼び出されました。<br /><br /> (DM) 操作に失敗しました、非同期操作が実行中に関連付けられている接続ハンドルをキャンセル*StatementHandle*します。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY018|キャンセル要求を拒否されたサーバー|サーバーは、キャンセル要求を拒否します。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 **SQLCancel**次の種類のステートメントで処理を取り消すことができます。  
  
-   ステートメントで非同期的に実行されている関数。  
  
-   データを必要があるステートメントでの関数。  
  
-   別のスレッドでのステートメントで実行する関数。  
  
 ODBC 2。*x*アプリケーションを呼び出す場合は、 **SQLCancel**場合、ステートメントの処理は行われません**SQLCancel**と同じ効果**SQLFreeStmt** SQL_CLOSE オプション。この動作は完全を期すのためだけ定義され、アプリケーションを呼び出す必要があります**SQLFreeStmt**または**SQLCloseCursor**カーソルを閉じます。  
  
 ときに**SQLCancel**ニーズ データ、取り消される関数によって投稿された診断レコードがオフになっているステートメントで関数またはステートメントで非同期的に実行する関数を取り消すために呼び出されると**SQLCancel**独自の診断レコードを投稿するときに**SQLCancel**が別のスレッドでのステートメントで実行されている関数を取り消す場合に、ただしは消去されません、診断と呼ばれる関数とがないキャンセル中のレコード独自の診断レコードを投稿します。  
  
## <a name="canceling-asynchronous-processing"></a>非同期処理のキャンセル  
 アプリケーションでは、関数を非同期的に呼び出す後、は、処理が終了したかどうか確認するには、繰り返し関数を呼び出します。 関数がまだ処理中、SQL_STILL_EXECUTING が返されます。 関数が処理を完了している場合は、さまざまなコードを返します。  
  
 すべての呼び出しを SQL_STILL_EXECUTING を返す関数に、アプリケーションを呼び出すことが**SQLCancel**関数をキャンセルします。 取り消し要求が成功した場合、ドライバーは SQL_SUCCESS を返します。 このメッセージは、関数が実際にキャンセルされたことを示していませんこれは、キャンセル要求が処理されたことを示します。 か、関数が実際に取り消されたかどうかは、ドライバーに依存し、データ ソースに依存します。 リターン コードが SQL_STILL_EXECUTING されるまで、元の関数を呼び出すアプリケーションを続行する必要があります。 関数が正常に取り消された場合、戻り値のコードは SQL_ERROR と SQLSTATE HY008 (操作が取り消されました)。 関数には、通常の処理が完了したら場合、戻り値のコードは SQL_SUCCESS や関数が成功した場合、SQL_SUCCESS_WITH_INFO または SQL_ERROR HY008 以外の SQLSTATE (操作が取り消されました)、関数が失敗した場合。  
  
> [!NOTE]  
>  ODBC 3.5 への呼び出しで**SQLCancel**と処理は行われません、ステートメントとして扱われません**SQLFreeStmt**が SQL_CLOSE のオプションで影響をまったくはありません。 カーソルを閉じるには、アプリケーションを呼び出す必要があります**SQLCloseCursor**ではなく、 **SQLCancel**します。  
  
 非同期処理の詳細については、次を参照してください。[非同期実行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)します。  
  
## <a name="canceling-functions-that-need-data"></a>データを必要とする関数のキャンセル  
 後**SQLExecute**または**SQLExecDirect** SQL_NEED_DATA を返しますのすべての実行時データ パラメーター データを送信すると、前に、アプリケーションを呼び出すことができます**SQLCancel**ステートメントの実行をキャンセルします。 ステートメントが取り消され、アプリケーションを呼び出すことが**SQLExecute**または**SQLExecDirect**もう一度です。 詳細については、次を参照してください。 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)します。  
  
 後**SQLBulkOperations**または**SQLSetPos** SQL_NEED_DATA を返しますのすべての実行時データ列のデータが送信されたアプリケーションを呼び出すことができます、 **SQLCancel**操作をキャンセルします。 操作が取り消され、アプリケーションを呼び出すことが**SQLBulkOperations**または**SQLSetPos**もう一度; 取り消すには影響しません、カーソルの状態または現在のカーソル位置。 詳細については、次を参照してください。 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)または[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>別のスレッドで実行されている関数のキャンセル  
 マルチ スレッド アプリケーションでは、アプリケーションは、別のスレッドで実行されている関数をキャンセルできます。 関数では、アプリケーション呼び出しをキャンセルする**SQLCancel**対象の関数によって、別のスレッドで使用すると同じステートメント ハンドルを使用します。 関数の取り消し方法は、ドライバーとオペレーティング システムによって異なります。 キャンセルのリターン コードを非同期的に実行されている関数のように、 **SQLCancel**のみに、ドライバーが正常に要求を処理するかどうかを示します。 SQL_SUCCESS や SQL_ERROR のみが返されることができます。診断情報は返されません。 SQLSTATE HY008、SQL_ERROR を返しますが、元の関数が取り消された場合 (操作が取り消されました)。  
  
 SQL ステートメントの中の場合は実行すると実行**SQLCancel**はステートメントの実行をキャンセルする別のスレッドで呼び出されるを正常に実行可能であり、キャンセル中に戻り値に関係なく SQL_SUCCESS も成功します。 この場合、ドライバー マネージャーは、ため、アプリケーションは、カーソルを使用できない、キャンセル、ステートメントの実行によって開かれたカーソルが閉じられることを前提とします。  
  
 スレッド処理の詳細については、次を参照してください。[マルチ スレッド](../../../odbc/reference/develop-app/multithreading.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーをパラメーターにバインドします。|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|実行する一括挿入または更新操作|[SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|関数を実行して非同期的に、接続ハンドルでさらの機能にキャンセル**SQLCancel**します。|[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|ステートメント ハンドルの解放|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|診断レコードのフィールドまたは診断のヘッダーのフィールドを取得します。|[SQLGetDiagField 関数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|診断データの構造体の複数のフィールドを取得します。|[SQLGetDiagRec 関数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|実行時にパラメーターのデータを送信します。|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|行セットのカーソルを配置する、行セットのデータの更新や更新、または、結果セット内のデータを削除します。|[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
