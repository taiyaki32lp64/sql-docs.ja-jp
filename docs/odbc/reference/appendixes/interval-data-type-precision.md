---
title: Interval データ型の有効桁数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3424c58d25be69d2ddc42a3088aa457ebddf1d4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947603"
---
# <a name="interval-data-type-precision"></a>Interval データ型の精度
間隔のデータ型の有効桁数には、有効桁数、間隔の有効桁数、および秒の有効桁数を先頭の間隔が含まれています。  
  
 間隔の先頭のフィールドは、符号付き数値です。 先頭のフィールドの最大桁数と呼ばれる数量によって決まります*間隔の先頭の有効桁数、* データ型の宣言の一部であります。 たとえば、次のような宣言があるとします。間隔 HOUR(5) 1 分間に、間隔に、5; の先頭有効桁数1 時間フィールドには、99999 を通じて-99999 値を取ります。 先頭の有効桁数の間隔は、記述子のレコードの SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドに含まれます。  
  
 間隔のデータ型から成るフィールドの一覧と呼ばれる*間隔精度*します。 "Precision"という用語が示すように数値の値はありません。 2 つ目は日、時間、リストをなど、interval 型の有効桁数、INTERVAL DAY TO 分、秒。 この値を保持する記述子フィールドはありません。間隔の有効桁数は、interval データ型が常に判断できます。  
  
 2 番目のフィールドを含む任意の間隔のデータの種類が、*秒の有効桁数*します。 これは、秒の値の小数部で許可されている 10 進数字の数です。 これは、有効桁数が小数点の前に数字の数を示す他のデータ型と異なります。 間隔のデータ型の秒の有効桁数が、小数点の桁数。 たとえば、秒の有効桁数が 6 に設定されている場合番号 123456 小数フィールドでと解釈.123456 と番号 1230.001230 として解釈できます。 他のデータ型では、これと呼ぶスケールします。 間隔の秒の有効桁数は、記述子の SQL_DESC_PRECISION フィールドに含まれます。 SQL の間隔の値の秒の小数部のコンポーネントの有効桁数がどのような C interval 構造体に格納できるよりも大きい場合は、これはドライバー定義 SQL 間隔の秒の小数部の値が丸められますまたは C に変換されるときに切り捨てられるかどうか間隔の構造体。  
  
 SQL_DESC_TYPE フィールドが SQL_INTERVAL に設定されている SQL_DESC_CONCISE_TYPE フィールドが間隔のデータ型に設定されている場合、SQL_DESC_DATETIME_INTERVAL_CODE が interval データ型のコードに設定されているとします。 SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドは 2 に、既定の間隔先頭有効桁数に自動的に設定し、SQL_DESC_PRECISION フィールドが自動的に 6 の既定の間隔 (秒) の有効桁数を設定します。 これらの値のいずれかの情報が適切でない場合、アプリケーションへの呼び出しを通じて記述子フィールドに明示的に設定する必要があります**SQLSetDescField**します。
