---
title: SQLExecDirect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0fa34020478308c1e0d5c5fe112bbeb04920f07e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003123"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLExecDirect**ステートメントにパラメーターが存在しない場合は、パラメーター マーカーの変数の現在の値を使用して、準備可能なステートメントを実行します。 **SQLExecDirect**は 1 回だけ実行に対して SQL ステートメントを送信する最も簡単な方法です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *StatementText*  
 [入力]実行される SQL ステートメント。  
  
 *TextLength*  
 [入力]長さ **StatementText*文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_NO_DATA、SQL_INVALID_HANDLE、または SQL_PARAM_DATA_AVAILABLE  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLExecDirect** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*sql_handle_stmt としての*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLExecDirect** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01001|カーソル操作の競合|\**StatementText*行または複数の行が更新または削除されると、位置指定の update または delete ステートメントを包含します。 (1 つ以上の行に更新プログラムの詳細については、SQL_ATTR_SIMULATE_CURSOR の説明を参照してください*属性*で**SQLSetStmtAttr**。)。<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01003|NULL 値は関数のセットで削除されました|引数*StatementText* set 関数に含まれている (など**AVG**、**最大**、 **MIN**など)、ではなく、**数**関数、および関数が適用される前に値が除外された NULL 引数を設定します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|空白以外の文字または NULL 以外のバイナリ データの切り捨てが発生した出力パラメーターまたは入力/出力の文字列またはバイナリ データが返されます。 文字列値がいた場合は、右側から切り捨てられますことでした。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01006|権限が失効していません。|\**StatementText*に含まれている、**取り消す**ステートメント、およびユーザーに指定した権限がないです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01007|特権は与えられません|*\*StatementText*が、 **GRANT**ステートメント、およびユーザーは許可されませんでした特権を指定します。|  
|01S02|オプション値が変更されました|指定したステートメント属性は、ような値が一時的に代用するための実装の動作状態のため無効でした。 (**SQLGetStmtAttr**一時的に置換された値を特定するということができます)。代替値が有効、 *StatementHandle*カーソルが閉じられるまで、ステートメント属性はこの時点で、前の値に元に戻します。 変更可能なステートメント属性は次のとおりです。<br /><br /> SQL _ ATTR_CONCURRENCY SQL _ ATTR_CURSOR_TYPE SQL _ ATTR_KEYSET_SIZE SQL _ ATTR_MAX_LENGTH SQL _ ATTR_MAX_ROWS SQL _ ATTR_QUERY_TIMEOUT SQL _ ATTR_SIMULATE_CURSOR<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S07|分数が切り捨てられました|入力/出力の返されるデータまたは数値データ型の小数部が切り捨てられましたや時刻、タイムスタンプ、またはその間隔のデータ型の時刻部分の小数部が切り捨てられたように、出力パラメーターが切り捨てられました。<br /><br /> (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|07002|COUNT フィールドが正しくありません。|指定されたパラメーターの数**SQLBindParameter**に含まれる SQL ステートメントのパラメーターの数より少なくなった\* *StatementText*します。<br /><br /> **SQLBindParameter**で呼び出されました*ParameterValuePtr*を null ポインターの場合は、設定*StrLen_or_IndPtr* SQL_NULL_DATA または SQL_DATA_AT_EXEC に設定されていないと*InputOutputType*パラメーターの数で指定できるように、SQL_PARAM_OUTPUT を未設定**SQLBindParameter**に含まれる SQL ステートメントのパラメーターの数よりも大きかった **StatementText*.|  
|07006|制限付きのデータ型の属性違反|識別されるデータ値、 *ValueType*引数**SQLBindParameter**のバインドされたパラメーターがで識別されるデータ型に変換できませんでした、 *ParameterType*引数**SQLBindParameter**します。<br /><br /> SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT で識別されるデータ型に変換しないとしてバインドされたパラメーターのデータ値が返される、 *ValueType*引数**SQLBindParameter**します。<br /><br /> (1 つまたは複数の行のデータ値を変換できませんでした、1 つまたは複数の行が正常に返された場合は、この関数を返します SQL_SUCCESS_WITH_INFO。)|  
|07007|@Restricted パラメーター値の違反|SQL_PARAM_INPUT_OUTPUT_STREAM パラメーターの型は、部分のデータを送受信するパラメーターにのみ使用されます。 このパラメーターの型では、入力バインドされたバッファーは許可されません。<br /><br /> パラメーターの型が、SQL_PARAM_INPUT_OUTPUT とき、および、このエラーが発生、 \* *StrLen_or_IndPtr*で指定されている**SQLBindParameter** SQL_NULL_DATA、SQL_DEFAULT_ と等しくないです。PARAM、SQL_LEN_DATA_AT_EXEC(len)、または SQL_DATA_AT_EXEC です。|  
|07S01|既定のパラメーターの使い方が正しくありません。|パラメーターの値の設定で**SQLBindParameter**が SQL_DEFAULT_PARAM、および対応するパラメーターは、既定値はありませんでした。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|21S01|挿入値のリストは、列リストと一致しません|\**StatementText*に含まれている、**挿入**ステートメント、および挿入する値の数と一致しませんでした、派生テーブルの次数。|  
|21S02|派生テーブルの次数が列の一覧と一致しません|\**StatementText*に含まれている、 **CREATE VIEW**ステートメント、および非修飾の列の一覧 (でビューの指定された列の数、*列識別子*SQL の引数ステートメント) によって定義されている派生テーブルの列の数よりも多くの名に含まれている、*クエリ仕様*SQL ステートメントの引数。|  
|22001|文字列データの右側が切り捨てられました|文字値または列にバイナリ値の割り当ては、空白以外の文字データまたは null 以外のバイナリ データの切り捨てが発生しました。|  
|22002|インジケーター変数が必要ですが、指定されていません|NULL データが出力パラメーターにバインドされましたが*StrLen_or_IndPtr*によって設定**SQLBindParameter**が null ポインター。|  
|22003|数値が範囲外|**StatementText*値が関連付けられているテーブル列に割り当てられたときに切り詰められる数値の (ではなく小数部) 全体の一部を原因し、なった数値パラメーターがバインドされているか、リテラルを含む SQL ステートメントに含まれています。<br /><br /> 1 つまたは複数の入力/出力または出力パラメーター (数値または文字列) としての数値の値が返される原因となる (ではなく小数部) 整数部分が切り捨てられる数値。|  
|22007|無効な datetime 形式|**StatementText*日付、時刻、またはバインドされたパラメーターとしてタイムスタンプの構造体を含む SQL ステートメントに含まれているし、パラメーターが、それぞれ、無効な日付、時刻、またはタイムスタンプ。<br /><br /> または入力/出力の出力パラメーターは、日付、時刻、またはタイムスタンプ C 構造体にバインドされていたし、返されるパラメーターの値が、それぞれ、無効な日付、時刻、またはタイムスタンプ。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|22008|Datetime フィールド オーバーフロー|**StatementText*包含 datetime 式が、計算、日付が発生したときに、時刻、またはタイムスタンプ構造体を含む SQL ステートメントが無効です。<br /><br /> Datetime 式が入力/出力の計算または出力パラメーターの日付、時刻、または無効なタイムスタンプ C の構造体が発生しました。|  
|22012|0 による除算|**StatementText* 0 による除算する算術式を含む SQL ステートメントに含まれています。<br /><br /> 算術式の入力/出力の計算または 0 による除算で出力パラメーターが発生しました。|  
|22015|Interval フィールド オーバーフロー|*\*StatementText*正確な数値または間隔パラメーターに含まれている、間隔の SQL データ型に変換するときは、有効桁数の損失を原因となった。<br /><br /> *\*StatementText*は間隔パラメーターは、複数のフィールドに含まれる、列の数値データ型に変換するときになかった表現で数値データ型。<br /><br /> *\*StatementText*間隔 SQL 型に割り当てられたパラメーター データが含まれているし、SQL 型の間隔で C 型の値の表現はありませんでした。<br /><br /> 真数型または SQL 型の有効桁数が失われました C の間隔の種類の間隔、または入力/出力の出力パラメーターを割り当てます。<br /><br /> C interval 構造体を入力/出力または出力パラメーターが割り当てられると、間隔のデータ構造内のデータの表現はありませんでした。|  
|22018|キャストの無効な文字の値|*\*StatementText* C 型が含まれている、真数または概数の数値、datetime、または間隔のデータ型があった; 列の SQL 型が文字データ型と列の値がバインドされた C 型の有効なリテラルではありませんでした。<br /><br /> SQL 型が、真数または概数の数値、datetime、または、interval データ型が、入力/出力または出力パラメーターが返されると、C 型が SQL_C_CHAR;列の値がバインドされた SQL 型の有効なリテラルではありませんでした。|  
|22019|無効なエスケープ文字|\**StatementText*を含む SQL ステートメントに含まれている、**LIKE**の述語では、**エスケープ**で、**WHERE**句とエスケープの長さ次の文字**エスケープ**が 1 と等しくありません。|  
|22025|無効なエスケープ シーケンス|\**StatementText*を含む SQL ステートメントに含まれる"**LIKE**_パターン値_**エスケープ**_エスケープ文字_"で、**WHERE**句、およびパターンの値のエスケープ文字の後の文字が「%」または「_」のいずれか。|  
|23000|整合性制約違反|**StatementText*パラメーターまたはリテラルを含む SQL ステートメントに含まれています。 パラメーターの値が NULL、関連付けられているテーブル列に NOT NULL として定義されている列、制約を一意の値のみを含む列の重複する値が指定されてまたはその他の整合性制約に違反していた。|  
|24000|カーソル状態が無効|カーソルが配置されている、 *StatementHandle*によって**SQLFetch**または**SQLFetchScroll**します。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いていてもいないに配置されている、 *StatementHandle*します。<br /><br /> **StatementText*または結果セットの終了後に、結果セットの開始前に、カーソルが配置された位置指定の update または delete ステートメント、および含まれています。|  
|34000|カーソル名が無効|**StatementText*包含の位置指定の update または delete ステートメント、および実行中のステートメントによって参照されたカーソルが開かれていませんでした。|  
|3D000|無効なカタログ名|指定されたカタログ名*StatementText*が無効です。|  
|3F000|無効なスキーマ名|指定されたスキーマ名*StatementText*が無効です。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|42000|構文エラーまたはアクセス違反|\**StatementText*準備可能な型がないか、構文エラーに含まれる SQL ステートメントに含まれています。<br /><br /> ユーザーに含まれる SQL ステートメントを実行する権限を持っていません **StatementText*します。|  
|42S01|ベース テーブルまたはビューが既に存在します|\**StatementText*に含まれている、 **CREATE TABLE**または**CREATE VIEW**ステートメントでは、およびテーブル名またはビューの指定名は既に存在します。|  
|42S02|ベース テーブルまたはビューが見つかりません|\**StatementText*に含まれている、 **DROP TABLE**または**DROP VIEW**ステートメント、および指定したテーブル名またはビュー名がありませんでした。<br /><br /> \**StatementText*に含まれている、 **ALTER TABLE**ステートメント、および指定したテーブル名が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **CREATE VIEW**ステートメントとテーブル名またはビューのクエリ仕様で定義された名前がありませんでした。<br /><br /> \**StatementText*に含まれている、 **CREATE INDEX**ステートメント、および指定したテーブル名が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **GRANT**または**取り消す**ステートメント、および指定したテーブル名またはビュー名がありませんでした。<br /><br /> \**StatementText*に含まれている、**選択**ステートメント、および指定したテーブル名またはビュー名がありませんでした。<br /><br /> \**StatementText*に含まれている、**削除**、**挿入**、または**UPDATE**ステートメント、および指定したテーブル名が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **CREATE TABLE**ステートメント、および制約 (テーブルを参照する他にも作成されているもの) で指定されたテーブルが存在しなかった。<br /><br /> \**StatementText*に含まれている、 **CREATE SCHEMA**ステートメント、および指定したテーブル名またはビュー名がありませんでした。|  
|42S11|インデックスが既に存在します|\**StatementText*に含まれている、 **CREATE INDEX**ステートメント、および指定したインデックス名が既に存在します。<br /><br /> \**StatementText*に含まれている、 **CREATE SCHEMA**ステートメント、および指定したインデックス名が既に存在します。|  
|42S12|インデックスが見つかりません|\**StatementText*に含まれている、 **DROP INDEX**ステートメント、および指定したインデックス名が存在しなかった。|  
|42S21|列が既に存在します|\**StatementText*に含まれている、 **ALTER TABLE**ステートメントとで指定された列、**追加**句が一意でない、またはベース テーブルの既存の列を識別します。|  
|42S22|列が見つかりません|\**StatementText*に含まれている、 **CREATE INDEX**ステートメント、および 1 つ以上の列リストで指定された名前が存在しない列です。<br /><br /> \**StatementText*に含まれている、 **GRANT**または**取り消す**ステートメント、および指定された列名が存在しなかった。<br /><br /> \**StatementText*に含まれている、**選択**、**削除**、**挿入**、または**UPDATE**ステートメント、および指定された列名存在しませんでした。<br /><br /> \**StatementText*に含まれている、 **CREATE TABLE**ステートメント、および制約 (テーブルを参照する他にも作成されているもの) で指定された列が存在しなかった。<br /><br /> \**StatementText*に含まれている、 **CREATE SCHEMA**ステートメント、および指定された列名が存在しなかった。|  
|44000|WITH CHECK OPTION 違反|引数*StatementText*に含まれている、**挿入**表示されているテーブルに対して実行されるステートメントまたは指定することによって作成された表示されているテーブルから派生したテーブル**WITH CHECK OPTION**によって 1 つまたは複数の行が影響を受けるような**挿入**ステートメントは、表示されているテーブル内に存在できなきます。<br /><br /> 引数*StatementText*に含まれている、 **UPDATE**表示されているテーブルに対して実行されるステートメントまたは指定することによって作成された表示されているテーブルから派生したテーブル**WITH CHECK OPTION**によって 1 つまたは複数の行が影響を受けるような**UPDATE**ステートメントは、表示されているテーブル内に存在できなきます。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|(DM) **StatementText*が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLExecDirect**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 引数*TextLength*以下を 0 には、SQL_NTS 等しくもありませんでした。<br /><br /> パラメーターの値の設定で**SQLBindParameter**が null ポインターの場合、パラメーターの長さの値が 0、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM SQL_LEN_DATA_AT_EXEC_OFFSET 未満。<br /><br /> パラメーターの値の設定で**SQLBindParameter**、null ポインターでした; C データ型が SQL_C_BINARY または SQL_C_CHAR; およびパラメーターの長さの値が 0 未満の値がでした、SQL_NTS、SQL_NULL_DATA、SQL_DATA_AT_EXEC SQL_DEFAULT_PARAM、SQL_LEN_DATA_AT_EXEC_OFFSET 未満。<br /><br /> パラメーターの長さの値制約を受けます**SQLBindParameter** SQL_DATA_AT_EXEC に設定されました SQL 型が SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型では; および SQL_NEED_LONG_DATA_LEN 情報。入力**SQLGetInfo** "Y"でした。|  
|HY105|無効なパラメーターの型|引数が指定された値*InputOutputType*で**SQLBindParameter** SQL_PARAM_OUTPUT、パラメーターが入力パラメーターをでした。|  
|HY109|無効なカーソルの位置|\**StatementText* 、カーソルが置かれていると、位置指定の update または delete ステートメントを包含 (によって**SQLSetPos**または**SQLFetchScroll**) の行に削除されたかをフェッチできませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、クエリのタイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 アプリケーション呼び出し**SQLExecDirect**データ ソースに SQL ステートメントを送信します。 直接実行の詳細については、次を参照してください。[を直接実行](../../../odbc/reference/develop-app/direct-execution-odbc.md)します。 ドライバーは、データ ソースで使用される SQL の形式を使用するステートメントが変更され、データ ソースに送信します。 具体的には、ドライバーは、SQL の特定の機能を定義するために使用するエスケープ シーケンスを変更します。 エスケープ シーケンスの構文を参照してください。 [odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)します。  
  
 アプリケーションでは、SQL ステートメントの 1 つまたは複数のパラメーター マーカーを含めることができます。 パラメーター マーカーを含めるには、アプリケーションは、適切な位置にある SQL ステートメントに疑問符 (?) を埋め込みます。 パラメーターについては、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)します。  
  
 SQL ステートメントがある場合、**選択**ステートメントと、アプリケーションと呼ばれるかどうか**SQLSetCursorName**をステートメントにカーソルを関連付けるにし、ドライバーを使用して指定したカーソル。 それ以外の場合、ドライバーは、カーソル名を生成します。  
  
 (明示的なトランザクションの開始に使用が必要) 手動コミット モードでのデータ ソースが、トランザクションは既に開始されていない場合は、ドライバーは、SQL ステートメントを送信する前に、トランザクションを開始します。 詳細については、次を参照してください。[手動コミット モード](../../../odbc/reference/develop-app/manual-commit-mode.md)します。  
  
 アプリケーションで使用する場合**SQLExecDirect**を送信する、**コミット**または**ロールバック**ステートメントでは、ことがない DBMS の製品間で相互運用可能な。 トランザクションをロールバックまたはコミットは、アプリケーションが呼び出す**SQLEndTran**します。  
  
 場合**SQLExecDirect**検出すると、実行時データ パラメーターでは、SQL_NEED_DATA が返されます。 アプリケーションを使用してデータを送信する**SQLParamData**と**SQLPutData**します。 参照してください[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)、 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)、および[長い形式のデータを送信する](../../../odbc/reference/develop-app/sending-long-data.md)します。  
  
 場合**SQLExecDirect**検索更新、挿入、またはデータ ソースへの呼び出しですべての行には影響しません delete ステートメントを実行します。 **SQLExecDirect** sql_no_data が返されます。  
  
 SQL_ATTR_PARAMSET_SIZE ステートメント属性の値が 1 より大きい場合、SQL ステートメントには、少なくとも 1 つのパラメーター マーカーが含まれています**SQLExecDirect**からパラメーター値のセットごとに、SQL ステートメントを実行。によって示される、配列、 *ParameterValuePointer*への呼び出しで引数**SQLBindParameter**します。 詳細については、次を参照してください。[パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)します。  
  
 ブックマークは有効にして、クエリを実行する場合は、ブックマークをサポートすることはできません、ドライバーは属性値を変更し、SQLSTATE 01S02 を返すことでブックマークをサポートしている環境を強制的に試みる必要がある (オプションの値が変更されました)。 属性を変更できない場合、ドライバーは SQLSTATE HY024 を返す必要があります (無効な属性値)。  
  
> [!NOTE]  
>  アプリケーションがなど、データベースまたはデータベースのコンテキストを変更する SQL ステートメントを実行する必要がありますいない接続プールを使用する場合、**使用**_データベース_を変更する SQL Server 内のステートメントデータ ソースによって使用されるカタログ。  
  
## <a name="code-example"></a>コード例  
 参照してください[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)、および[サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|コミットまたはロールバック操作を実行します。|[SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|準備された SQL ステートメントを実行します。|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|複数行のデータをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
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
