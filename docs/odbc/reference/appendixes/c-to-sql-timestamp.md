---
title: 'C から SQL へ: タイムスタンプ |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa75299f4d8e8f15293064d0bf3fb3979fe382d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037702"
---
# <a name="c-to-sql-timestamp"></a>C から SQL へ: Timestamp
Timestamp ODBC C データ型の識別子です。  
  
 SQL_C_TYPE_TIMESTAMP  
  
 次の表は、ODBC SQL データ型が C のタイムスタンプ データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列のバイト長 > バイト長の文字を =<br /><br /> 19 < = バイト長の列 < バイト長の文字<br /><br /> 列のバイトの長さ < 19<br /><br /> データの値が有効なタイムスタンプ|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列の文字の長さ > データの文字の長さを =<br /><br /> 19 < 列の文字の長さを = < データの文字長<br /><br /> 列の長さ < 19 文字します。<br /><br /> データの値が有効なタイムスタンプ|n/a<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|時刻フィールドは 0<br /><br /> 時刻フィールドは 0 以外の場合<br /><br /> データ値に有効な日付が含まれていません|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|秒の小数部のフィールドは 0 を [a]<br /><br /> 秒の小数部のフィールドは、0 以外の場合 [a]<br /><br /> データ値に有効な時刻が含まれていません|n/a<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|フィールドの秒の小数部が切り捨てられていません。<br /><br /> 秒の小数部のフィールドは切り捨てられます<br /><br /> データの値が有効なタイムスタンプ|n/a<br /><br /> 22008<br /><br /> 22007|  
  
 [a] の日付のタイムスタンプの構造体のフィールドは無視されます。  
  
 SQL_C_TIMESTAMP 構造で有効な値については、次を参照してください。 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)、この付録で以前のバージョン。  
  
 C のタイムスタンプ データは、SQL データの文字に変換するときに、結果の文字データは、"*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.*f.* ]"の形式。  
  
 ドライバーでは、タイムスタンプ C データ型からデータを変換するとき長さ/インジケーター値を無視し、データ バッファーのサイズがタイムスタンプ C データ型のサイズであると仮定します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.
