---
title: SQLProcedureColumns 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5a869d38782478b69ce47656455c38c2b4645b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005744"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLProcedureColumns**入力と出力のパラメーターとして指定したプロシージャの結果セットを構成する列の一覧を返します。 ドライバーは、指定したステートメントの結果として設定情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
 *カタログ名*  
 [入力]プロシージャのカタログ名。 ドライバーをドライバーがさまざまな Dbms、空の文字列からデータを取得する場合など、他ではなく一部のプロシージャのカタログをサポートしている場合 ("") のカタログはありません。 それらの手順を示します。 *CatalogName*文字列の検索パターンを含めることはできません。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*CatalogName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *CatalogName*は通常の引数です。 文字どおり、扱われ、そのケースは重要では。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 *NameLength1*  
 [入力]文字の長さ **CatalogName*します。  
  
 *スキーマ名*  
 [入力]プロシージャのスキーマ名の文字列の検索パターン。 ドライバーをドライバーがさまざまな Dbms、空の文字列からデータを取得する場合など、他ではなく一部のプロシージャのスキーマをサポートしている場合 ("") のスキーマはありません。 それらの手順を示します。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*SchemaName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *SchemaName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength2*  
 [入力]文字の長さ **SchemaName*します。  
  
 *ProcName*  
 [入力]プロシージャ名の文字列の検索パターン。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*ProcName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *ProcName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength3*  
 [入力]文字の長さ **ProcName*します。  
  
 *[ColumnName]*  
 [入力]列名の文字列の検索パターン。  
  
 SQL_ATTR_METADATA_ID ステートメント属性は、SQL_TRUE に設定されている場合*ColumnName*は識別子として扱われますそのケースは重要ではありません。 場合は sql_false になります、 *ColumnName*パターン引数の値は、; 文字どおり、扱われ、そのケースは重要です。  
  
 *NameLength4*  
 [入力]文字の長さ **ColumnName*します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLProcedureColumns** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType*sql_handle_stmt としての*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLProcedureColumns** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前に、ドライバーによって返されるについての説明マネージャー。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|24000|カーソル状態が無効|カーソルが開いて、 *StatementHandle*、および**SQLFetch**または**SQLFetchScroll**が呼び出されました。 このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。<br /><br /> カーソルが開いて、 *StatementHandle*が**SQLFetch**または**SQLFetchScroll**呼び出されていない必要があります。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|、この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLError**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*します。 後でもう一度関数が呼び出された、 *StatementHandle*します。<br /><br /> 関数が呼び出された、および実行を完了する前に**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY009|無効な null ポインターの使用|SQL_ATTR_METADATA_ID のステートメント属性、SQL_TRUE に設定されて、 *CatalogName*引数が null ポインターの場合は、および、SQL_CATALOG_NAME*情報の種類*カタログ名を返しますがサポートされています。<br /><br /> (DM) SQL_ATTR_METADATA_ID ステートメント属性の SQL_TRUE に設定された、 *SchemaName*、 *ProcName*、または*ColumnName*引数が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 SQLProcedureColumns 関数が呼び出されたときにも、この aynschronous 関数が実行されました。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 名の長の引数のいずれかの値が 0 未満でしたが、SQL_NTS と等しくありません。<br /><br /> 名の長の引数のいずれかの値には、対応するカタログ、スキーマ、プロシージャ、または列名の最大長の値を超えています。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能な機能が実装されていません|プロシージャのカタログが指定されていると、ドライバーまたはデータ ソースがカタログをサポートしていません。<br /><br /> プロシージャのスキーマが指定されていると、ドライバーまたはデータ ソース スキーマはサポートしません。<br /><br /> プロシージャのスキーマ、プロシージャ名、または列名、文字列の検索パターンが指定されて、データ ソースがこれらの引数の 1 つ以上の検索パターンをサポートしていません。<br /><br /> SQL_ATTR_CURSOR_TYPE、SQL_ATTR_CONCURRENCY ステートメント属性の現在の設定の組み合わせが、ドライバーまたはデータ ソースでサポートされていません。<br /><br /> SQL_ATTR_USE_BOOKMARKS ステートメント属性は SQL_UB_VARIABLE に設定されており、SQL_ATTR_CURSOR_TYPE ステートメント属性は、ドライバーがブックマークをできません、カーソルの種類に設定されました。|  
|HYT00|タイムアウトが発生しました|データ ソースには、結果セットが返される前に、タイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 この関数は、プロシージャのパラメーターと存在する場合、結果セットまたはプロシージャによって返されたセットを構成する列についての情報を取得するステートメントを実行する前に通常使用されます。 詳細については、「[プロシージャ](../../../odbc/reference/develop-app/procedures-odbc.md)」を参照してください。  
  
> [!NOTE]  
>  **SQLProcedureColumns**プロシージャで使用されるすべての列が返されない可能性があります。 たとえば、ドライバーは、プロシージャ、および生成の結果セットの列によって使用されるパラメーターに関する情報だけを返す可能性があります。  
  
 *SchemaName*、 *ProcName*、および*ColumnName*引数は、検索パターンをそのまま使用します。 有効な検索パターンの詳細については、次を参照してください。[パターン値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)します。  
  
> [!NOTE]  
>  一般的な使用、引数、および ODBC カタログ関数の返されたデータの詳細については、次を参照してください。[カタログ関数](../../../odbc/reference/develop-app/catalog-functions.md)します。  
  
 **SQLProcedureColumns** PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME、および COLUMN_TYPE 順に並べ、標準的な結果セットとして結果を返します。 次の順序で各プロシージャの列名が返されます。 戻り値の名前、プロシージャの呼び出し (呼び出し順) での各パラメーターの名前、および (列の順序) で、プロシージャによって返される結果セット内の各列の名前。  
  
 アプリケーションでは、結果セットの末尾からの相対ドライバー固有の列をバインドする必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
 アプリケーションが呼び出すことができますを PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME、および COLUMN_NAME 列の実際の長さを判断する**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_ でPROCEDURE_NAME_LEN、および SQL_MAX_COLUMN_NAME_LEN オプション。  
  
 次の列は、ODBC 3 の名前に変更されています。*x*します。 列名の変更では、アプリケーションは、列番号でバインドため、旧バージョンとの互換性は影響しません。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|プロシージャ _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 によって返される結果セットに次の列が追加されている**SQLProcedureColumns** ODBC 3 *。x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 次の表には、結果セット内の列が一覧表示します。 ドライバーでは、19 (によって IS_NULLABLE) 列を超える追加の列を定義できます。 アプリケーションでは、明示的な序数位置を指定するのではなく、結果セットの末尾からカウント ダウンによって、ドライバー固有の列へのアクセスを得る必要があります。 詳細については、次を参照してください。[カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)します。  
  
|列名|列番号|データ型|コメント|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|プロシージャのカタログ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のプロシージャのカタログをサポートする場合 ("") のカタログはありません。 それらの手順。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|プロシージャのスキーマ名。データ ソースに適用されない場合は NULL です。 ドライバーの空の文字列を返します、ドライバーは、さまざまな Dbms からデータを取得するときなどに、他のユーザーではなく一部のプロシージャのスキーマをサポートする場合 ("") のスキーマはありません。 それらの手順。|  
|PROCEDURE_NAME (ODBC 2.0)|3|NULL 以外の Varchar|プロシージャの名前。 空の文字列には、名前がないプロシージャが返されます。|  
|COLUMN_NAME (ODBC 2.0)|4|NULL 以外の Varchar|プロシージャ列の名前。 ドライバーは、名前がないプロシージャ列の空の文字列を返します。|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint (NULL 以外)|プロシージャのパラメーターとして列または結果セット列を定義します。<br /><br /> SQL_PARAM_TYPE_UNKNOWN:プロシージャの列は、パラメーターの型が不明です。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT:プロシージャの列は、入力パラメーターです。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT:プロシージャの列は、入力/出力パラメーターです。 (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT:プロシージャの列は、出力パラメーターです。 (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE:プロシージャの列は、プロシージャの戻り値です。 (ODBC 2.0)<br /><br /> SQL_RESULT_COL:プロシージャの列は、結果セットの列です。 (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint (NULL 以外)|SQL データ型です。 これには、ODBC SQL データ型をまたはドライバーに固有の SQL データ型を指定できます。 Datetime と間隔のデータ型は、この列は、簡潔なデータ型 (たとえば、SQL_TYPE_TIME または SQL_INTERVAL_YEAR_TO_MONTH) を返します。 有効な ODBC SQL データ型の一覧は、次を参照してください[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)付録 d:。データ型。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。|  
|TYPE_NAME (ODBC 2.0)|7|NULL 以外の Varchar|データ ソースに依存するデータ型名です。たとえば、"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY"、または「CHAR FOR BIT DATA ()」。|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|データ ソースでプロシージャの列の列のサイズ。 NULL を返しますのデータ型の列のサイズは適用されません。 有効桁数をに関する詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型。|  
|BUFFER_LENGTH 列 (ODBC 2.0)|9|Integer|転送されるデータの長さ (バイト単位)、 **SQLGetData**または**SQLFetch** SQL_C_DEFAULT が指定されている場合に操作します。 数値データは、このサイズは、データ ソースに格納されたデータのサイズよりも異なる場合があります。 詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)、付録 d:。データ型。|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|データ ソースでプロシージャの列の 10 進数字。 NULL を返しますのデータ型の 10 進数字は適用されません。 詳細については 10 進数字、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)、付録 d:。データ型。|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|数値データ型の場合は、10、または 2 のいずれか。<br /><br /> 10 場合、COLUMN_SIZE と DECIMAL_DIGITS の値は、列に格納できる 10 進数字の数を提供します。 たとえば、DECIMAL(12,5) 列は 10、12、column_size 値と 5 は、DECIMAL_DIGITS の NUM_PREC_RADIX を返しますFLOAT 列では、10、15、column_size 値と NULL の DECIMAL_DIGITS の NUM_PREC_RADIX を返すことができます。<br /><br /> 2 の場合、COLUMN_SIZE と DECIMAL_DIGITS の値はビット列で許容数を提供します。 たとえば、FLOAT 列では、2 の 53、column_size 値と NULL の DECIMAL_DIGITS の NUM_PREC_RADIX を返すことができます。<br /><br /> NULL を返しますのデータ型 NUM_PREC_RADIX は適用されません。|  
|NULL 許容型 (ODBC 2.0)|12|Smallint (NULL 以外)|かどうか、プロシージャの列は NULL 値を受け取ります。<br /><br /> SQL_NO_NULLS:プロシージャの列は NULL 値を受け入れられません。<br /><br /> SQL_NULLABLE:プロシージャの列は、NULL 値を指定できます。<br /><br /> SQL_NULLABLE_UNKNOWN:プロシージャの列が NULL 値を受け取る場合は不明です。|  
|「解説」(ODBC 2.0)|13|Varchar|プロシージャの列の説明です。|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|列の既定値です。<br /><br /> 既定値として NULL が指定されている場合、この列は null の場合、引用符で囲まれていない、単語になります。 場合は切り捨てることがなく、既定値を表すことができない、このコラムでそれを囲む単一引用符が切り捨てられて、含まれています。 既定値が指定されていない場合、この列は NULL を使用します。<br /><br /> COLUMN_DEF の値は、切り捨てられた値が含まれている場合を除き、新しい列定義の生成に使用できます。|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint (NULL 以外)|記述子の SQL_DESC_TYPE フィールドとして、SQL データ型の値が表示されます。 この列は、datetime と間隔のデータ型を除く、DATA_TYPE 列と同じです。<br /><br /> Datetime と間隔のデータ型の SQL_INTERVAL または SQL_DATETIME、結果セットに SQL_DATA_TYPE フィールドを返すし、SQL_DATETIME_SUB フィールドには、特定の間隔または datetime データ型のサブコードが返されます。 (を参照してください[付録 d:データ型](../../../odbc/reference/appendixes/appendix-d-data-types.md))。|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|Datetime と間隔のデータ型のサブタイプ コード。 その他のデータ型の場合は、NULL が返されます。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|文字またはバイナリ データの最大長 (バイト単位) は、列を入力します。 他のすべてのデータ型の場合、この列は NULL を返します。|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer (NULL 以外)|入力と出力パラメーターの場合 (パラメーター、昇順に 1 から始まる) プロシージャの定義でパラメーターの序数位置。 戻り値 (ある場合)、0 が返されます。 結果内の列の序数位置が設定の結果セットの列に設定されている結果の最初の列番号は 1 です。 複数の結果セットがある場合は、ドライバー固有の方法で列の序数位置が返されます。|  
|によって IS_NULLABLE (ODBC 3.0)|19|Varchar|"NO"、列に null 値が含まれていない場合。<br /><br /> "YES"場合は、列が null 値を含めることができます。<br /><br /> NULL が許可されているかどうかがわからない列は、長さ 0 の文字列を返します。<br /><br /> NULL 値の許容属性の検査は ISO の規則に従います。 ISO SQL に準拠している DBMS では、空文字列を返すことはできません。<br /><br /> この列に返される値は、NULLABLE 列に返される値とは異なります。 (Null 許容の列の説明を参照してください)。|  
  
## <a name="code-example"></a>コード例  
 参照してください[プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|バッファーを結果セット内の列にバインドします。|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|データ ソース内のプロシージャの一覧を返す|[SQLProcedures 関数](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
