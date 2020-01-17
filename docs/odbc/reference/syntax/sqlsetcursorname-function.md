---
title: SQLSetCursorName 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 842d21bc36b9360826b4b85aa7da2798782995c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092989"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLSetCursorName**カーソル名をアクティブなステートメントに関連付けます。 アプリケーションが要求されていない場合**SQLSetCursorName**ドライバーでは、SQL ステートメントの処理に必要なカーソル名が生成されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カーソル名*  
 [入力]カーソルの名前。 効率的な処理は、カーソル名で、カーソル名の先頭または末尾の空白を含める必要がありますいないと、カーソル名の最初の文字として区切り記号を配置する必要があります、カーソル名には、区切られた識別子が含まれている場合。  
  
 *NameLength*  
 [入力]文字の長さ **カーソル名*します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLSetCursorName** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt として、*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLSetCursorName** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|カーソル名が上限を超えた、したがって文字の最大許容数のみが使用されました。|  
|24000|カーソル状態が無効|対応するステートメント*StatementHandle*が既に実行された、またはカーソル位置の状態であった。|  
|34000|カーソル名が無効|指定されたカーソル名 **カーソル名*がドライバーで定義されている最大長を超えたか、"SQLCUR"または"SQL_CUR"で開始が無効です。|  
|3C000|カーソル名が重複しています|指定されたカーソル名 **カーソル名*既に存在します。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|無効な null ポインターの使用|(DM) 引数*カーソル名*が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLSetCursorName**関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 引数*NameLength* SQL_NTS 等しくもありませんが、0 より小さいをでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 カーソル名が位置指定更新でのみ使用、および delete ステートメント (たとえば、**更新**_テーブル名_.**WHERE CURRENT OF** _カーソル名_)。 詳細については、次を参照してください。[配置の更新と削除ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)します。 アプリケーションが要求されていない場合**SQLSetCursorName**ドライバー SQL_CUR 文字で始まり、18 文字の長さを超えていない名前を生成するクエリ ステートメントの実行時に、カーソル名を定義します。  
  
 接続内のすべてのカーソル名は一意である必要があります。 カーソル名の最大長は、ドライバーによって定義されます。 相互運用性を最大に、アプリケーションは 18 個までの文字にカーソル名を制限することをお勧めします。 ODBC 3 *.x*カーソル名は引用符で囲まれた識別子かどうかは、大文字小文字を区別の方法で扱われ、SQL の構文について、ことを認めていないまたは空白などの特別な処理はまたは予約済みキーワードで、文字を含めることができます。 カーソル名は、大文字と小文字で扱う必要があるを場合は、引用符で囲まれた識別子として渡す必要があります。  
  
 カーソル名または暗黙的にも明示的に設定されている設定を使用して、それが関連付けられているステートメントが削除されるまで**SQLFreeHandle**します。 **SQLSetCursorName**カーソルが割り当てられたまたは準備された状態である限り、ステートメントのカーソルの名前を変更するということができます。  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションを使用して**SQLSetCursorName**ステートメントのカーソル名を設定します。 そのステートメントを使用して、CUSTOMERS テーブルから結果を取得します。 最後に、John Smith の電話番号を変更する位置指定更新を実行します。 アプリケーションのさまざまなステートメント ハンドルを使用して、**選択**と**更新**ステートメント。  
  
 別のコード例では、次を参照してください。 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|カーソル名を返す|[SQLGetCursorName 関数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|カーソルがスクロール オプションの設定|[SQLSetScrollOptions 関数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
