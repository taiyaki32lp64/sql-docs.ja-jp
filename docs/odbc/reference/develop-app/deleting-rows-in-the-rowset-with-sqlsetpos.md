---
title: SQLSetPos による行セット内の行の削除 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e39b70f92f7b239b011cdd4fdd6abd36c27561c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076803"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos による行セットの行の削除
削除操作の**SQLSetPos**データ ソースのテーブルの 1 つまたは複数の選択した行を削除します。 行を削除する**SQLSetPos**、アプリケーション呼び出し**SQLSetPos**で*操作*SQL_DELETE に設定と*RowNumber*に設定します削除する行の数。 場合*RowNumber*が 0 の行セット内のすべての行が削除されます場合、。  
  
 後**SQLSetPos**削除された行は、現在の行とその状態は SQL_ROW_DELETED を返します。 呼び出しなど、さらに位置指定操作で行を使用することはできません**SQLGetData**または**SQLSetPos**します。  
  
 行セットのすべての行を削除するときに (*RowNumber*が 0)、アプリケーションは、ドライバーを防ぐための更新操作と同じ方法で、行操作配列を使用して、特定の行を削除していますから**SQLSetPos**. (を参照してください[SQLSetPos による行セットの行を更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md))。  
  
 削除対象の各行は、行セット内に存在する行でなければなりません。 アプリケーション バッファーをフェッチすることによって入力された場合、および行の状態配列が維持されている場合が SQL_ROW_DELETED、SQL_ROW_ERROR、または sql_row_norow であっても、それらの行位置の各値はできません。
