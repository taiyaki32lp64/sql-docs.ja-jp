---
title: 'SQL から C へ: Numeric |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a23e60b161c09367cfb079cea1f7ca146b4ebee5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056851"
---
# <a name="sql-to-c-numeric"></a>SQL から C へ: 数値

識別子の数値の ODBC SQL データ型に次のとおりです。

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

次の表は、ODBC C データ型が数値の SQL データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。  

|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|バイトの長さを文字 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 > = *BufferLength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|文字長 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 < *BufferLength*<br /><br /> (ではなく小数部) 全体の桁数 > = *BufferLength*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|データの文字の長さ<br /><br /> データの文字の長さ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|[A] を切り捨てることがなく変換されたデータ<br /><br /> データを変換する小数部の桁数が [a] の切り捨て<br /><br /> データの変換が [a] (ではなく小数部) の整数桁の損失になります|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> C データ型のサイズ<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|データは、数の変換先のデータ型の範囲内で、[a]<br /><br /> データが数の変換先のデータ型の範囲外 [a]|データ<br /><br /> 未定義。|C データ型のサイズ<br /><br /> 未定義。|n/a<br /><br /> 22003|  
|SQL_C_BIT|データが 0 または 1 [a]<br /><br /> データが 2 よりも小さいと等しくない [a] の 1、0 より大きい<br /><br /> データが 0 未満またはより大きい、または [a] の 2|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|データのバイト長 < = *BufferLength*<br /><br /> データのバイト長 > *BufferLength*|データ<br /><br /> 未定義。|データの長さ<br /><br /> 未定義。|n/a<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] [c] SQL_C_INTERVAL_DAY SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|データは切り捨てられません<br /><br /> 秒の小数部分が切り捨てられます<br /><br /> 数値の切り捨ての全体の一部|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|数値の切り捨ての全体の一部|未定義。|未定義。|22015|  
  
 [a] の値*BufferLength*この変換は無視されます。 ドライバーでのサイズ **TargetValuePtr* C データ型のサイズです。  
  
 [b] これは、対応する C データ型のサイズです。  
  
 [c] この変換は、真数データ型 (SQL_DECIMAL、SQL_NUMERIC、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、および SQL_BIGINT) のみサポートされます。 (SQL_REAL、使用できます、または SQL_DOUBLE) のおおよその数値データ型はサポートされません。  

## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC と SQLSetDescField

 [SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)SQL_C_NUMERIC 値で手動のバインディングを実行するが必要です。 (SQLSetDescField が ODBC 3.0 で追加されたことに注意してください)。手動バインドを実行するには、まず記述子ハンドルを取得する必要があります。  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
