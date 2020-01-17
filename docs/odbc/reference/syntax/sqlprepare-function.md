---
title: SQLPrepare 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 292b1c4d9cd0281de610af4e53f25aa3d0ab6f90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005767"
---
# <a name="sqlprepare-function"></a>SQLPrepare 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLPrepare**実行 SQL 文字列を準備します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *StatementText*  
 [入力]SQL テキストの文字列です。  
  
 *TextLength*  
 [入力]長さ **StatementText*文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLPrepare** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLPrepare** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|指定したステートメント属性は、ような値が一時的に代用するための実装の動作状態のため無効でした。 (**SQLGetStmtAttr**一時的に置換された値を特定するということができます)。代替値が有効、 *StatementHandle*カーソルが閉じられるまでです。 変更可能なステートメント属性は次のとおりです。SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|21S01|挿入値のリストは、列リストと一致しません|\**StatementText*に含まれている、**挿入**ステートメント、および挿入する値の数と一致しませんでした、派生テーブルの次数。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|\**StatementText*に含まれている、 **CREATE VIEW**ステートメント、および指定した名前の数は、クエリの仕様で定義されている派生テーブルと同じレベルではありません。|  
|22018|キャストの無効な文字の値|**StatementText*リテラルまたはパラメーターを含む SQL ステートメントに含まれているし、値が関連付けられているテーブル列のデータ型と互換性がありません。|  
|22019|無効なエスケープ文字|引数*StatementText*に含まれている、**など**の述語では、**エスケープ**で、**場所**句とエスケープの長さ次の文字**エスケープ**が 1 と等しくありません。|  
|22025|無効なエスケープ シーケンス|引数*StatementText*に含まれている"**など**_パターン値_**エスケープ**_エスケープ文字_"で、**場所**句、およびパターンの値のエスケープ文字の後の文字が「%」も「_」。|  
|24000|カーソル状態が無効|(DM)、カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|34000|カーソル名が無効|\**StatementText*位置指定に含まれる**削除**または位置指定**UPDATE**、準備されているステートメントによって参照されたカーソルが開いていなかったとします。|  
|3D000|無効なカタログ名|指定されたカタログ名*StatementText*が無効です。|  
|3F000|無効なスキーマ名|指定されたスキーマ名*StatementText*が無効です。|  
|42000|構文エラーまたはアクセス違反|\**StatementText*準備可能な型がないか、構文エラーに含まれる SQL ステートメントに含まれています。<br /><br /> **StatementText*対象のユーザー権限がない、必要なステートメントに含まれています。|  
|42S01|ベース テーブルまたはビューが既に存在します|\**StatementText*に含まれている、 **CREATE TABLE**または**CREATE VIEW**ステートメントでは、およびテーブル名またはビューの指定名は既に存在します。|  
|42S02|ベース テーブルまたはビューが見つかりません|\**StatementText*に含まれている、 **DROP TABLE**または**DROP VIEW**ステートメント、および指定したテーブル名またはビュー名がありませんでした。<br /><br /> \**StatementText*に含まれている、 **ALTER TABLE**ステートメント、および指定したテーブル名が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **CREATE VIEW**ステートメントとテーブル名またはビューのクエリ仕様で定義された名前がありませんでした。<br /><br /> \**StatementText*に含まれている、 **CREATE INDEX**ステートメント、および指定したテーブル名が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **GRANT**または**取り消す**ステートメント、および指定したテーブル名またはビュー名がありませんでした。<br /><br /> \**StatementText*に含まれている、**選択**ステートメント、および指定したテーブル名またはビュー名がありませんでした。<br /><br /> \**StatementText*に含まれている、**削除**、**挿入**、または**UPDATE**ステートメント、および指定したテーブル名が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **CREATE TABLE**ステートメント、および制約 (テーブルを参照する他にも作成されているもの) で指定されたテーブルが存在しなかった。|  
|42S11|インデックスが既に存在します|\**StatementText*に含まれている、 **CREATE INDEX**ステートメント、および指定したインデックス名が既に存在します。|  
|42S12|インデックスが見つかりません|\**StatementText*に含まれている、 **DROP INDEX**ステートメント、および指定したインデックス名が存在しなかった。|  
|42S21|列が既に存在します|\**StatementText*に含まれている、 **ALTER TABLE**ステートメントとで指定された列、**追加**句が一意でない、またはベース テーブルの既存の列を識別します。|  
|42S22|列が見つかりません|\**StatementText*に含まれている、 **CREATE INDEX**ステートメント、および 1 つ以上の列リストで指定された名前が存在しない列です。<br /><br /> \**StatementText*に含まれている、 **GRANT**または**取り消す**ステートメント、および指定された列名が存在しなかった。<br /><br /> \**StatementText*に含まれている、**選択**、**削除**、**挿入**、または**UPDATE**ステートメント、および指定された列名存在しませんでした。<br /><br /> \**StatementText*に含まれている、 **CREATE TABLE**ステートメント、および制約 (テーブルを参照する他にも作成されているもの) で指定された列が存在しなかった。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*関数が呼び出された後、もう一度、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|(DM) *StatementText*が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLPrepare**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 引数*TextLength*以下を 0 には、SQL_NTS 等しくもありませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|同時実行の設定が定義されているカーソルの種類の無効でした。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、タイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 アプリケーション呼び出し**SQLPrepare**準備のためのデータ ソースに SQL ステートメントを送信します。 準備実行の詳細については、次を参照してください。[準備された実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)します。 アプリケーションでは、SQL ステートメントの 1 つまたは複数のパラメーター マーカーを含めることができます。 パラメーター マーカーを含めるには、アプリケーションは、適切な位置にある SQL 文字列に疑問符 (?) を埋め込みます。 パラメーターについては、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)します。  
  
> [!NOTE]  
>  アプリケーションで使用する場合**SQLPrepare**を準備して**SQLExecute**を送信する、**コミット**または**ロールバック**ステートメントでは、ことはできませんDBMS の製品間で相互運用可能です。 トランザクションをロールバックまたはコミットは、呼び出す**SQLEndTran**します。  
  
 ドライバーは、データ ソースで使用される SQL のフォームを使用して、準備のためのデータ ソースに送信するステートメントを変更できます。 具体的には、ドライバーは、特定の機能の SQL 構文を定義するために使用するエスケープ シーケンスを変更します。 (SQL ステートメントの文法の説明は、次を参照してください[odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)と[付録 c:。SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md))。ドライバーの場合は、ステートメント ハンドルは埋め込まれた SQL コードでステートメントの識別子に似ています。 データ ソースは、ステートメントの識別子をサポートする場合、ドライバーは、データ ソースにステートメントの識別子とパラメーター値を送信できます。  
  
 ステートメントは準備ができたら、アプリケーションは、ステートメント ハンドルを使用して、後続の関数呼び出しでステートメントを参照してください。 呼び出して、ステートメント ハンドルに関連付けられている、準備されたステートメントを再実行できます**SQLExecute**アプリケーションへの呼び出しでステートメントを解放するまで**SQLFreeStmt** SQL_DROP オプションまたはステートメント ハンドルがへの呼び出しで使用されるまで**SQLPrepare**、 **SQLExecDirect**、またはカタログ関数のいずれか (**SQLColumns**、 **SQLTables**など)。 アプリケーションは、ステートメントを準備すると、結果セットの形式に関する情報を要求できます。 実装によって呼び出す**SQLDescribeCol**または**SQLDescribeParam**後**SQLPrepare** 後に、関数の呼び出しとして効率的でない可能性があります**SQLExecute**または**SQLExecDirect**します。  
  
 一部のドライバーが構文エラーが返されることはできませんまたはアプリケーションを呼び出すとき、アクセス違反**SQLPrepare**します。 ドライバーは構文エラーを処理し、アクセス違反、のみ、構文エラーまたは構文エラーでもアクセス違反が発生します。 そのため、アプリケーションが関数など、関連する後続の呼び出し時に、これらの条件を処理することがあります**SQLNumResultCols**、 **SQLDescribeCol**、 **SQLColAttribute**、および**SQLExecute**します。  
  
 データ ソースのドライバーの機能、に応じて (すべてのパラメーターがバインドされている) 場合、ステートメントが準備されたときに、パラメーター情報 (などのデータ型) をオンになってまたは (すべてのパラメーターがバインドされていない) 場合の実行時。 相互運用性を最大に、アプリケーションは同じステートメントで新しい SQL ステートメントを準備する前に古い SQL ステートメントに適用されるすべてのパラメーターをバインド解除する必要があります。 これには、新しいステートメントに適用されるパラメーターの情報が古いため、エラーができないようにします。  
  
> [!IMPORTANT]  
>  明示的に呼び出すことによって、トランザクションのコミット**SQLEndTran**自動コミット モードで作業しての接続ですべてのステートメントへのアクセスの計画を削除するデータ ソースとなることができます。 詳細についてで SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類を参照してください。 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)と[カーソルと準備されたステートメントでトランザクションの効果](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)します。  
  
## <a name="code-example"></a>コード例  
 参照してください[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)、および[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ステートメント ハンドルの割り当てください。|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|バッファーをパラメーターにバインドします。|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|コミットまたはロールバック操作を実行します。|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|ステートメントによって影響を受ける行の数を返す|[SQLRowCount 関数](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|カーソル名を設定します。|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
