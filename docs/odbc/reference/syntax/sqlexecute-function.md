---
title: SQLExecute 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecute
helpviewer_keywords:
- SQLExecute function [ODBC]
ms.assetid: 9286a01d-cde2-4b90-af94-9fd7f8da48bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12dffe315485aadc839654996f6af3a561161246
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003126"
---
# <a name="sqlexecute-function"></a>SQLExecute 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLExecute**ステートメントですべてのパラメーター マーカーが存在しない場合は、パラメーター マーカーの変数の現在の値を使用して、準備されたステートメントを実行します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_NO_DATA、SQL_INVALID_HANDLE、または SQL_PARAM_DATA_AVAILABLE  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLExecute** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_stmt として、*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLExecute** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01001|カーソル操作の競合|関連付けられている、準備されたステートメント、 *StatementHandle*行または複数の行が更新または削除されると、位置指定の update または delete ステートメントを包含します。 (1 つ以上の行に更新プログラムの詳細については、SQL_ATTR_SIMULATE_CURSOR の説明を参照してください*属性*で**SQLSetStmtAttr**。)。<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01003|NULL 値は関数のセットで削除されました|関連付けられている、準備されたステートメント*StatementHandle* set 関数に含まれている (など**AVG**、**最大**、 **MIN**など) がありません**カウント**関数、および関数が適用される前に値が除外された NULL 引数を設定します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|文字列またはバイナリ データが出力パラメーターに対して返される空白文字または NULL 以外のバイナリ データの切り捨てが発生しました。 文字列値がいた場合は、右側から切り捨てられますことでした。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01006|権限が失効していません。|関連付けられている、準備されたステートメント、 *StatementHandle*が、**取り消す**ステートメント、およびユーザーに指定した権限がないです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01007|特権は与えられません|関連付けられている、準備されたステートメント、 *StatementHandle*が、 **GRANT**ステートメント、およびユーザーは許可されませんでした特権を指定します。|  
|01S02|オプション値が変更されました|指定したステートメント属性は、ような値が一時的に代用するための実装の動作状態のため無効でした。 (**SQLGetStmtAttr**一時的に置換された値を特定するということができます)。代替値が有効、 *StatementHandle*カーソルが閉じられるまで、ステートメント属性はこの時点で、前の値に元に戻します。 変更可能なステートメント属性は次のとおりです。SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_KEYSET_SIZE、SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、SQL_ATTR_QUERY_TIMEOUT、および SQL_ATTR_SIMULATE_CURSOR します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S07|分数が切り捨てられました|入力/出力の返されるデータまたは数値データ型の小数部が切り捨てられましたや時刻、タイムスタンプ、またはその間隔のデータ型の時刻部分の小数部が切り捨てられたように、出力パラメーターが切り捨てられました。<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07002|COUNT フィールドが正しくありません。|指定されたパラメーターの数**SQLBindParameter**に含まれる SQL ステートメントのパラメーターの数より少なくなった\* *StatementText*します。<br /><br /> **SQLBindParameter**で呼び出されました*ParameterValuePtr*を null ポインターの場合は、設定*StrLen_or_IndPtr* SQL_NULL_DATA または SQL_DATA_AT_EXEC に設定されていないと*InputOutputType*パラメーターの数で指定できるように、SQL_PARAM_OUTPUT を未設定**SQLBindParameter**に含まれる SQL ステートメントのパラメーターの数よりも大きかった **StatementText*.|  
|07006|制限付きのデータ型の属性違反|識別されるデータ値、 *ValueType*引数**SQLBindParameter**のバインドされたパラメーターがで識別されるデータ型に変換できませんでした、 *ParameterType*引数**SQLBindParameter**します。<br /><br /> SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT で識別されるデータ型に変換しないとしてバインドされたパラメーターのデータ値が返される、 *ValueType*引数**SQLBindParameter**します。<br /><br /> (1 つまたは複数の行のデータ値を変換できませんでした、1 つまたは複数の行が正常に返された場合は、この関数を返します SQL_SUCCESS_WITH_INFO。)|  
|07007|@Restricted パラメーター値の違反|SQL_PARAM_INPUT_OUTPUT_STREAM パラメーターの型は、部分のデータを送受信するパラメーターにのみ使用されます。 このパラメーターの型では、入力バインドされたバッファーは許可されません。<br /><br /> パラメーターの型が、SQL_PARAM_INPUT_OUTPUT とき、および、このエラーが発生、 \* *StrLen_or_IndPtr*で指定されている**SQLBindParameter** SQL_NULL_DATA、SQL_DEFAULT_ と等しくないです。PARAM、SQL_LEN_DATA_AT_EXEC(len)、または SQL_DATA_AT_EXEC です。|  
|07S01|既定のパラメーターの使い方が正しくありません。|パラメーターの値の設定で**SQLBindParameter**が SQL_DEFAULT_PARAM、および対応するパラメーターが、ODBC の標準的なプロシージャ呼び出しのパラメーター。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|関連付けられている、準備されたステートメント、 *StatementHandle*に含まれている、 **CREATE VIEW**ステートメント、および非修飾の列の一覧 (でビューの指定された列の数、 *列識別子*SQL ステートメントの引数) で定義されている派生テーブルの列の数よりも多くの名が含まれている、*クエリ仕様*SQL ステートメントの引数。|  
|22001|文字列データの右側が切り捨てられました|文字値または列にバイナリ値の割り当ては、空白 (文字) または null 以外 (バイナリ) の文字またはバイトの切り捨てが発生しました。|  
|22002|インジケーター変数が必要ですが、指定されていません|NULL データが出力パラメーターにバインドされましたが*StrLen_or_IndPtr*によって設定**SQLBindParameter**が null ポインター。|  
|22003|数値が範囲外|関連付けられている、準備されたステートメント、 *StatementHandle* 、バインドされている数値パラメーターが含まれているし、関連付けられている割り当てられたときに切り詰められる数値のではなく小数部) 全体の一部の原因となったパラメーターの値テーブルの列です。<br /><br /> 1 つまたは複数の入力/出力または出力パラメーター (数値または文字列) としての数値の値が返される原因となる (ではなく小数部) 整数部分が切り捨てられる数値。|  
|22007|無効な datetime 形式|関連付けられている、準備されたステートメント、 *StatementHandle*日付、時刻、またはバインドされたパラメーターとしてタイムスタンプの構造体を含む SQL ステートメントに含まれているし、パラメーターが、それぞれ、無効な日付、時刻、またはタイムスタンプ。<br /><br /> または入力/出力の出力パラメーターは、日付、時刻、またはタイムスタンプ C 構造体にバインドされていたし、返されるパラメーターの値が、それぞれ、無効な日付、時刻、またはタイムスタンプ。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|22008|Datetime フィールド オーバーフロー|関連付けられている、準備されたステートメント、 *StatementHandle*包含 datetime 式が、計算、日付が発生したときに、時刻、またはタイムスタンプ構造体を含む SQL ステートメントが無効です。<br /><br /> Datetime 式が入力/出力の計算または出力パラメーターの日付、時刻、または無効なタイムスタンプ C の構造体が発生しました。|  
|22012|0 による除算|関連付けられている、準備されたステートメント、 *StatementHandle* 0 による除算する算術式に含まれています。<br /><br /> 算術式の入力/出力の計算または 0 による除算で出力パラメーターが発生しました。|  
|22015|Interval フィールド オーバーフロー|*\*StatementText*正確な数値または間隔パラメーターに含まれている、間隔の SQL データ型に変換するときは、有効桁数の損失を原因となった。<br /><br /> *\*StatementText*は間隔パラメーターは、複数のフィールドに含まれる、列の数値データ型に変換するときになかった表現で数値データ型。<br /><br /> *\*StatementText*間隔 SQL 型に割り当てられたパラメーター データが含まれているし、SQL 型の間隔で C 型の値の表現はありませんでした。<br /><br /> 真数型または SQL 型の有効桁数が失われました C の間隔の種類の間隔、または入力/出力の出力パラメーターを割り当てます。<br /><br /> C interval 構造体を入力/出力または出力パラメーターが割り当てられると、間隔のデータ構造内のデータの表現はありませんでした。|  
|22018|キャストの無効な文字の値|*\*StatementText* C 型が含まれている、真数または概数の数値、datetime、または間隔のデータ型があった; 列の SQL 型が文字データ型と列の値がバインドされた C 型の有効なリテラルではありませんでした。<br /><br /> SQL 型が、真数または概数の数値、datetime、または、interval データ型が、入力/出力または出力パラメーターが返されると、C 型が SQL_C_CHAR;列の値がバインドされた SQL 型の有効なリテラルではありませんでした。|  
|22019|無効なエスケープ文字|関連付けられている、準備されたステートメント*StatementHandle*に含まれている、**など**() 述語が、**エスケープ**で、**場所**句、およびエスケープ文字の次の長さ**エスケープ**が 1 と等しくありません。|  
|22025|無効なエスケープ シーケンス|関連付けられている、準備されたステートメント*StatementHandle*に含まれている"**など**_パターン値_**エスケープ**_エスケープ文字_"で、**場所**句、およびパターンの値のエスケープ文字の後の文字が「%」または「_」のいずれか。|  
|23000|整合性制約違反|関連付けられている、準備されたステートメント、 *StatementHandle*パラメーターに含まれています。 パラメーターの値が NULL、関連付けられているテーブル列に NOT NULL として定義されている列、制約を一意の値のみを含む列の重複する値が指定されてまたはその他の整合性制約に違反していた。|  
|24000|カーソル状態が無効|カーソルが配置されている、 *StatementHandle*によって**SQLFetch**または**SQLFetchScroll**します。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*します。<br /><br /> 関連付けられている、準備されたステートメント、 *StatementHandle*位置指定更新に含まれているか、または結果セットの終了後に、結果セットの開始前に配置された削除 statemen、t、カーソル。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|42000|構文エラーまたはアクセス違反|ユーザーに関連付けられている、準備されたステートメントを実行する権限を持っていません、 *StatementHandle*します。|  
|44000|WITH CHECK OPTION 違反|関連付けられている、準備されたステートメント*StatementHandle*に含まれている、**挿入**表示されているテーブルに対して実行されるステートメントまたはを指定することによって作成された表示されているテーブルから派生したテーブル**WITH CHECK OPTION**によって 1 つまたは複数の行が影響を受けるような**挿入**ステートメントは、表示されているテーブル内に存在できなきます。<br /><br /> 関連付けられている、準備されたステートメント、 *StatementHandle*に含まれている、 **UPDATE**表示されているテーブルに対して実行されるステートメントまたはを指定することによって作成された表示されているテーブルから派生したテーブル**WITH CHECK OPTION**によって 1 つまたは複数の行が影響を受けるような**UPDATE**ステートメントは、表示されているテーブル内に存在できなきます。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLExecute**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。<br /><br /> (DM)、 *StatementHandle*準備されていませんでした。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|パラメーターの値の設定で**SQLBindParameter**が null ポインターの場合、パラメーターの長さの値が 0、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM SQL_LEN_DATA_AT_EXEC_OFFSET 未満。<br /><br /> パラメーターの値の設定で**SQLBindParameter**、null ポインターでした; C データ型が SQL_C_BINARY または SQL_C_CHAR; およびパラメーターの長さの値が 0 未満の値がでした SQL_NTS、SQL_NULL_DATA、SQL_DEFAULT_PARAM、または SQL_DATA_AT_EXEC、SQL_LEN_DATA_AT_EXEC_OFFSET 未満。<br /><br /> パラメーターの長さの値制約を受けます**SQLBindParameter** SQL_DATA_AT_EXEC に設定されました SQL 型が SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型では; および SQL_NEED_LONG_DATA_LEN 情報。入力**SQLGetInfo** "Y"でした。|  
|HY105|無効なパラメーターの型|引数が指定された値*InputOutputType*で**SQLBindParameter** SQL_PARAM_OUTPUT、パラメーターが入力パラメーターをでした。|  
|HY109|無効なカーソルの位置|準備されたステートメントが位置指定の update または delete ステートメントと、カーソルが配置された (によって**SQLSetPos**または**SQLFetchScroll**) の行に削除されたかをフェッチできませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、クエリのタイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
 **SQLExecute**によって返される任意の SQLSTATE を返すことができます**SQLPrepare**を基に、データ ソースが、ステートメントに関連付けられた SQL ステートメントと評価される場合。  
  
## <a name="comments"></a>コメント  
 **SQLExecute**によって準備されたステートメントが実行される**SQLPrepare**します。 アプリケーションを処理するかへの呼び出しから結果を破棄した後**SQLExecute**、アプリケーションが呼び出すことができます**SQLExecute**新しいパラメーター値をもう一度使用します。 準備実行の詳細については、次を参照してください。[準備された実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)します。  
  
 実行する、**選択**ステートメントが複数回、アプリケーションが呼び出す必要があります**SQLCloseCursor**の前に、**選択**ステートメント。  
  
 (明示的なトランザクションの開始に使用が必要) 手動コミット モードでのデータ ソースが、トランザクションは既に開始されていない場合は、ドライバーは、SQL ステートメントを送信する前に、トランザクションを開始します。 詳細については、次を参照してください。[トランザクション](../../../odbc/reference/develop-app/transactions-odbc.md)です。  
  
 アプリケーションで使用する場合**SQLPrepare**を準備して**SQLExecute**を送信する、**コミット**または**ロールバック**ステートメントでは、ことはできませんDBMS の製品間で相互運用可能です。 トランザクションをロールバックまたはコミットは、呼び出す**SQLEndTran**します。  
  
 場合**SQLExecute**検出すると、実行時データ パラメーターでは、SQL_NEED_DATA が返されます。 アプリケーションを使用してデータを送信する**SQLParamData**と**SQLPutData**します。 参照してください[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)、 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)、および[長い形式のデータを送信する](../../../odbc/reference/develop-app/sending-long-data.md)します。  
  
 場合**SQLExecute**検索更新、挿入、またはデータ ソースへの呼び出しですべての行には影響しません delete ステートメントを実行します。 **SQLExecute** sql_no_data が返されます。  
  
 SQL_ATTR_PARAMSET_SIZE ステートメント属性の値が 1 より大きい場合、SQL ステートメントには、少なくとも 1 つのパラメーター マーカーが含まれています**SQLExecute** 、配列内のパラメーター値のセットごとに、SQL ステートメントを実行します。によって示される、  *\*ParameterValuePtr*への呼び出しで引数**SQLBindParameter**します。 詳細については、次を参照してください。[パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)します。  
  
 ブックマークが有効になっており、クエリが実行されるブックマークをサポートすることはできません、ドライバーが属性値を変更し、SQLSTATE 01S02 を返すことでブックマークをサポートしている環境を強制的に試行する必要があります (オプションの値が変更されました)。 属性を変更できない場合、ドライバーは SQLSTATE HY024 を返す必要があります (無効な属性値)。  
  
> [!NOTE]  
>  アプリケーションがなど、データベースまたはデータベースのコンテキストを変更する SQL ステートメントを実行する必要がありますいない接続プールを使用する場合、**使用**_データベース_を変更する SQL Server 内のステートメントデータ ソースによって使用されるカタログ。  
  
## <a name="code-example"></a>コード例  
 参照してください[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)、および[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|カーソルを閉じる|[SQLCloseCursor 関数](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|コミットまたはロールバック操作を実行します。|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|SQL ステートメントを実行します。|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|複数行のデータをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|ステートメント ハンドルの解放|[SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|カーソル名を返す|[SQLGetCursorName 関数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|列のデータの一部またはすべてをフェッチしています|[SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|データを送信する次のパラメーターを返す|[SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|実行するステートメントを準備します。|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|実行時にパラメーターのデータを送信します。|[SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|カーソル名を設定します。|[SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|ステートメント属性を設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
