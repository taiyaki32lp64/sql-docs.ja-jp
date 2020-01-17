---
title: Interval のリテラル構文 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6352a5ae894adb09f714a78386bfecfa3ce1df77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041625"
---
# <a name="interval-literal-syntax"></a>Interval のリテラルの構文
次の構文は、ODBC で interval のリテラルに使用されます。  
  
 *間隔リテラル:: = 間隔*[+ *&#124;* -]*間隔文字列間隔修飾子*  
  
 *間隔文字列*:: =*見積もり*{*年-月-リテラル*&#124; です。*日付時刻リテラル*}*見積もり*  
  
 *年-月-リテラル*:: =*年値*&#124;です。[*年値*-]*月の値*  
  
 *日付時刻リテラル*:: =*日間隔*&#124; です。*時間間隔*  
  
 *1 日間隔*:: =*日数値*[*時間値*[:*分値*[:*秒値*]]  
  
 *時間間隔*:: =*時間値*[:*分値*[:*秒値*]  
  
 &#124; です。*分値*[:*秒値*]  
  
 &#124; です。*秒の値*  
  
 *年の値*:: = *datetime 値*  
  
 *か月間値*:: = *datetime 値*  
  
 *日数値*:: = *datetime 値*  
  
 *時間値*:: = *datetime 値*  
  
 *分値*:: = *datetime 値*  
  
 *秒の値*:: =*秒整数*[. [*秒の端数*]  
  
 *整数値の秒*:: =*符号なし整数*  
  
 *秒の端数*:: =*符号なし整数*  
  
 *datetime 値*:: =*符号なし整数*  
  
 *間隔修飾子*:: =*開始フィールド*TO*終了フィールド*&#124;*単一 datetime フィールド*  
  
 *開始フィールド*:: =*秒-datetime-フィールド以外*[(*間隔リード フィールド精度*)]  
  
 *終了フィールド*:: =*非秒 datetime のフィールドの*&#124;です。2 番目 [(*間隔--秒の有効桁数*)]  
  
 *単一 datetime フィールド*:: =*非秒 datetime のフィールドの*[(*間隔先頭フィールド精度*)] &#124; です。2 番目 [(*間隔先頭フィールド精度*[、(*間隔--秒の有効桁数*)]  
  
 *datetime フィールド*:: =*非秒 datetime のフィールドの*&#124; です。1 秒  
  
 *2 番目の datetime のフィールド以外*:: = 年 &#124; です。月 &#124; です。1 日 &#124; です。1 時間 &#124; です。1 分  
  
 *間隔--秒の有効桁数*:: =*符号なし整数*  
  
 *間隔をリード フィールド精度*:: =*符号なし整数*  
  
 *見積もり*:: = '  
  
 *符号なし整数*:: =*桁.*
