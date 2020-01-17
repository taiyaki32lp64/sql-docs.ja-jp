---
title: 'SQL から C へ: 文字 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a649e1ec27261551b7a64e09310ce99b6140a15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056919"
---
# <a name="sql-to-c-character"></a>SQL から C へ: 文字

識別子の文字の ODBC SQL データ型に次のとおりです。

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

次の表は、ODBC C データ型の SQL データの文字が変換される可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。  

|C 型識別子|テスト|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|データのバイト長 < *BufferLength*<br /><br /> データのバイト長の > = *BufferLength*|データ<br /><br /> 切り捨てられたデータ|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|データの長さを文字 < *BufferLength*<br /><br /> データの文字長 > = *BufferLength*|データ<br /><br /> 切り捨てられたデータ|データの文字の長さ<br /><br /> データの文字の長さ|n/a<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|[B] を切り捨てることがなく変換されたデータ<br /><br /> データを変換する小数部の桁数が [a] の切り捨て<br /><br /> データの変換が [a] (ではなく小数部) の整数桁の損失になります<br /><br /> データは、*数値リテラル*[b]。|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。<br /><br /> 未定義。|C データ型のバイト数<br /><br /> C データ型のバイト数<br /><br /> 未定義。<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|データは、数の変換先のデータ型の範囲内で、[a]<br /><br /> データが数の変換先のデータ型の範囲外 [a]<br /><br /> データは、*数値リテラル*[b]。|データ<br /><br /> 未定義。<br /><br /> 未定義。|C データ型のサイズ<br /><br /> 未定義。<br /><br /> 未定義。|n/a<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|データが 0 または 1 です。<br /><br /> データが 2 よりも小さいと 1 に等しく、0 より大きい<br /><br /> データが 0 未満またはより大きい、または 2 と等しい<br /><br /> データは、*数値リテラル*|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。<br /><br /> 未定義。|1 [b]<br /><br /> 1 [b]<br /><br /> 未定義。<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|データのバイト長 < = *BufferLength*<br /><br /> データのバイト長 > *BufferLength*|データ<br /><br /> 切り捨てられたデータ|バイト単位でデータの長さ<br /><br /> データの長さ|n/a<br /><br /> 01004|  
|SQL_C_TYPE_DATE|データの値が有効な*日付値*[a]<br /><br /> データの値が有効な*タイムスタンプ値*時刻部分が 0 [a]。<br /><br /> データの値が有効な*タイムスタンプ値*時刻部分が 0 以外の場合 [a] [c]。<br /><br /> データの値が有効な*日付値*または*タイムスタンプ値*[a]|データ<br /><br /> データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定義。|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|データの値が有効な*時刻値と値は 0 秒の小数部*[a]<br /><br /> データの値が有効な*タイムスタンプ値または有効な時刻値*; 小数秒の部分が 0 [a]、[d]<br /><br /> データの値が有効な*タイムスタンプ値*; 小数秒の部分が 0 以外の場合 [a]、[d] [e]<br /><br /> データの値が有効な*時刻値*または*タイムスタンプ値*[a]|データ<br /><br /> データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定義。|n/a<br /><br /> n/a<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|データの値が有効な*タイムスタンプ値または有効な時刻値*; 小数秒の部分を切り捨てることができません [a]<br /><br /> データの値が有効な*タイムスタンプ値または有効な時刻値*; 小数秒の部分を切り捨てる [a]<br /><br /> データの値が有効な*日付値*[a]<br /><br /> データの値が有効な*時刻値*[a]<br /><br /> データの値が有効な*日付値*、*時刻値*、または*タイムスタンプ値*[a]|データ<br /><br /> 切り捨てられたデータ<br /><br /> データ [f]<br /><br /> データ [g]<br /><br /> 未定義。|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> n/a<br /><br /> n/a<br /><br /> 22018|  
|すべての C interval 型|データの値が有効な*間隔値*; 損失はありません。<br /><br /> データの値が有効な*間隔値*; 後続のフィールドを 1 つまたは複数の切り捨て<br /><br /> データが有効な間隔です。先頭のフィールドの大きな有効桁数が失われる<br /><br /> データの値が有効な間隔の値|データ<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。<br /><br /> 未定義。|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ<br /><br /> 未定義。<br /><br /> 未定義。|n/a<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] の値*BufferLength*この変換は無視されます。 ドライバーでのサイズ **TargetValuePtr* C データ型のサイズです。  
  
 [b] これは、対応する C データ型のサイズです。  
  
 [c] の時刻部分、*タイムスタンプ値*は切り捨てられます。  
  
 [d] の日付部分、*タイムスタンプ値*は無視されます。  
  
 [電子メール]、タイムスタンプの秒の小数部の部分は切り捨てられます。  
  
 [f] の時刻のタイムスタンプの構造体のフィールドは、0 に設定されます。  
  
 [g] タイムスタンプの構造体の日付フィールドは、現在の日付に設定されます。  

**余分なスペース**

SQL 文字データは、次の種類のいずれかに変換する場合、先頭と末尾のスペースは無視されます。

- 日付
- NUMERIC
- time
- TIMESTAMP
- データ間隔 C
