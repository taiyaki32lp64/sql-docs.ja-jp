---
title: SQLGetInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e62e7aaba276643a2874a22e74a08214cfe51e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030662"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLGetInfo**接続に関連付けられているドライバーとデータ ソースに関する一般的な情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *情報の種類*  
 [入力]情報の種類。  
  
 *InfoValuePtr*  
 [出力]情報を返すバッファーへのポインター。 に応じて、*情報の種類*要求されると、返される情報が、次のいずれか: null で終わる文字列、SQLUSMALLINT 値を、SQLUINTEGER ビットマスク、SQLUINTEGER フラグ、SQLUINTEGER バイナリ値の場合、または値の sqlulen です。  
  
 場合、*情報の種類*引数が SQL_DRIVER_HDESC または SQL_DRIVER_HSTMT、 *InfoValuePtr*引数が入力し、出力します。 (詳細についてはこの関数の説明の後で SQL_DRIVER_HDESC または SQL_DRIVER_HSTMT 記述子を参照してください)。  
  
 場合*InfoValuePtr*が null の場合、 *StringLengthPtr*はまだバイト (文字データの null 終端文字を除く) の合計数を返しますが指すバッファーに返される使用可能な*InfoValuePtr*します。  
  
 *BufferLength*  
 [入力]長さ、 \* *InfoValuePtr*バッファー。 場合の値 *\*InfoValuePtr*文字の文字列でない場合、または*InfoValuePtr*が null ポインターの場合、 *BufferLength*引数は無視されます。 ドライバーを前提としているサイズの *\*InfoValuePtr* SQLUSMALLINT またはに基づいて SQLUINTEGER、*情報の種類*。 場合 *\*InfoValuePtr*は Unicode 文字列です (呼び出し時に**SQLGetInfoW**)、 *BufferLength*引数は、SQLSTATE HY090 (そうでない場合は偶数にする必要があります文字列またはバッファーの長さが無効です) が返されます。  
  
 *StringLengthPtr*  
 [出力]バイト (文字データの null 終端文字を除く) の合計数を返すバッファーへのポインターで返される使用可能な **InfoValuePtr*します。  
  
 返される使用可能なバイト数がより大きいまたは等しい場合は、文字データ*BufferLength*の情報は、 \* *InfoValuePtr*に切り捨てられます*BufferLength* null 終了の長さマイナス バイト文字し、は、ドライバーが null で終わります。  
  
 他のすべての種類の値のデータの*BufferLength*は無視されますと、ドライバーのサイズを想定しています\* *InfoValuePtr* SQLUSMALLINT または SQLUINTEGER、によっては、 *情報の種類*します。  
  
## <a name="return-value"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetInfo** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_dbc として、*処理*の*ConnectionHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLGetInfo** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *InfoValuePtr*要求されたすべての情報を返すのに十分な大きさがありません。 そのため、情報が切り捨てられました。 切り詰められていない形式で要求された情報の長さが返される **StringLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続は開いていません|(DM) で情報の種類が要求された*情報の種類*に対して開いている接続が必要です。 ODBC によって予約されている情報の種類の接続を開くことがなく SQL_ODBC_VER のみが返されます。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY024|無効な属性値|(DM)、*情報の種類*引数が SQL_DRIVER_HSTMT、およびによって示される値*InfoValuePtr*が有効なステートメント ハンドル。<br /><br /> (DM)、*情報の種類*引数が SQL_DRIVER_HDESC、およびによって示される値*InfoValuePtr*が有効な記述子ハンドル。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*BufferLength*が 0 未満でした。<br /><br /> (DM) の指定された値*BufferLength* 、奇数と *\*InfoValuePtr*されましたが、Unicode データ型。|  
|HY096|範囲外の情報の種類|引数が指定された値*情報の種類*ODBC ドライバーでサポートされているのバージョンには無効です。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYC00|省略可能なフィールドが実装されていません|引数が指定された値*情報の種類*がドライバーによってサポートされていないドライバー固有の値。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に対応するドライバー、 *ConnectionHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 現在定義されている情報の種類が「情報の種類、」このセクションの後半で示すように詳細は、さまざまなデータ ソースを活用するために定義することが期待されます。 さまざまな情報の種類が ODBC; によって予約されていますドライバー開発者向けには、Open Group から個々 のドライバーの使用するための値を予約する必要があります。 **SQLGetInfo** Unicode 変換は行われませんか*サンキング*(を参照してください[付録 a:ODBC エラー コード](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)の*ODBC プログラマ リファレンス*) のドライバー定義*InfoTypes*します。 詳細については、次を参照してください。[ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)します。 返される情報の形式\* *InfoValuePtr*によって異なります、*情報の種類*を要求します。 **SQLGetInfo**で 5 つの異なる形式のいずれかの情報が返されます。  
  
-   Null で終わる文字列  
  
-   SQLUSMALLINT 値  
  
-   SQLUINTEGER ビットマスク  
  
-   SQLUINTEGER 値  
  
-   SQLUINTEGER バイナリ値  
  
 形式は次の情報の種類のそれぞれは、型の説明に記録されます。 アプリケーションに返される値をキャストする必要があります **InfoValuePtr*それに応じて。 アプリケーションが SQLUINTEGER ビットマスクからデータを取得できる方法の例は、「コードの使用例」を参照してください。  
  
 ドライバーは、次の表で定義されている情報の種類ごとの値を返す必要があります。 情報の種類が、ドライバーまたはデータ ソースに適用されない場合、ドライバーは、次の表に記載した値のいずれかを返します。  
  
 文字の文字列 ("Y"または"N")  
 "N"  
  
 文字の文字列 ("Y"または"N"ではありません)  
 空の文字列  
  
 SQLUSMALLINT  
 0  
  
 SQLUINTEGER ビットマスクまたは SQLUINTEGER バイナリ値  
 0 L  
  
 たとえば、データ ソースは、プロシージャをサポートしていない場合**SQLGetInfo**の値については、次の表に記載した値を返します*情報の種類*プロシージャに関連します。  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 空の文字列  
  
 **SQLGetInfo** SQLSTATE HY096 を返します (無効な引数値) の値の*情報の種類*を ODBC で使用するために予約されている情報の種類の範囲内にあるが、ドライバーでサポートされている ODBC のバージョンで定義されていません。 アプリケーションを呼び出す ODBC のバージョンに準拠しているドライバーを特定する**SQLGetInfo** SQL_DRIVER_ODBC_VER 情報の種類にします。 **SQLGetInfo** SQLSTATE HYC00 を返します (省略可能な機能が実装されていません) の値の*情報の種類*ドライバー固有の使用のため予約の種類の情報の範囲内にあるは、ドライバーではサポートされていません。  
  
 すべての呼び出しを**SQLGetInfo**場合を除き、開いている接続が必要、*情報の種類*は SQL_ODBC_VER で、ドライバー マネージャーのバージョンを返します。  
  
## <a name="information-types"></a>情報の種類  
 このセクションでサポートされている情報の種類を一覧表示**SQLGetInfo**します。 情報の種類が明確にグループ化し、アルファベット順に表示します。 情報の種類を追加または ODBC 3 の名前が変更された *.x*も一覧表示されます。  
  
## <a name="driver-information"></a>ドライバー情報  
 次の値の*情報の種類*引数には、アクティブなステートメント、データ ソース名、およびインターフェイスの標準準拠のレベルの数など、ODBC ドライバーに関する情報が返されます。  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  実装するときに**SQLGetInfo**ドライバーは、情報の送信や、サーバーから要求された回数を最小限に抑えることでパフォーマンスを向上できます。  
  
## <a name="dbms-product-information"></a>DBMS の製品情報  
 次の値の*情報の種類*引数には、DBMS 名とバージョンなど、DBMS の製品に関する情報が返されます。  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>データ ソース情報  
 次の値の*情報の種類*引数には、カーソルの特性とトランザクション機能など、データ ソースに関する情報が返されます。  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>サポートされている SQL  
 次の値の*情報の種類*引数には、データ ソースでサポートされる SQL ステートメントの詳細についての情報が返されます。 これらの情報の種類によって説明されている各機能の SQL 構文は、SQL 92 構文です。 これらの情報の種類は、徹底的全体の SQL 92 文法を説明しません。 代わりに、データのソース通常提供さまざまなレベルのサポートの文法の部品がについて説明します。 具体的には、ほとんどの SQL 92 で DDL ステートメントがについて説明します。  
  
 アプリケーションは、SQL_SQL_CONFORMANCE 情報の種類からサポートされている文法の一般的なレベルを決定して、その他の情報の種類を使用して、示された標準準拠のレベルからのバリエーションを特定する必要があります。  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>SQL の制限事項  
 次の値の*情報の種類*引数には、識別子および識別子と、選択リスト内の列の最大数の最大の長さなどの SQL ステートメントの句に適用される制限についての情報が返されます。 制限事項は、ドライバーまたはデータ ソースのいずれかによって課されることができます。  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>スカラー関数の情報  
 次の値の*情報の種類*引数は、データ ソースと、ドライバーでサポートされているスカラー関数に関する情報を返します。 スカラー関数の詳細については、次を参照してください[付録 e:。スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)します。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>変換情報  
 次の値の*情報の種類*引数は、データ ソースが指定した SQL データ型を変換できる、SQL データ型の一覧を返す、**変換**スカラー関数。  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>情報の種類の追加の ODBC 3.x  
 次の値の*情報の種類*引数に追加された ODBC 3 *.x*:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>ODBC の名前が変更の種類の情報 3.x  
 次の値の*情報の種類*ODBC 3 の名前を変更した引数 *.x*します。  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>情報の種類が ODBC で非推奨と 3.x  
 次の値の*情報の種類*ODBC 3 引数が非推奨とされました *.x*します。 ODBC 3 *.x*ドライバーは ODBC 2 の旧バージョンと互換性のため、これらの情報の種類をサポートするために続行する必要があります *.x*アプリケーション。 (これらの種類の詳細については、次を参照してください[SQLGetInfo のサポート](../../../odbc/reference/appendixes/sqlgetinfo-support.md)で付録 g:。ドライバーに関するガイドラインの下位互換性です。)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>情報の種類の説明  
 次の表は、各情報の種類、バージョンが導入された ODBC とその説明のアルファベット順に一覧表示します。  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 文字の文字列。ユーザーは、によって返されるすべてのプロシージャを実行できる場合は"Y" **SQLProcedures**;"N"プロシージャが可能性がある場合は、ユーザーが実行できないことを返されます。  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 文字の文字列。"Y"、ユーザーが保証される場合**選択**によって返されるすべてのテーブルに特権**SQLTables**;ユーザーがアクセスできない場合、テーブルがある可能性があります"N"が返されます。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 ドライバーがサポートできるアクティブな環境の最大数を示す SQLUSMALLINT 値を指定します。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 集計関数のサポートを列挙する SQLUINTEGER ビットマスク。  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 サポートされている、SQL 92 エントリのレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **ALTER ドメイン**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。 SQL 92 完全レベル準拠のドライバーは、すべてのビットマスクを常に返します。 「0」の戻り値。 つまり、 **ALTER ドメイン**ステートメントはサポートされていません。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 追加のドメインの制約がサポートされています (フル レベル)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT =\<ドメインが alter > \<set ドメイン既定句 > はサポートされています (フル レベル)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<制約定義名句 > はドメインの制約 (中間レベル) の名前付けのサポートされています  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop ドメイン制約句 > はサポートされています (フル レベル)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT =\<ドメインが alter > \<drop ドメイン既定句 > はサポートされています (フル レベル)  
  
 次のビットをサポートされている指定\<制約属性 > 場合\<ドメインの制約の追加 > はサポートされて (SQL_AD_ADD_DOMAIN_CONSTRAINT ビットが設定されます)。  
  
 (完全レベル) SQL_AD_ADD_CONSTRAINT_DEFERRABLE SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (完全レベル) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (完全レベル) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (完全レベル)  
  
 SQL_ALTER_TABLE(ODBC 2.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **ALTER TABLE**ステートメント、データ ソースでサポートされています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<列の追加 > 句はサポートされて、列の照合順序 (完全レベル) を指定する機能を使用 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<列の追加 > 句はサポートされて、列の既定値 (FIPS 過渡期レベル) を指定する機能を使用 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<列の追加 > は (FIPS 過渡期レベル) のサポート (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<列の追加 > 句はサポートされて、列の制約 (FIPS 過渡期レベル) を指定する機能を使用 (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<テーブル制約の追加 > 句がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<制約名の定義 > 列およびテーブルの制約 (中間レベル) の名前付けはサポートされて (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<列の削除 > CASCADE がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter 列 > \<drop 列の既定の句 > は、(中間レベル) をサポート (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<列の削除 > 制限がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<列の削除 > 制限がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter 列 >\<セット列の既定の句 > は、(中間レベル) をサポート (ODBC 3.0)  
  
 次のビットのサポートを指定する\<制約属性 > 列またはテーブルの制約を指定することがサポートされている場合 (SQL_AT_ADD_CONSTRAINT ビットが設定されます)。  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (完全レベル) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (完全レベル) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (完全レベル) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (完全レベル) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 かどうか、ドライバーに対して実行できます関数非同期接続ハンドルを示す SQLUINTEGER 値。  
  
 SQL_ASYNC_DBC_CAPABLE = ドライバーでは、接続の機能を非同期的に実行できます。  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = ドライバーの接続の機能を非同期的に実行しないことができます。  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 ドライバーでの非同期サポートのレベルを示す SQLUINTEGER 値:  
  
 SQL_AM_CONNECTION = 接続レベルの非同期実行がサポートされています。 指定された接続ハンドルに関連付けられたすべてのステートメント ハンドルは非同期モードか、同期モードではすべて。 接続のステートメント ハンドルは、同じ接続上の別のステートメント ハンドルが同期モードでは、その逆で非同期モードですることはできません。  
  
 SQL_AM_STATEMENT = ステートメント レベルの非同期実行がサポートされています。 接続ハンドルに関連付けられたステートメント ハンドルをいくつかは、同じ接続上で他のステートメント ハンドルを同期モードでは、非同期モードで指定できます。  
  
 SQL_AM_NONE = 非同期モードはサポートされていません。  
  
 SQL_ASYNC_NOTIFICATION  
 ドライバーが非同期通知をサポートしているかを示す SQLUINTEGER 値:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE**非同期実行の通知が、ドライバーによってサポートされています。  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE**非同期実行の通知は、ドライバーによってサポートされていません。  
  
 ODBC の非同期操作の 2 つのカテゴリがあります: 接続レベルの非同期操作およびステートメント レベルの非同期操作。  ドライバー SQL_ASYNC_NOTIFICATION_CAPABLE を返す場合は、非同期的に実行できるすべての Api の通知をサポートしてする必要があります。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 行の可用性に関して、ドライバーの動作を列挙する SQLUINTEGER ビットマスクをカウントします。 情報の種類と共に、次の各ビットマスクが使用されます。  
  
 SQL_BRC_ROLLED_UP = 行カウントの連続する INSERT、DELETE、または UPDATE ステートメントが 1 つにロール アップされます。 このビットが設定されていない場合の行数は各ステートメントで使用できます。  
  
 SQL_BRC_PROCEDURES バッチがストアド プロシージャで実行されると、いずれかが使用可能な場合は、行の数を = です。 行カウントが使用可能な場合は、上または SQL_BRC_ROLLED_UP ビットによって、個別に使用できる、ロールバックすることができます。  
  
 SQL_BRC_EXPLICIT バッチを呼び出すことによって直接実行すると、いずれかが使用可能な場合は、行の数を = **SQLExecute**または**SQLExecDirect**します。 行カウントが使用可能な場合は、上または SQL_BRC_ROLLED_UP ビットによって、個別に使用できる、ロールバックすることができます。  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 バッチのドライバーのサポートを列挙する SQLUINTEGER ビットマスク。 次のビットマスクを使用して、どのレベルがサポートされているを調べます。  
  
 SQL_BS_SELECT_EXPLICIT できますが結果セットのステートメントを生成するドライバー サポートの明示的なバッチを = です。  
  
 SQL_BS_ROW_COUNT_EXPLICIT =、ドライバー サポート明示的なバッチを生成するステートメントの行の数を持つことができます。  
  
 SQL_BS_SELECT_PROC できますが結果セットのステートメントを生成するドライバー サポート明示的なプロシージャを = です。  
  
 SQL_BS_ROW_COUNT_PROC 生成するステートメントの行の数を持つドライバー サポート明示的なプロシージャを = です。  
  
 SQL_BOOKMARK_PERSISTENCE(ODBC 2.0)  
 ブックマークの永続化、操作を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクは、オプションのブックマークが保持されるかを決定するフラグと共に使用されます。  
  
 SQL_BP_CLOSE = アプリケーションを呼び出してから、ブックマークは有効な**SQLFreeStmt** SQL_CLOSE オプション、または**SQLCloseCursor**ステートメントに関連付けられているカーソルを閉じます。  
  
 SQL_BP_DELETE、行が有効ではその行が削除された後、ブックマークを = です。  
  
 SQL_BP_DROP = アプリケーションを呼び出してから、ブックマークは有効な**SQLFreeHandle**で、 *HandleType* sql_handle_stmt としてステートメントを削除するのです。  
  
 SQL_BP_TRANSACTION = アプリケーションがコミットまたはトランザクションをロールバックした後、ブックマークは有効です。  
  
 SQL_BP_UPDATE 行が有効ではキー列を含め、その行の任意の列が更新された後、ブックマークを = です。  
  
 SQL_BP_OTHER_HSTMT いずれかに関連付けられているブックマークを = 別のステートメントでステートメントを使用することができます。 SQL_BP_CLOSE または SQL_BP_DROP を指定しない場合は、最初のステートメントでカーソルが開く必要があります。  
  
 SQL_CATALOG_LOCATION(ODBC 2.0)  
 修飾テーブル名で、カタログの位置を示す SQLUSMALLINT 値を指定します。  
  
 SQL_CL_STARTSQL_CL_END  
  
 たとえば、ディレクトリ (カタログ) 名は \EMPDATA\EMP のように、テーブル名の先頭にあるため、Xbase ドライバーは SQL_CL_START を返します。DBF します。 カタログとしてでは、テーブル名の末尾にあるため、ORACLE サーバーのドライバーが SQL_CL_END を返しますADMIN.EMP@EMPDATAします。  
  
 SQL 92 フルのレベルに準拠のドライバーでは、SQL_CL_START は常に返します。 カタログは、データ ソースではサポートされていない場合、値 0 が返されます。 カタログはサポートされているかどうかを決定するには、アプリケーションが呼び出す**SQLGetInfo** SQL_CATALOG_NAME 情報の種類にします。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_QUALIFIER_LOCATION します。  
  
 SQL_CATALOG_NAME(ODBC 3.0)  
 文字の文字列。"Y"そうでない場合、カタログ名または"N"をサーバーがサポートする場合。  
  
 SQL 92 フルのレベルに準拠のドライバーでは、"Y"は常に返します。  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1.0)  
 文字の文字列: カタログ名、および依存するか、その前にあるされる修飾名要素間の区切り記号として、データ ソースを定義する文字。  
  
 カタログは、データ ソースではサポートされていない場合は、空の文字列が返されます。 カタログはサポートされているかどうかを決定するには、アプリケーションが呼び出す**SQLGetInfo** SQL_CATALOG_NAME 情報の種類にします。 SQL 92 フルのレベルに準拠のドライバーは常に返します"."です。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_QUALIFIER_NAME_SEPARATOR します。  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 カタログ; のデータ ソースの仕入先の名前を持つ文字の文字列たとえば、"database"または"directory"。 この文字列は、上部、下部、または大文字と小文字にすることができます。  
  
 カタログは、データ ソースではサポートされていない場合は、空の文字列が返されます。 カタログはサポートされているかどうかを決定するには、アプリケーションが呼び出す**SQLGetInfo** SQL_CATALOG_NAME 情報の種類にします。 「カタログ」は、SQL 92 全体のレベルに準拠ドライバーによって常に返します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_QUALIFIER_TERM します。  
  
 SQL_CATALOG_USAGE(ODBC 2.0)  
 カタログを使用できるステートメントを列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用して、カタログを使用できる場所を調べます。  
  
 SQL_CU_DML_STATEMENTS = カタログがすべてのデータ操作言語ステートメントでサポートされています。**選択**、**挿入**、**更新**、**削除**、サポートされている場合**更新の選択**と位置指定更新と削除ステートメント。  
  
 SQL_CU_PROCEDURE_INVOCATION = カタログは ODBC のプロシージャ呼び出しステートメントでサポートされています。  
  
 SQL_CU_TABLE_DEFINITION = カタログがすべてのテーブル定義ステートメントでサポートされています。**テーブルを作成する**、**ビューを作成する**、 **ALTER TABLE**、 **DROP TABLE**、および**ドロップ ビュー**します。  
  
 SQL_CU_INDEX_DEFINITION = カタログがすべてのインデックス定義ステートメントでサポートされています。**インデックス作成**と**DROP INDEX**します。  
  
 SQL_CU_PRIVILEGE_DEFINITION = カタログがすべての特権定義ステートメントでサポートされています。**GRANT**と**取り消す**します。  
  
 カタログは、データ ソースではサポートされていない場合、値 0 が返されます。 カタログはサポートされているかどうかを決定するには、アプリケーションが呼び出す**SQLGetInfo** SQL_CATALOG_NAME 情報の種類にします。 SQL 92 フルのレベルに準拠のドライバーは、これらのビット セットのすべてのビットマスクを常に返します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_QUALIFIER_USAGE します。  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 照合順序の名前。 これは、既定の文字がこのサーバーの設定の既定の照合順序の名前を示す文字列 (たとえば、' ISO 8859-1' または EBCDIC)。 これが不明の場合は空の文字列が返されます。 SQL 92 フルのレベルに準拠のドライバーは、空でない文字列を常に返します。  
  
 SQL_COLUMN_ALIAS(ODBC 2.0)  
 文字の文字列。"Y"データ ソースは、列の別名をサポートしている場合それ以外の場合、"N"です。  
  
 列の別名は、AS 句を使用して、選択リスト内の列に指定できる代替名です。 SQL 92 エントリのレベルに準拠ドライバーでは、"Y"は常に返します。  
  
 SQL_CONCAT_NULL_BEHAVIOR(ODBC 1.0)  
 データ ソースが NULL を連結したものを処理する方法を示す SQLUSMALLINT 値は、NULL 以外の値を持つ文字データ型の列を文字データ型の列を値しました。  
  
 SQL_CB_ = NULL 値になります。  
  
 SQL_CB_NON_ = NULL 以外の値を持つ列または列の連結になります。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、SQL_CB_ は常に返します。  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 SQLUINTEGER ビットマスク。 ビットマスクを持つデータ ソースでサポートされる変換を示します、**変換**でという名前の型のデータのスカラー関数、*情報の種類*します。 ビットマスクが 0 の場合、データ ソースには、同じデータ型への変換を含む、名前付きの型のデータから、変換はできません。  
  
 たとえば、データ ソースが SQL_INTEGER データの SQL_BIGINT データ型への変換をサポートしているかどうかを判断する、アプリケーション呼び出し**SQLGetInfo**で、*情報の種類*SQL_CONVERT_INTEGER の。 アプリケーションは、実行、 **AND** SQL_CVT_BIGINT と返されるビットマスクで操作します。 結果の値が 0 以外の場合は、変換はサポートされています。  
  
 次のビットマスクを使用して、どの変換がサポートされているを調べます。  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) (ODBC 1.0) SQL_CVT_DOUBLE SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME SQL_CVT_LONGVARBINARY (ODBC 1.0) (ODBC 1.0) SQL_CVT_LONGVARCHAR SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) (ODBC 1.0) SQL_CVT_SMALLINT SQL_CVT_TIME (ODBC 1.0) SQL_CVT_タイムスタンプ (ODBC 1.0) (ODBC 1.0) を SQL_CVT_TINYINT、SQL_CVT_VARBINARY、(ODBC 1.0)、SQL_CVT_VARCHAR、(ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 ドライバーと関連付けられているデータ ソースでサポートされているスカラー変換関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする変換関数を調べます。  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME(ODBC 1.0)  
 テーブルの相関名がサポートされているかどうかを示す SQLUSMALLINT 値を指定します。  
  
 SQL_CN_NONE = 関連付けの名前はサポートされていません。  
  
 SQL_CN_DIFFERENT = 相関名がサポートされますが、それらを表すテーブルの名前と異なる必要があります。  
  
 SQL_CN_ANY = 相関名はサポートされているし、有効なユーザー定義名を指定できます。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、SQL_CN_ANY は常に返します。  
  
 SQL_CREATE_ASSERTION(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**作成アサーション**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CA_CREATE_ASSERTION  
  
 制約の属性を明示的に指定する機能がサポートされている場合、次のビットがサポートされている制約属性を指定します (SQL_ALTER_TABLE と SQL_CREATE_TABLE 情報の種類を参照してください)。  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 サポートされている、SQL 92 完全のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。 「0」の戻り値。 つまり、**作成アサーション**ステートメントはサポートされていません。  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**文字セットの作成**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 サポートされている、SQL 92 完全のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。 「0」の戻り値。 つまり、**文字セットの作成**ステートメントはサポートされていません。  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**照合順序の作成**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CCOL_CREATE_COLLATION  
  
 SQL 92 フルのレベルに準拠ドライバーでは、サポートされているため、このオプションは常に返します。 「0」の戻り値。 つまり、**照合順序の作成**ステートメントはサポートされていません。  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**ドメインの作成**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CDO_CREATE_DOMAIN = ドメインの作成ステートメントがサポートされています (中間レベル)。  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION =\<制約名の定義 > は、ドメインの制約 (中間レベル) の名前付けのサポートされています。  
  
 次のビット列の制約: SQL_CDO_DEFAULT を作成する機能を指定する = ドメインの制約を指定することは (中間レベル) SQL_CDO_CONSTRAINT = ドメインの既定値を指定することは (中間レベル) SQL_CDO_COLLATION =ドメインの照合順序を指定することは (フル レベル)  
  
 ドメインの制約を指定することがサポートされている場合、次のビットがサポートされている制約の属性を指定 (SQL_CDO_DEFAULT が設定されます)。  
  
 (完全レベル) SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (完全レベル) SQL_CDO_CONSTRAINT_DEFERRABLE (完全レベル) SQL_CDO_CONSTRAINT_NON_DEFERRABLE (完全レベル)  
  
 「0」の戻り値。 つまり、**ドメインの作成**ステートメントはサポートされていません。  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **CREATE SCHEMA**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL 92 中間のレベルに準拠ドライバーでは、サポートされているため、および SQL_CS_AUTHORIZATION、SQL_CS_CREATE_SCHEMA オプションは常に返します。 また、SQL 92 エントリ レベルが SQL ステートメントとは限らないこれらもサポートする必要があります。 サポートされている、SQL 92 完全のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **CREATE TABLE**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CT_CREATE_TABLE =、CREATE TABLE ステートメントがサポートされています。 (エントリ レベル)  
  
 SQL_CT_TABLE_CONSTRAINT = テーブル制約を指定することは (FIPS 過渡期レベル)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION =、\<制約名の定義 > 句は、列およびテーブルの制約 (中間レベル) の名前付けのサポート  
  
 次のビットは、一時テーブルを作成する機能を指定します。  
  
 SQL_CT_COMMIT_PRESERVE = 削除された行がコミット時に保持されます。 (完全レベル)SQL_CT_COMMIT_DELETE = 削除された行がコミット時に削除されます。 (完全レベル)SQL_CT_GLOBAL_TEMPORARY = グローバル一時テーブルを作成できます。 (完全レベル)SQL_CT_LOCAL_TEMPORARY = ローカル一時テーブルを作成できます。 (完全レベル)  
  
 次のビットは、列の制約を作成する機能を指定します。  
  
 SQL_CT_COLUMN_CONSTRAINT = 列制約を指定することは (FIPS 過渡期レベル) SQL_CT_COLUMN_DEFAULT = 列の既定値を指定することは (FIPS 過渡期レベル) SQL_CT_COLUMN_COLLATION = 列の照合順序の指定サポートされる (完全レベル)  
  
 次のビットは、列またはテーブルの制約を指定することがサポートされている場合に、サポートされている制約の属性を指定します。  
  
 (完全レベル) SQL_CT_CONSTRAINT_INITIALLY_DEFERRED SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (完全レベル) SQL_CT_CONSTRAINT_DEFERRABLE (完全レベル) SQL_CT_CONSTRAINT_NON_DEFERRABLE (完全レベル)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**作成翻訳**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 SQL 92 全体のレベルに準拠ドライバーでは、サポートされているため、これらのオプションは常に返します。 「0」の戻り値。 つまり、**翻訳の作成**ステートメントはサポートされていません。  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **CREATE VIEW**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 「0」の戻り値。 つまり、 **CREATE VIEW**ステートメントはサポートされていません。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、サポートされている、および SQL_CV_CHECK_OPTION、SQL_CV_CREATE_VIEW オプションは常に返します。  
  
 サポートされている、SQL 92 完全のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 示す SQLUSMALLINT 値方法、**コミット**操作は、カーソルとデータ ソース (トランザクションをコミットするときに、データ ソースの動作) で準備されたステートメントに影響します。  
  
 この属性の値には、次の設定の現在の状態が反映されます。SQL_COPT_SS_PRESERVE_CURSORS します。  
  
 SQL_CB_DELETE = カーソルを閉じると、準備されたステートメントを削除します。 カーソルを使用するには、もう一度アプリケーションする必要がありますを再び準備し、ステートメントを再実行します。  
  
 SQL_CB_CLOSE 閉じるカーソルを = です。 アプリケーションを呼び出して、準備されたステートメントは、用**SQLExecute**呼び出さずに、ステートメントで**SQLPrepare**もう一度です。 SQL の ODBC ドライバーの既定値は、SQL_CB_CLOSE です。 これは、トランザクションをコミットするときに、SQL の ODBC ドライバーが、カーソルを閉じることを意味します。  
  
 SQL_CB_PRESERVE 以前と同じ位置にカーソルを保持を =、**コミット**操作。 アプリケーションがデータをフェッチし続けることができますか、カーソルを閉じる再準備せずに、ステートメントを再実行します。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1.0)  
 示す SQLUSMALLINT 値方法、**ロールバック**操作は、カーソルと準備されたステートメントでデータ ソースに影響します。  
  
 SQL_CB_DELETE = カーソルを閉じると、準備されたステートメントを削除します。 カーソルを使用するには、もう一度アプリケーションする必要がありますを再び準備し、ステートメントを再実行します。  
  
 SQL_CB_CLOSE 閉じるカーソルを = です。 アプリケーションを呼び出して、準備されたステートメントは、用**SQLExecute**呼び出さずに、ステートメントで**SQLPrepare**もう一度です。  
  
 SQL_CB_PRESERVE 以前と同じ位置にカーソルを保持を =、**ロールバック**操作。 データをフェッチするアプリケーションを続行またはカーソルを閉じて、再びその準備せず、ステートメントを再実行します。  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 カーソルの感度のサポートを示す SQLUINTEGER 値を指定します。  
  
 SQL_INSENSITIVE によって、同じトランザクション内の他のすべてのカーソル ステートメント ハンドルを表示する結果セットのことに加えられた変更を反映せず、すべてのカーソルを = です。  
  
 SQL_UNSPECIFIED = かどうかのカーソル ステートメント ハンドルに表示されるように、同じトランザクション内の別のカーソルが結果セットに加えられた変更指定ではありません。 ステートメント ハンドルでカーソルが表示されるようになしでは、このようないくつか、またはすべての変更。  
  
 SQL_SENSITIVE = カーソルは、同じトランザクション内の他のカーソルによって行われた変更に影響します。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、サポートされている、SQL_UNSPECIFIED オプションは常に返します。  
  
 SQL 92 全体のレベルに準拠ドライバーでは、サポートされている、SQL_INSENSITIVE オプションは常に返します。  
  
 SQL_DATA_SOURCE_NAME(ODBC 1.0)  
 接続中に使用されたデータ ソース名を持つ文字列を返します。 アプリケーションが呼び出された場合**SQLConnect**、これは、値、 *szDSN*引数。 アプリケーションが呼び出された場合**SQLDriverConnect**または**SQLBrowseConnect**、これは、DSN キーワードと、ドライバーに渡される接続文字列内の値です。 接続文字列が含まれていない場合、 **DSN**キーワード (がある場合など、**ドライバー**キーワード)、これは、空の文字列。  
  
 SQL_DATA_SOURCE_READ_ONLY(ODBC 1.0)  
 文字列を返します。 "Y"場合は、それ以外の場合、READ ONLY モードを"N"をデータ ソースが設定されている場合。  
  
 このような特性がデータ ソース自体にのみ関連します。データ ソースにアクセスできるようにするドライバーの特性はありません。 読み取り専用であるデータ ソースとは、読み取り/書き込みであるドライバーを使用できます。 ドライバーが読み取り専用の場合は、すべてのデータ ソースの読み取り専用にする必要があり、SQL_DATA_SOURCE_READ_ONLY を返す必要があります。  
  
 SQL_DATABASE_NAME (ODBC 1.0)  
 文字は、データ ソースに「データベース」と呼ばれる名前付きオブジェクトが定義されている場合、使用中の現在のデータベースの名前を含む文字列します。  
  
> [!NOTE]
>  ODBC 3 *.x*、この値が返されます*情報の種類*呼び出しによって返されることができますも**SQLGetConnectAttr**で、*属性*SQL_ATTR_CURRENT_CATALOG の引数です。  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 データ ソースでサポートされる SQL 92 datetime リテラルを列挙する SQLUINTEGER ビットマスク。 これらは、sql-92 規格に表示する日付時刻リテラルと、ODBC で定義されている datetime リテラルのエスケープ句とは別ことに注意してください。 ODBC datetime リテラルのエスケープ句の詳細については、次を参照してください。[日付、時刻、およびタイムスタンプのリテラル](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)します。  
  
 過渡期の FIPS 準拠レベル ドライバーは、次の一覧内のビットのビットマスクの「1」の値を常に返します。 「0」の場合は、sql-92 日付時刻リテラルがサポートされていないことの値。  
  
 次のビットマスクを使用して、どのようなリテラルがサポートされるを調べます。  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 ドライバーによってアクセスされる DBMS の製品の名前を持つ文字列を返します。  
  
 SQL_DBMS_VER (ODBC 1.0)  
 ドライバーによってアクセスされる DBMS の製品のバージョンを示す文字列。 バージョンの形式は、##. ##. ### 最初の 2 つの数字は、メジャー バージョン、次の 2 つの数字は、マイナーのバージョン、最後の 4 桁の数字は、リリース バージョン。 ドライバーは、このフォームでの DBMS の製品バージョンを表示する必要がありますが、DBMS の製品に固有のバージョンを追加することもします。 たとえば、"04.01.0000 Rdb 4.1"。  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 作成とインデックスのドロップ サポートを示す SQLUINTEGER 値を指定します。  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1.0)  
 データ ソースのドライバーまたはデータ ソース、または場合は 0 でサポートされる既定のトランザクション分離レベルを示す SQLUINTEGER 値は、トランザクションをサポートしていません。 トランザクション分離レベルを定義する、次の用語が使用されます。  
  
 **ダーティ リード**トランザクションの 1 行を変更します。 トランザクション 2 は、トランザクション 1 が、変更をコミットする前に、変更された行を読み取ります。 変更をロールバック トランザクション 1 場合、トランザクション 2 には、存在しないと見なされる行が読み取りです。  
  
 **反復不能読み取り**トランザクション 1 は、行を読み取ります。 トランザクション 2 は、更新またはその行を削除し、この変更をコミットします。 場合は、行を再読み込みしようとすると、トランザクション 1 を別の行の値を受け取るまたは、行が削除されたことを検出します。  
  
 **ファントム**トランザクション 1 が一連の一部の検索条件を満たす行を読み取ります。 トランザクション 2 は、検索条件に一致する (挿入または更新のいずれか) を 1 つまたは複数の行を生成します。 場合 1 をトランザクションは、行を読み取るステートメントを reexecutes、異なる一連の行を受け取ります。  
  
 データ ソースは、トランザクションをサポートする場合、ドライバーはビットマスクを次のいずれかを返します。  
  
 SQL_TXN_READ_UNCOMMITTED = ダーティ リード、反復不能読み取り、およびファントムがあります。  
  
 SQL_TXN_READ_COMMITTED = ダーティ リードすることはできません。 反復不能読み取りおよびファントムがあります。  
  
 SQL_TXN_REPEATABLE_READ = ダーティ リードと反復不能読み取りは実現できません。 ファントム場合があります。  
  
 SQL_TXN_SERIALIZABLE = トランザクションはシリアル化します。 シリアル化可能なトランザクションでは、ダーティ リード、反復不能読み取りやファントムは使用できません。  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 文字の文字列。"Y"場合、パラメーターを記述できます。"N"、ない場合。  
  
 サポートする必要があるため、SQL 92 完全なレベルに準拠ドライバーは"Y"を返します、通常、**について説明する入力**ステートメント。 これは直接を指定しない SQL のサポートを基になるため、ただし、パラメーターを記述する可能性がありますではサポートされない、でも、sql-92 完全準拠レベル ドライバー。  
  
 SQL_DM_VER (ODBC 3.0)  
 ドライバー マネージャーのバージョンと文字の文字列。 バージョンの形式は、##. ##. ###. ###、場所。  
  
 最初の 2 桁の数字のセットは、定数 SQL_SPEC_MAJOR によって指定された、主要な ODBC バージョンです。  
  
 2 桁の数字の 2 番目のセットは、定数 SQL_SPEC_MINOR によって指定された、マイナーの ODBC バージョンです。  
  
 4 桁の数字の 3 番目のセットは、ドライバー マネージャーのメジャー ビルド番号です。  
  
 最後の 4 桁の数字のセットは、ドライバー マネージャーのマイナー ビルド番号です。  
  
 Windows 7 ドライバー マネージャーのバージョンは、03.80 です。 Windows 8 のドライバー マネージャーのバージョンは、03.81 です。  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 SQLUINTEGER 値を示す場合は、ドライバーがドライバー対応のプールをサポートします。 (詳細については、次を参照してください。[ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)します。  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE では、ドライバーがドライバー対応のプーリング メカニズムをサポートできることを示します。  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE では、ドライバーがドライバー対応のプーリング メカニズムをサポートできないことを示します。  
  
 ドライバーは SQL_DRIVER_AWARE_POOLING_SUPPORTED を実装する必要はありませんし、ドライバー マネージャーは、ドライバーの戻り値には許可されません。  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 Sqlulen です値、ドライバーの環境ハンドルまたは接続ハンドルを引数によって決定*情報の種類*します。  
  
 これらの情報の種類は、ドライバー マネージャーによってのみ実装されます。  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 入力に渡す必要がありますドライバー マネージャーの記述子ハンドルによって決定されます、ドライバーの記述子ハンドル値を sqlulen です\* *InfoValuePtr*アプリケーションから。 この場合、 *InfoValuePtr*は入力と出力の両方の引数です。 入力記述子ハンドルが渡されました\* *InfoValuePtr*する必要があります明示的または暗黙的に割り当て済みで、 *ConnectionHandle*します。  
  
 アプリケーションが処理を呼び出す前に、ドライバー マネージャーの記述子のコピーを作成する必要があります**SQLGetInfo**でこの情報の種類、出力時に、ハンドルが上書きされないことを確認します。  
  
 この情報の種類は、ドライバー マネージャーによってのみ実装されます。  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 Sqlulen ですを値として、 *hinst*ロード ライブラリから返されるドライバー マネージャーに Microsoft Windows オペレーティング システム、またはそれと同等の別のオペレーティング システム上のドライバー DLL が読み込まれるときにします。 ハンドルはへの呼び出しで指定された接続ハンドルでのみ有効です**SQLGetInfo**します。  
  
 この情報の種類は、ドライバー マネージャーによってのみ実装されます。  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 入力に渡す必要がある、ドライバー マネージャーのステートメント ハンドルによって決定されます、ドライバーのステートメント ハンドル値を sqlulen です\* *InfoValuePtr*アプリケーションから。 この場合、 *InfoValuePtr*は入力と出力引数の両方。 渡された入力ステートメント ハンドル\* *InfoValuePtr*引数に対して割り当てられている必要があります*ConnectionHandle*します。  
  
 アプリケーションが処理を呼び出す前に、ドライバー マネージャーのステートメントのコピーを作成する必要があります**SQLGetInfo**でこの情報の種類、出力時に、ハンドルが上書きされることを確認します。  
  
 この情報の種類は、ドライバー マネージャーによってのみ実装されます。  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 データ ソースへのアクセスに使用されるドライバーのファイル名と文字列を返します。  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 ドライバーがサポートする ODBC のバージョンと文字の文字列。 バージョンの形式は、##. ## 最初の 2 つの数字、メジャー バージョンとは、次の 2 つの数字はマイナー バージョン。 SQL_SPEC_MAJOR と SQL_SPEC_MINOR、メジャーおよびマイナー バージョン番号を定義します。 このマニュアルで説明されている ODBC のバージョンでは、これらは、3 と 0 の場合と、ドライバーは、「03.00」で返す必要があります。  
  
 ODBC ドライバー マネージャーでは、既存のアプリケーションとの下位互換性を維持するために SQLGetInfo(SQL_DRIVER_ODBC_VER) の戻り値は変更されません。 ドライバーは、返される値を指定します。 ただし、C データ型の拡張機能をサポートしているドライバーが 3.8 (またはそれ以降) の場合を返す必要があります、アプリケーションが呼び出す**SQLSetEnvAttr** 3.8 SQL_ATTR_ODBC_VERSION に設定します。 詳細については、次を参照してください。 [ODBC における C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)します。  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 ドライバーのバージョンと必要に応じて、ドライバーの説明文字列を返します。 形式は、バージョンには、少なくとも ##. ##. ### 最初の 2 つの数字は、メジャー バージョン、次の 2 つの数字は、マイナーのバージョン、最後の 4 桁の数字は、リリース バージョン。  
  
 SQL_DROP_ASSERTION(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**ドロップ アサーション**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DA_DROP_ASSERTION  
  
 SQL 92 フルのレベルに準拠ドライバーでは、サポートされているため、このオプションは常に返します。  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**文字セットの削除**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 SQL 92 フルのレベルに準拠ドライバーでは、サポートされているため、このオプションは常に返します。  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**照合順序のドロップ**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DC_DROP_COLLATION  
  
 SQL 92 フルのレベルに準拠ドライバーでは、サポートされているため、このオプションは常に返します。  
  
 SQL_DROP_DOMAIN(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**ドロップ ドメイン**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 サポートされている、SQL 92 中間のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **DROP SCHEMA**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 サポートされている、SQL 92 中間のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **DROP TABLE**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 サポートされている、FIPS 過渡期のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_DROP_TRANSLATION(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、**ドロップ翻訳**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DTR_DROP_TRANSLATION  
  
 SQL 92 フルのレベルに準拠ドライバーでは、サポートされているため、このオプションは常に返します。  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **DROP VIEW**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 サポートされている、FIPS 過渡期のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 ドライバーでサポートされている、動的カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには属性の最初のサブセットが含まれています2 番目のサブセット SQL_DYNAMIC_CURSOR_ATTRIBUTES2 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 Sql_ca1_next、A を = *FetchOrientation* SQL_FETCH_NEXT の引数がへの呼び出しでサポートされている**SQLFetchScroll**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* SQL_FETCH_FIRST、SQL_FETCH_LAST、および SQL_FETCH_ABSOLUTE の引数への呼び出しではサポートされて**SQLFetchScroll**カーソルがある場合、動的カーソル。 (フェッチされる行セットは、現在のカーソル位置に依存しない)。  
  
 SQL_CA1_RELATIVE = *FetchOrientation* SQL_FETCH_PRIOR と SQL_FETCH_RELATIVE の引数への呼び出しではサポートされて**SQLFetchScroll**カーソルがある場合、動的カーソル。 (フェッチされる行セットは、現在のカーソル位置によって異なります。 注: これが、順方向専用カーソルで前方のみがサポートされているため、SQL_FETCH_NEXT から分離されている。)  
  
 SQL_CA1_BOOKMARK A を = *FetchOrientation*への呼び出しに SQL_FETCH_BOOKMARK の引数がサポートされている**SQLFetchScroll**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_LOCK_EXCLUSIVE A を = *LockType* SQL_LOCK_EXCLUSIVE の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 Sql_ca1_lock_no_change、A を = *LockType* SQL_LOCK_NO_CHANGE の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_LOCK_UNLOCK A を = *LockType* SQL_LOCK_UNLOCK の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_POS_POSITION =、*操作*SQL_POSITION の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_POS_UPDATE =、*操作*SQL_UPDATE の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_POS_DELETE =、*操作*SQL_DELETE の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_POS_REFRESH =、*操作*SQL_REFRESH の引数がへの呼び出しでサポートされている**SQLSetPos**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_POSITIONED_UPDATE = 更新プログラムが現在の SQL ステートメントはカーソルが動的カーソルでサポートされています。 (SQL 92 エントリのレベル-に準拠するドライバーは常に返しますこのオプション サポートされている)。  
  
 SQL_CA1_POSITIONED_DELETE = 削除が現在の SQL ステートメントはカーソルが動的カーソルでサポートされています。 (SQL 92 エントリのレベル-に準拠するドライバーは常に返しますこのオプション サポートされている)。  
  
 SQL_CA1_SELECT_FOR_UPDATE UPDATE SQL ステートメントがカーソル、動的カーソルがある場合にサポートされている SELECT を = です。 (SQL 92 エントリのレベル-に準拠するドライバーは常に返しますこのオプション サポートされている)。  
  
 Sql_ca1_bulk_add、=、*操作*SQL_ADD の引数がへの呼び出しでサポートされている**SQLBulkOperations**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK =、*操作*SQL_UPDATE_BY_BOOKMARK の引数がへの呼び出しでサポートされている**SQLBulkOperations**カーソルがある場合、動的カーソル。  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK =、*操作*SQL_DELETE_BY_BOOKMARK の引数がへの呼び出しでサポートされている**SQLBulkOperations**カーソルがある場合、動的カーソル。  
  
 Sql_ca1_bulk_fetch_by_bookmark、=、*操作*SQL_FETCH_BY_BOOKMARK の引数がへの呼び出しでサポートされている**SQLBulkOperations**カーソルがある場合、動的カーソル。  
  
 SQL 92 中間レベルに準拠ドライバーは、通常は返します SQL_CA1_NEXT、SQL_CA1_ABSOLUTE、SQL_CA1_RELATIVE オプション、サポートされている SQL のフェッチに埋め込みステートメントを通じてスクロール可能なカーソルをサポートしているため。 基になる SQL のサポートは直接は決定されません、ため、ただし、スクロール可能なカーソル可能性がありますがサポートされていない、でも、SQL 92 中間レベルに準拠ドライバー。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 ドライバーでサポートされている、動的カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには、2 つ目の属性です。 サブセットが含まれています。最初のサブセット SQL_DYNAMIC_CURSOR_ATTRIBUTES1 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 読み取り専用で更新プログラムは許可されず、動的カーソルがサポートされています。 (動的カーソルについて、また、ステートメント属性 SQL_ATTR_CONCURRENCY では SQL_CONCUR_READ_ONLY を使用できます。)  
  
 SQL_CA2_LOCK_CONCURRENCY = 最小のレベルを使用する動的カーソルのことを確認するための十分なロックはサポートされて、行を更新することができます。 (動的カーソルのまた、ステートメント属性 SQL_ATTR_CONCURRENCY では SQL_CONCUR_LOCK を指定できます)。これらのロックは、SQL_ATTR_TXN_ISOLATION 接続属性で、トランザクション分離レベルと一致する必要があります。  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY、動的カーソルを使用してオプティミスティック同時実行制御の比較する行のバージョンがサポートされていることを = です。 (動的カーソルのまた、ステートメント属性 SQL_ATTR_CONCURRENCY では SQL_CONCUR_ROWVER を指定できます)。  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY、動的カーソルを使用してオプティミスティック同時実行制御の比較値がサポートされていることを = です。 (動的カーソルのまた、ステートメント属性 SQL_ATTR_CONCURRENCY では SQL_CONCUR_VALUES を指定できます)。  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = 追加された行が、動的カーソルに表示されます。これらの行にカーソルがスクロールできます。 (カーソルにこれらの行が追加される、ドライバーによって異なります) です。  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 削除された行は、動的カーソルは使用できなくと; 結果セットに「穴」せず削除された行から動的カーソルがスクロールした後は、その行を返すことはできません。  
  
 SQL_CA2_SENSITIVITY_UPDATES = 行の更新が、動的カーソルに表示されます。動的カーソルからまでスクロールし、更新された行を返します、カーソルによって返されるデータが元のデータではなく、更新されたデータ。  
  
 SQL_CA2_MAX_ROWS_SELECT、SQL_ATTR_MAX_ROWS ステートメント属性に影響を =**選択**ステートメントのカーソルが動的カーソル。  
  
 SQL_CA2_MAX_ROWS_INSERT、SQL_ATTR_MAX_ROWS ステートメント属性に影響を =**挿入**ステートメントのカーソルが動的カーソル。  
  
 SQL_CA2_MAX_ROWS_DELETE、SQL_ATTR_MAX_ROWS ステートメント属性に影響を =**削除**ステートメントのカーソルが動的カーソル。  
  
 SQL_CA2_MAX_ROWS_UPDATE、SQL_ATTR_MAX_ROWS ステートメント属性に影響を = **UPDATE**ステートメントのカーソルが動的カーソル。  
  
 SQL_CA2_MAX_ROWS_CATALOG、SQL_ATTR_MAX_ROWS ステートメント属性に影響を =**カタログ**カーソルが動的カーソルの結果セット。  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL、SQL_ATTR_MAX_ROWS ステートメント属性に影響を =**選択**、**挿入**、**削除**、および**更新**ステートメント、および**カタログ**カーソルが動的カーソルの結果セット。  
  
 SQL_CA2_CRC_EXACT、正確な = 行の数が使用可能な SQL_DIAG_CURSOR_ROW_COUNT 診断フィールドにカーソルが動的カーソル。  
  
 SQL_CA2_CRC_APPROXIMATE 概算値 = 行の数が使用可能な SQL_DIAG_CURSOR_ROW_COUNT 診断フィールドにカーソルが動的カーソル。  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = ドライバーはシミュレートされた保証しない更新または位置指定のカーソルが動的カーソルの場合は、delete ステートメントは 1 行のみに影響これを保証するために、アプリケーションの役目です。 (ステートメントが 1 つ以上の行に影響する場合**SQLExecute**または**SQLExecDirect** SQLSTATE 01001 [カーソルの操作が衝突] を返します)。この動作では、アプリケーション呼び出しを設定する**SQLSetStmtAttr** SQL_ATTR_SIMULATE_CURSOR で属性 SQL_SC_NON_UNIQUE に設定します。  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = シミュレートされた位置指定の update または delete ステートメントの影響を与えること 1 行のみのカーソルが動的カーソルを保証するためにドライバーが試行されます。 ドライバーは、このようなステートメントを常に実行する場合など、複数の行に影響を与える可能性がある場合でも一意のキーはありません。 (ステートメントが 1 つ以上の行に影響する場合**SQLExecute**または**SQLExecDirect** SQLSTATE 01001 [カーソルの操作が衝突] を返します)。この動作では、アプリケーション呼び出しを設定する**SQLSetStmtAttr** SQL_ATTR_SIMULATE_CURSOR で属性 SQL_SC_TRY_UNIQUE に設定します。  
  
 SQL_CA2_SIMULATE_UNIQUE = ドライバー シミュレートされた保証には、更新プログラムが配置されている、または delete ステートメントがカーソルは動的カーソルとに 1 行のみに影響します。 ドライバーは、特定のステートメントにこれを保証できない場合**SQLExecDirect**または**SQLPrepare** SQLSTATE 01001 (カーソル操作の競合) を返します。 この動作では、アプリケーション呼び出しを設定する**SQLSetStmtAttr** SQL_ATTR_SIMULATE_CURSOR で属性 SQL_SC_UNIQUE に設定します。  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1.0)  
 文字の文字列。"Y"データ ソース内の式をサポートしている場合、 **ORDER BY**一覧表示します。"N"そうでない場合。  
  
 SQL_FILE_USAGE(ODBC 2.0)  
 1 階層のドライバーが直接データ ソース内のファイルを処理する方法を示す SQLUSMALLINT 値を指定します。  
  
 SQL_FILE_NOT_SUPPORTED = ドライバーが 1 階層のドライバーではありません。 たとえば、ORACLE、ドライバーは、2 階層ドライバーです。  
  
 SQL_FILE_TABLE データ ソースのテーブルとして 1 階層のドライバーの処理のファイルを = です。 たとえば、Xbase ドライバーはテーブルとして各 Xbase ファイルを扱います。  
  
 SQL_FILE_CATALOG = カタログとしてデータ ソース内の 1 階層のドライバー扱いますファイル。 たとえば、Microsoft Access ドライバーは完全なデータベースとして各 Microsoft Access ファイルを扱います。  
  
 アプリケーションは、これを使用のユーザーがデータを選択する方法を決定するのに可能性があります。 たとえば、Xbase ユーザーはテーブルに格納されている、この ORACLE および Microsoft Access のユーザーは、通常のデータと考える一方、ファイルに格納されているデータの多くの場合と考えます。  
  
 ユーザーは、Xbase のデータ ソースを選択するときに、アプリケーションが、Windows を表示でした**ファイルを開く**コモン ダイアログ ボックスは、ユーザーが Microsoft Access、ORACLE のデータ ソースを選択すると、アプリケーションは、カスタム表示でした**テーブルの選択** ダイアログ ボックス。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 ドライバーでサポートされている順方向専用カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには属性の最初のサブセットが含まれています2 番目のサブセット SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 これらのビットマスクの説明については、SQL_DYNAMIC_CURSOR_ATTRIBUTES1 を参照してください (および、説明に「動的カーソル」の「カーソルの前方参照専用」に置き換えてください)。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 ドライバーでサポートされている順方向専用カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには、2 つ目の属性です。 サブセットが含まれています。最初のサブセット SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 これらのビットマスクの説明については、SQL_DYNAMIC_CURSOR_ATTRIBUTES2 を参照してください (および、説明に「動的カーソル」の「カーソルの前方参照専用」に置き換えてください)。  
  
 SQL_GETDATA_EXTENSIONS(ODBC 2.0)  
 拡張機能を列挙する、SQLUINTEGER ビットマスク**SQLGetData**します。  
  
 次のビットマスク フラグと共に使用して、ドライバーのサポートの一般的な拡張機能を決定**SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData**最後の列をバインドする前に含めて、任意のバインドされていない列を呼び出すことができます。 SQL_GD_ANY_ORDER も返されない限り、列番号を昇順の順序で列を呼び出す必要がありますに注意してください。  
  
 SQL_GD_ANY_ORDER = **SQLGetData**任意の順序でバインドされていない列を呼び出すことができます。 なお**SQLGetData** SQL_GD_ANY_COLUMN も返されない限り最後の列がバインドされた列に対してのみ呼び出すことができます。  
  
 SQL_GD_BLOCK = **SQLGetData**でその行に配置した後 (場所は、行セット サイズが 1 より大きい) データのブロックの任意の行にバインドされていない列に対して呼び出すことが**SQLSetPos**します。  
  
 SQL_GD_BOUND = **SQLGetData**連結された列の非バインド列だけでなく呼び出すことができます。 ドライバーは、SQL_GD_ANY_COLUMN を返す場合を除き、この値を返すことはできません。  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData**出力パラメーターの値を返すを呼び出すことができます。 詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)します。  
  
 **SQLGetData**最後の列にバインドされた後に発生する非バインド列からのみデータが列の数を増やすことの順序で呼び出されます、行のブロック内の行にないを返すときに必要です。  
  
 呼び出し元をサポートする必要があります、ドライバーは、ブックマーク (固定長または可変長) をサポートする場合**SQLGetData**列 0 にします。 このサポートは、ドライバーを返しますの呼び出しに関係なく必要な**SQLGetInfo** 、SQL_GETDATA_EXTENSIONS で*情報の種類*します。  
  
 SQL_GROUP_BY (ODBC 2.0)  
 内の列間のリレーションシップを示す SQLUSMALLINT 値を**GROUP BY**句と、選択リスト内の非集計列。  
  
 SQL_GB_COLLATE A を = **COLLATE**句をグループ化の各列の最後に指定できます。 (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY**句はサポートされていません。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT =、 **GROUP BY**句は、選択リスト内のすべての非集計列を含める必要があります。 その他の列を含めることはできません。 たとえば、 **DEPT、MAX(SALARY) から従業員グループの選択で DEPT**します。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT =、 **GROUP BY**句は、選択リスト内のすべての非集計列を含める必要があります。 選択リストにない列を含めることができます。 たとえば、 **、期間、DEPT、MAX(SALARY) から従業員グループの選択で DEPT**します。 (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = 内の列、 **GROUP BY**句と select リストは関連しません。 選択リストで nongrouped、非集計列の意味は、データ ソースに依存します。 たとえば、 **、期間、部署、給与の従業員グループの選択で DEPT**します。 (ODBC 2.0)  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、サポートされている、SQL_GB_GROUP_BY_EQUALS_SELECT オプションは常に返します。 SQL 92 全体のレベルに準拠ドライバーでは、サポートされている、SQL_GB_COLLATE オプションは常に返します。 いずれのオプションがサポートされている場合、 **GROUP BY**句は、データ ソースでサポートされていません。  
  
 SQL_IDENTIFIER_CASE(ODBC 1.0)  
 値のとおり、SQLUSMALLINT:  
  
 SQL_IC_UPPER = SQL の識別子の小文字は区別されませんに格納されている場合はシステム カタログに大文字です。  
  
 SQL_IC_LOWER = SQL の識別子の小文字は区別されません、システム カタログ内の小文字で格納されます。  
  
 SQL_IC_SENSITIVE = SQL の識別子の大文字と小文字は、システム カタログ内の大文字小文字混在で格納されます。  
  
 SQL_IC_MIXED = SQL の識別子の小文字は区別されません、システム カタログ内の大文字小文字混在で格納されます。  
  
 Sql-92 に識別子が大文字小文字が区別されないため、SQL 92 (すべてのレベル) に厳密に準拠したドライバーを返さない SQL_IC_SENSITIVE オプション サポートされています。  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 文字の文字列を引用符で囲まれたの開始と終了の区切り記号として使用される (区切り) SQL ステートメント内の識別子。 (ODBC 関数に引数として渡される識別子する必要はありませんは引用符で囲む。)データ ソースが引用符で囲まれた識別子をサポートしていない場合は、空白が返されます。  
  
 この文字の文字列は、接続属性 SQL_ATTR_METADATA_ID が SQL_TRUE に設定されている場合は、カタログ関数の引数を囲むためも使用できます。  
  
 SQL 92 で識別子の引用符文字が二重引用符 (") であるため、準拠しているドライバー厳密に sql-92 には常に返します二重引用符文字。  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 ドライバーでサポートされている CREATE INDEX ステートメントでキーワードを列挙する SQLUINTEGER ビットマスク。  
  
 SQL_IK_NONE = キーワードのいずれもサポートされています。  
  
 SQL_IK_ASC = ASC キーワードがサポートされています。  
  
 SQL_IK_DESC = DESC キーワードがサポートされています。  
  
 SQL_IK_ALL = All キーワードがサポートされています。  
  
 CREATE INDEX ステートメントがサポートされているかどうかを表示するには、アプリケーションが呼び出す**SQLGetInfo** SQL_DLL_INDEX 情報の種類にします。  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 ドライバーでサポートされている INFORMATION_SCHEMA ビューを列挙する SQLUINTEGER ビットマスク。 では、ビューとの内容 INFORMATION_SCHEMA、sql-92 で定義されます。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、ビューがサポートされているを調べます。  
  
 SQL_ISV_ASSERTIONS = 特定のユーザーによって所有されているカタログのアサーションを識別します。 (完全レベル)  
  
 SQL_ISV_CHARACTER_SETS = 特定のユーザーによってアクセスできるカタログの文字セットを識別します。 (中間レベル)  
  
 SQL_ISV_CHECK_CONSTRAINTS = の識別、チェック制約、特定のユーザーによって所有されています。 (中間レベル)  
  
 SQL_ISV_COLLATIONS = 特定のユーザーによってアクセスできるカタログの文字の照合順序を識別します。 (完全レベル)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = カタログで定義されているドメインに依存し、特定のユーザーによって所有されているカタログの列を識別します。 (中間レベル)  
  
 SQL_ISV_COLUMN_PRIVILEGES = 権限は使用または付与特定のユーザーによって永続的なテーブルの列を識別します。 (FIPS 過渡期レベル)  
  
 SQL_ISV_COLUMNS = 特定のユーザーによってアクセスできる永続的なテーブルの列を識別します。 (FIPS 過渡期レベル)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = と同様、特定のユーザーによって所有されているさまざまな制約の CONSTRAINT_TABLE_USAGE ビューに列が識別されます。 (中間レベル)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 制約で使用されるテーブルを識別します (参照、一意でとアサーション)、特定のユーザーによって所有されているとします。 (中間レベル)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 特定のユーザーによってアクセスできます (カタログ内のドメイン) のドメインの制約を識別します。 (中間レベル)  
  
 SQL_ISV_DOMAINS = ユーザーがアクセスできるカタログで定義されているドメインを識別します。 (中間レベル)  
  
 SQL_ISV_KEY_COLUMN_USAGE = カタログで定義されている特定のユーザーがキーとして制約を識別します列。 (中間レベル)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 特定のユーザーによって所有されている参照に関する制約を識別します。 (中間レベル)  
  
 SQL_ISV_SCHEMATA = 特定のユーザーによって所有されているスキーマを識別します。 (中間レベル)  
  
 SQL_ISV_SQL_LANGUAGES = SQL 実装によってサポートされている SQL の適合性レベル、オプション、および言語を識別します。 (中間レベル)  
  
 SQL_ISV_TABLE_CONSTRAINTS = 特定のユーザーによって所有されているテーブルの制約を識別します。 (中間レベル)  
  
 SQL_ISV_TABLE_PRIVILEGES = 永続的な使用可能なテーブルまたは付与して、特定のユーザー権限を識別します。 (FIPS 過渡期レベル)  
  
 SQL_ISV_TABLES = 特定のユーザーによってアクセスできるカタログで定義されている永続的なテーブルを識別します。 (FIPS 過渡期レベル)  
  
 SQL_ISV_TRANSLATIONS = 特定のユーザーによってアクセスできるカタログの文字変換を識別します。 (完全レベル)  
  
 SQL_ISV_USAGE_PRIVILEGES = が利用できる、または特定のユーザーによって所有されているカタログ オブジェクトへの権限の使用状況を識別します。 (FIPS 過渡期レベル)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 特定のユーザーによって所有されているカタログを表示する列を識別依存しています。 (中間レベル)  
  
 SQL_ISV_VIEW_TABLE_USAGE = 特定のユーザーによって所有されているカタログを表示するテーブルを識別依存しています。 (中間レベル)  
  
 SQL_ISV_VIEWS = 特定のユーザーによってアクセスできるこのカタログで定義されている表示されているテーブルを識別します。 (FIPS 過渡期レベル)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 サポートを示す SQLUINTEGER ビットマスク**挿入**ステートメント。  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 サポートされている、SQL 92 エントリのレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_INTEGRITY (ODBC 1.0)  
 文字の文字列。"Y"データ ソースが Integrity Enhancement Facility; をサポートしている場合"N"そうでない場合。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_ODBC_SQL_OPT_IEF します。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 ドライバーでサポートされている、キーセット カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには属性の最初のサブセットが含まれています2 番目のサブセット SQL_KEYSET_CURSOR_ATTRIBUTES2 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 これらのビットマスクの説明については、SQL_DYNAMIC_CURSOR_ATTRIBUTES1 を参照してください (および、説明に「動的カーソル」の「カーソルのキーセット ドリブン」に置き換えてください)。  
  
 SQL 92 中間レベルに準拠ドライバーは、通常は返します SQL_CA1_NEXT、SQL_CA1_ABSOLUTE、SQL_CA1_RELATIVE オプション、サポートされているドライバーが埋め込み SQL FETCH ステートメントを通じてスクロール可能なカーソルをサポートしているため。 基になる SQL のサポートは直接は決定されません、ため、ただし、スクロール可能なカーソル可能性がありますがサポートされていない、でも、SQL 92 中間レベルに準拠ドライバー。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 ドライバーでサポートされている、キーセット カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには、2 つ目の属性です。 サブセットが含まれています。最初のサブセット SQL_KEYSET_CURSOR_ATTRIBUTES1 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 これらのビットマスクの説明については、SQL_DYNAMIC_CURSOR_ATTRIBUTES1 を参照してください (および、説明に「動的カーソル」の「カーソルのキーセット ドリブン」に置き換えてください)。  
  
 SQL_KEYWORDS (ODBC 2.0)  
 すべてのデータ ソースに固有のキーワードのコンマ区切りのリストを含む文字列。 この一覧は、ODBC に固有のキーワードまたはデータ ソースと ODBC の両方で使用されるキーワードは含まれません。 この一覧は、すべての予約済みキーワードを表します。相互運用可能なアプリケーションでは、オブジェクト名でこれらの単語を使用する必要があります。  
  
 ODBC キーワードの一覧は、次を参照してください[予約済みキーワード](../../../odbc/reference/appendixes/reserved-keywords.md)で[付録 c:。SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)します。 **#Define**値 SQL_ODBC_KEYWORDS ODBC キーワードのコンマ区切りの一覧が含まれています。  
  
 付録 CSQL 文法  
  
 SQL_LIKE_ESCAPE_CLAUSE(ODBC 2.0)  
 文字の文字列。"Y"データ ソースは、パーセント (%) の文字のエスケープ文字をサポートしている場合アンダー スコア文字 (_) と、**など**述語とドライバーの定義に ODBC 構文をサポートしています、**など**述語のエスケープ文字。"N"それ以外の場合。  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 ドライバーでは、特定の接続をサポートする非同期モードでのアクティブな同時実行ステートメントの最大数を示す SQLUINTEGER 値を指定します。 特定の制限はありません、または既知の制限は、この値は 0 です。  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 最大長を指定する SQLUINTEGER 値 (リテラル プレフィックスおよびサフィックスによって返されるを除く、16 進数の文字数**SQLGetTypeInfo**) の SQL ステートメント内のバイナリ リテラル。 たとえば、バイナリ リテラル 0xFFAA では、長さは 4 があります。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 SQL_MAX_CATALOG_NAME_LEN(ODBC 1.0)  
 データ ソースのカタログ名の最大長を示す SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 FIPS フルのレベルに準拠のドライバーでは、少なくとも 128 を返します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_MAX_QUALIFIER_NAME_LEN します。  
  
 SQL_MAX_CHAR_LITERAL_LEN(ODBC 2.0)  
 最大長を指定する SQLUINTEGER 値 (リテラル プレフィックスおよびサフィックスによって返される文字数**SQLGetTypeInfo**) の SQL ステートメント内の文字リテラル。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 データ ソース内の列名の最大長を示す SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、18 以上を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 128 を返します。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY(ODBC 2.0)  
 許可されている列の最大数を示す SQLUSMALLINT 値を**GROUP BY**句。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、少なくとも 6 を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 15 を返します。  
  
 SQL_MAX_COLUMNS_IN_INDEX(ODBC 2.0)  
 インデックスで許可されている列の最大数を示す SQLUSMALLINT 値を指定します。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY(ODBC 2.0)  
 許可されている列の最大数を示す SQLUSMALLINT 値を**ORDER BY**句。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、少なくとも 6 を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 15 を返します。  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 選択リストで許可されている列の最大数を示す SQLUSMALLINT 値を指定します。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、少なくとも 100 を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 250 を返します。  
  
 SQL_MAX_COLUMNS_IN_TABLE(ODBC 2.0)  
 テーブルで許可されている列の最大数を示す SQLUSMALLINT 値を指定します。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、少なくとも 100 を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 250 を返します。  
  
 SQL_MAX_CONCURRENT_ACTIVITIES(ODBC 1.0)  
 接続の場合、ドライバーがサポートできるアクティブなステートメントの最大数を指定する SQLUSMALLINT 値を指定します。 用語「結果」意味行と、保留中の結果がある場合に、アクティブとして、ステートメントが定義されている、**選択**操作または影響を受ける行を**挿入**、 **UPDATE**、または**削除**(行カウントの場合) などの操作が NEED_DATA 状態にある場合またはします。 この値は、ドライバーまたはデータ ソースのいずれかによって課される制限を反映できます。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_ACTIVE_STATEMENTS します。  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 データ ソースでカーソル名の最大長を示す SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、18 以上を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 128 を返します。  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 環境のドライバーがサポートできるアクティブな接続の最大数を指定する SQLUSMALLINT 値を指定します。 この値は、ドライバーまたはデータ ソースのいずれかによって課される制限を反映できます。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_ACTIVE_CONNECTIONS します。  
  
 SQL_MAX_IDENTIFIER_LEN(ODBC 3.0)  
 ユーザー定義の名前のデータ ソースをサポートする文字の最大サイズを示す SQLUSMALLINT します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、18 以上を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 128 を返します。  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 インデックスの結合されたフィールドに許可されるバイトの最大数を指定する SQLUINTEGER 値を指定します。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 データ ソースでプロシージャ名の最大長を示す SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 テーブルの 1 つの行の最大長を指定する SQLUINTEGER 値。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 2,000 以上では、FIPS エントリ レベル準拠のドライバーを返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 8,000 を返します。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 文字の文字列。"Y"SQL_MAX_ROW_SIZE 情報の種類を最大行サイズが返された場合に、SQL_LONGVARCHAR および SQL_LONGVARBINARY のすべての列の長さには、行が含まれています"N"それ以外の場合。  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 データ ソースのスキーマ名の最大長を指定する SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、18 以上を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 128 を返します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_MAX_OWNER_NAME_LEN します。  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 SQL ステートメントの最大長 (文字などの空白文字の数) を示す SQLUINTEGER 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 データ ソースのテーブル名の最大長を示す SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、18 以上を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 128 を返します。  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 許容されるテーブルの最大数を示す SQLUSMALLINT 値を**FROM**の句、**選択**ステートメント。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 FIPS エントリのレベルに準拠ドライバーでは、少なくとも 15 を返します。 FIPS の中間のレベルに準拠のドライバーでは、少なくとも 50 を返します。  
  
 SQL_MAX_USER_NAME_LEN(ODBC 2.0)  
 データ ソースのユーザー名の最大長を示す SQLUSMALLINT 値を指定します。 最大長がないか、長さが不明な場合、この値は 0 に設定します。  
  
 SQL_MULT_RESULT_SETS (ODBC 1.0)  
 文字の文字列。"Y"データ ソースは、そうでない場合、"N"、複数の結果セットをサポートしている場合。  
  
 複数の結果セットの詳細については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 文字の文字列。"Y"、ドライバーは、いつでもアクティブにできる 1 つのトランザクションのみの場合、同時に、"N"は、複数のアクティブなトランザクションをサポートしている場合。  
  
 この情報の種類に対して返される情報は、分散トランザクションの場合は適用されません。  
  
 SQL_NEED_LONG_DATA_LEN(ODBC 2.0)  
 文字の文字列。"Y"(データ型は、SQL_LONGVARCHAR、SQL_LONGVARBINARY、または長い形式のデータ ソースに固有のデータ型には) その値の前に長い形式のデータ値の長さがデータ ソースに必要がある場合は、そうでない場合、"N"のデータ ソースに送信されます。 詳細については、次を参照してください。 [SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)と[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 データ ソースが列に NOT NULL をサポートするかどうかを指定する SQLUSMALLINT 値:  
  
 SQL_NNC_NULL = すべての列が null 許容にする必要があります。  
  
 SQL_NNC_NON_NULL = 列は null 許容にすることはできません。 (データ ソースのサポート、 **NOT NULL**内の列制約**CREATE TABLE**ステートメントです)。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、SQL_NNC_NON_NULL を返します。  
  
 SQL_NULL_COLLATION(ODBC 2.0)  
 結果セット内の Null の配置場所を指定する SQLUSMALLINT 値:  
  
 SQL_NC_END = null 値は ASC または DESC キーワードに関係なく、結果セットの末尾に並べ替えられます。  
  
 SQL_NC_HIGH = 高 ASC または DESC キーワードに応じて、結果セットの末尾に null 値を並べ替えます。  
  
 SQL_NC_LOW = 低 ASC または DESC キーワードに応じて、結果セットの末尾に null 値を並べ替えます。  
  
 SQL_NC_START = Null は、ASC または DESC キーワードに関係なく、結果セットの先頭に配置します。  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1.0)  
 注:情報の種類が ODBC 1.0; で導入されました。各ビットマスクが導入されたバージョンが付いています。  
  
 ドライバーと関連付けられているデータ ソースでサポートされている数値のスカラー関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする数値関数を調べます。  
  
 SQL_FN_NUM_ABS (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_ACOS SQL_FN_NUM_ASIN (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_ATAN SQL_FN_NUM_ATAN2 (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_CEILING SQL_FN_NUM_COS (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_COT SQL_FN_NUM_DEGREES (ODBC 2.0) の SQL _FN_NUM_EXP (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_FLOOR SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_PI SQL_FN_NUM_POWER (ODBC 2.0) (ODBC 2.0) SQL_FN_NUM_RADIANS SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) (ODBC 1.0) SQL_FN_NUM_SQRT、SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE(ODBC 3.0)  
 ODBC 3 のレベルを示す SQLUINTEGER 値 *.x*ドライバーに準拠しているインターフェイス。  
  
 SQL_OIC_CORE:準拠するすべての ODBC ドライバーである最小のレベルが必要です。 このレベルには、接続の機能、準備および SQL ステートメントを実行するための関数、基本的な結果セットのメタデータ関数、関数の基本的なカタログなどの基本的なインターフェイス要素が含まれています。  
  
 SQL_OIC_LEVEL1:配置されている、core 標準準拠のレベルの機能と、カーソルがスクロール可能なブックマークを含むレベルでは、更新、削除、およびとなどです。  
  
 SQL_OIC_LEVEL2。さらに機密性の高いカーソルなどの高度な機能のレベル 1 標準コンプライアンス レベル機能を含むレベル更新、削除、およびブックマークを更新ストアド プロシージャのサポートカタログ関数の主キーと外部キーです。複数のカタログのサポート。などなど。  
  
 詳細については、次を参照してください。[インターフェイスの適合性レベル](../../../odbc/reference/develop-app/interface-conformance-levels.md)します。  
  
 SQL_ODBC_VER (ODBC 1.0)  
 ODBC ドライバー マネージャーは、準拠しているのバージョンと文字の文字列。 バージョンの形式は、##. ##. 0000 で、最初の 2 つの数字は、メジャー バージョンと、次の 2 つの数字はマイナー バージョン。 これにより、ドライバー マネージャーでのみが実装されます。  
  
 SQL_OJ_CAPABILITIES(ODBC 2.01)  
 ドライバーとデータ ソースでサポートされる外部結合の種類を列挙する SQLUINTEGER ビットマスク。 次のビットマスクを使用して、種類がサポートされているを調べます。  
  
 SQL_OJ_LEFT = 左外部結合はサポートされています。  
  
 SQL_OJ_RIGHT = 右外部結合はサポートされています。  
  
 SQL_OJ_FULL = 完全外部結合はサポートされています。  
  
 SQL_OJ_NESTED = 入れ子になった外部結合はサポートされています。  
  
 SQL_OJ_NOT_ORDERED = 列の外部結合の ON 句での名は、内のそれぞれのテーブル名と同じ順序にする必要はありません、**外部結合**句。  
  
 SQL_OJ_INNER = 内部テーブル (左外部結合の右側のテーブル) または右外部結合の左側のテーブルは内部結合でも使用できます。 これは、内部テーブルがない、完全外部結合には適用されません。  
  
 SQL_OJ_ALL_COMPARISON_OPS = 比較演算子、ON 句では、ODBC の比較演算子のいずれかを指定できます。 このビットが設定されていない場合、外部結合で等号 (=) 比較演算子のみを使用できます。  
  
 これらのオプションには、サポートされているが返されます、外部結合句はサポートされません。  
  
 SELECT ステートメント内のリレーショナル結合演算子のサポートについては、sql-92 で定義された、SQL_SQL92_RELATIONAL_JOIN_OPERATORS を参照してください。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 文字の文字列。"Y"場合内の列、 **ORDER BY**句が select リストである必要がありますそれ以外の場合、"N"です。  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 パラメーター化された実行中の行の可用性に関するドライバーのプロパティの列挙、SQLUINTEGER をカウントします。 次の値があります。  
  
 SQL_PARC_BATCH = 個別行の数がパラメーターの各セットで使用します。 これは、概念的には、配列内に設定するパラメーターごとに 1 つの SQL ステートメントのバッチを生成するドライバーと同じです。 拡張エラー情報は、SQL_PARAM_STATUS_PTR の記述子フィールドを使用して取得できます。  
  
 SQL_PARC_NO_BATCH = 結果パラメーターの配列全体のステートメントの実行の累積的な行の数である、使用可能な 1 つだけ行カウントがあります。 これは、概念的には、完全なパラメーター配列と、ステートメントを 1 つのアトミック単位として扱うことに相当します。 1 つのステートメントが実行された場合に、エラーは同じで処理されます。  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 パラメーター化された実行の結果の可用性に関するドライバーのプロパティの列挙、SQLUINTEGER を設定します。 次の値があります。  
  
 SQL_PAS_BATCH = 設定パラメーターのセットごとに利用可能な 1 つの結果があります。 これは、概念的には、配列内に設定するパラメーターごとに 1 つの SQL ステートメントのバッチを生成するドライバーと同じです。  
  
 SQL_PAS_NO_BATCH = は累積的な結果を表す 1 つだけの結果セットの使用可能なは、パラメーターの完全な配列のステートメントの実行の結果を設定します。 これは、概念的には、完全なパラメーター配列と、ステートメントを 1 つのアトミック単位として扱うことに相当します。  
  
 SQL_PAS_NO_SELECT A を = ドライバーには、パラメーターの配列を実行するときに結果セットを生成するステートメントはできません。  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 手順については、データ ソースのベンダーの名前を持つ文字の文字列たとえば、"データベース procedure"、「ストアド プロシージャ」、"procedure"、"package"または「ストアド クエリ」。  
  
 SQL_PROCEDURES (ODBC 1.0)  
 文字の文字列。"Y"データ ソースには、プロシージャと、ドライバーがサポートしている場合は、ODBC のプロシージャの呼び出し構文をサポートしています。"N"それ以外の場合。  
  
 SQL_POS_OPERATIONS(ODBC 2.0)  
 列挙で操作をサポートする SQLINTEGER ビットマスク**SQLSetPos**します。  
  
 以下のビットマスクは、どのオプションがサポートされているかを決定するフラグと共に使用されます。  
  
 SQL_POS_POSITION (ODBC 2.0) (ODBC 2.0) SQL_POS_REFRESH SQL_POS_UPDATE (ODBC 2.0) (ODBC 2.0) SQL_POS_DELETE SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE(ODBC 2.0)  
 値のとおり、SQLUSMALLINT:  
  
 SQL_IC_UPPER 引用符で囲まれた = SQL の識別子の小文字は区別されませんに格納されている場合はシステム カタログに大文字です。  
  
 SQL_IC_LOWER 引用符で囲まれた = SQL の識別子の小文字は区別されません、システム カタログ内の小文字で格納されます。  
  
 SQL_IC_SENSITIVE 引用符で囲まれた = SQL の識別子の大文字と小文字は、システム カタログ内の大文字小文字混在で格納されます。 (SQL 92 準拠データベースの場合、引用符で囲まれた識別子は常に大文字小文字を区別します。)  
  
 SQL_IC_MIXED 引用符で囲まれた = SQL の識別子の小文字は区別されません、システム カタログ内の大文字小文字混在で格納されます。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、SQL_IC_SENSITIVE は常に返します。  
  
 SQL_ROW_UPDATES (ODBC 1.0)  
 文字の文字列。"Y"キーセット ドリブンまたは混合カーソルがすべての行のバージョンまたは値を保持している場合は、行をフェッチされ、行が最後にフェッチしたためすべてのユーザーが行に行われた更新プログラムを検出できます。 (これにのみ適用されますが削除または挿入、更新プログラムです。)ドライバーが SQL_ROW_UPDATED フラグを行の状態に戻すことができる場合に配列**SQLFetchScroll**が呼び出されます。 それ以外の場合、"N"です。  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 スキーマのデータ ソースの仕入先の名前を持つ文字の文字列たとえば、「所有者」、"承認 ID"または"Schema"にします。  
  
 上部、下部、または大文字と小文字の文字の文字列が返されます。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、"schema"は常に返します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_OWNER_TERM します。  
  
 SQL_SCHEMA_USAGE(ODBC 2.0)  
 スキーマを使用できるステートメントを列挙する SQLUINTEGER ビットマスク。  
  
 SQL_SU_DML_STATEMENTS = すべてのデータ操作言語ステートメントでスキーマがサポートされています。**選択**、**挿入**、**更新**、**削除**、サポートされている場合**更新の選択**と位置指定更新と削除ステートメント。  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC のプロシージャ呼び出しステートメントでスキーマがサポートされています。  
  
 SQL_SU_TABLE_DEFINITION = すべてのテーブル定義ステートメントでスキーマがサポートされています。**テーブルを作成する**、**ビューを作成する**、 **ALTER TABLE**、 **DROP TABLE**、および**ドロップ ビュー**します。  
  
 SQL_SU_INDEX_DEFINITION = すべてのインデックス定義ステートメントでスキーマがサポートされています。**インデックス作成**と**DROP INDEX**します。  
  
 SQL_SU_PRIVILEGE_DEFINITION = すべての特権定義ステートメントでスキーマがサポートされています。**GRANT**と**取り消す**します。  
  
 SQL 92 エントリ レベルに準拠のドライバーでは、サポートされている、SQL_SU_DML_STATEMENTS、SQL_SU_TABLE_DEFINITION、および SQL_SU_PRIVILEGE_DEFINITION のオプションは常に返します。  
  
 これは、*情報の種類*ODBC 2.0 から ODBC 3.0 の名前を変更した*情報の種類*SQL_OWNER_USAGE します。  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 注:情報の種類が ODBC 1.0; で導入されました。各ビットマスクが導入されたバージョンが付いています。  
  
 スクロール可能なカーソルのサポートされているスクロール オプションを列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用して、どのオプションがサポートされているを調べます。  
  
 SQL_SO_FORWARD_ONLY = カーソルだけスクロール転送します。 (ODBC 1.0)  
  
 SQL_SO_STATIC = データ結果セットが静的です。 (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = ドライバー保存し、結果セット内のすべての行のキーを使用します。 (ODBC 1.0)  
  
 SQL_SO_DYNAMIC、ドライバーを保持 (キーセットのサイズは、同じ行セットのサイズです)、行セット内のすべての行のキーを = です。 (ODBC 1.0)  
  
 SQL_SO_MIXED = ドライバーにより、キー、keyset、およびキーセットのサイズのすべての行が行セットのサイズより大きい。 カーソルのキーセット ドリブンのキーセット内とキーセットの外側は動的です。 (ODBC 1.0)  
  
 スクロール可能なカーソルについては、次を参照してください。[スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)します。  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1.0)  
 パターン一致のメタ文字のアンダー スコア (_)、パーセント記号 (%) の使用を許可するエスケープ文字としてサポートするドライバーを指定する文字列検索パターンの有効な文字をします。 このエスケープ文字は、検索文字列をサポートするこれらのカタログ関数の引数に対してのみ適用されます。 この文字列が空の場合、ドライバーは、検索パターンのエスケープ文字をサポートしていません。  
  
 この情報の種類が内のエスケープ文字の一般的なサポートを示していないため、**など**述語、sql-92 含まないこの文字の文字列の要件。  
  
 これは、*情報の種類*カタログ関数に制限されています。 検索パターン文字列にエスケープ文字の使用については、次を参照してください。[パターン値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)します。  
  
 SQL_SERVER_NAME (ODBC 1.0)  
 文字の文字列が実際のデータ ソースに固有のサーバー名データ ソース名を使用する際に便利です。 **SQLConnect**、 **SQLDriverConnect**、および**SQLBrowseConnect**します。  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 テーブル名、列名、またはデータ ソースでのインデックス名など、識別子名で使用できるすべて特殊文字 (つまり、すべて文字 a ~ z、A ~ Z、0 ~ 9、およびアンダー スコアを除く) を含む文字列。 たとえば、"#$^"。 1 つ以上のこれらの文字が識別子が含まれる場合、識別子は、区切られた識別子である必要があります。  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Sql-92、ドライバーによってサポートのレベルを示す SQLUINTEGER 値:  
  
 SQL_SC_SQL92_ENTRY エントリ レベルの sql-92 準拠を = です。  
  
 SQL_SC_FIPS127_2_TRANSITIONAL FIPS 127-2 移行レベルの準拠を = です。  
  
 SQL_SC_SQL92_FULL = 完全レベル sql-92 に準拠します。  
  
 SQL_SC_ SQL92_INTERMEDIATE 中間レベルの sql-92 準拠を = です。  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 Sql-92 で定義されている、ドライバーと、関連付けられているデータ ソースによってサポートされている datetime スカラー関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする日付時刻関数を調べます。  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 外部キーのサポートされているルールの列挙、SQLUINTEGER ビットマスクを**削除**ステートメントでは、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句は、データ ソースでサポートされてを調べます。  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 サポートされている、FIPS 過渡期のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 外部キーのサポートされているルールの列挙、SQLUINTEGER ビットマスク、 **UPDATE**ステートメントでは、sql-92 で定義されています。  
  
 次のビットマスクを使用して、どの句は、データ ソースでサポートされてを調べます。  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 サポートされている、SQL 92 完全のレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 サポートされている句を列挙する SQLUINTEGER ビットマスク、 **GRANT**ステートメントでは、sql-92 で定義されています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句は、データ ソースでサポートされてを調べます。  
  
 SQL_SG_DELETE_TABLE (エントリ レベル) SQL_SG_INSERT_COLUMN (中間レベル) SQL_SG_INSERT_TABLE (エントリ レベル) SQL_SG_REFERENCES_TABLE (エントリ レベル) SQL_SG_REFERENCES_COLUMN (エントリ レベル) SQL_SG_SELECT_TABLE (エントリ レベル) SQL_SG_UPDATE_COLUMN (エントリ レベル) SQL_SG_UPDATE_TABLE (エントリ レベル) SQL_SG_USAGE_ON_DOMAIN (FIPS 過渡期レベル) SQL_SG_USAGE_ON_CHARACTER_SET (FIPS 過渡期レベル) SQL_SG_USAGE_ON_COLLATION (FIPS 過渡期レベル) SQL_SG_USAGE_ON_TRANSLATION (FIPS移行のレベル) SQL_SG_WITH_GRANT_OPTION (エントリ レベル)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 Sql-92 で定義されているドライバーと、関連付けられているデータ ソースでサポートされている数値のスカラー関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする数値関数を調べます。  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 サポートされている述語を列挙する SQLUINTEGER ビットマスクを**選択**ステートメントでは、sql-92 で定義されています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どのオプションは、データ ソースでサポートを調べます。  
  
 SQL_SP_BETWEEN (エントリ レベル) SQL_SP_COMPARISON (エントリ レベル) SQL_SP_EXISTS (エントリ レベル) SQL_SP_IN (エントリ レベル) SQL_SP_ISNOTNULL (エントリ レベル) SQL_SP_ISNULL (エントリ レベル) SQL_SP_LIKE (エントリ レベル) SQL_SP_MATCH_FULL (完全レベル) SQL_SP_MATCH_PARTIAL(完全レベル)(完全レベル) SQL_SP_MATCH_UNIQUE_FULL SQL_SP_MATCH_UNIQUE_PARTIAL (完全レベル) SQL_SP_OVERLAPS (FIPS 過渡期レベル) SQL_SP_QUANTIFIED_COMPARISON (エントリ レベル)、SQL_SP_UNIQUE (エントリ レベル)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 サポートされているリレーショナル結合演算子を列挙する SQLUINTEGER ビットマスクを**選択**ステートメントでは、sql-92 で定義されています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どのオプションは、データ ソースでサポートを調べます。  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (中間レベル) SQL_SRJO_CROSS_JOIN (完全レベル) SQL_SRJO_EXCEPT_JOIN (中間レベル) SQL_SRJO_FULL_OUTER_JOIN (中間レベル) SQL_SRJO_INNER_JOIN (FIPS 過渡期レベル) SQL_SRJO_INTERSECT_JOIN(中間レベル)SQL_SRJO_LEFT_OUTER_JOIN (FIPS 過渡期レベル) SQL_SRJO_NATURAL_JOIN (FIPS 過渡期レベル) SQL_SRJO_RIGHT_OUTER_JOIN (FIPS 過渡期レベル) SQL_SRJO_UNION_JOIN (完全レベル)  
  
 SQL_SRJO_INNER_JOIN のサポートを指定する、 **INNER JOIN**内部結合機能ではなく、構文。 サポート、 **INNER JOIN**構文が FIPS 移行中に、内部結合機能はサポート**エントリ**します。  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 サポートされている句を列挙する SQLUINTEGER ビットマスク、**取り消す**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句は、データ ソースでサポートされてを調べます。  
  
 SQL_SR_CASCADE (FIPS 過渡期レベル) SQL_SR_DELETE_TABLE (エントリ レベル) SQL_SR_GRANT_OPTION_FOR (中間レベル) SQL_SR_INSERT_COLUMN (中間レベル) SQL_SR_INSERT_TABLE (エントリ レベル) SQL_SR_REFERENCES_COLUMN (エントリ レベル) SQL_SR_REFERENCES_TABLE (エントリ レベル) SQL_SR_RESTRICT (FIPS 過渡期レベル) SQL_SR_SELECT_TABLE (エントリ レベル) SQL_SR_UPDATE_COLUMN (エントリ レベル) SQL_SR_UPDATE_TABLE (エントリ レベル) SQL_SR_USAGE_ON_DOMAIN (FIPS 過渡期レベル) SQL_SR_USAGE_ON_CHARACTER_SET (FIPS 過渡期レベル) SQL_SR_USAGE_ON_COLLATION (FIPS 過渡期レベル) SQL_SR_USAGE_ON_TRANSLATION (FIPS 過渡期レベル)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 サポートされている行値コンス トラクター式を列挙する SQLUINTEGER ビットマスクを**選択**ステートメントでは、sql-92 で定義されています。 次のビットマスクを使用して、どのオプションは、データ ソースでサポートを調べます。  
  
 SQL_SRVC_VALUE_EXPRESSION、SQL_SRVC_ SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 Sql-92 で定義されているドライバーと、関連付けられているデータ ソースでサポートされている文字列のスカラー関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする文字列関数を調べます。  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Sql-92 で定義されている、サポートされている値の式を列挙する SQLUINTEGER ビットマスク。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どのオプションは、データ ソースでサポートを調べます。  
  
 (中間レベル) SQL_SVE_CASE、SQL_SVE_CAST (FIPS 過渡期レベル)、(中間レベル) sql_sve_coalesce、SQL_SVE_NULLIF (中間レベル)  
  
 SQL_STANDARD_CLI_CONFORMANCE(ODBC 3.0)  
 ドライバーが準拠する CLI 標準または標準を列挙する SQLUINTEGER ビットマスク。 次のビットマスクを使用して、ドライバーに準拠しているレベルを調べます。  
  
 SQL_SCC_XOPEN_CLI_VERSION1:ドライバーは、開いているグループの CLI バージョン 1 に準拠します。  
  
 SQL_SCC_ISO92_CLI:ISO 92 CLI を使用したドライバーが準拠しています。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 ドライバーでサポートされている静的カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには属性の最初のサブセットが含まれています2 番目のサブセット SQL_STATIC_CURSOR_ATTRIBUTES2 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 これらのビットマスクの説明については、SQL_DYNAMIC_CURSOR_ATTRIBUTES1 を参照してください (および、説明に「動的カーソル」を"静的 cursor"に置き換えてください)。  
  
 SQL 92 中間レベルに準拠ドライバーは、通常は返します SQL_CA1_NEXT、SQL_CA1_ABSOLUTE、SQL_CA1_RELATIVE オプション、サポートされているドライバーが埋め込み SQL FETCH ステートメントを通じてスクロール可能なカーソルをサポートしているため。 基になる SQL のサポートは直接は決定されません、ため、ただし、スクロール可能なカーソル可能性がありますがサポートされていない、でも、SQL 92 中間レベルに準拠ドライバー。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 ドライバーでサポートされている静的カーソルの属性を記述する SQLUINTEGER ビットマスク。 このビットマスクには、2 つ目の属性です。 サブセットが含まれています。最初のサブセット SQL_STATIC_CURSOR_ATTRIBUTES1 を参照してください。  
  
 次のビットマスクを使用して、どの属性がサポートされているを調べます。  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 これらのビットマスクの説明については、SQL_DYNAMIC_CURSOR_ATTRIBUTES2 を参照してください (および、説明に「動的カーソル」を"静的 cursor"に置き換えてください)。  
  
 SQL_STRING_FUNCTIONS(ODBC 1.0)  
 注:情報の種類が ODBC 1.0; で導入されました。各ビットマスクが導入されたバージョンが付いています。  
  
 ドライバーと関連付けられているデータ ソースでサポートされているスカラー文字列関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする文字列関数を調べます。  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) (ODBC 3.0) SQL_FN_STR_CHAR_LENGTH SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) (ODBC 1.0) SQL_FN_STR_CONCAT SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) (ODBC 1.0) SQL_FN_STR_LENGTH SQL_FN_STR_LOCATE (ODBC 1.0) (ODBC 1.0) SQL_FN_STR_LTRIM SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_(ODBC 1.0) できるような SQL_FN_STR_RIGHT (ODBC 1.0) (ODBC 1.0) SQL_FN_STR_RTRIM SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) (ODBC 1.0) SQL_FN_STR_SUBSTRING、SQL_FN_STR_UCASE (ODBC 1.0)  
  
 アプリケーションが呼び出すことができる場合、**検索**でスカラー関数、 *string_exp1*、 *string_exp2*と*開始*引数、ドライバーSQL_FN_STR_LOCATE ビットマスクを返します。 アプリケーションでのみ使用して、検索スカラー関数を呼び出すことができる場合、 *string_exp1*と*string_exp2*引数、ドライバーは SQL_FN_STR_LOCATE_2 ビットマスクを返します。 完全にサポートするドライバー、**検索**スカラー関数は、両方のビットマスクを返します。  
  
 (詳細については、次を参照してください[文字列関数](../../../odbc/reference/appendixes/string-functions.md)、付録 e"スカラー関数です。")。  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 サブクエリをサポートする述語を列挙する SQLUINTEGER ビットマスク。  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES ビットマスクは、サブクエリをサポートするすべての述語が相関サブクエリをサポートすることを示します。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、すべてのこれらのビットが設定されているビットマスクは常に返します。  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1.0)  
 ドライバーと関連付けられているデータ ソースでサポートされているスカラー システム関数を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートするシステム関数を調べます。  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 テーブルのデータ ソースの仕入先の名前を持つ文字の文字列たとえば、"table"または"file"です。  
  
 この文字の文字列は、上部、下部、または大文字と小文字で指定できます。  
  
 SQL 92 エントリのレベル-に準拠するドライバーは、"table"を常に返します。  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 ドライバーと TIMESTAMPADD のスカラー関数の関連するデータ ソースでサポートされているタイムスタンプ間隔を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用して、どの間隔がサポートされているを調べます。  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 過渡期のレベルに準拠のドライバーでは、すべてのこれらのビットが設定されているビットマスクは常に返します。  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 ドライバーと TIMESTAMPDIFF のスカラー関数の関連するデータ ソースでサポートされているタイムスタンプ間隔を列挙する SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用して、どの間隔がサポートされているを調べます。  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 過渡期のレベルに準拠のドライバーでは、すべてのこれらのビットが設定されているビットマスクは常に返します。  
  
 SQL_TIMEDATE_FUNCTIONS(ODBC 1.0)  
 注:情報の種類が ODBC 1.0; で導入されました。各ビットマスクが導入されたバージョンが付いています。  
  
 スカラーの日付と時刻の関数のドライバーと関連付けられているデータ ソースでサポートされている列挙 SQLUINTEGER ビットマスク。  
  
 次のビットマスクを使用してがサポートする日付と時刻の関数を調べます。  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) (ODBC 3.0) SQL_FN_TD_CURRENT_TIME SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) (ODBC 2.0) SQL_FN_TD_DAYNAME SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK (ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) (ODBC 1.0) SQL_FN_TD_MINUTE SQL_FN_TD_MONTH (ODBC 1.0) (ODBC 2.0) SQL_FN_TD_MONTHNAME SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_2 番目 (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) (ODBC 1.0) SQL_FN_TD_WEEK、SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 注:情報の種類が ODBC 1.0; で導入されました。戻り値の各値には、導入されたバージョンが付いています。  
  
 ドライバーまたはデータ ソースでサポートされるトランザクションを記述する SQLUSMALLINT 値:  
  
 SQL_TC_NONE = トランザクションはサポートされていません。 (ODBC 1.0)  
  
 SQL_TC_DML = トランザクションは、データ操作言語 (DML) ステートメントのみを含めることができます (**選択**、**挿入**、 **UPDATE**、**削除**). データ定義言語 (DDL) ステートメントのトランザクションの原因でエラーが発生しました。 (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT = トランザクションは、DML ステートメントのみを含めることができます。 DDL ステートメント (**CREATE TABLE**、 **DROP INDEX**など)、トランザクションをコミットするトランザクションの原因で発生しました。 (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = トランザクションは、DML ステートメントのみを含めることができます。 トランザクションで発生した DDL ステートメントは無視されます。 (ODBC 2.0)  
  
 SQL_TC_ALL = トランザクションは、DDL ステートメントや DML ステートメントで任意の順序で含めることができます。 (ODBC 1.0)  
  
 (トランザクションのサポートは、sql-92 で必須であるため、sql-92 に準拠するドライバー [任意のレベル] を返さない SQL_TC_NONE。)  
  
 SQL_TXN_ISOLATION_OPTION (ODBC 1.0)  
 ドライバーまたはデータ ソースから使用可能なトランザクション分離レベルを列挙する SQLUINTEGER ビットマスク。  
  
 以下のビットマスクは、どのオプションがサポートされているかを判断するフラグと共に使用されます。  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 これらの分離レベルの説明については、SQL_DEFAULT_TXN_ISOLATION の説明を参照してください。  
  
 トランザクション分離レベルを設定するアプリケーションを呼び出す**SQLSetConnectAttr** SQL_ATTR_TXN_ISOLATION 属性を設定します。 詳細については、次を参照してください。 [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)します。  
  
 SQL 92 エントリのレベルに準拠ドライバーでは、サポートされている、SQL_TXN_SERIALIZABLE は常に返します。 サポートされている、FIPS 過渡期レベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_UNION(ODBC 2.0)  
 列挙のサポート、SQLUINTEGER ビットマスク、**共用体**句。  
  
 SQL_U_UNION、データ ソースがサポートを =、**共用体**句。  
  
 SQL_U_UNION_ALL =、データ ソースがサポートする、**すべて**キーワード、**共用体**句。 (**SQLGetInfo** SQL_U_UNION と、SQL_U_UNION_ALL の両方をここで返します)。  
  
 サポートされている、SQL 92 エントリのレベルに準拠ドライバーはこれらのオプションの両方を返します常にされます。  
  
 SQL_USER_NAME(ODBC 1.0)  
 ログイン名と異なる場合、特定のデータベースで使用される名前の文字列を返します。  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 使用するバージョンの ODBC ドライバー マネージャーが完全に準拠 Open Group の仕様のパブリケーションの年を示す文字列。  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 文字の文字列。ユーザーは、によって返されるすべてのプロシージャを実行できる場合は"Y" **SQLProcedures**;"N"プロシージャが可能性がある場合は、ユーザーが実行できないことを返されます。  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 文字の文字列。"Y"、ユーザーが保証される場合**選択**によって返されるすべてのテーブルに特権**SQLTables**;ユーザーがアクセスできない場合、テーブルがある可能性があります"N"が返されます。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 ドライバーがサポートできるアクティブな環境の最大数を示す SQLUSMALLINT 値を指定します。 指定された制限はありません、または既知の制限は、この値は 0 に設定します。  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 集計関数のサポートを列挙する SQLUINTEGER ビットマスク。  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 サポートされている、SQL 92 エントリのレベルに準拠ドライバーはこれらのオプションすべてを返します常にされます。  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **ALTER ドメイン**ステートメントでは、データ ソースでサポートされる、sql-92 で定義されています。 SQL 92 完全レベル準拠のドライバー、ビットマスクのすべては常に返します。 「0」の戻り値。 つまり、 **ALTER ドメイン**ステートメントはサポートされていません。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 追加のドメインの制約がサポートされています (フル レベル)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT =\<ドメインが alter > \<set ドメイン既定句 > はサポートされています (フル レベル)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<制約定義名句 > はドメインの制約 (中間レベル) の名前付けのサポートされています  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop ドメイン制約句 > はサポートされています (フル レベル)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT =\<ドメインが alter > \<drop ドメイン既定句 > はサポートされています (フル レベル)  
  
 次のビットをサポートされている指定\<制約属性 > 場合\<ドメインの制約の追加 > はサポートされて (SQL_AD_ADD_DOMAIN_CONSTRAINT ビットが設定されます)。  
  
 (完全レベル) SQL_AD_ADD_CONSTRAINT_DEFERRABLE SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (完全レベル) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (完全レベル) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (完全レベル)  
  
 SQL_ALTER_TABLE(ODBC 2.0)  
 内の句を列挙する SQLUINTEGER ビットマスク、 **ALTER TABLE**ステートメント、データ ソースでサポートされています。  
  
 この機能をサポートする必要があります、sql-92 または FIPS 準拠のレベルは、各ビットマスクの横にかっこに表示されます。  
  
 次のビットマスクを使用して、どの句がサポートされているを調べます。  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<列の追加 > 句はサポートされて、列の照合順序 (完全レベル) を指定する機能を使用 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<列の追加 > 句はサポートされて、列の既定値 (FIPS 過渡期レベル) を指定する機能を使用 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<列の追加 > は (FIPS 過渡期レベル) のサポート (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<列の追加 > 句はサポートされて、列の制約 (FIPS 過渡期レベル) を指定する機能を使用 (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<テーブル制約の追加 > 句がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<制約名の定義 > 列およびテーブルの制約 (中間レベル) の名前付けはサポートされて (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<列の削除 > CASCADE がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<alter 列 > \<drop 列の既定の句 > は、(中間レベル) をサポート (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<列の削除 > 制限がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<列の削除 > 制限がサポートされています (FIPS 過渡期レベル) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<alter 列 >\<セット列の既定の句 > は、(中間レベル) をサポート (ODBC 3.0)  
  
 次のビットのサポートを指定する\<制約属性 > 列またはテーブルの制約を指定することがサポートされている場合 (SQL_AT_ADD_CONSTRAINT ビットが設定されます)。  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (完全レベル) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (完全レベル) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (完全レベル) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (完全レベル) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 ドライバーでの非同期サポートのレベルを示す SQLUINTEGER 値:  
  
 SQL_AM_CONNECTION = 接続レベルの非同期実行がサポートされています。 指定された接続ハンドルに関連付けられたすべてのステートメント ハンドルは非同期モードか、同期モードではすべて。 接続のステートメント ハンドルは、同じ接続上の別のステートメント ハンドルが同期モードでは、その逆で非同期モードですることはできません。  
  
 SQL_AM_STATEMENT = ステートメント レベルの非同期実行がサポートされています。 接続ハンドルに関連付けられたステートメント ハンドルをいくつかは、同じ接続上で他のステートメント ハンドルを同期モードでは非同期モードで指定できます。  
  
 SQL_AM_NONE = 非同期モードはサポートされていません。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 行の可用性に関して、ドライバーの動作を列挙する SQLUINTEGER ビットマスクをカウントします。 情報の種類と共に、次の各ビットマスクが使用されます。  
  
 SQL_BRC_ROLLED_UP = 行カウントの連続する INSERT、DELETE、または UPDATE ステートメントが 1 つにロール アップされます。 このビットが設定されていない場合の行数は各ステートメントで使用できます。  
  
 SQL_BRC_PROCEDURES バッチがストアド プロシージャで実行されると、いずれかが使用可能な場合は、行の数を = です。 行カウントが使用可能な場合は、上または SQL_BRC_ROLLED_UP ビットによって、個別に使用できる、ロールバックすることができます。  
  
 SQL_BRC_EXPLICIT バッチを呼び出すことによって直接実行すると、いずれかが使用可能な場合は、行の数を = **SQLExecute**または**SQLExecDirect**します。 行カウントが使用可能な場合は、上または SQL_BRC_ROLLED_UP ビットによって、個別に使用できる、ロールバックすることができます。  
  
## <a name="example"></a>例  
 **SQLGetInfo** SQLUINTEGER、ビットマスクのとしてサポートされているオプションの一覧を返します **InfoValuePtr*します。 各オプションのビットマスクは、オプションはサポートされているかどうかを決定するフラグと共に使用されます。  
  
 など、アプリケーションでは、部分文字列のスカラー関数が、接続に関連付けられたドライバーでサポートされているかどうかを判断するのに、次のコードを使用できます。  
  
 別の使用例について**SQLGetInfo**を参照してください[SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)します。  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>関連する関数  
 接続属性の設定を返す  
 [SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 ドライバーが関数をサポートしているかどうかを決定します。  
 [SQLGetFunctions 関数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 ステートメント属性の設定を返す  
 [SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 データ ソースのデータ型に関する情報を返す  
 [SQLGetTypeInfo 関数](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
