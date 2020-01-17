---
title: 列のサイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5639828c90141079ab66f6cceb466328ddb3f56d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019235"
---
# <a name="column-size"></a>列サイズ
数値データ型の列 (またはパラメーター) のサイズは、列またはパラメーターのデータ型またはデータの有効桁数で使用される最大桁数として定義されます。 文字型の場合、これは、データの文字の長さバイナリ データ型の列のサイズは、データの長さ (バイト単位) として定義されます。 時刻、タイムスタンプ、および間隔のすべてのデータ型の場合は、これは、このデータの文字表現の文字数です。 簡潔な SQL データ型ごとに定義されている列のサイズは、次の表に示します。  
  
|SQL 型識別子|列のサイズ|  
|-------------------------|-----------------|  
|すべての文字の種類 [a] [b]。|列またはパラメーター (と SQL_DESC_LENGTH の記述子フィールドに含まれる) の文字で定義されている、または最大列サイズ。 たとえば、char (10) として定義されている 1 バイト文字列の列のサイズには 10 です。|  
|SQL_DECIMAL SQL_NUMERIC|数字の定義済みの数。 たとえば、NUMERIC(10,3) として定義されている列の有効桁数には 10 です。|  
|SQL_BIT [c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (符号付き) の場合、または 20 (符号なし) の場合|  
|SQL_REAL [c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE [c]|15|  
|すべてバイナリ型 [a] [b]。|定義済みまたは最大長さ (バイト単位) の列またはパラメーター。 たとえば、binary (10) として定義されている列の長さには 10 です。|  
|SQL_TYPE_DATE[c]|10 (文字数、 *- yyyy-mm-dd*形式)。|  
|SQL_TYPE_TIME [c]|8 (文字数、 *hh mm ss*形式)、または 9 + *s* (文字数、 *hh:mm:ss*[.fff...] 形式では、場所*の*秒の有効桁数です)。|  
|SQL_TYPE_TIMESTAMP|16 (文字数、 *- yyyy-mm-dd hh:mm*形式)<br /><br /> 19 (文字数、 *- yyyy-mm-dd* *hh:mm:ss*形式)<br /><br /> または<br /><br /> 20 + *s* (文字数、 *- yyyy-mm-dd hh:mm:ss*[.fff...] 形式、場所*s*秒の有効桁数です)。|  
|SQL_INTERVAL_SECOND|場所*p*は先頭の有効桁数の間隔と*s*秒の有効桁数は、 *p* (場合*s*= 0) または*p* + *s*+1 (場合*s*> 0). [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|場所*p*は先頭の有効桁数の間隔と*s*は秒の有効桁数、9 +*p* (場合*s*= 0) または 10 +*p*+ *s* (場合*s*> 0). [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|場所*p*は先頭の有効桁数の間隔と*s*は秒の有効桁数を 6 +*p* (場合*s*= 0)、または 7 +*p* + *s* (場合*s*> 0). [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|場所*p*は先頭の有効桁数の間隔と*s*は秒の有効桁数を 3 +*p* (場合*s*= 0) または 4 +*p* + *s* (場合*s*> 0). [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*ここで、 *p*は先頭の有効桁数の間隔です [。d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*ここで、 *p*は先頭の有効桁数の間隔です [。d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*ここで、 *p*は先頭の有効桁数の間隔です [。d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*ここで、 *p*は先頭の有効桁数の間隔です [。d]|  
|SQL_GUID|36 (文字数、 *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*形式)|  
  
 [a] an ODBC 1.0 アプリケーション呼び出し**SQLSetParam** 、2.0 の ODBC ドライバーでは ODBC 2.0 アプリケーションの呼び出し元の**SQLBindParameter** 1.0 の ODBC ドライバーでは、ときに\* *StrLen_or_IndPtr* SQL_LONGVARCHAR または SQL_LONGVARBINARY 型の場合は、SQL_DATA_AT_EXEC *ColumnSize*送信される、有効桁数ではない次の表で定義されているデータの合計の長さを設定する必要があります。  
  
 [b] 場合は、変数の型の列またはパラメーターの長さを判断できないのは、ドライバー、SQL_NO_TOTAL が返されます。  
  
 [c]、 *ColumnSize*の引数**SQLBindParameter**はこのデータ型は無視されます。  
  
 [d] の interval データ型の列の長さに関する一般的な規則は、次を参照してください。 [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)、この付録で以前のバージョン。  
  
 列 (またはパラメーター) のサイズに対して返される値は、任意の 1 つの記述子フィールドの値に対応していません。 値は、次の表に示すように、SQL_DESC_PRECISION または SQL_DESC_LENGTH フィールドには、データの種類に応じてのいずれかから取得できます。  
  
|SQL 型|対応する記述子フィールド<br /><br /> 列またはパラメーターのサイズ|  
|--------------|--------------------------------------------------------------------|  
|すべての文字とバイナリ型|LENGTH|  
|すべての数値型|PRECISION|  
|すべての日付時刻と間隔の種類|LENGTH|  
|SQL_BIT|LENGTH|
