---
title: 64 ビット整数の構造 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d9e6fd01d6b9ef98ebb10f6728ec4ba205fbb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996259"
---
# <a name="64-bit-integer-structures"></a>64 ビットの整数の構造
Microsoft C コンパイラで SQL_C_SBIGINT、SQL_C_UBIGINT データ型識別子の C 型は、_ _int64 です。 Microsoft® C コンパイラよりも他のコンパイラを使用する場合は、C 型が異なる可能性があります。 コンパイラは、ネイティブ 64 ビット整数をサポートする場合、ドライバーまたはアプリケーションはネイティブの 64 ビット整数型である ODBCINT64 を定義する必要があります。 コンパイラで 64 ビット整数がネイティブでサポートされていない場合、アプリケーションやドライバーはこのデータにアクセスすることができるように、次の構造を定義できます。  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 これらの構造は、64 ビット整数を 8 バイト境界に配置するため、8 バイト境界にアライン必要があります。
