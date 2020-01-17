---
title: 構成のグレゴリオ暦カレンダーの制約 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67d313f5a1261dba1f88e9ef3a70d30c1cd503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019178"
---
# <a name="constraints-of-the-gregorian-calendar"></a>グレゴリオ暦カレンダーの制限
日付、および日時のデータ型、および、interval データ型の後続のフィールドは、グレゴリオ暦の制約に従う必要があります。 これらの制約は次のとおりです。  
  
-   月のフィールドの値は、1 ~ 12、包括的でなければなりません。  
  
-   日フィールドの値は、1 ~、1 か月の日数の範囲内である必要があります。 月の日数は年と月のフィールドの値から決定され、28、29、30、または 31 を指定できます。 (月の日数もに依存できます閏年かどうかが。)  
  
-   1 時間フィールドの値は 0 ~ 23 の範囲の範囲にある必要があります。  
  
-   分単位のフィールドの値は 0 ~ 59、包括的である必要があります。  
  
-   Interval データ型の末尾 (秒) フィールドに、秒フィールドの値が 0 と 59.9 間である必要があります (*n*) までの値を*n*秒の小数部の桁の番号です。  
  
-   Datetime データ型の末尾 (秒) フィールドに、秒のフィールドの値は 0 ~ 61.9 の間にある必要があります (*n*) までの値を*n* 「9」の数字の数との値を指定します*n*秒の小数部の有効桁数です。 (秒の範囲は、sidereal 時間の同期を維持するように 2 つのうるう秒を許可します)。
