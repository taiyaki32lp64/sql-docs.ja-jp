---
title: 10 進数字 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e58551ae3c6edda3cd865817223fd8052d03ec5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130048"
---
# <a name="decimal-digits"></a>10 進数字
*10 進数字*decimal および numeric のデータの種類は、またはデータの小数点以下桁数、小数点の右側に桁の数字の最大数として定義されます。 浮動小数点概数の数値列またはパラメーターの場合、小数点の右側にある数字の数が固定されていないため、小数点以下桁数が定義されていません。 秒コンポーネントを含む datetime または間隔のデータ、10 進数字は、データの秒部分の小数点の右側にある数字の数として定義されます。  
  
 SQL_DECIMAL および SQL_NUMERIC のデータ型の最大スケールは、通常は、最大有効桁数と同じ。 ただし、一部のデータ ソースは、最大の小数点以下桁数に個別の制限を強制します。 アプリケーションを呼び出すデータ型の許容最小値と最大のスケールを決定する**SQLGetTypeInfo**します。  
  
 簡潔な SQL データ型ごとに定義されている 10 進数字は、次の表に示します。  
  
|SQL 型|10 進数字|  
|--------------|--------------------|  
|すべての文字とバイナリの型が [a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|小数点の右側にある数字の定義済みの数。 たとえば、NUMERIC(10,3) として定義されている列の小数点以下桁数には 3 です。 負の数値を指数表記を使用せずに膨大な数のストレージをサポートできます。たとえば、「12000」-3 の桁数には、「12」として格納します。|  
|SQL_DECIMAL と SQL_NUMERIC [a] 以外のすべての正確な数値型|0|  
|すべて概数のデータ型 [a]|n/a|  
|SQL_TYPE_DATE とコンポーネントがありません。 秒 [a] すべて間隔型|n/a|  
|SQL_TYPE_DATE を除くすべての datetime 型と秒の部分ですべての間隔の種類|値 (秒の小数部) の秒の部分の小数点の右側にある数字の数。 この数値は負の値にすることはできません。|  
|SQL_GUID|n/a|  
  
 [a]、 *DecimalDigits*の引数**SQLBindParameter**はこのデータ型は無視されます。  
  
 10 進数字に対して返される値は、任意の 1 つの記述子フィールドの値に対応していません。 値は、次の表に示すように、SQL_DESC_SCALE または SQL_DESC_PRECISION フィールドには、データの種類に応じてのいずれかから取得できます。  
  
|SQL 型|対応する記述子フィールド<br /><br /> 10 進数字|  
|--------------|----------------------------------------------------------|  
|すべての文字とバイナリ型|n/a|  
|すべての正確な数値型|SCALE|  
|SQL_BIT|n/a|  
|すべての概数型|n/a|  
|すべての datetime 型|PRECISION|  
|秒の部分ですべての間隔の種類|PRECISION|  
|秒コンポーネントがありません。 されたすべての間隔の種類|n/a|
