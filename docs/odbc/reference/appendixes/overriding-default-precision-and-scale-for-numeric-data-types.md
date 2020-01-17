---
title: 数値データ型の既定の精度とスケールのオーバーライド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66fc728440808314dbdaa30065c68232f4a89fba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100613"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>数値データ型での既定の有効桁数と小数点以下桁数のオーバーライド
ARD の SQL_DESC_TYPE フィールド設定されている場合、SQL_C_NUMERIC にいずれかを呼び出して**SQLBindCol**または**SQLSetDescField**ARD SQL_DESC_SCALE フィールドが 0 に設定されて、SQL_DESC_PRECISION フィールドが設定されますドライバーで定義された既定の有効桁数。 これは、場合でも、APD の SQL_DESC_TYPE フィールドは、いずれかを呼び出すことによって、SQL_C_NUMERIC に設定されて**SQLBindParameter**または**SQLSetDescField**します。 これは、入力、入力/出力、または出力パラメーターの場合は true。  
  
 アプリケーションが呼び出すことによって、SQL_DESC_SCALE または SQL_DESC_PRECISION のフィールドを設定する必要があります説明されている既定値のいずれかの前でない場合、アプリケーションで受け入れ**SQLSetDescField**または**SQLSetDescRec**.  
  
 アプリケーションを呼び出す場合**SQLGetData** SQL_C_NUMERIC 構造にデータを返す既定 SQL_DESC_SCALE と SQL_DESC_PRECISION フィールドは、使用します。 既定値が許容されない場合、アプリケーションを呼び出す必要があります**SQLSetDescRec**または**SQLSetDescField**フィールドを設定し、呼び出す**SQLGetData** で*TargetType* SQL_ARD_TYPE 記述子フィールドの値を使用するのです。  
  
 ときに**SQLPutData**が呼び出されるとの呼び出しは、実行時データ パラメーターまたは列に対応する記述子レコードのフィールドの SQL_DESC_SCALE と SQL_DESC_PRECISION フィールドで使用して APD フィールドへの呼び出しには**SQLExecute**または**SQLExecDirect**、ARD フィールドへの呼び出しを**SQLBulkOperations**または**SQLSetPos**します。
