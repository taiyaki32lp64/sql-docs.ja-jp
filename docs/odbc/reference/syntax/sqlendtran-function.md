---
title: SQLEndTran 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98a0f072af79c2c6e39d0cfc49e72cbeef1c2193
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344768"
---
# <a name="sqlendtran-function"></a>SQLEndTran 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **SQLEndTran**は、接続に関連付けられているすべてのステートメントに対するすべてのアクティブな操作に対して、コミットまたはロールバックの操作を要求します。 **SQLEndTran**は、環境に関連付けられているすべての接続に対して、コミットまたはロールバックの操作を実行するように要求することもできます。  
  
> [!NOTE]  
>  ドライバーマネージャーが ODBC 3 でこの関数をマップする方法の詳細については、「」を参照してください。*x*アプリケーションは ODBC 2 で動作しています。*x*ドライバー、「[アプリケーションの旧バージョンとの互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 代入ハンドル型識別子。 SQL_HANDLE_ENV ( *handle*が環境ハンドルの場合) または SQL_HANDLE_DBC (*ハンドル*が接続ハンドルの場合) のいずれかが含まれます。  
  
 *Handle*  
 代入*Handletype*によって示される型のハンドル。トランザクションのスコープを示します。 詳細については、「コメント」を参照してください。  
  
 *入力型*  
 代入次の2つの値のいずれかです。  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診断  
 **SQLEndTran**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、適切な*Handletype*と*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連する SQLSTATE 値を取得できます。 次の表に、 **SQLEndTran**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続が開かれていません|(DM) *Handletype*が SQL_HANDLE_DBC で、*ハンドル*が connected 状態ではありませんでした。|  
|08007|トランザクション中の接続エラー|*Handletype*が SQL_HANDLE_DBC で、*ハンドル*に関連付けられている接続が関数の実行中に失敗しました。また、要求された**コミット**または**ロールバック**がの前に発生したかどうかを判断できません。不具合.|  
|25S01|トランザクションの状態が不明です|*ハンドル*内の1つ以上の接続が、指定された結果でトランザクションを完了できませんでした。結果は不明です。|  
|25S02|トランザクションはまだアクティブです|ドライバーは、グローバルトランザクション内のすべての作業がアトミックに完了し、トランザクションがアクティブであることを保証できませんでした。|  
|25S03|トランザクションがロールバックされます|ドライバーは、グローバルトランザクション内のすべての作業をアトミックに完了できることを保証できませんでした。また、*ハンドル*でアクティブになっているトランザクション内のすべての作業がロールバックされました。|  
|40001|シリアル化エラー|リソースが別のトランザクションでデッドロックしているため、トランザクションがロールバックされました。|  
|40002|整合性制約違反|*入力型*は SQL_COMMIT でしたが、変更のコミットメントによって整合性制約違反が発生しました。 その結果、トランザクションがロールバックされました。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Szmessagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|*Connectionhandle*に対して非同期処理が有効になりました。 関数が呼び出され、 [Sqlcancelhandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)の実行が完了する前に、 *connectionhandle*でが呼び出されました。 次に、 *Connectionhandle*で関数が再度呼び出されました。<br /><br /> 関数が呼び出され、 **Sqlcancelhandle**の実行が完了する前に、マルチスレッドアプリケーションの別のスレッドからの*connectionhandle*でが呼び出されました。|  
|HY010|関数のシーケンスエラー|(DM) 非同期的に実行する関数が、 *Connectionhandle*に関連付けられているステートメントハンドルに対して呼び出されましたが、 **SQLEndTran**が呼び出されたときにまだ実行されていました。<br /><br /> (DM) 非同期的に実行する関数 (この1つではない) が*Connectionhandle*に対して呼び出されましたが、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **Sqlbulkoperations**、または**SQLSetPos**が、 *connectionhandle*に関連付けられたステートメントハンドルに対して呼び出され、SQL_NEED_DATA が返されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) 非同期的に実行されている関数 (この1つではない) が、 *Handletype*が SQL_HANDLE_DBC に設定されていて、この関数が呼び出されたときに実行中だった*ハンドル*に対して呼び出されました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が、 *Handle*に関連付けられたステートメントハンドルの1つに対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY012|無効なトランザクション操作コード|(DM) 引数の*種類*に指定された値は、SQL_COMMIT でも SQL_ROLLBACK でもありません。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY092|属性またはオプションの識別子が無効です|(DM) 引数*Handletype*に指定された値は、SQL_HANDLE_ENV でも SQL_HANDLE_DBC でもありませんでした。|  
|HY115|非同期関数実行が有効になっている接続を含む環境では、SQLEndTran は許可されていません|接続関数の非同期実行が環境内の接続に対して有効になっている場合、(DM) *Handletype*を SQL_HANDLE_ENV に設定することはできません。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、このトピックの「コメント」セクションを参照してください。|  
|HYC00|省略可能な機能は実装されていません|ドライバーまたはデータソースでは、**ロールバック**操作はサポートされていません。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Connectionhandle*に関連付けられているドライバーでは、関数はサポートされていません。|  
|IM017|非同期通知モードでは、ポーリングは無効になっています|通知モデルが使用されるたびに、ポーリングは無効になります。|  
|IM018|**Sqlcompleteasync**は、このハンドルで前の非同期操作を完了するために呼び出されていません。|ハンドルに対する前の関数呼び出しで SQL_STILL_EXECUTING が返され、通知モードが有効になっている場合は、処理を完了するために、ハンドルで**Sqlcompleteasync**を呼び出して、操作を完了する必要があります。|  
  
## <a name="comments"></a>コメント  
 ODBC 3 の場合。*x*ドライバー。 *HANDLETYPE*が SQL_HANDLE_ENV で、 *handle*が有効な環境ハンドルである場合、ドライバーマネージャーは環境に関連付けられている各ドライバーで**SQLEndTran**を呼び出します。 ドライバーの呼び出しの*ハンドル*引数は、ドライバーの環境ハンドルになります。 ODBC 2 の場合。*x*ドライバー。 *HANDLETYPE*が SQL_HANDLE_ENV で、 *HANDLE*が有効な環境ハンドルであり、その環境で接続された状態に複数の接続が存在する場合、ドライバーマネージャーはドライバーで**sqltransact**を呼び出します。接続された状態では、その環境で1回。 各呼び出しの*handle*引数は、接続のハンドルになります。 どちらの場合も、ドライバーは、その環境で接続された状態にあるすべての接続について、*完了の値*に応じてトランザクションのコミットまたはロールバックを試行します。 アクティブでない接続は、トランザクションに影響しません。  
  
> [!NOTE]  
>  **SQLEndTran**を使用して、共有環境でトランザクションをコミットまたはロールバックすることはできません。 **SQLEndTran**が呼び出されると、共有環境のハンドルまたは共有環境上の接続のハンドルのいずれか*に設定さ*れている場合、SQLSTATE HY092 (無効な属性/オプション識別子) が返されます。  
  
 ドライバーマネージャーは、接続ごとに SQL_SUCCESS を受信した場合にのみ、SQL_SUCCESS を返します。 ドライバーマネージャーは、1つまたは複数の接続で SQL_ERROR を受信すると、SQL_ERROR をアプリケーションに返し、診断情報は環境の診断データ構造に配置されます。 コミットまたはロールバック操作中に失敗した接続または接続を調べるために、アプリケーションは接続ごとに**SQLGetDiagRec**を呼び出すことができます。  
  
> [!NOTE]  
>  ドライバーマネージャーは、すべての接続にわたってグローバルトランザクションをシミュレートするわけではないため、2フェーズコミットプロトコルを使用しません。  
  
 SQL_COMMIT は、*入力*候補がの場合、影響を受ける接続に関連付けられているすべてのステートメントで、すべてのアクティブな操作に対するコミット要求**を発行し**ます。 SQL_ROLLBACK*の場合、* **SQLEndTran**は、影響を受ける接続に関連付けられているすべてのアクティブな操作に対して、ロールバック要求を発行します。 アクティブなトランザクションがない場合、 **SQLEndTran**は、どのデータソースにも影響を与えずに SQL_SUCCESS を返します。 詳細については、「[トランザクションのコミットとロールバック](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)」を参照してください。  
  
 ドライバーが手動コミットモード (SQL_ATTR_AUTOCOMMIT 属性が SQL_AUTOCOMMIT_OFF に設定された**SQLSetConnectAttr**を呼び出すことによって) の場合、トランザクション内に含めることができる SQL ステートメントが暗黙的に開始されます。現在のデータソースに対して実行されます。 詳細については、「[コミットモード](../../../odbc/reference/develop-app/commit-mode.md)」を参照してください。  
  
 トランザクション操作がカーソルに与える影響を決定するために、アプリケーションは SQL_CURSOR_ROLLBACK_BEHAVIOR オプションと SQL_CURSOR_COMMIT_BEHAVIOR オプションを使用して**SQLGetInfo**を呼び出します。 詳細については、次の段落を参照してください。また、[カーソルおよび準備されたステートメントに対するトランザクションの影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)についても説明します。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR または SQL_CURSOR_COMMIT_BEHAVIOR の値が SQL_CB_DELETE の場合、 **SQLEndTran**は、接続に関連付けられているすべてのステートメントで開いているすべてのカーソルを閉じて削除し、すべての保留中の結果を破棄します。 **SQLEndTran**は、割り当てられた (準備されていない) 状態にあるすべてのステートメントを残します。アプリケーションは、後続の SQL 要求に再利用できます。または、SQL_HANDLE_STMT の*Handletype*を使用して**SQLFreeStmt**または**sqlfreehandle**を呼び出して、割り当てを解除することができます。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR または SQL_CURSOR_COMMIT_BEHAVIOR の値が SQL_CB_CLOSE の場合、 **SQLEndTran**は、接続に関連付けられているすべてのステートメントで開いているすべてのカーソルを閉じます。 **SQLEndTran**は、準備された状態にあるすべてのステートメントを残します。アプリケーションでは、最初に**SQLPrepare**を呼び出さなくても、接続に関連付けられているステートメントに対して**sqlexecute**を呼び出すことができます。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 値または SQL_CURSOR_COMMIT_BEHAVIOR 値が SQL_CB_PRESERVE と等しい場合、 **SQLEndTran**は接続に関連付けられた開いているカーソルには影響しません。 カーソルは、 **SQLEndTran**の呼び出しの前にポインターがある行にとどまります。  
  
 トランザクションをサポートするドライバーとデータソースの場合、トランザクションがアクティブでないときに SQL_COMMIT または SQL_ROLLBACK を指定して**SQLEndTran**を呼び出すと、SQL_SUCCESS (コミットまたはロールバックする作業がないことを示す) が返され、には影響しません。データソース。  
  
 ドライバーが自動コミットモードの場合、ドライバーマネージャーはドライバーで**SQLEndTran**を呼び出しません。 **SQLEndTran**は、SQL_COMMIT または SQL_ROLLBACK の*型*を使用して呼び出されているかどうかに関係なく、常に SQL_SUCCESS を返します。  
  
 トランザクションをサポートしていないドライバーまたはデータソース (**SQLGetInfo** *OPTION* SQL_TXN_CAPABLE は SQL_TC_NONE) は実質的にオートコミットモードであるため、SQL_SUCCESS がSQL_COMMIT または SQL_ROLLBACK の*入力型*を使用して呼び出されます。 このようなドライバーやデータソースは、要求されたときにトランザクションをロールバックしません。  
  
## <a name="suspended-state"></a>中断状態  
 Windows 7 より前にリリースされたドライバーマネージャーでは、 **SQLEndTran**がドライバーから SQL_ERROR を返した場合、トランザクションはアクティブでした。 ただし、トランザクションがサーバー上で正常にコミットされたが、クライアント上のドライバーが通知されていない可能性があります (たとえば、ネットワークエラーが発生したため)。 これにより、接続が正しくない状態のままになります。 Windows 7 以降では、 **SQLEndTran**が SQL_ERROR を返したときに、接続が中断状態になっている可能性があります。 中断された状態では、読み取り専用関数を呼び出すことができます。 最終的には、アプリケーションは中断された接続で**Sqldisconnect**を呼び出してリソースを解放する必要があります。  
  
 次のすべての条件に該当する場合、接続は中断状態になります。  
  
-   ドライバーは**SQLEndTran**から SQL_ERROR を返します。  
  
-   ドライバーは ODBC バージョン3.8 以降です。  
  
-   アプリケーションのバージョンは3.8 以降です。または、再コンパイルされた ODBC 2.x または2.x アプリケーションは、 **Sqlcancelhandle**を使用して**SQLEndTran**関数を正常に取り消しました。  
  
-   ドライバーが次のメッセージのいずれかを返しませんでした。トランザクションが完了していないことを確認します。  
  
    -   25S03:トランザクションがロールバックされます  
  
    -   40001:シリアル化エラー  
  
    -   40002:整合性の制約  
  
    -   HYC00:省略可能な機能は実装されていません  
  
 環境ハンドルで**SQLEndTran**が呼び出され、その接続のいずれかが上記の条件を満たしている場合、同じドライバーに接続しているすべての接続が中断状態になります。  
  
 アプリケーションが中断された接続で**Sqldisconnect**を呼び出した後、接続を使用して別のデータソースまたは同じデータソースに再接続することができます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|接続ハンドルで非同期に実行されている関数をキャンセルする。|[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|ドライバーまたはデータソースに関する情報を返す|[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|ステートメントハンドルの解放|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
