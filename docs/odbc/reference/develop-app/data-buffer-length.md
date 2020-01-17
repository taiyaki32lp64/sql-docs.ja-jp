---
title: データ バッファーの長さ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40fe9d23f14d4a7af80fe31a418cccf7133b7252
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067417"
---
# <a name="data-buffer-length"></a>データ バッファーの長さ
アプリケーションでは、データ バッファーのバイトの長さを渡すという名前を引数にドライバー *BufferLength*または類似する名前。 たとえば、以下でを呼び出す**SQLBindCol**、アプリケーションがの長さを指定します、 *ValuePtr*バッファー (**sizeof (***ValuePtr***)** ):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 ドライバーは、関数には、出力文字列引数のバッファー長の引数で、文字の数ではなく、バイト数を常に返します。  
  
 データ バッファーの長さが出力バッファーにのみ必要ドライバーでは、バッファーの末尾を越えて書き込みを回避するために、それらを使用します。 ただし、バッファーに文字またはバイナリ データなどの可変長データが含まれている場合にのみ、ドライバーは、データ バッファーの長さを確認します。 バッファーには、整数や日付構造体などの固定長データが含まれている場合、ドライバーはデータ バッファーの長さは無視され、バッファーには、データを保持するために十分な大きさが前提としています。つまり、固定長のデータを切り捨てますことはありません。 したがって、固定長のデータを十分な大きさのバッファーを割り当て、アプリケーションにとって重要です。  
  
 以外のデータの切り捨てが文字列を出力するときに発生します (など、カーソル名が返されます。 **SQLGetCursorName**)、バッファー長の引数で返される長さは、可能な最大文字数。  
  
 ドライバーがこれらのバッファーに書き込まれませんので、データ バッファーの長さは入力バッファーに必要ではありません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [長さまたはインジケーターの値を使用してください。](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [データの長さ、バッファー長、および切り捨て](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [文字データと C 文字列](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
