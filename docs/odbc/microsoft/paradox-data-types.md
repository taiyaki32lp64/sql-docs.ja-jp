---
title: Paradox データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8478e80ae2ebd19a3e0f2aa8307e0985b2c092d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043689"
---
# <a name="paradox-data-types"></a>Paradox データ型
ODBC Paradox ドライバーは、Paradox データ型を ODBC SQL データ型にマップします。 次の表では、すべて Paradox データ型の一覧し、ODBC SQL データの型にマップされますを示しています。  
  
|Paradox データ型|ODBC データ型|  
|-----------------------|--------------------|  
|英数字|SQL_VARCHAR|  
|[自動増分] [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|バイト [1]|SQL_BINARY|  
|[DATE]|SQL_DATE|  
|イメージ [2]|SQL_LONGVARBINARY|  
|論理 [1]|SQL_BIT|  
|時間の長い [1]|SQL_INTEGER|  
|[2] のメモ|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|時間 [1]|SQL_TIMESTAMP|  
|[1] のタイムスタンプ|SQL_TIMESTAMP|  
  
 Paradox バージョン 5 には [1] 有効です。*x*します。  
  
 Paradox バージョン 4 に対してのみ有効なを [2]。*x* 5 *。x*します。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL データ型を返します。 付録 d のすべての変換、 *ODBC プログラマ リファレンス*このトピックで前述した ODBC SQL データ型はサポートされます。  
  
 次の表では、Paradox データ型の制限事項を示します。  
  
|データの種類|説明|  
|---------------|-----------------|  
|英数字|0 の英数字の列を作成または指定されていない長さが実際には 255 バイト列を返します。|  
|BYTES|Paradox5 ドライバーとバイナリ列に NULL を挿入する場合は、0 に変更されます。|  
|LONG|Paradox 5 で長い形式のデータ型の Paradox ドライバーでサポートされている負の値の最大値。*x*は-2 ^31 (-2147483648)、ODBC データに長いマップ以降が必要です、入力 SQL_INTEGER します。 時間の長いのサポートされる最大の負の値が実際には-2 ^31 + 1 (-2147483647)。|  
|timestamp|値は、Paradox ドライバーによって TIMESTAMP 列に挿入し、列から取得した後、取得した値によって異なる場合が挿入された値から 1 秒程度切り捨てられるためです。|  
  
 データ型の複数の制限事項が記載[データ型の制限事項](../../odbc/microsoft/data-type-limitations.md)します。
