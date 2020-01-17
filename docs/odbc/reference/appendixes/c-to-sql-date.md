---
title: 'C から SQL へ: 日付 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02ee7c1fb396dc1c9c0708cf6c0e7a52ff1c11ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019410"
---
# <a name="c-to-sql-date"></a>C から SQL へ: date
日付の ODBC C データ型の識別子を示します。  
  
 SQL_C_TYPE_DATE  
  
 次の表は、ODBC SQL データ型の C データの日付を変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列のバイト長 > = 10<br /><br /> 列のバイトの長さ < 10<br /><br /> データの値が有効な日付|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列の文字の長さ > = 10<br /><br /> 列の文字の長さ < 10<br /><br /> データの値が有効な日付|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|データの値が有効な日付<br /><br /> データの値が有効な日付|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|データの値が有効な日付 [a]<br /><br /> データの値が有効な日付|n/a<br /><br /> 22007|  
  
 [a] タイムスタンプの時刻部分が 0 に設定されます。  
  
 SQL_C_TYPE_DATE 構造で有効な値については、次を参照してください。 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)、この付録で以前のバージョン。  
  
 C 日付データは、SQL データの文字に変換するときに、結果の文字データは、"*yyyy*-*mm*-*dd*"形式です。  
  
 ドライバーは、日付 C データ型からデータを変換するときに長さ/インジケーター値を無視し、データ バッファーのサイズが、日付の C データ型のサイズであると仮定します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.
