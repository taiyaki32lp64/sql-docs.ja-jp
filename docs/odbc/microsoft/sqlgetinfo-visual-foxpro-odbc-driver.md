---
title: SQLGetInfo (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14837bc5ba3368fbb0d33680ee1c54936ab0a224
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898847"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:レベル 1  
  
 Visual FoxPro ODBC ドライバーと、接続ハンドルに関連付けられているデータ ソースに関する一般的な情報を返します*hdbc*します。 次の一覧には、各 Visual FoxPro ODBC ドライバーによって返される値が表示されます。 *fInfoType*引数と戻り値に関するコメント。  
  
 詳細については、次を参照してください。 [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)で、 *ODBC プログラマ リファレンス*します。  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES 返します 'N' です。  
  
 SQL_ACCESSIBLE_TABLES 'Y' を返します。  
  
 SQL_ACTIVE_CONNECTIONS では、0 を返します。  
  
 SQL_ACTIVE_STATEMENTS では、0 を返します。  
  
 SQL_ALTER_TABLE は、SQL_AT_ADD_COLUMN または SQL_AT_DROP_COLUMN のいずれかを返します。  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE SQL_BP_SCROLL を返します。  
  
## <a name="c"></a>c  
 SQL_COLUMN_ALIAS 'Y' を返します。  
  
 SQL_CONCAT_NULL_BEHAVIOR SQL_CB_ を返します。  
  
 SQL_CONVERT_BIGINT では、0 を返します。 Visual FoxPro ODBC ドライバーがサポートしていません*BigInt*します。  
  
 SQL_CONVERT_BINARY では、0 を返します。  
  
 SQL_CONVERT_BIT では、0 を返します。  
  
 SQL_CONVERT_CHAR では、0 を返します。  
  
 SQL_CONVERT_DATE では、0 を返します。  
  
 SQL_CONVERT_DECIMAL では、0 を返します。  
  
 SQL_CONVERT_DOUBLE では、0 を返します。  
  
 SQL_CONVERT_FLOAT では、0 を返します。  
  
 SQL_CONVERT_INTEGER では、0 を返します。  
  
 SQL_CONVERT_LONGVARBINARY では、0 を返します。  
  
 SQL_CONVERT_LONGVARCHAR では、0 を返します。  
  
 SQL_CONVERT_NUMERIC では、0 を返します。  
  
 SQL_CONVERT_REAL では、0 を返します。  
  
 SQL_CONVERT_SMALLINT では、0 を返します。  
  
 SQL_CONVERT_TIME では、0 を返します。  
  
 SQL_CONVERT_TIMESTAMP では、0 を返します。  
  
 SQL_CONVERT_TINYINT では、0 を返します。  
  
 SQL_CONVERT_VARBINARY では、0 を返します。  
  
 SQL_CONVERT_VARCHAR では、0 を返します。  
  
 SQL_CONVERT_FUNCTIONS では、0 を返します。  
  
 SQL_CORRELATION_NAME SQL_CN_ANY を返します。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_PRESERVE を返します。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR SQL_CB_PRESERVE を返します。  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME を DSN として渡される値を返します[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)、または[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md); DSN が指定されていない場合は、空の文字列を返します。  
  
 SQL_DATA_SOURCE_READ_ONLY 返します 'N' です。  
  
 データ ソースがある場合、SQL_DATABASE_NAME が現在のデータベースに完全な UNC パスを返します、[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)します。 データ ソースのディレクトリに接続している場合[テーブル](../../odbc/microsoft/visual-foxpro-terminology.md)関数が、ディレクトリへのパスを返します。  
  
 SQL_DBMS_NAME では、"Visual FoxPro"を返します。  
  
 SQL_DBMS_VER「03.00.0000」を返します。  
  
 SQL_DEFAULT_TXN_ISOLATION SQL_TXN_READ_COMMITTED を返します。 ダーティ リードが可能であればではありませんが、反復不能読み取りおよびファントム場合があります。  
  
 SQL_DRIVER_HDBC は、ドライバー マネージャーによって実装されます。  
  
 SQL_DRIVER_HENV は、ドライバー マネージャーによって実装されます。  
  
 SQL_DRIVER_HLIB は、ドライバー マネージャーによって実装されます。  
  
 SQL_DRIVER_HSTMT は、ドライバー マネージャーによって実装されます。  
  
 SQL_DRIVER_NAME"vfpodbc.dll"を返します。  
  
 SQL_DRIVER_ODBC_VER「02.50」(SQL_SPEC_MAJOR、SQL_SPEC_MINOR) を返します。  
  
 SQL_DRIVER_VER「01.00.0000」を返します。  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY 返します 'N' です。  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION が返されます。  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK です。  
  
 SQL_FILE_USAGE では、データベース (.dbc ファイル) の両方の SQL_FILE_QUALIFIER を取得し、テーブル (.dbf ファイル) のデータ ソースの無料します。  
  
## <a name="g-h"></a>G H  
 SQL_GETDATA_EXENSIONS が返されます。  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY SQL_GB_NO_RELATION を返します。  
  
## <a name="i-j"></a>J  
 SQL_IDENTIFIER_CASE SQL_IC_MIXED を返します。  
  
 SQL_IDENTIFIER_QUOTE_CHAR 返します '。  
  
## <a name="k"></a>K  
 SQL_KEYWORDS 返します""です。  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE 返します 'N' です。  
  
 SQL_LOCK_TYPES SQL_LCK_NO_CHANGE を返します。  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN では、0 を返します。  
  
 SQL_MAX_CHAR_LITERAL_LEN 254 を返します。  
  
 SQL_MAX_COLUMN_NAME_LEN では、128 を返します。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY では、16 を返します。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY では、16 を返します。  
  
 SQL_MAX_COLUMNS_IN_INDEX では、0 を返します。  
  
 SQL_MAX_COLUMNS_IN_SELECT 254 を返します。  
  
 SQL_MAX_COLUMNS_IN_TABLE 254 を返します。  
  
 SQL_MAX_CURSOR_NAME_LEN 254 を返します。  
  
 SQL_MAX_INDEX_SIZE では、0 を返します。  
  
 SQL_MAX_OWNER_NAME_LEN では、0 を返します。  
  
 SQL_MAX_PROCEDURE_NAME_LEN では、0 を返します。 Visual FoxPro ODBC ドライバーでは、Visual FoxPro のストアド プロシージャへの直接アクセスをできません。  
  
 SQL_MAX_QUALIFIER_NAME_LEN では、オペレーティング システムの最大パス長を返します。  
  
 SQL_MAX_ROW_SIZE 返します 254 ^2。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG 返します 'N' です。  
  
 SQL_MAX_STATEMENT_LEN 8192 を返します。  
  
 SQL_MAX_TABLE_NAME_LEN では、128 を返します。  
  
 SQL_MAX_TABLES_IN_SELECT では、16 を返します。  
  
 SQL_MAX_USER_NAME_LEN では、0 を返します。  
  
 SQL_MULT_RESULT_SETS 'Y' を返します。  
  
 SQL_MULTIPLE_ACTIVE_TXN 'Y' を返します。 複数の接続には、複数のトランザクションが、一度に開くことができます。  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN 返します 'N' です。  
  
 SQL_NON_NULLABLE_COLUMNS SQL_NNC_NON_NULL を返します。  
  
 SQL_NULL_COLLATION SQL_NC_LOW を返します。  
  
 SQL_NUMERIC_FUNCTIONS は、SQL_FN_NUM_POWER、Visual FoxPro ODBC ドライバーでサポートされていないを除くすべての関数を返します。 次の関数がサポートされています。  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE SQL_OAC_LEVEL1 を返します。  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE SQL_OSCC_COMPLIANT を返します。  
  
 SQL_ODBC_SQL_CONFORMANCE SQL_OSC_MINIMUM を返します。 最低限の SQL 構文がサポートされています。  
  
 SQL_ODBC_SQL_OPT_IEF"N"を返します。  
  
 SQL_ODBC_VER は、ドライバー マネージャーによって実装されます。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT"N"を返します。  
  
 SQL_OUTER_JOINS"N"を返します。  
  
 SQL_OWNER_TERM 返します""です。 Visual FoxPro ODBC ドライバーは、そのオブジェクトの所有者をサポートしていません。  
  
 SQL_OWNER_USAGE では、0 を返します。 Visual FoxPro ODBC ドライバーは、そのオブジェクトの所有者をサポートしていません。  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS SQL_POS_POSITION を返します。  
  
 SQL_POSITIONED_STATEMENTS では、0 を返します。  
  
 SQL_PROCEDURE_TERM 返します""です。  
  
 SQL_PROCEDURES 返します 'N' です。  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION SQL_QL_START を返します。  
  
 SQL_QUALIFIER_NAME_SEPARATOR 返します '!' または '\\'。 データベースとテーブル間の区切り記号は、'!' に接続されているデータ ソースの[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)、および '\\' のディレクトリにあるデータ ソースの[テーブルを無料](../../odbc/microsoft/visual-foxpro-terminology.md)します。  
  
 SQL_QUALIFIER_TERM では、"database"または"directory"を返します。 修飾子"database"に接続されたデータ ソースについては、[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)とのディレクトリにあるデータ ソースの「ディレクトリ」[テーブルを無料](../../odbc/microsoft/visual-foxpro-terminology.md)します。  
  
 SQL_QUALIFIER_USAGE は SQL_QU_PRIVILEGE_DEFINITION; をサポートしていませんSQL_QU_DML_STATEMENT または SQL_QU_TABLE_DEFINITION のいずれかを返します。  
  
 SQL_QUOTED_IDENTIFIER_CASE SQL_IC_MIXED を返します。  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES"N"を返します。 Visual FoxPro ODBC ドライバーには、のみ静的カーソルと順方向カーソルがサポートしています。  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY SQL_SCCO_READ_ONLY を返します。  
  
 SQL_SCROLL_OPTIONS は、SQL_SO_STATIC または SQL_SO_READONLY のいずれかを返します。  
  
 SQL_SEARCH_PATTERN_ESCAPE 返します"\\"。  
  
 SQL_SERVER_NAME 返します""です。  
  
 SQL_SPECIAL_CHARACTERS 返します"~ @# $% ^"。  
  
 SQL_STATIC_SENSITIVITY では、0 を返します。 Visual FoxPro ODBC ドライバーは、位置指定更新をサポートしていません。  
  
 SQL_STRING_FUNCTIONS は SQL_FN_STR_INSERT、SQL_FN_STR_LOCATE、SQL_FN_STR_LOCATE_2、または SQL_FN_STR_SOUNDEX をサポートしていません。  
  
 返されます。  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE します。  
  
 SQL_SUBQUERIES が返されます。  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED します。  
  
 SQL_SYSTEM_FUNCTIONS が返されます。  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 ありません。  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM では、"table"を返します。  
  
 SQL_TIMEDATE_ADD_INTERVALS が返されます。  
  
-   SQL_FN_TSI_ 秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 ありません。  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS が返されます。  
  
-   SQL_FN_TSI_ 秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS は SQL_FN_TD_QUARTER、SQL_FN_TD_TIMESTAMPADD、SQL_FN_TD_DAYOFYEAR、または SQL_FN_TD_WEEK をサポートしていません。  
  
 返されます。  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR します。  
  
 SQL_TXN_CAPABLE SQL_TC_DML を返します。  
  
 SQL_TXN_ISOLATION_OPTION SQL_TXN_READ_COMMITTED を返します。  
  
## <a name="u-z"></a>U Z  
 SQL_UNION は、SQL_U_UNION または、SQL_U_UNION_ALL のいずれかを返します。  
  
 SQL_USER_NAME 返します\<空白 >。
