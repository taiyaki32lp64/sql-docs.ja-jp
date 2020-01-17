---
title: 'C から SQL へ: Numeric |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6dc440e27b362fef9c9794cf0005c6af0b435efc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019313"
---
# <a name="c-to-sql-numeric"></a>C から SQL へ: 数値
数値の ODBC C データ型の識別子は次のとおりです。  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 次の表は、ODBC SQL データ型が数値の C データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|桁数 < = バイト長の列<br /><br /> 数字の数 > バイト長の列|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|文字の数 < = 列の文字の長さ<br /><br /> 文字の数 > 列の文字の長さ|n/a<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|データの切り捨てなしの変換またはを使用する桁の小数部の切り捨て<br /><br /> 整数の桁に切り捨てに変換されたデータ|n/a<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|データが数の変換先のデータ型の範囲内<br /><br /> データが数の変換先のデータ型の範囲外です。|n/a<br /><br /> 22003|  
|SQL_BIT|データが 0 または 1 です。<br /><br /> データが 2 よりも小さいと 1 に等しく、0 より大きい<br /><br /> データが 0 未満またはより大きい、または 2 と等しい|n/a<br /><br /> 22001<br /><br /> 22003|  
|[A] SQL_INTERVAL_YEAR<br /><br /> [A] SQL_INTERVAL_MONTH<br /><br /> [A] SQL_INTERVAL_DAY<br /><br /> [A] SQL_INTERVAL_HOUR<br /><br /> [A] SQL_INTERVAL_MINUTE<br /><br /> [A] SQL_INTERVAL_SECOND|データは切り捨てられません。<br /><br /> データが切り捨てられました。|n/a<br /><br /> 22015|  
  
 [a] (SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_SSHORT、SQL_C_USHORT、SQL_C_SLONG、SQL_C_ULONG、または SQL_C_NUMERIC) 真数データ型に対してのみこれらの変換がサポートされています。 (SQL_C_FLOAT または SQL_C_DOUBLE) のおおよその数値データ型はサポートされません。 正確な数値の C データ型は、間隔間隔有効桁数は 1 つのフィールドがありません。 SQL 型に変換できません。  
  
 [b]"n/a"の場合も、ドライバーが必要に応じてを返す SQL_SUCCESS_WITH_INFO と 01S07 小数部の切り捨てがある場合です。  
  
 ドライバーでは、数値の C データ型からデータを変換するとき長さ/インジケーター値を無視し、データ バッファーのサイズが数値の C データ型のサイズであると仮定します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.
