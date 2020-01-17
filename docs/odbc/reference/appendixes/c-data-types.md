---
title: C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fe4383e397c0fd06197be2ff25e6dbb876f6c0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037771"
---
# <a name="c-data-types"></a>C データ型
ODBC C データ型は、アプリケーションでデータの格納に使用される C バッファーのデータ型を示します。  
  
 すべてのドライバーでは、すべての C データ型をサポートする必要があります。 これが必要なすべてのドライバーをサポートする SQL 型を変換できる、すべての C 型をサポートする必要があり、すべてのドライバーが SQL 型に少なくとも 1 つの文字をサポートします。 C のすべての型と文字 SQL 型を変換できる、ために、すべてのドライバーはすべての C 型をサポートする必要があります。  
  
 C データ型がで指定された、 **SQLBindCol**と**SQLGetData**関数、 *TargetType*引数および、 **SQLBindParameter**関数と、 *ValueType*引数。 呼び出すことによって指定することも**SQLSetDescField** ARD または、APD のまたは呼び出すことによって、SQL_DESC_CONCISE_TYPE フィールドを設定する**SQLSetDescRec**で、*型*引数 (および*サブタイプ*引数が必要な場合)、 *DescriptorHandle*引数 ARD または APD のハンドルに設定します。  
  
 次の表は、C のデータ型の有効な型の識別子を一覧表示します。 また、テーブルには、各識別子とこのデータ型の定義に対応する ODBC C データ型が一覧表示します。  
  
|C 型識別子|ODBC C の typedef|C 型|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT|符号なし short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|符号なし long int|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE、SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_ _int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|符号なし _ _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK[i]|ブックマーク|unsigned long int[d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|すべての C interval データ型|SQL_INTERVAL_STRUCT|参照してください、 [C Interval 構造体](../../../odbc/reference/appendixes/c-interval-structure.md)セクションで、この付録の「します。|  
  
 **C 型識別子**SQL_C_TYPE_DATE [c]  
  
 **ODBC C の typedef** SQL_DATE_STRUCT  
  
 **C 型**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 型識別子**SQL_C_TYPE_TIME [c]  
  
 **ODBC C の typedef** SQL_TIME_STRUCT  
  
 **C 型**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 型識別子**SQL_C_TYPE_TIMESTAMP [c]  
  
 **ODBC C の typedef** SQL_TIMESTAMP_STRUCT  
  
 **C 型**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **C 型識別子**SQL_C_NUMERIC  
  
 **ODBC C の typedef** SQL_NUMERIC_STRUCT  
  
 **C 型**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C 型識別子**SQL_C_GUID  
  
 **ODBC C の typedef** SQLGUID  
  
 **C 型**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 年、月、日、時間、分、および C の datetime データ型の 2 つ目のフィールドの値はグレゴリオ暦の制約に従う必要があります。 (を参照してください[グレゴリオ暦の制約](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)後の「します。)  
  
 [b] 小数フィールドの値では、2 つ目の範囲は 0 ~ 999,999,999 (1 10億より小さい) 10億の数です。 たとえば、0.5 秒の小数フィールドの値には 1 秒あたりの 1/10,000 の 500,000,000 (1 ミリ秒) は、1,000,000、分の 1 秒の (1 つのマイクロ秒) が 1,000、ありの 10億分の 1 秒 (1 ナノ秒) は 1 です。  
  
 [c] で、ODBC 2。*x*C の日付、時刻、タイムスタンプ データ型は、SQL_C_DATE、SQL_C_TIME、SQL_C_TIMESTAMP します。  
  
 [d] は、ODBC 3 *.x*アプリケーション SQL_C_VARBOOKMARK、SQL_C_BOOKMARK いないを使用する必要があります。 ときに、ODBC 3 *.x*アプリケーションは、ODBC 2 で動作します *。x*ドライバー、ODBC 3 *.x*ドライバー マネージャーが SQL_C_VARBOOKMARK を SQL_C_BOOKMARK にマップされます。  
  
 [e] A 数が格納されている、 *val*リトル エンディアン モード (最下位バイトをされている最も左にあるバイト) でのスケールを整数としての SQL_NUMERIC_STRUCT 構造体のフィールド。 たとえば、第 4 の小数点以下桁数で数値を 10.001 の底 10 で 100010 の整数にスケーリングします。 186AA を 16 進形式ではこのための SQL_NUMERIC_STRUCT での値となります"AA 86 01 00 00. です。00"、SQL_MAX_NUMERIC_LEN によって定義されたバイト数で **#define**します。  
  
 詳細については**SQL_NUMERIC_STRUCT**を参照してください[HOWTO:SQL_NUMERIC_STRUCT で数値データを取得する](retrieve-numeric-data-sql-numeric-struct-kb222831.md)します。  
  
 [SQL_C_NUMERIC データの f] で、有効桁数と小数点フィールドでは、アプリケーションからの入力と、アプリケーション、ドライバーからの出力が使われるを入力します。 ドライバーでは、数値の値を書き込む、SQL_NUMERIC_STRUCT に、独自ドライバー固有の既定の値として使用されます、*精度*フィールド、およびそのアプリケーションの記述子 (の SQL_DESC_SCALE フィールドに、値が使用されます既定では 0) の*スケール*フィールド。 アプリケーションは、アプリケーションの記述子の SQL_DESC_PRECISION および SQL_DESC_SCALE のフィールドを設定して、有効桁数と小数点の独自の値を指定できます。  
  
 [g] で、サインイン フィールドが 1 の正数の場合、負の場合は 0。  
  
 [一部のコンパイラで、h] _ _int64 を提供されない可能性があります。  
  
 [ODBC 3 _SQL_C_BOOKMARK i] が非推奨とされました *.x*します。  
  
 [j] _SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT に置換された ODBC の符号付きと符号なし型。SQL_C_SSHORT、SQL_C_USHORT、SQL_C_SLONG、SQL_C_ULONG と SQL_C_STINYINT および SQL_C_UTINYINT。 ODBC 3 *.x* ODBC 2 で動作するドライバー *。x*アプリケーションから呼び出されると、ドライバー マネージャーに渡すためのドライバー、SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT をサポートする必要があります。  
  
 [k] SQL_C_GUID SQL_CHAR または SQL_WCHAR にのみ変換できます。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [64 ビットの整数の構造](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>関連項目  
 [ODBC の C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
