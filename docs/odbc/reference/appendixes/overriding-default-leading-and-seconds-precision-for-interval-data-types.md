---
title: Interval データ型の先頭と秒の有効桁数をオーバーライド |Microsoft Docs
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
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13adfb16b772acc5fac30cf3d10c6199f16f479d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100622"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Interval データ型での既定の先頭有効桁数と秒小数部分のオーバーライド
ARD の SQL_DESC_TYPE フィールド設定されている場合、datetime または間隔の C 型をいずれかを呼び出して**SQLBindCol**または**SQLSetDescField**、SQL_DESC_PRECISION フィールド (を含む間隔 (秒)有効桁数) は、次の既定値に設定されます。  
  
-   タイムスタンプと 2 番目のコンポーネントの interval データ型をすべて 6。  
  
-   その他のすべてのデータ型は 0 です。  
  
 すべての interval データ型の間隔の先頭フィールドの精度が含まれている、SQL_DESC_DATETIME_INTERVAL_PRECISION 記述子フィールドは、既定値は 2 に設定されます。  
  
 APD の SQL_DESC_TYPE フィールド設定されている場合、datetime または間隔の C 型をいずれかを呼び出して**SQLBindParameter**または**SQLSetDescField**、SQL_DESC_PRECISION および SQL_DESC_DATETIME_INTERVAL_APD の有効桁数のフィールドは、以前に指定された既定値に設定されます。 これは、true または入力/出力の出力パラメーターではなく入力パラメーター。  
  
 呼び出し**SQLSetDescRec**間隔の既定値を先頭の有効桁数を設定しますが、(SQL_DESC_PRECISION フィールド) の間隔の秒の有効桁数を設定の値にその*精度*引数。  
  
 アプリケーションが呼び出すことによって、SQL_DESC_PRECISION または SQL_DESC_DATETIME_INTERVAL_PRECISION のフィールドを設定する必要がありますの既定の設定のいずれか以前が許容されない場合、アプリケーションに、 **SQLSetDescField**します。  
  
 アプリケーションを呼び出す場合**SQLGetData** datetime または C 型の間隔にデータを返す既定の間隔の先頭有効桁数と間隔の秒の有効桁数を使用します。 いずれかの既定値が許容されない場合、アプリケーションを呼び出す必要があります**SQLSetDescField**いずれかの記述子フィールドを設定または**SQLSetDescRec** SQL_DESC_PRECISION を設定します。 呼び出し**SQLGetData**する必要がありますが、 *TargetType* SQL_ARD_TYPE 記述子フィールドの値を使用するのです。  
  
 ときに**SQLPutData**が呼び出され、精度と間隔 (秒) の有効桁数は、実行時データ パラメーターまたは列に対応する記述子レコードのフィールドから読み取られます APD のフィールドの呼び出しである先頭の間隔**SQLExecute**または**SQLExecDirect**、ARD フィールドへの呼び出しを**SQLBulkOperations**または**SQLSetPos**します。
