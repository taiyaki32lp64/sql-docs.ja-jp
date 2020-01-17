---
title: 'SQL から C へ: バイナリ |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280afb03eeac46a58943d276137e2019340a0a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057002"
---
# <a name="sql-to-c-binary"></a>SQL から C へ: Binary
バイナリの ODBC SQL データ型の識別子は次のとおりです。  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 次の表は、ODBC C データ型がバイナリの SQL データを変換する可能性がありますを示します。 列とテーブルの用語の詳細については、次を参照してください。 [SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)します。  
  
|C 型識別子|テスト|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(データのバイト長)\* 2 < *BufferLength*<br /><br /> (データのバイト長)\* 2 > = *BufferLength*|data<br /><br /> 切り捨てられたデータ|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|(データの文字長)\* 2 < *BufferLength*<br /><br /> (データの文字長)\* 2 > = *BufferLength*|data<br /><br /> 切り捨てられたデータ|データの文字の長さ<br /><br /> データの文字の長さ|n/a<br /><br /> 01004|  
|SQL_C_BINARY|データのバイト長 < = *BufferLength*<br /><br /> データのバイト長 > *BufferLength*|データ<br /><br /> 切り捨てられたデータ|バイト単位でデータの長さ<br /><br /> バイト単位でデータの長さ|n/a<br /><br /> 01004|  
  
 SQL のバイナリ データが文字データに変換されると、ソース データの各バイト (8 ビット) は 2 つの ASCII 文字として表されます。 これらの文字は、16 進数形式で番号の ASCII 文字の表現です。 たとえば、バイナリ 00000001 は「01」に変換され、バイナリで 11111111 は、"FF"に変換されます。  
  
 常に、ドライバーは、個々 のバイトを 16 進数のペアに変換し、null バイトの文字の文字列を終了します。 このため場合、 *BufferLength*が偶数で、変換後のデータの最後のバイトの長さより小さい、**TargetValuePtr*バッファーは使用されません。 (変換後のデータには、偶数のバイト数が必要です、[次へ]、最後のバイトが null バイト、および最後のバイトを使用することはできません。)  
  
> [!NOTE]  
>  アプリケーション開発者は、文字の C データ型にバインド バイナリ SQL データから推奨されません。 この変換は、通常非効率的で低速です。
