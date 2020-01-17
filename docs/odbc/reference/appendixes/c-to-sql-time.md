---
title: 'C から SQL へ: 時間 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4a3734ff8d9f0cb120e1d33433ee3a301bb59ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019303"
---
# <a name="c-to-sql-time"></a>C から SQL へ: Time
時間の ODBC C データ型の識別子を示します。  
  
 SQL_C_TYPE_TIME  
  
 次の表は、ODBC SQL データ型が time C のデータを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)します。  
  
|SQL 型識別子|テスト|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列のバイト長 > = 8<br /><br /> 列のバイトの長さ < 8<br /><br /> データの値が有効な時刻|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列の文字の長さ > = 8<br /><br /> 列の文字の長さ < 8<br /><br /> データの値が有効な時刻|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|データの値が有効な時刻<br /><br /> データの値が有効な時刻|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|データの値が有効な時刻 [a]<br /><br /> データの値が有効な時刻|n/a<br /><br /> 22007|  
  
 [a] 日付、タイムスタンプの部分が現在の日付とタイムスタンプの部分が 0 に設定されている秒の小数部を設定します。  
  
 SQL_C_TYPE_TIME 構造で有効な値については、次を参照してください。 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)、この付録で以前のバージョン。  
  
 C の時刻のデータは SQL データの文字に変換するときに、結果の文字データは、"*hh*:*mm*:*ss*"形式です。  
  
 ドライバーは、C データ型で、データ バッファーのサイズが時間の C データ型のサイズであると仮定の時刻からデータを変換するときに長さ/インジケーター値を無視します。 長さまたはインジケーターの値が渡さ、 *StrLen_or_Ind*引数**SQLPutData**とで指定したバッファー、 *StrLen_or_IndPtr* 引数**SQLBindParameter**します。 データ バッファーを指定した、 *DataPtr*引数**SQLPutData**と*ParameterValuePtr*引数**SQLBindParameter**.
