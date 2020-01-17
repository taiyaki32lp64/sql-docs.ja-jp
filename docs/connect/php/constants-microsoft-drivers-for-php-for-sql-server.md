---
title: 定数 (Microsoft Drivers for PHP for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4081e9db30e3607d783de40a71d9d7b2e7599c76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993703"
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>定数 (Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]で定義される定数について説明します。  
  
## <a name="pdosqlsrv-driver-constants"></a>PDO_SQLSRV ドライバー定数  
[PDO Web サイト](https://php.net/manual/book.pdo.php)に記載されている定数は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] で有効です。  
  
次に、PDO_SQLSRV ドライバーの Microsoft 固有の定数について説明します。  
  
### <a name="transaction-isolation-level-constants"></a>トランザクション分離レベルの定数  
**PDO::__construct** と共に使用される [TransactionIsolation](../../connect/php/pdo-construct.md)キーは、次のいずれかの定数を受け入れます。  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
**TransactionIsolation** キーの詳細については、「 [Connection Options](../../connect/php/connection-options.md)」を参照してください。  
  
### <a name="encoding-constants"></a>エンコード定数  
The PDO::SQLSRV_ATTR_ENCODING 属性は、[PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)、[PDO::setAttribute](../../connect/php/pdo-setattribute.md), [PDO::prepare](../../connect/php/pdo-prepare.md)、[PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md)、[PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) に渡すことができます。  
  
PDO::SQLSRV_ATTR_ENCODING に渡すために使用できる値は次のとおりです。  
  
|PDO_SQLSRV ドライバー定数|[説明]|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|データは、エンコードや変換されていない、サーバーからの未加工のバイト ストリームです。<br /><br />PDO::setAttribute では無効です。|  
|PDO::SQLSRV_ENCODING_SYSTEM|データは、システムで設定された Windows ロケールのコード ページに指定されているとおりの 8 ビット文字です。 任意のマルチバイト文字またはこのコード ページにマップされていない文字は、1 バイトの疑問符 (?) 文字に置き換えられます。|  
|PDO::SQLSRV_ENCODING_UTF8|データは UTF-8 エンコードです。 これが既定のエンコードです。|  
|PDO::SQLSRV_ENCODING_DEFAULT|接続時に指定した場合は、PDO::SQLSRV_ENCODING_SYSTEM を使用します。<br /><br />準備ステートメントで指定した場合は、接続のエンコードを使用します。|  
  
### <a name="query-timeout"></a>[クエリ タイムアウト]  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT 属性は、タイムアウト時間を秒単位で表す任意の負以外の整数です。 既定値はゼロ (0) で、タイムアウトがないことを意味します。  
  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT 属性と共に、[PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)、[PDO::setAttribute](../../connect/php/pdo-setattribute.md)、および [PDO::prepare](../../connect/php/pdo-prepare.md) を指定できます。  
  
### <a name="direct-or-prepared-execution"></a>直接または準備実行  
PDO::SQLSRV_ATTR_DIRECT_QUERY 属性を使用して、直接クエリの実行または準備済みステートメントの実行を選択できます。 PDO::SQLSRV_ATTR_DIRECT_QUERY は、[PDO::prepare](../../connect/php/pdo-prepare.md) または [PDO::setAttribute](../../connect/php/pdo-setattribute.md) で設定できます。 PDO::SQLSRV_ATTR_DIRECT_QUERY の詳細については、「[PDO_SQLSRV ドライバーでの直接ステートメントの実行と準備されたステートメントの実行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)」を参照してください。  

### <a name="handling-numeric-fetches"></a>数値フェッチの処理
PDO:: SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 属性は、数値の SQL 型 (bit、integer、smallint、tinyint、float、real) を持つ列からの数値のフェッチを処理するために使用できます。 PDO:: SQLSRV_ATTR_FETCHES_NUMERIC_TYPE が true に設定されている場合、整数列の結果は int として表され、SQL float と reals は float として表されます。 この属性は、 [PDOStatement:: setAttribute](../../connect/php/pdostatement-setattribute.md)で設定できます。 

PDO:: SQLSRV_ATTR_FORMAT_DECIMALS 属性と PDO:: SQLSRV_ATTR_DECIMAL_PLACES 属性を使用して、既定の10進形式の動作を変更できます。 これらの属性の動作は、SQLSRV 側 (**Formatdecimals**および**DecimalPlaces**) の対応するオプションと同じですが、書式設定では出力パラメーターがサポートされていません。 これらの属性は、 [PDO:: setAttribute](../../connect/php/pdo-setattribute.md)または[PDOStatement:: setAttribute](../../connect/php/pdostatement-setattribute.md)の接続レベルまたはステートメントレベルで設定できますが、いずれのステートメント属性も、対応する接続属性より優先されます。 詳細については、「[10 進数文字列と金額の書式設定 (PDO_SQLSRV ドライバー)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)」をご覧ください。

### <a name="handling-date-and-time-fetches"></a>日付と時刻のフェッチの処理

PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE は、日付と時刻の型を[PHP DATETIME](http://php.net/manual/en/class.datetime.php)オブジェクトとして取得するかどうかを指定します。 false のままにすると、文字列として返すことが既定の動作となります。 この属性は、 [PDO:: setAttribute](../../connect/php/pdo-setattribute.md)または[PDOStatement:: setAttribute](../../connect/php/pdostatement-setattribute.md)の接続レベルまたはステートメントレベルで設定できますが、ステートメント属性は対応する接続属性よりも優先されます。 詳細については、「[方法: PDO_SQLSRV ドライバーを使用して日付/時刻型を PHP DateTime オブジェクトとして取得する](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)」を参照してください。

## <a name="sqlsrv-driver-constants"></a>SQLSRV ドライバーの定数  
次のセクションでは、SQLSRV ドライバーが使用する定数を一覧表示します。  
  
### <a name="err-constants"></a>ERR 定数  
次の表に、[sqlsrv_errors](../../connect/php/sqlsrv-errors.md) がエラー、警告、または両方を返す場合に、指定するために使用される定数を示します。  
  
|[値]|[説明]|  
|---------|---------------|  
|SQLSRV_ERR_ALL|**sqlsrv** 関数の最後の呼び出しで生成されたエラーと警告が返されます。 これが既定値です。|  
|SQLSRV_ERR_ERRORS|**sqlsrv** 関数の最後の呼び出しで生成されたエラーが返されます。|  
|SQLSRV_ERR_WARNINGS|**sqlsrv** 関数の最後の呼び出しで生成された警告が返されます。|  
  
### <a name="fetch-constants"></a>FETCH 定数  
次の表に、 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)によって返される配列の種類を指定するために使用される定数を示します。  
  
|SQLSRV 定数|[説明]|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** は、次のデータ行を連想配列として返します。|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** は、次のデータ行を、数値キーと連想キーを持つ配列として返します。 これが既定値です。|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** は、次のデータ行を数値インデックス配列として返します。|  
  
### <a name="logging-constants"></a>ログ記録の定数  
このセクションでは、 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)でログ記録の設定を変更するために使用する定数を一覧表示します。 ログ記録アクティビティの詳細については、「 [Logging Activity](../../connect/php/logging-activity.md)」を参照してください。  
  
次の表に、 **LogSubsystems** 設定の値として使用できる定数を示します。  
  
|SQLSRV 定数 (かっこ内と同等の整数)|[説明]|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|すべてのサブシステムのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_CONN (2)|接続アクティビティのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_INIT (1)|初期化アクティビティのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_OFF (0)|ログ記録をオフにします。|  
|SQLSRV_LOG_SYSTEM_STMT (4)|ステートメント アクティビティのログ記録をオンにします。|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|エラー関数アクティビティ (**handle_error** や **handle_warning** など) のログ記録をオンにします。|  
  
次の表に、 **LogSeverity** 設定の値として使用できる定数を示します。  
  
|SQLSRV 定数 (かっこ内と同等の整数)|[説明]|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|エラー、警告、および通知をログ記録することを指定します。|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|エラーをログ記録することを指定します。|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|通知をログ記録することを指定します。|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|警告をログ記録することを指定します。|  
  
### <a name="nullable-constants"></a>null 許容型の定数  
次の表に、この情報が使用できない場合に、列で null が使用可能かどうかを判断するために使用できる定数を示します。 **sqlsrv_field_metadata** によって返される [null 許容](../../connect/php/sqlsrv-field-metadata.md) キーの値を比較して、列で null が使用可能かどうかを判断できます。  
  
|SQLSRV 定数 (かっこ内と同等の整数)|[説明]|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|列で NULL 値が許容されます。|  
|SQLSRV_NULLABLE_NO (1)|この列では null 値は使用できません。|  
|SQLSRV_NULLABLE_UNKNOWN (2)|列で null 値が使用できるかどうかが不明です。|  
  
### <a name="param-constants"></a>PARAM 定数  
次の表に、 [sqlsrv_query](../../connect/php/sqlsrv-query.md) または [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)を呼び出すときにパラメーターの方向を指定する定数を示します。  
  
|SQLSRV 定数|[説明]|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|入力パラメーターを示します。|  
|SQLSRV_PARAM_INOUT|双方向のパラメーターを示します。|  
|SQLSRV_PARAM_OUT|出力パラメーターを示します。|  
  
### <a name="phptype-constants"></a>PHPTYPE 定数  
次の表に、PHP データ型の記述に使用される定数を示します。 PHP データ型の詳細については、 [PHP 型](https://php.net/manual/en/language.types.php)を参照してください。  
  
|SQLSRV 定数|PHP データ型|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Integer|  
|SQLSRV_PHPTYPE_DATETIME|DATETIME|  
|SQLSRV_PHPTYPE_FLOAT|float|  
|SQLSRV_PHPTYPE_STREAM ($encoding<sup>1</sup>)|STREAM|  
|SQLSRV_PHPTYPE_STRING ($encoding<sup>1</sup>)|String|  
  
1. **SQLSRV_PHPTYPE_STREAM** と **SQLSRV_PHPTYPE_STRING** は、ストリームのエンコードを指定するパラメーターを受け入れます。 次の表には、受け入れ可能なパラメーターの SQLSRV 定数と、対応するエンコードの説明が含まれています。  
  
|SQLSRV 定数|[説明]|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|データは、エンコードまたは変換されず、生のバイト ストリームとしてサーバーから返されます。|  
|SQLSRV_ENC_CHAR|データは、システムに設定された Windows ロケールのコード ページに指定されているとおりに、8 ビット文字で返されます。 任意のマルチバイト文字またはこのコード ページにマップされていない文字は、1 バイトの疑問符 (?) 文字に置き換えられます。<br /><br />これが既定のエンコードです。|  
|"UTF-8"|データは UTF-8 エンコードで返されます。 この定数は、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 1.1 で追加されました。 UTF-8 のサポートの詳細については、「[方法: 組み込みの UTF-8 サポートを使用した UTF-8 データの送信と取得](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)」を参照してください。|  
  
> [!NOTE]  
> **SQLSRV_PHPTYPE_STREAM** または **SQLSRV_PHPTYPE_STRING** を使用する場合、エンコードを指定する必要があります。 パラメーターを省略すると、エラーが返されます。  
  
これらの定数の詳細については、「 [方法: PHP データ型を指定する](../../connect/php/how-to-specify-php-data-types.md)」および「 [方法: SQLSRV ドライバーを使用したストリームとしての文字データの取得](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)」を参照してください。  
  
### <a name="sqltype-constants"></a>SQLTYPE 定数  
次の表に、SQL Server データ型の記述に使用される定数を示します。 一部の定数は関数に似ており、有効桁数、小数点以下桁数、または長さに対応するパラメーターを受け取ることができます。  パラメーターをバインドする場合は、関数に似た定数を使用する必要があります。 型の比較では、標準 (関数に似ていない) 定数が必要です。 SQL Server データ型の詳細については、「[データ型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。 有効桁数、小数点以下桁数、長さの詳細については、「[有効桁数、小数点以下桁数、および長さ (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)」を参照してください。  
  
|SQLSRV 定数|SQL Server データ型|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|BIGINT|  
|SQLSRV_SQLTYPE_BINARY|binary|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|文字<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char|  
|SQLSRV_SQLTYPE_DATE|date<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|DATETIME|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|10進数<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|Decimal|  
|SQLSRV_SQLTYPE_FLOAT|FLOAT|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|INT|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|nchar<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|数値<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|NUMERIC|  
|SQLSRV_SQLTYPE_NVARCHAR|nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|NVARCHAR|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|REAL|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|SMALLINT|  
|SQLSRV_SQLTYPE_SMALLMONEY|SMALLMONEY|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|TIMESTAMP|  
|SQLSRV_SQLTYPE_TINYINT|TINYINT|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|  
|SQLSRV_SQLTYPE_UDT|UDT (UDT)|  
|SQLSRV_SQLTYPE_VARBINARY|varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary (max)|  
|SQLSRV_SQLTYPE_VARCHAR|varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARCHAR('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|xml|  
  
1.  これは、varbinary(max) 型にマップされる従来の型です。  
  
2.  これは、新しい nvarchar 型にマップされる従来の型です。  
  
3.  これは、新しい varchar 型にマップされる従来の型です。  
  
4.  この型のサポートは、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 1.1 で追加されました。  

5.  これらの定数は、型比較演算で使用する必要があり、関数に似た定数を同様の構文に置き換えることはできません。 バインドパラメーターの場合は、関数に似た定数を使用する必要があります。

  
次の表に、パラメーターを受け入れる SQLTYPE 定数とパラメーターに許容される値の範囲を示します。  
  
|SQLTYPE|パラメーター|パラメーターの許容範囲|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR,<br /><br />SQLSRV_SQLTYPE_VARCHAR|charCount|1 - 8000|  
|SQLSRV_SQLTYPE_NCHAR,<br /><br />SQLSRV_SQLTYPE_NVARCHAR|charCount|1 - 4000|  
|SQLSRV_SQLTYPE_BINARY,<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1 - 8000|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|有効桁数 (precision)|1 - 38|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|scale|1 - 有効桁数|  
  
### <a name="transaction-isolation-level-constants"></a>トランザクション分離レベルの定数  
**sqlsrv_connect** と共に使用される [TransactionIsolation](../../connect/php/sqlsrv-connect.md)キーは、次のいずれかの定数を受け入れます。  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>カーソルとスクロールの定数  
次の定数は、結果セットで使用できるカーソルの種類を指定します。  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
次の定数は、結果セットに選択する行を指定します。  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
これらの定数の使用の詳細については、「 [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
  
