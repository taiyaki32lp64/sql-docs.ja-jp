---
title: SQL C データ変換の例から |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84161501d3d705ef60559340502ee702e7c28437
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056890"
---
# <a name="sql-to-c-data-conversion-examples"></a>SQL から C へのデータ変換の例

次の表に示した例では、ドライバーが SQL のデータを C データに変換する方法を示します。  
  
|SQL 型<br /><br /> identifier|SQL data<br /><br /> value|C 型<br /><br /> identifier|バッファー<br /><br /> 長さ|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|n/a|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|[a] 1234.56\0|n/a|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|[a] 1234\0|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|無視|1234.56|n/a|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|無視|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|無視|----|22003|  
|SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|無視|1.2345678|n/a|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|無視|1.234567|n/a|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|無視|1|n/a|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31\0 [a]|n/a|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|無視|1992,12,31、0,0,0,0 [b]|n/a|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|[a] 1992-12-31 23:45:55.12\0|n/a|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|[a] 1992-12-31 23:45:55.1\0|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a]「\0」は、null 終了バイトを表します。 ドライバー常に null で終端します SQL_C_CHAR データ。  
  
 [この一覧に b] の数値は、TIMESTAMP_STRUCT 構造体のフィールドに格納されている番号です。
