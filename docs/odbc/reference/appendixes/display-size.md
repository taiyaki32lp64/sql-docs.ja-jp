---
title: サイズの表示 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61afd5c9932f58c49e54b4aff8b053d0a25a6e3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130017"
---
# <a name="display-size"></a>表示サイズ
列の表示サイズは、文字形式でデータを表示するために必要な文字の最大数です。 次の表では、各 ODBC SQL データ型の表示サイズを定義します。  
  
|SQL 型識別子|ディスプレイ サイズ|  
|-------------------------|------------------|  
|すべての文字の種類 [a]|(固定型) に対して定義されているか (変数の型) の最大文字形式でデータを表示するために必要な文字数。|  
|SQL_DECIMAL SQL_NUMERIC|列と 2 の有効桁数 (記号、*精度*桁の数字と小数点 10 進数)。 たとえば、NUMERIC(10,3) として定義されている列の表示サイズには 12 です。|  
|SQL_BIT|1 (1 桁)。|  
|SQL_TINYINT|4 (記号、および 3 桁の数字) が署名されている場合、または 3 (3 桁) が署名されていない場合。|  
|SQL_SMALLINT|6 (記号、および 5 桁の数字) が署名されている場合、または 5 (5 桁の数字) が署名されていない場合。|  
|SQL_INTEGER|11 (記号、および 10 桁) に署名されている場合、または 10 (10 進数) が署名されていない場合。|  
|SQL_BIGINT|20 (符号と 19 桁署名されている場合、または署名されていない場合、20 桁)。|  
|SQL_REAL|14 (、記号、7 桁の数字、小数点 10 進数文字*E*、記号、および 2 桁の数字)。|  
|SQL_DOUBLE を使用できます。|24 (、記号、15 桁、小数点 10 進数文字*E*、記号、および 3 桁)。|  
|[A] すべてのバイナリ型|定義済みまたは (変数の型) の最大の列の長さが 2 を倍です。 (各バイナリ バイトは、2 桁の 16 進数で表される)。|  
|SQL_TYPE_DATE|10 (形式で日付 *- yyyy-mm-dd*)。|  
|SQL_TYPE_TIME|8 (形式の時刻*hh:mm:ss*)<br /><br /> または<br /><br /> 9 + *s* (形式の時刻*hh:mm:ss*[.fff...]、場所*s*秒の小数部の有効桁数です)。|  
|SQL_TYPE_TIMESTAMP|19 (のタイムスタンプを *- yyyy-mm-dd hh:mm:ss*形式)<br /><br /> または<br /><br /> 20 + *s* (のタイムスタンプを *- yyyy-mm-dd hh:mm:ss*[.fff...] 形式、場所*s*秒の小数部の有効桁数です)。|  
|間隔のすべてのデータ型|参照してください[Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)します。|  
|SQL_GUID|36 (文字数、 *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*形式|  
  
 [a] 変数の型の列またはパラメーターの長さを判断できないのは、ドライバー、SQL_NO_TOTAL が返されます。
