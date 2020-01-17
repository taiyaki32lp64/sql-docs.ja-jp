---
title: SQLGetTypeInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c597cd4ca51ca578ca90c4e95db584dec4bcd6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030593"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetTypeInfo**データ ソースでサポートされるデータ型に関する情報を返します。 ドライバーは、SQL の結果セットの形式で情報を返します。 データ型は、データ定義言語 (DDL) ステートメントで使用します。  
  
> [!IMPORTANT]  
>  アプリケーションの TYPE_NAME 列に返される型名を使用する必要があります、 **SQLGetTypeInfo**の結果セット**ALTER TABLE**と**CREATE TABLE**ステートメント。 **SQLGetTypeInfo** DATA_TYPE 列の値が同じでは、複数の行を返す可能性があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]結果セットのステートメント ハンドルです。  
  
 *DataType*  
 [入力]SQL データ型です。 内の値のいずれかにあるこの必要があります、 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d: のセクションデータ型、またはドライバーに固有の SQL データ型。 SQL_ALL_TYPES では、すべてのデータ型に関する情報が返されることを指定します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetTypeInfo** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* SQL の_HANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLGetTypeInfo** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|指定したステートメント属性は、ような値が一時的に代用するための実装の動作状態のため無効でした。 (呼び出し**SQLGetStmtAttr**を一時的に置換された値を決定します)。代替値が有効、 *StatementHandle*カーソルが閉じられるまでです。 変更可能なステートメント属性は次のとおりです。SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_KEYSET_SIZE、SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、SQL_ATTR_QUERY_TIMEOUT、および SQL_ATTR_SIMULATE_CURSOR します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle、* と**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> 結果セットが上で開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY004|無効な SQL データ型|引数が指定された値*DataType*が ODBC SQL データ型の有効な識別子でも、ドライバーでサポートされるドライバー固有のデータ型識別子。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*関数が呼び出されたし、前に、実行を完了**SQLCancel**または**SQLCancelHandle**されました呼び出される、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出され、前に、実行を完了**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLGetTypeInfo**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、クエリのタイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に対応するドライバー、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SQLGetTypeInfo** DATA_TYPE をしにどのデータ型が対応する ODBC SQL データ型にマップして順序付けられた、標準的な結果セットとして結果を返します。 データ ソースで定義されているデータ型は、ユーザー定義データ型よりも優先されます。 その結果、並べ替え順序は必ずしも一致しませんが、まず DATA_TYPE として一般化、TYPE_NAME、昇順のどちらに続きます。 たとえば、データ ソースに、カウンターは、自動インクリメントは、整数およびカウンターのデータ型が定義されていると、ユーザー定義データ型 WHOLENUM も定義されていること。 これらは、整数、WHOLENUM の順序で返されるであり、カウンター、ODBC SQL データに最も近い WHOLENUM マップ型 SQL_INTEGER、自動インクリメント データが入力と同時に、データ ソースでサポートされている場合でもにマップされない密接に ODBC SQL データ型を。 この情報の用途については、次を参照してください。 [DDL ステートメント](../../../odbc/reference/develop-app/ddl-statements.md)します。  
  
 場合、 *DataType*引数は、ドライバーでサポートされている ODBC のバージョンの有効なデータ型を指定しますが、ドライバーではサポートされていませんし、空の結果セットが返されます。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 次の列は、ODBC 3 の名前に変更されています。*x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 によって返される結果セットに次の列が追加されている**SQLGetTypeInfo** ODBC 3 *。x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、19 (INTERVAL_PRECISION) 列を超える追加の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウント ダウンによって、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**すべてのデータ型を返さない可能性があります。 たとえば、ドライバーはユーザー定義データ型を返さない可能性があります。 アプリケーションがによって返されるかどうかに関係なく、任意の有効なデータ型を使用できます**SQLGetTypeInfo**します。 によって返されるデータ型**SQLGetTypeInfo**はデータ ソースでサポートされています。 データ定義言語 (DDL) ステートメントで使用することは想定されています。 ドライバーがによって返される型以外のデータ型を使用してデータを結果セットを返す**SQLGetTypeInfo**します。 カタログ関数の結果セットを作成するで、ドライバーは、データ ソースでサポートされていないデータ型を使用する場合があります。  
  
|列名|[列]<br /><br /> number|データ型|コメント|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|NULL 以外の Varchar|データ ソースに依存するデータ型名です。たとえば、"CHAR()"、"VARCHAR()"、"MONEY"、"LONG VARBINARY"、または「CHAR FOR BIT DATA ()」。 アプリケーションでは、この名前を使用する必要があります**CREATE TABLE**と**ALTER TABLE**ステートメント。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint (NULL 以外)|SQL データ型です。 これには、ODBC SQL データ型をまたはドライバーに固有の SQL データ型を指定できます。 Datetime または間隔のデータ型は、この列は、(SQL_TYPE_TIME SQL_INTERVAL_YEAR_TO_MONTH など) の簡潔なデータ型を返します。 有効な ODBC SQL データ型の一覧は、次を参照してください[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d:。データ型。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|このデータ型のサーバーでサポートされている列の最大サイズ。 数値データは、これは、最大有効桁数です。 文字列のデータの文字の長さになります。 Datetime データ型の長さ (秒の小数部のコンポーネントの最大有効桁数を想定) の文字列表現の文字数になります。 NULL を返しますのデータ型の列のサイズは適用されません。 Interval データ型では、これは、文字形式のリテラルの間隔の文字数 (先頭の有効桁数です間隔で定義されているを参照してください。 [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)付録 d:。データ型の場合)。<br /><br /> 列のサイズの詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|文字または文字列リテラルをプレフィックスとして使用たとえばを単一引用符 (') の文字データ型またはバイナリ データ型の 0 xNULL を返しますのデータ型リテラル プレフィックスは適用されません。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|文字または文字列リテラルを終了するために使用たとえば、文字データ型の単一の引用符 (')NULL を返しますのデータ型のリテラル サフィックスは適用されません。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|キーワード、TYPE_NAME フィールドで返される名前を使用する場合、アプリケーションがかっこ内に指定できる各パラメーターに対応する、コンマ区切りの一覧。 リストのキーワードは、次のいずれかを指定できます。 長さ、有効桁数または小数点。 構文が使用することが必要である順序で表示されます。 たとえば、CREATE_PARAMS は 10 進数には「有効桁数、小数点」;VARCHAR の CREATE_PARAMS「の長さ」になります データ型を定義します。 パラメーターがない場合、NULL が返されますたとえば、整数です。<br /><br /> ドライバーが使用されている国/地域の言語で CREATE_PARAMS テキストを提供します。|  
|NULL 許容型 (ODBC 2.0)|7|Smallint (NULL 以外)|かどうか、データ型は NULL 値を受け取ります。<br /><br /> データ型が NULL 値を受け付けない場合 SQL_NO_NULLS します。<br /><br /> データ型が NULL 値を受け取る場合 SQL_NULLABLE します。<br /><br /> SQL_NULLABLE_UNKNOWN 列が NULL 値を受け入れるかどうかが不明である場合。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint (NULL 以外)|文字データを入力するかどうかは、照合順序との比較で大文字小文字が区別は。<br /><br /> SQL_TRUE 場合は、データ型は文字データ型であり、小文字が区別されます。<br /><br /> データ型が文字データ型ではない、または小文字は区別されません sql_false になります。|  
|検索可能な (ODBC 2.0)|9|Smallint (NULL 以外)|データ型の使用方法、**WHERE**句。<br /><br /> SQL_PRED_NONE で列を使用できない場合、**WHERE**句。 (これは ODBC 2.*x* の SQL_UNSEARCHABLE 値と同じです。)。<br /><br /> SQL_PRED_CHAR 列で使用できる場合は、**WHERE**句でのみ、**LIKE**述語。 (これは ODBC 2.*x* の SQL_LIKE_ONLY 値と同じです。)。<br /><br /> SQL_PRED_BASIC 列で使用できる場合は、**WHERE**を除くすべての比較演算子を含む句**など**(比較、定量化された比較は、 **BETWEEN**、 **DISTINCT**、 **IN**、**MATCH**、および**UNIQUE**)。 (これは ODBC 2.*x* の SQL_ALL_EXCEPT_LIKE 値と同じです。)。<br /><br /> SQL_SEARCHABLE 列で使用できる場合は、**WHERE**任意の比較演算子を含む句。|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|かどうか、データ型が符号なしです。<br /><br /> データ型が署名されていない場合は SQL_TRUE にします。<br /><br /> データ型が符号付き場合は sql_false になります。<br /><br /> 属性は、データ型に適用可能でないまたはデータ型が数値でない場合は、NULL が返されます。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint (NULL 以外)|データ型が定義済みかどうか、有効桁数と小数点 (これは、データ ソースに固有)、money データ型などが修正済み。<br /><br /> SQL_TRUE に事前定義された場合は、有効桁数と小数点を修正しました。<br /><br /> 定義済みの固定有効桁数と小数点がない場合は sql_false になります。|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|データ型が自動増分されるかどうか。<br /><br /> データ型が自動増分される場合は SQL_TRUE にします。<br /><br /> データ型でない自動増分される場合は sql_false になります。<br /><br /> 属性は、データ型に適用可能でないまたはデータ型が数値でない場合は、NULL が返されます。<br /><br /> アプリケーションは、この属性を持つ列に値を挿入することができますが、通常、列の値を更新することはできません。<br /><br /> 自動インクリメント列に挿入が行われる挿入時に、一意の値が列に挿入されます。 増分値は定義されていませんがデータ ソースに固有です。 アプリケーションでは、特定の値によって、特定の時点またはインクリメントで、自動インクリメント列が開始されるは想定しないでください。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|データ ソースに依存するデータ型のローカライズされた名前です。 ローカライズされた名前がそのデータ ソースによってサポートされない場合は NULL が返されます。 この名前は表示のみ、このようなダイアログ ボックスのように対象としています。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|データ ソースでのデータ型の最小のスケール。 データ型の小数点以下桁数が固定されている場合は、MINIMUM_SCALE 列および MAXIMUM_SCALE 列の両方にこの値が入ります。 たとえば、sql_type_timestamp 型の列では、秒の小数部の固定のスケールがあります。 小数点以下桁数が適用されない場合は NULL が返されます。 詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|データ ソースでのデータ型の最大の小数点以下桁数。 小数点以下桁数が適用されない場合は NULL が返されます。 最大の小数点以下桁数が、データ ソースでは別に定義されず、最大有効桁数と同じであると定義されている場合、この列には、COLUMN_SIZE 列と同じ値が含まれています。 詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|smallint NOT NULL|記述子の SQL_DESC_TYPE フィールドとして、SQL データ型の値が表示されます。 この列は、間隔と datetime データ型を除く、DATA_TYPE 列と同じです。<br /><br /> 間隔および datetime データ型の SQL_INTERVAL または SQL_DATETIME、結果セットに SQL_DATA_TYPE フィールドを返すし、SQL_DATETIME_SUB フィールドには、特定の間隔または datetime データ型のサブコードが返されます。 (を参照してください[付録 d:データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md))。|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|SQL_DATA_TYPE の値が SQL_DATETIME または SQL_INTERVAL の場合は、この列には、datetime/間隔サブコードが含まれています。 データ型 datetime と間隔以外、このフィールドは NULL です。<br /><br /> 期間または日時のデータ型の SQL_INTERVAL または SQL_DATETIME、結果セットに SQL_DATA_TYPE フィールドを返すし、SQL_DATETIME_SUB フィールドには、特定の間隔または datetime データ型のサブコードが返されます。 (を参照してください[付録 d:データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md))。|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|データ型が概数型の場合は、この列には、COLUMN_SIZE がビット数を指定することを示す 2 の値が含まれています。 正確な数値型では、この列には 10 COLUMN_SIZE が 10 進数を指定することを示す値が含まれます。 それ以外は、この列は NULL です。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|データ型が間隔のデータ型の場合は、この列は間隔の先頭有効桁数の値を格納します。 (を参照してください[Interval データ型の有効桁数](../../../odbc/reference/appendixes/interval-data-type-precision.md)付録 d:データ型です。)それ以外は、この列は NULL です。|  
  
 属性情報は、結果セット内の特定の列またはデータ型に適用できます。 **SQLGetTypeInfo**データ型に関連付けられている属性に関する情報を返します**SQLColAttribute**結果セット内の列に関連付けられている属性に関する情報を返します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|結果セット内の列に関する情報を返す|[SQLColAttribute 関数](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|ドライバーまたはデータ ソースに関する情報を返す|[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
