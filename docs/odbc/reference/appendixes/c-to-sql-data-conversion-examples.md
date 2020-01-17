---
title: C SQL データ変換の例から |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e475abb699c7fa7240ca6eb39b1b32f1730d33c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125735"
---
# <a name="c-to-sql-data-conversion-examples"></a>C から SQL へのデータ変換の例
次の例では、ドライバーに SQL データを C データを変換する方法を示します。  
  
|C 型識別子|C のデータ値|SQL 型<br /><br /> identifier|[列]<br /><br /> 長さ|SQL data<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|n/a|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|[a] 1234.56\0|SQL_DECIMAL|8 [b]|1234.56|n/a|  
|SQL_C_CHAR|[a] 1234.56\0|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|[a] 1234.56\0|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/a|1234.56|n/a|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/a|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/a|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|n/a|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|n/a|1992-12-31 00:00:00.0|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、23,45,55、120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、23,45,55、120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、23,45,55、120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a]「\0」は、null 終了バイトを表します。 データの長さが SQL_NTS である場合にのみ、null 終端バイトが必要です。  
  
 [b] に加えバイトの数字、1 バイトは、記号の必要であり、もう 1 つのバイトは、10 進数のポイントに必要です。  
  
 [この一覧で c] の数値は、SQL_DATE_STRUCT 構造体のフィールドに格納されている番号です。  
  
 [この一覧に d] で、数値は、SQL_TIMESTAMP_STRUCT 構造体のフィールドに格納されている番号です。
