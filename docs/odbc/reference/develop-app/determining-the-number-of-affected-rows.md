---
title: 影響を受けた行の数を決定する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6a1bebf7d5cfb85e49fb0e382dacc4f4464054e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039982"
---
# <a name="determining-the-number-of-affected-rows"></a>影響を受ける行数の決定
アプリケーションが行を更新、削除、または挿入後、 **SQLRowCount** を呼び出し影響を受けた行の数を判断できます。 **SQLRowCount** は、 **UPDATE**、**DELETE**、または**INSERT**ステートメントの実行により、位置指定、更新、削除、または **SQLSetPos** の呼び出しによって行が更新、削除または挿入されたかどうかに関わらず、この値を返します。  
  
 SQL ステートメントのバッチを実行すると、バッチ内のすべてのステートメントの総数または個々 のカウント、バッチ内の各ステートメントの影響を受ける行の数。 可能性があります。 詳細については、次を参照してください。 [SQL ステートメントのバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)と[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 影響を受けた行の数は、ステートメント ハンドルに関連付けられている診断の区分の SQL_DIAG_ROW_COUNT 診断ヘッダー フィールドにも返されます。 ただし、このフィールドのデータはリセット後、同一ステートメント ハンドルですべての関数を呼び出すによって返される値は**SQLRowCount**への呼び出しまでは同じ**SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPrepare**、または**SQLSetPos**します。
