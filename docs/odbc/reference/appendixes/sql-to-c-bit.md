---
title: 'SQL から C へ: ビット |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d00a3c26d842b196e20861da6d8ae3e818d4cbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056903"
---
# <a name="sql-to-c-bit"></a>SQL から C へ: ビット
ODBC SQL データ型がビットの識別子。  
  
 SQL_BIT  
  
 次の表は、ODBC C データ型のビットの SQL データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* < = 1|data<br /><br /> 未定義。|1<br /><br /> 未定義。|n/a<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|[A] [なし]|data|C データ型のサイズ|n/a|  
|SQL_C_BIT|[A] [なし]|data|1 [b]|n/a|  
|SQL_C_BINARY|*BufferLength* > = 1<br /><br /> *BufferLength* < 1|data<br /><br /> 未定義。|1<br /><br /> 未定義。|n/a<br /><br /> 22003|  
  
 [a] の値*BufferLength*この変換は無視されます。 ドライバーでのサイズ **TargetValuePtr* C データ型のサイズです。  
  
 [b] これは、対応する C データ型のサイズです。  
  
 ビットの SQL のデータが文字データに変換されると、使用可能な値は「0」および「1」です。
