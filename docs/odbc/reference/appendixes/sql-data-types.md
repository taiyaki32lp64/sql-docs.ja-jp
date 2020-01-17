---
title: SQL データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4be0e017988670d740067011f775f8477037aa18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057031"
---
# <a name="sql-data-types"></a>SQL データ型
各 DBMS は、独自の SQL 型を定義します。 各 ODBC ドライバーでは、関連付けられている DBMS 定義 SQL データ型のみを公開します。 SQL の ODBC で定義された型の識別子にドライバーをマップする方法については DBMS SQL 型し、独自ドライバー固有の SQL 型識別子に、ドライバーが DBMS SQL 型をマップする方法を呼び出すことによって返される**SQLGetTypeInfo**します。 ドライバーは、列との呼び出しを通じてパラメーターのデータ型を記述するときにも、SQL データ型を返します**SQLColAttribute**、 **SQLColumns**、 **SQLDescribeCol**、**SQLDescribeParam**、 **SQLProcedureColumns**、および**SQLSpecialColumns**します。  
  
> [!NOTE]  
>  SQL データ型の実装記述子 SQL_DESC_ CONCISE_TYPE、SQL_DESC_TYPE、および SQL_DESC_DATETIME_INTERVAL_CODE フィールドに格納されます。 SQL データ型の特性の実装記述子の SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、および SQL_DESC_OCTET_LENGTH フィールドに格納されます。 詳細については、次を参照してください。[データ型識別子と記述子](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)後の「します。  
  
 特定のドライバーとデータ ソースは、必ずしもこの付録で定義されているすべての SQL データ型をサポートできません。 SQL データ型に対するドライバーのサポートは、ドライバーに準拠している SQL 92 のレベルによって異なります。 ドライバーによってサポートされている SQL 92 文法のレベルを決定するには、アプリケーションが呼び出す**SQLGetInfo** SQL_SQL_CONFORMANCE 情報の種類にします。 また、特定のドライバーとデータ ソースは、追加のドライバー固有の SQL データ型をサポートする可能性があります。 サポートするデータ型、ドライバーを決定する、アプリケーションを呼び出す**SQLGetTypeInfo**します。 ドライバー固有の SQL データ型については、ドライバーのドキュメントを参照してください。 特定のデータ ソース内のデータ型については、そのデータ ソースのドキュメントを参照してください。  
  
> [!IMPORTANT]  
>  この付録でテーブルは、唯一のガイドラインと名前を表示するために通常使用、範囲、および SQL データ型の制限です。 指定したデータ ソースは、表示されているデータ型の一部のみをサポート可能性があり、サポートされるデータ型の特性が示されていると異なることができます。  
  
 次の表では、すべての SQL データ型の有効な SQL 型の識別子を示します。 (存在する場合に、名前と説明、sql-92 から対応するデータ型の表にも示します。  
  
|SQL 型識別子 [1]|一般的な SQL データ<br /><br /> [2] の種類|一般的な種類の説明|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|文字の固定文字列長の文字列*n*します。|  
|SQL_VARCHAR|VARCHAR(*n*)|文字列の最大長の可変長文字列*n*します。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可変長文字データ。 最大長は、データ ソースに依存します。[9]|  
|SQL_WCHAR|WCHAR (*n*)|固定文字列長の Unicode 文字の文字列*n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|文字列の最大長を Unicode 文字の可変長文字列*n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode の可変長文字データです。 最大長は、データ ソースに依存しますです。|  
|SQL_DECIMAL|10 進数 (*p*、*s*)|署名、有効桁数の数値の正確な値には少なくとも*p*有効桁数と小数点*秒。* (最大有効桁数はドライバーの定義) です。(1 < = *p* < = 15;*s* <= *p*). [4]|  
|SQL_NUMERIC|数値 (*p*、*s*)|署名済み、有効桁数を持つの正確な数値値*p*有効桁数と小数点*s* (1 < = *p* < = 15;*s* <= *p*). [4]|  
|SQL_SMALLINT|SMALLINT|固定精度が 5 の数値と桁数が 0 (署名:-32,768 < = *n* < = 32,767、符号なし。0 <= *n* <= 65,535)[3].|  
|SQL_INTEGER|INTEGER|固定精度が 10 の数値と桁数が 0 (署名:-2 [31] < = *n* < = 2 [31] - 1、符号なし。0 < = *n* < = 2 [32] - 1) [3]。|  
|SQL_REAL|real|バイナリ精度が 24 の符号付き概数数値 (0、または絶対値が 10 [-38] 10[38]) します。|  
|SQL_FLOAT|FLOAT (*p*)|署名済み、バイナリの有効桁数を持つ概数数値には少なくとも*p*します。 (最大有効桁数はドライバーの定義) です。[5]|  
|SQL_DOUBLE|DOUBLE PRECISION|バイナリ精度が 53 の符号付き概数数値 (0、または絶対値が 10 [-308] 10[308]) します。|  
|SQL_BIT|BIT|1 つのビットのバイナリ データ。[8]|  
|SQL_TINYINT|TINYINT|固定精度が 3 で数値および桁数が 0 (署名:-128 < = *n* < = 127、符号なし。0 <= *n* <= 255)[3].|  
|SQL_BIGINT|bigint|正確な数値有効桁数 19 (符号付き) の場合または 20 (符号なし) の場合、桁数が 0 (署名:-2 [63] < = *n* < = 2 [63] - 1、符号なし。0 <= *n* <= 2[64] - 1)[3],[9].|  
|SQL_BINARY|バイナリ (*n*)|固定長のバイナリ データ*n*[。9]|  
|SQL_VARBINARY|VARBINARY (*n*)|最大長の可変長バイナリ データ*n*します。 最大値は、ユーザーによって設定されます。[9]|  
|SQL_LONGVARBINARY|長い VARBINARY|可変長バイナリ データ。 最大長は、データ ソースに依存します。[9]|  
|SQL_TYPE_DATE[6]|[DATE]|年、月、および日フィールド、グレゴリオ暦の規則に準拠します。 (を参照してください[グレゴリオ暦の制約](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)、この付録で後述します)。|  
|SQL_TYPE_TIME[6]|時間 (*p*)|1 時間、分、および 2 番目のフィールド、00 ~ 59 の分を 00 ~ 23 の有効な値の時間の有効な値と 61 を 00 の秒の有効な値。 有効桁数*p*秒の有効桁数を示します。|  
|SQL_TYPE_TIMESTAMP[6]|タイムスタンプ (*p*)|年、月、日、時間、分、および、日付と時刻のデータ型に対して定義されている有効な値を持つ 2 つ目のフィールド。|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|年、月、日、時、分、秒、utchour、および utcminute フィールドです。 Utchour と utcminute フィールドは、1/10 マイクロ秒の有効桁数を含めます。|  
|SQL_TYPE_UTCTIME|UTCTIME|1 時間、分、秒、utchour、および utcminute フィールドです。 Utchour と utcminute フィールドは、1/10 マイクロ秒の有効桁数を含める.|  
|SQL_INTERVAL_MONTH [7]|INTERVAL MONTH (*p*)|2 つの日付間の月数*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_YEAR [7]|INTERVAL YEAR (*p*)|2 つの日付間の年の数*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|INTERVAL YEAR (*p*) の月|年と 2 つの日付間の月の数*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_DAY [7]|間隔の日 (*p*)|2 つの日付間の日数*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_HOUR[7]|間隔の時間 (*p*)|日付/時刻の 2 つの間の時間数。*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_MINUTE [7]|INTERVAL MINUTE (*p*)|2 つの間隔 (分) の日付/時刻です。*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_SECOND [7]|間隔 2 番目 (*p*、*q*)|日付/時刻の 2 つの間の秒数。*p*は先頭の有効桁数の間隔と*q*間隔の秒の有効桁数です。|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|間隔の日 (*p*) 1 時間|日付/時刻の 2 つの間の日数/時間数。*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|間隔の日 (*p*) 分|2 つの日、時間と分の日付/時刻です。*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|間隔の日 (*p*) 2 番目 (*q*)|日/時間/分/秒間に 2 つの日付/時刻です。*p*は先頭の有効桁数の間隔と*q*間隔の秒の有効桁数です。|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|間隔の時間 (*p*) 分|日付/時刻の 2 つの分単位の時間数。*p*は先頭の有効桁数の間隔です。|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|間隔の時間 (*p*) 2 番目 (*q*)|2 つの時間、分/秒の日付/時刻です。*p*は先頭の有効桁数の間隔と*q*間隔の秒の有効桁数です。|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|間隔分 (*p*) 2 番目 (*q*)|分/秒間に 2 つの日付/時刻です。*p*は先頭の有効桁数の間隔と*q*間隔の秒の有効桁数です。|  
|SQL_GUID|GUID|固定長 GUID。|  
  
 [1] これは、DATA_TYPE 列への呼び出しによって返される値**SQLGetTypeInfo**します。  
  
 [2] これは、名前とパラメーターの作成の列への呼び出しによって返される値**SQLGetTypeInfo**します。 [名前] 列の表記を返します-たとえば、CHAR-作成 PARAMS 列は、有効桁数、小数点、および長さなどの作成パラメーターのコンマ区切りの一覧を返しますが、します。  
  
 [3]、アプリケーションを使用して**SQLGetTypeInfo**または**SQLColAttribute**かどうか、特定のデータ型または特定の結果セット列が署名されていないかを判断します。  
  
 [4] SQL_DECIMAL と SQL_NUMERIC のデータ型は、その有効桁数でのみが異なります。 10 進数の有効桁数 (*p*、*s*) は、実装で定義された小数点以下有効桁数である以上*p*であるのに対し、数値の有効桁数 (*p*、*s*) に正確に一致*p*します。  
  
 [24 または 53 5] の実装にに応じて使用できますの有効桁数ができます: SQL_REAL; と同じで使用できますのデータ型は、24 の場合、53 の場合は、使用できますのデータ型は SQL_DOUBLE と同じです。  
  
 [6] ODBC *3.x*、SQL の日付、時刻、タイムスタンプ データ型には、SQL_TYPE_DATE、SQL_TYPE_TIME、および SQL_TYPE_TIMESTAMP、ODBC でそれぞれ; *2.x*データ型は、SQL_DATE、SQL_TIME、および sql _タイムスタンプ。  
  
 [7] の間隔の SQL データ型の詳細については、次を参照してください。、 [Interval データ型](../../../odbc/reference/appendixes/interval-data-types.md)セクションで、この付録の「します。  
  
 [8] SQL_BIT データ型では、SQL 92 BIT 型よりも異なる特性があります。  
  
 [9] このデータ型には、sql-92 で対応するデータ型はありません。  
  
 このセクションでは、次の例を提供します。  
  
-   [SQLGetTypeInfo 結果セットの例](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
