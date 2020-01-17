---
title: 日付、時刻、およびタイムスタンプのリテラル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6191995c9d1c488fc5af056248ba39dd3eb4607
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076981"
---
# <a name="date-time-and-timestamp-literals"></a>日付、時刻、およびタイムスタンプのリテラル
日付、時刻、およびタイムスタンプのリテラルのエスケープ シーケンスは、します。  
  
 **{** _-型_ **'** _値_ **'}**  
  
 場所*リテラル型*は、値の 1 つは、次の表に表示されています。  
  
|*リテラル型*|説明|書式設定*値*|  
|---------------------|-------------|-----------------------|  
|**d**|date|*yyyy*-*mm*-*dd*|  
|**t**|Time*|*hh*:*mm*:*ss*[1]|  
|**ts**|Timestamp|*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.*f.* ] [1]|  
  
 [秒コンポーネントを含むリテラル、時刻、またはタイムスタンプ間隔で小数点の右側にある数字の 1] の番号は SQL_DESC_PRECISION の記述子フィールドに含まれる秒の有効桁数に依存します。 (詳細については、次を参照してください[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)。  
  
 詳細については、日付、時刻、およびタイムスタンプ エスケープ シーケンスは、次を参照してください[日付、時刻、およびタイムスタンプ エスケープ シーケンス](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)付録 c:。SQL 文法。  
  
 たとえば、次の SQL ステートメントの両方、Orders テーブルの販売注文 1023 の開いている日付を更新します。 最初のステートメントでは、エスケープ シーケンスの構文を使用します。 2 番目のステートメントでは、日付列の Oracle Rdb ネイティブ構文を使用して、相互運用可能ではありません。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日付、時刻、またはタイムスタンプのリテラルのエスケープ シーケンスは、日付、時刻、またはタイムスタンプ パラメーターにバインドされている文字変数にも配置できます。 たとえば、次のコードでは、文字変数にバインドされている日付パラメーターを使用して、Orders テーブルの販売注文 1023 の開いている日付を更新します。  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 ただし、日付構造体に直接、パラメーターをバインドする方が効率的です。  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 アプリケーションを呼び出すドライバーが、日付、時刻、またはタイムスタンプのリテラルの ODBC エスケープ シーケンスをサポートするかどうかを判断する**SQLGetTypeInfo**します。 データ ソースは、日付、時刻、またはタイムスタンプのデータ型をサポートする場合、対応するエスケープ シーケンスもサポートする必要があります。  
  
 データ ソースには、日付、時刻、またはタイムスタンプのリテラルの ODBC エスケープ シーケンスは、異なるは、ANSI sql-92 仕様で定義されている datetime リテラルもサポートできます。 データ ソースが ANSI リテラルをサポートしているかどうかを決定するには、アプリケーションを呼び出す**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS オプションを使用します。  
  
 アプリケーションを呼び出すドライバーが interval のリテラルの ODBC エスケープ シーケンスをサポートするかどうかを判断する**SQLGetTypeInfo**します。 データ ソースは、datetime 間隔のデータ型をサポートする場合、対応するエスケープ シーケンスもサポートする必要があります。  
  
 データ ソースは、ANSI sql-92 仕様で定義されている datetime interval のリテラルの ODBC エスケープ シーケンスとは異なる日付時刻リテラルもサポートできます。 データ ソースが ANSI リテラルをサポートしているかどうかを決定するには、アプリケーションを呼び出す**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS オプションを使用します。
