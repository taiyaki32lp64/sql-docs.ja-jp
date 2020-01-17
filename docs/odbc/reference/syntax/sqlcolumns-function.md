---
title: SQLColumns 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8de1a2053913ee0339c58a4a27ccd45772487e77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118672"
---
# <a name="sqlcolumns-function"></a>SQLColumns 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。[グループを開く]  
  
 **まとめ**  
 **SQLColumns**指定したテーブルに列名の一覧を返します。 ドライバーは結果セットとして、指定したこの情報を返します*StatementHandle*します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カタログ名*  
 [入力]カタログの名前。 ドライバーは、いくつかのテーブルのドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく、カタログをサポートしている場合 ("") それらのテーブルのカタログがないことを示します。 *CatalogName*文字列の検索パターンを含めることはできません。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*CatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *CatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]文字の長さ **CatalogName*します。  
  
 *スキーマ名*  
 [入力]スキーマ名の文字列の検索パターン。 ドライバーは、ドライバーをさまざまな Dbms、空の文字列からデータを取得した場合など、他ではなく一部のテーブルのスキーマをサポートしている場合 ("") それらのテーブル スキーマがないことを示します。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*SchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *SchemaName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength2*  
 [入力]文字の長さ **SchemaName*します。  
  
 *TableName*  
 [入力]テーブル名の文字列の検索パターン。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*TableName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *TableName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength3*  
 [入力]文字の長さ **TableName*します。  
  
 *[ColumnName]*  
 [入力]列名の文字列の検索パターン。  
  
> [!NOTE]  
>  SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*ColumnName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *ColumnName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength4*  
 [入力]文字の長さ **ColumnName*します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLColumns** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLColumns** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *CatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *SchemaName*、 *TableName*、または*ColumnName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLColumns**関数が呼び出されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 名の長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。|  
|||名の長の引数のいずれかの値には、対応するカタログまたは名前の最大長の値を超えています。 各カタログまたは名前の最大長を呼び出すことによって取得できる**SQLGetInfo**で、*情報の種類*値。 (「コメントです」を参照してください)|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|カタログ名が指定されました、およびドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> スキーマ名を指定してから、およびドライバーまたはデータ ソースがスキーマをサポートしていません。<br /><br /> スキーマ名、テーブル名、または列名、文字列の検索パターンが指定されて、データ ソースがこれらの引数の 1 つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、クエリのタイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 この関数通常は使用ステートメントを実行する前に、データ ソースのカタログからテーブルまたはテーブルの列に関する情報を取得します。 **SQLColumns**によって返される項目のすべての種類のデータを取得するために使用できる**SQLTables**します。 ベース テーブルだけでなくこの可能性があります (ただし、これに限定されません) ビュー、シノニム、システム テーブル、およびなど。 一方、関数によって**SQLColAttribute**と**SQLDescribeCol**結果セットと、関数内の列について説明する**SQLNumResultCols**の数を返します結果セット内の列。 詳細については、次を参照してください。[カタログ データの使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)します。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 **SQLColumns** TABLE_CAT、TABLE_SCHEM、TABLE_NAME、および ORDINAL_POSITION 順に並べ、標準的な結果セットとして結果を返します。  
  
> [!NOTE]  
>  ときに、アプリケーションは、ODBC 2 で動作します。*x*ドライバー、ORDINAL_POSITION 列が返されない結果セットにします。 結果として、ODBC 2 を使用する場合。*x*ドライバー、によって返される列リスト内の列の順序**SQLColumns**必ずしも列の順序と同じ場合は返されません、アプリケーションは、すべての SELECT ステートメントを実行そのテーブルの列。  
  
> [!NOTE]  
>  **SQLColumns**すべての列が返されない可能性があります。 たとえば、ドライバーでは、Oracle ROWID などの擬似列に関する情報は返さ可能性があります。 によって返されるかどうか、アプリケーションは、任意の有効な列を使用できます**SQLColumns**します。  
>   
>  一部の列によって返される**SQLStatistics**では返されません**SQLColumns**します。 たとえば、 **SQLColumns**式またはフィルター、給与 + メリットや部門などを介して作成されたインデックスの列を返さない 0012 を = です。  
  
 VARCHAR 列の長さは、テーブルには表示されません。実際の長さは、データ ソースに依存します。 アプリケーションが呼び出すことができますを TABLE_CAT、TABLE_SCHEM、TABLE_NAME、COLUMN_NAME、列の実際の長さを判断する**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN オプション。  
  
 次の列は、ODBC 3 の名前に変更されています。*x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 によって返される結果セットに次の列が追加されている**SQLColumns** ODBC 3 *。x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、18 (によって IS_NULLABLE) 列を超える追加の列を定義できます。 アプリケーションでは、結果の明示的な位置を表す序数を指定する代わりにセットの末尾からカウント ダウンして、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|[列]<br /><br /> number|データ型|コメント|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|カタログ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのカタログをサポートする場合 ("")、それらのテーブルのカタログがないです。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|スキーマ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のテーブルのスキーマをサポートする場合 ("")、それらのテーブル スキーマがないです。|  
|TABLE_NAME (ODBC 1.0)|3|NULL 以外の Varchar|テーブル名です。|  
|COLUMN_NAME (ODBC 1.0)|4|NULL 以外の Varchar|列名 ドライバーは、名前がない列の空の文字列を返します。|  
|DATA_TYPE (ODBC 1.0)|5|Smallint (NULL 以外)|SQL データ型です。 これには、ODBC SQL データ型をまたはドライバーに固有の SQL データ型を指定できます。 Datetime と間隔のデータ型は、この列は、(SQL_TYPE_DATE SQL_DATETIME または SQL_INTERVAL など nonconcise データ型ではなく、SQL_INTERVAL_YEAR_TO_MONTH など) の簡潔なデータ型を返します。 有効な ODBC SQL データ型の一覧は、次を参照してください[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d:。データ型。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。<br /><br /> ODBC 3 に対して返されるデータ型。*x*および ODBC 2 *。x*アプリケーションが異なる場合があります。 詳細については、次を参照してください。[旧バージョンとの互換性と標準準拠](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)します。|  
|TYPE_NAME (ODBC 1.0)|6|NULL 以外の Varchar|データ ソースに依存するデータ型名です。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINAR"または「CHAR FOR BIT DATA ()」。|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|DATA_TYPE が SQL_CHAR、SQL_VARCHAR またはの場合は、この列には、最大長列の文字にはが含まれます。 Datetime データ型の文字に変換された場合、値を表示するために必要な文字の合計数になります。 数値データ型の場合は、これは数字の合計数または合計 列で許可されているビット数のいずれかに従って NUM_PREC_RADIX 列です。 Interval データ型では、これは、文字形式のリテラルの間隔の文字数 (先頭の有効桁数の間隔によって定義されたを参照してください[Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)付録 d:。データ型の場合)。 詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|BUFFER_LENGTH 列 (ODBC 1.0)|8|Integer|SQL_C_DEFAULT が指定されている場合、データの長さ (バイト単位) は、SQLGetData、SQLFetch、または SQLFetchScroll 操作で転送されます。 数値データは、このサイズは、データ ソースに格納されているデータのサイズを異なる場合があります。 この値は、COLUMN_SIZE 列の文字データに対して異なる場合があります。 長さの詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|有効桁数、小数点の右側に合計数。 SQL_TYPE_TIME と sql_type_timestamp 型の場合は、この列には、秒の小数部のコンポーネントの桁数が含まれています。 他のデータ型では、これは、データ ソースの列の 10 進数字です。 時刻部分が含まれている interval データ型のこの列には、小数点 (秒の小数部) の右側にある数字の数が含まれています。 Interval データ型を時刻部分を含まない、この列は 0 です。 10 進数字の詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。 DECIMAL_DIGITS は適用されませんデータ型の NULL を返します。|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|数値データ型の場合は、10、または 2 のいずれか。 10 の場合は、COLUMN_SIZE と DECIMAL_DIGITS の値は、列に格納できる 10 進数字の数を提供します。 たとえば、DECIMAL(12,5) 列は 10、12、column_size 値と 5 は、DECIMAL_DIGITS の NUM_PREC_RADIX を返しますFLOAT 列では、10、15、column_size 値と NULL の DECIMAL_DIGITS の NUM_PREC_RADIX を返すことができます。<br /><br /> 2 の場合は、COLUMN_SIZE と DECIMAL_DIGITS の値はビット列で許容数を提供します。 たとえば、FLOAT 列では、第 2 の 53、column_size 値と NULL の DECIMAL_DIGITS の基数を返すことができます。<br /><br /> NULL を返しますのデータ型 NUM_PREC_RADIX は適用されません。|  
|NULL 許容型 (ODBC 1.0)|11|Smallint (NULL 以外)|SQL_NO_NULLS 列が含まれていない場合は NULL 値です。<br /><br /> SQL_NULLABLE 列で NULL 値許容される場合。<br /><br /> SQL_NULLABLE_UNKNOWN 列が NULL 値を受け入れるかどうかが不明である場合。<br /><br /> この列に返される値は、によって IS_NULLABLE 列に返される値によって異なります。 列が null 値を受け入れることができますが、列が null 値を受け付けないことで示すことはできませんの確実性で null 許容の列を示します。 によって IS_NULLABLE 列は、列が null 値を受け入れることはできませんが、確実性の列が null 値を受け入れることを示すことはできません、確信を示します。|  
|「解説」(ODBC 1.0)|12|Varchar|列の説明。|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|列の既定値です。 引用符で囲まれている場合、この列の値を文字列として解釈する必要があります。<br /><br /> 既定値として NULL が指定されている場合、この列は null の場合、引用符で囲まれていない、単語になります。 場合は切り捨てることがなく、既定値を表すことができない、単一引用符に囲まれていないが切り捨てられて、この列が含まれます。 既定値が指定されていない場合、この列は NULL を使用します。<br /><br /> COLUMN_DEF の値は、切り捨てられた値が含まれている場合を除き、新しい列定義の生成に使用できます。|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint (NULL 以外)|SQL データ型、IRD の SQL_DESC_TYPE レコード フィールドに表示されます。 これには、ODBC SQL データ型をまたはドライバーに固有の SQL データ型を指定できます。 この列は、datetime と間隔のデータ型を除く、DATA_TYPE 列と同じです。 この列は、datetime (SQL_TYPE_DATE SQL_INTERVAL_YEAR_TO_MONTH など) の簡潔なデータ型と interval データ型ではなく (SQL_DATETIME または SQL_INTERVAL) などの nonconcise データ型を返します。 SQL_DATETIME または SQL_INTERVAL にこの列が返される場合は、SQL_DATETIME_SUB 列から特定のデータ型を決定できます。 有効な ODBC SQL データ型の一覧は、次を参照してください[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d:。データ型。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。<br /><br /> ODBC 3 に対して返されるデータ型。*x*および ODBC 2 *。x*アプリケーションが異なる場合があります。 詳細については、次を参照してください。[旧バージョンとの互換性と標準準拠](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)します。|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|Datetime と間隔のデータ型のサブタイプ コード。 その他のデータ型の場合は、NULL が返されます。 Datetime と間隔サブコードの詳細についてを参照してください"SQL_DESC_DATETIME_INTERVAL_CODE" [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|文字またはバイナリ データの最大長 (バイト単位) は、列を入力します。 他のすべてのデータ型の場合、この列は NULL を返します。|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer (NULL 以外)|テーブル内の列の序数位置です。 テーブルの最初の列の番号は 1 です。|  
|によって IS_NULLABLE (ODBC 3.0)|18|Varchar|"NO"、列に null 値が含まれていない場合。<br /><br /> "YES"場合は、列が null 値を含めることができます。<br /><br /> NULL が許可されているかどうかがわからない列は、長さ 0 の文字列を返します。<br /><br /> NULL 値の許容属性の検査は ISO の規則に従います。 ISO SQL に準拠している DBMS では、空文字列を返すことはできません。<br /><br /> この列に返される値は null 許容の列に返される値によって異なります。 (Null 許容の列の説明を参照してください)。|  
  
## <a name="code-example"></a>コード例  
 次の例では、アプリケーションによって返される結果セットのバッファーを宣言して**SQLColumns**します。 呼び出す**SQLColumns**を従業員テーブル内の各列を表す結果セットを返します。 呼び出して**SQLBindCol**バッファーに結果セットで列をバインドします。 アプリケーションでデータの各行をフェッチする最後に、 **SQLFetch**しそれを処理します。  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|列または列に対する権限を返す|[SQLColumnPrivileges 関数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|複数行のデータをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|行を一意に識別する列または列が自動的にトランザクションによって更新を取得します。|[SQLSpecialColumns 関数](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|テーブルの統計情報とインデックスを返す|[SQLStatistics 関数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|データ ソース内のテーブルの一覧を返す|[SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)|  
|テーブルまたはテーブルに対する権限を返す|[SQLTablePrivileges 関数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
