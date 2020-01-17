---
title: リテラル プレフィックスおよびサフィックス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56ee50071f622c114bd6d8d04444e78c0fb69d67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915561"
---
# <a name="literal-prefixes-and-suffixes"></a>リテラル プレフィックスおよびサフィックス
SQL ステートメントで、*リテラル*は文字の実際のデータ値を表したものです。 たとえば、次のステートメントで ABC、FFFF、および 10 はリテラルです。  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 一部のデータ型のリテラルは、特別なプレフィックスとサフィックスが必要です。 前の例では、文字リテラル (ABC) では、プレフィックスとサフィックスの両方として単一引用符 (') が必要です、バイナリ リテラル (FFFF) には、0 x プレフィックス、および整数リテラル (10) としてからプレフィックスが必要またはサフィックスが付いていない文字が必要があります。  
  
 日付、時刻、およびタイムスタンプを除くすべてのデータ型の相互運用可能なアプリケーションが LITERAL_PREFIX と LITERAL_SUFFIX によって作成された結果セット列に返される値を使用する必要があります**SQLGetTypeInfo**します。 日付、時刻、タイムスタンプ、および datetime interval のリテラルの相互運用可能なアプリケーションは、前のセクションで説明されているエスケープ シーケンスを使用してください。
