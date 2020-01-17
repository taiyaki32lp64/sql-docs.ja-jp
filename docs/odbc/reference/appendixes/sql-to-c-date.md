---
title: 'SQL から C へ: 日付 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d282798a31ac9059ed3c1901ea01f1f3104f09c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056885"
---
# <a name="sql-to-c-date"></a>SQL から C へ: date
ODBC SQL データ型が日付の識別子。  
  
 SQL_TYPE_DATE  
  
 次の表は、ODBC C データ型の SQL データの日付を変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > バイト長の文字<br /><br /> 11 < = *BufferLength* < = バイト長の文字<br /><br /> *BufferLength* < 11|data<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|10<br /><br /> バイト単位でデータの長さ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 文字長<br /><br /> 11 < = *BufferLength* < = 文字の長さ<br /><br /> *BufferLength* < 11|data<br /><br /> 切り捨てられたデータ<br /><br /> 未定義。|10<br /><br /> データの文字の長さ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|データのバイト長 < = *BufferLength*<br /><br /> データのバイト長 > *BufferLength*|データ<br /><br /> 未定義。|バイト単位でデータの長さ<br /><br /> 未定義。|n/a<br /><br /> 22003|  
|SQL_C_TYPE_DATE|[A] [なし]|data|6 [c]|n/a|  
|SQL_C_TYPE_TIMESTAMP|[A] [なし]|データ [b]|16 [c]|n/a|  
  
 [a] の値*BufferLength*この変換は無視されます。 ドライバーでのサイズ **TargetValuePtr* C データ型のサイズです。  
  
 [b] の時刻のタイムスタンプの構造体のフィールドは、0 に設定されます。  
  
 [c] これは、対応する C データ型のサイズです。  
  
 SQL データの日付が文字データに変換されると、結果の文字列は、"*yyyy*-*mm*-*dd*"形式です。 この形式は、Windows® 国設定の影響を受けません。
