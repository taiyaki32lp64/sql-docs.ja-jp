---
title: 'SQL から C へ: 時間 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99f8219ef53f72b0d7ab1477bba5d24d441a3141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065079"
---
# <a name="sql-to-c-time"></a>SQL から C へ: Time
ODBC SQL データ型が時間の識別子。  
  
 SQL_TYPE_TIME  
  
 次の表は、ODBC C データ型が time の SQL データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > バイト長の文字<br /><br /> *9* <= *BufferLength* < = バイト長の文字<br /><br /> *BufferLength* < 9|data<br /><br /> [A] 切り捨てられたデータ<br /><br /> 未定義。|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 文字長<br /><br /> *9* <= *BufferLength* < = 文字の長さ<br /><br /> *BufferLength* < 9|data<br /><br /> [A] 切り捨てられたデータ<br /><br /> 未定義。|データの文字の長さ<br /><br /> データの文字の長さ<br /><br /> 未定義。|n/a<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|データのバイト長 < = *BufferLength*<br /><br /> データのバイト長 > *BufferLength*|データ<br /><br /> 未定義。|バイト単位でデータの長さ<br /><br /> 未定義。|n/a<br /><br /> 22003|  
|SQL_C_TYPE_TIME|[なし] [b]|data|6 [d]|n/a|  
|SQL_C_TYPE_TIMESTAMP|[なし] [b]|データ [c]|16 [d]|n/a|  
  
 [a]、時間の秒の小数部が切り捨てられます。  
  
 [b] の値*BufferLength*この変換は無視されます。 ドライバーでのサイズ **TargetValuePtr* C データ型のサイズです。  
  
 [タイムスタンプの構造体の場合は、c]、日付フィールドは、現在の日付に設定され、タイムスタンプの構造体の秒の小数部のフィールドが 0 に設定されます。  
  
 [d] これは、対応する C データ型のサイズです。  
  
 SQL データの時間が文字データに変換されると、結果の文字列は、"*hh*:*mm*:*ss*"形式です。 この形式は、Windows® 国設定の影響を受けません。
