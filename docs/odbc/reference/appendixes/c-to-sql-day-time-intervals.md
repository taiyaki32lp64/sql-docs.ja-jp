---
title: 'C から SQL へ: 日付と時刻の間隔 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3a4df236273b5afcaba78052ac236669bb133f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019369"
---
# <a name="c-to-sql-day-time-intervals"></a>C から SQL へ: 日付と時刻の間隔
日付と時刻の間隔の ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 次の表は、ODBC SQL データ型の C データの間隔を変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> [A] SQL_VARCHAR<br /><br /> [A] SQL_LONGVARCHAR|列のバイト長 > バイト長の文字を =<br /><br /> 列のバイト長 < 文字バイト長 [a]<br /><br /> データの値がリテラルの有効期間です。|n/a<br /><br /> 22001<br /><br /> 22015|  
|[A] SQL_WCHAR<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR[a]|列の文字の長さ > データの文字の長さを =<br /><br /> 列の文字の長さ < [a] のデータの文字長<br /><br /> データの値がリテラルの有効期間です。|n/a<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT [b] SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|単一フィールドの間隔の変換は整数の桁に切り捨てを実行できませんでした。<br /><br /> 変換の結果が整数の桁に切り捨て|n/a<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|すべてのフィールドに変換されたデータ値<br /><br /> データ値の 1 つまたは複数のフィールドが変換中に切り詰められました。|n/a<br /><br /> 22015|  
  
 [a] すべての C interval データ型は、文字データ型に変換できます。  
  
 [b] interval 構造体の型フィールドが、間隔が 1 つのフィールド (SQL_DAY、SQL_HOUR、SQL_MINUTE、または SQL_SECOND) の場合、間隔 C 型は、任意の正確な数値 (SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT に変換できます。、SQL_DECIMAL、または SQL_NUMERIC)。  
  
 C の間隔の種類の既定の変換では、対応する日付と時刻の間隔の SQL 型にします。  
  
 ドライバーでは、間隔 C データ型からデータを変換するとき長さ/インジケーター値を無視し、データ バッファーのサイズが間隔 C データ型のサイズであると仮定します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.  
  
 次の例では、データベース列に格納されている SQL_INTERVAL_STRUCT 構造間隔 C のデータを送信する方法を示します。 Interval 構造体には、DAY_TO_SECOND 間隔; が含まれています。SQL_INTERVAL_DAY_TO_MINUTE の種類のデータベース列に格納されます。  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
