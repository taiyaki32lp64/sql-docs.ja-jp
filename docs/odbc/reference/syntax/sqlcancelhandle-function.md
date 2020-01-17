---
title: SQLCancelHandle 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 629ff63f6fd06aaccc1f60209231f5c937f4a67d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036133"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 関数
**準拠**  
 バージョンが導入されました。ODBC 3.8  
  
 標準への準拠:なし  
  
 ほとんどの ODBC 3.8 (以降) のドライバーがこの関数を実装することが期待されます。 以外の場合、ドライバーは、呼び出しを**SQLCancelHandle**接続での処理、*処理*パラメーターには、SQLSTATE の IM001、メッセージの SQL_ERROR が返される 'ドライバーでは、この関数はサポートされていません' の呼び出し**SQLCancelHandle**ステートメントとして処理、*処理*パラメーターへの呼び出しにマップされる**SQLCancel**ドライバー マネージャーによって場合に処理できますドライバーの実装**SQLCancel**します。 アプリケーションで使用できます**SQLGetFunctions**ドライバーをサポートしているかを判断する**SQLCancelHandle**します。  
  
 **まとめ**  
 **SQLCancelHandle**接続やステートメントの処理を取り消します。 ドライバー マネージャーは、マップへの呼び出し**SQLCancelHandle**への呼び出しに**SQLCancel**とき*HandleType* sql_handle_stmt としては、します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 [入力]Cacel 処理へのハンドルの型。 有効な値は sql_handle_dbc としてまたは sql_handle_stmt として。  
  
 *Handle*  
 [入力]処理をキャンセルするハンドル。  
  
 場合*処理*で指定された型の有効なハンドルではありません*HandleType*、 **SQLCancelHandle** SQL_INVALID_HANDLE が返されます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLCancelHandle** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt としてとステートメントの処理*処理*または*HandleType* sql_handle_dbc としてと接続ハンドルの*処理*します。  
  
 次の表に、一般的にによって返される SQLSTATE 値**SQLCancelHandle** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)引数 *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|関連付けられているステートメント ハンドルのいずれかの非同期実行ステートメント関連の関数が呼び出された、*処理*、および*HandleType* sql_handle_dbc としてに設定されました。 非同期関数ではときに実行されている**SQLCancelHandle**が呼び出されました。<br /><br /> (DM)、 *HandleType*引数が sql_handle_stmt として、関連付けられている接続ハンドル; で非同期的に実行中の関数が呼び出されました; 関数は、この関数が呼び出されたときにまだ実行中だったとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に関連付けられているステートメント ハンドルのいずれかが呼び出された、*処理* *HandleType*が sql_handle_dbc としてに設定され、SQL_PARAM_DATA_AVAILABLE が返されます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> **SQLBrowseConnect**に対して呼び出された*ConnectionHandle*SQL_NEED_DATA が返されます。 この関数は、参照の処理を完了する前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY092|無効な属性またはオプション識別子|*HandleType* sql_handle_env としてまたは SQL_HANDLE_DESC に設定されました。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、*処理*関数をサポートしていません。|  
  
 場合**SQLCancelHandle**を使用して呼び出した*HandleType* sql_handle_stmt としてに設定すると、関数によって返される任意の SQLSTATE を返すこと**SQLCancel**します。  
  
## <a name="comments"></a>コメント  
 この機能に似ています**SQLCancel**ステートメント ハンドルだけではなく、パラメーターとして接続またはステートメントのいずれかのハンドルがかかる場合があります。 ドライバー マネージャーは、マップへの呼び出し**SQLCancelHandle**への呼び出しに**SQLCancel**とき*HandleType* sql_handle_stmt としては、します。 これにより、アプリケーションを使用する**SQLCancelHandle**ドライバーが実装していない場合でも、ステートメントの操作をキャンセルする**SQLCancelHandle**します。  
  
 ステートメントの操作を取り消しています。 詳細については、次を参照してください。 [SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)します。  
  
 進行中の操作がない場合*処理*呼び出し**SQLCancelHandle**も何も起こりません。  
  
 **SQLCancelHandle**接続では、ハンドルが次の種類の処理を取り消すことができます。  
  
-   接続で非同期に実行されている関数。  
  
-   別のスレッドで、接続ハンドルで実行する関数。  
  
 ときに**SQLCancelHandle**接続によって投稿された診断レコードで非同期的に実行されている関数を取り消すために呼び出される**SQLCancelHandle**操作によって返されるものに追加されます取り消されました。**SQLCancelHandle**返さない診断レコードは、ただし、別のスレッド上の接続で実行されている関数をキャンセルする場合。  
  
 使用して**SQLCancelHandle**をキャンセルする**SQLEndTran**中断された状態の接続を配置することがあります。 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。  
  
> [!NOTE]  
>  使用する方法については**SQLCancelHandle** Windows 7 より古い Windows オペレーティング システム上に配置されるアプリケーションで、次を参照してください。[の互換性対応表](../../../odbc/reference/develop-app/compatibility-matrix.md)します。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>接続に関連する非同期処理のキャンセル  
 アプリケーションを呼び出すことができる場合、関数が返す SQL_STILL_EXECUTING、 **SQLCancelHandle**操作をキャンセルします。 取り消し要求が成功すると場合、 **SQLCancelHandle** SQL_SUCCESS を返します。 元の関数が取り消されたことはありません。これは、キャンセル要求が処理されたことを示します。 ドライバーとデータ ソース、または、操作が取り消された場合を決定します。 リターン コードが SQL_STILL_EXECUTING されるまで、元の関数を呼び出すアプリケーションを続行する必要があります。 リターン コードが SQL_ERROR と SQLSTATE HY008 には、元の関数が取り消された場合 (操作が取り消されました)。 元の関数には、通常の処理が完了した場合 (キャンセルされていない)、リターン コードが SQL_SUCCESS や、SQL_SUCCESS_WITH_INFO または SQL_ERROR HY008 以外の SQLSTATE (操作が取り消されました)、元の関数が失敗した場合。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>別のスレッドで実行されている関数のキャンセル  
 マルチ スレッド アプリケーションでは、アプリケーションは、別のスレッドで実行されている操作をキャンセルできます。 アプリケーションの呼び出し、操作をキャンセルする**SQLCancelHandle**関数では、別のスレッドでハンドルを使用します。 ドライバーとオペレーティング システムは、操作をキャンセルする方法を決定します。 **SQLCancelHandle**返すコードでは、ドライバーが SQL_SUCCESS や SQL_ERROR (診断情報は返されません) のいずれかを返す要求を処理するかどうかを示します。 SQL_ERROR と SQLSTATE HY008、元の関数での処理が取り消された場合、元の関数が返されます (操作が取り消されました)。  
  
 関数の中の場合はときに実行**SQLCancelHandle**と呼びます関数をキャンセルする別のスレッドで関数が成功し、[キャンセル] を有効にするには、SQL_SUCCESS を返すことはできます。 呼び出し**SQLCancelHandle**場合は、操作を完了する前に影響を与えません**SQLCancelHandle**操作を取り消すことができます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|データを必要があるステートメントの関数を取り消すか、別のスレッドでのステートメントで実行されている関数のキャンセル、ステートメント ハンドルで非同期的に実行されている関数を取り消しています。|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
