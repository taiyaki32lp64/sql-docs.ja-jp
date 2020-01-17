---
title: SQLGetCursorName 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4017ed07681a74da4832db2db3aeabddf22edb19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020330"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetCursorName**指定したステートメントに関連付けられたカーソル名を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カーソル名*  
 [出力]カーソル名を返すバッファーへのポインター。  
  
 場合*カーソル名*が null の場合、 *NameLengthPtr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*カーソル名*します。  
  
 *BufferLength*  
 [入力]長さ\**カーソル名*、文字数。 場合の値 *\*カーソル名*は Unicode 文字列です (呼び出し時に**SQLGetCursorNameW**)、 *BufferLength*引数は偶数である必要があります。  
  
 *NameLengthPtr*  
 [出力]文字 (null 終了文字を除く) の合計数を返すメモリへのポインターで返される使用可能な\**カーソル名*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength*でカーソル名\**カーソル名*に切り捨てられます*BufferLength*null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetCursorName** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*sql_handle_stmt としての*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLGetCursorName** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \**カーソル名*が足りません全体のカーソルの名前を返すため、カーソル名は切り詰められました。 切り詰められていないカーソル名の長さが返される **NameLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLGetCursorName**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY015|使用可能なカーソル名|(DM)、ドライバーが、ODBC 2 *.x*ドライバーは、ステートメントで開いているカーソルがなかったし、でカーソル名が設定されていません**SQLSetCursorName**します。|  
|HY090|文字列またはバッファーの長さが無効です。|引数で指定された値 (DM) *BufferLength*が 0 未満でした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 カーソル名が位置指定更新でのみ使用、および delete ステートメント (たとえば、**更新**_テーブル名_.**WHERE CURRENT OF** _カーソル名_)。 詳細については、次を参照してください。[配置の更新と削除ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)します。 アプリケーションが要求されていない場合**SQLSetCursorName**ドライバーをカーソル名を定義するには、名前を生成します。 この名前は文字 SQL_CUR で開始します。  
  
> [!NOTE]
>  ODBC 2 *.x*開いているカーソルはありませんでしたしへの呼び出しで名前が設定されていないときに、 **SQLSetCursorName**への呼び出し**SQLGetCursorName** SQLSTATE HY015 が返されます (カーソル名がありません使用可能な) にします。 ODBC 3 *.x*、true 以外の場合に関係なくこれが不要になった**SQLGetCursorName**が呼び出されると、ドライバーは、カーソル名を返します。  
  
 **SQLGetCursorName**明示的または暗黙的に名前が作成されたかどうか、カーソルの名前を返します。 場合、カーソル名が暗黙的に生成された**SQLSetCursorName**は呼び出されません。 **SQLSetCursorName**カーソルが割り当てられたまたは準備された状態である限り、ステートメントのカーソルの名前を変更するということができます。  
  
 明示的または暗黙的に設定されているカーソル名が設定されるまで、 *StatementHandle*それが関連付けられているを使用して削除**SQLFreeHandle**で、 *HandleType* sql_handle_stmt としての。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|実行するステートメントを準備します。|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|カーソル名を設定します。|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
