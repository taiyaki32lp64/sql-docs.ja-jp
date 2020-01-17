---
title: SQL への準拠レベル (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 241f4f3da12f63c15d917a0e47cb13ad0e96e6e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063355"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL への準拠レベル (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 ODBC Driver for Oracle では、Minimum SQL 文法と Core SQL 文法をサポートしているしも SQL を次の ODBC 拡張機能をサポートします。  
  
-   日付、時刻、タイムスタンプ データ  
  
-   左と右外部結合  
  
-   数値関数:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |ceiling|log10|second|truncate|  
    |Cos|Mod|sign||  
    |Exp|Pi|sin||  
    |floor|Power|sqrt||  
  
-   日付関数:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|now|year|  
    |Dayofmonth|Month|quarter||  
  
-   文字列関数。  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|right|Ucase|  
    |Char|Length|rtrim||  
    |Concat|Ltrim|Soundex||  
    |Lcase|Replace|substring||  
  
-   型変換関数。  
  
    ||  
    |-|  
    |Convert|  
  
-   システム関数:  
  
    ||  
    |-|  
    |Ifnull|  
    |User|
