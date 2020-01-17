---
title: 'SQL から C へ: 日付と時刻の間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db39751059d84e4e3a7950acbbbcb7f1a2b0b00d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056860"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL から C へ: 日付と時刻の間隔

日付と時刻の間隔の ODBC SQL データ型の識別子、次に示します。

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

次の表は、ODBC C データ型の日付と時刻の間隔 SQL データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。

|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|すべての日付と時刻 C interval 型|末尾のフィールドの部分を切り捨てることができません。<br /><br /> 末尾のフィールドの部分が切り捨てられます<br /><br /> ソースからデータを保持するために十分な大きさが先頭のターゲットの有効桁数です。|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの長さ<br /><br /> データの長さ<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22015|  
|[B] [b] [b] [b] [b] [b] [b] [b] SQL_C_BIGINT SQL_C_NUMERIC SQL_C_ULONG SQL_C_SLONG SQL_C_SHORT SQL_C_USHORT SQL_C_UTINYINT SQL_C_STINYINT|間隔の有効桁数が 1 つのフィールドとデータを切り捨てることがなく変換されました。<br /><br /> 間隔の有効桁数が 1 つのフィールドと小数部の切り捨て<br /><br /> 間隔の有効桁数が 1 つのフィールドおよび全体が切り捨て<br /><br /> 間隔の有効桁数が 1 つのフィールド|データ<br /><br /> 切り捨てられたデータ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> データの長さ<br /><br /> データの長さ<br /><br /> C データ型のサイズ|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|データのバイト長 < = *BufferLength*<br /><br /> データのバイト長 > *BufferLength*|データ<br /><br /> 未定義。|データの長さ<br /><br /> 未定義。|n/a<br /><br /> 22003|  
|SQL_C_CHAR|バイトの長さを文字 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 > = *BufferLength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|文字長 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 > = *BufferLength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
  
 [a]、日付と時刻の間隔の SQL 型は、任意の日付と時刻の間隔 C 型に変換できます。  
  
 [b] 間隔の有効桁数が 1 つのフィールド (DAY、HOUR、MINUTE、または秒の 1 つ) の場合、SQL 型の間隔は、(SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG、または SQL_C_NUMERIC) の任意の正確な数値に変換できます。  
  
間隔の SQL 型の既定の変換は、対応する C interval データ型には。 アプリケーション、列またはパラメーターをバインドします (または、ARD の適切なレコードの SQL_DESC_DATA_PTR フィールドを設定します) に初期化された SQL_INTERVAL_STRUCT 構造体を指す (または、としてsql_INTERVAL_STRUCT構造体へのポインターを渡します*TargetValuePtr*への呼び出しで引数**SQLGetData**)。  
  
次の例では、DAY_TO_HOUR 間隔として戻ってくるように SQL_INTERVAL_STRUCT 構造に SQL_INTERVAL_DAY_TO_MINUTE 型の列からデータを転送する方法を示します。  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
