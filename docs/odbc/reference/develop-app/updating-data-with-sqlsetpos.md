---
title: SQLSetPos によるデータの更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2895ec765df3910dbbaa1e76ba1579e4afe5cca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091647"
---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos によるデータの更新
アプリケーションの更新または削除を含む行セットの任意の行**SQLSetPos**します。 呼び出す**SQLSetPos**を構築して、SQL ステートメントの実行に代わる便利な方法です。 位置指定更新をサポートして、データ ソースが配置されている SQL ステートメントをサポートしていない場合にも ODBC ドライバーことができます。 関数呼び出しを使用してデータベースの完全なアクセスを実現するためのパラダイムの一部になります。  
  
 **SQLSetPos**は現在の行セットを操作しへの呼び出し後にのみ使用することができます**SQLFetchScroll**します。 アプリケーションでは、更新、削除、または挿入する行の数を指定します。 および、ドライバーは、行セットのバッファーからその行の新しいデータを取得します。 **SQLSetPos**現在の行として指定した行を指定するか、データ ソースから行セット内の特定の行を更新するにも使用できます。  
  
 呼び出して行セットのサイズが設定されて**SQLSetStmtAttr**で、*属性*引数 sql_attr_row_array_size を指定します。 **SQLSetPos**への呼び出し後にのみ、ただし、新しい行セットのサイズを使用して**SQLFetch**または**SQLFetchScroll**します。 たとえば、次の行セットのサイズを変更すると、 **SQLSetPos**が呼び出され、 **SQLFetch**または**SQLFetchScroll**が呼び出されへの呼び出し**SQLSetPos**中に古い行セットのサイズを使用して**SQLFetch**または**SQLFetchScroll**新しい行セット サイズが使用されます。  
  
 行セット内の先頭行の行番号は 1 です。 *RowNumber*引数**SQLSetPos**行セット内の行を識別する必要がありますは、その値が 1 から最後にフェッチされた行の数の範囲である必要があります (なる可能性があるより小さい行セット サイズ)。 場合*RowNumber*が 0 の場合、操作は、行セット内のすべての行に適用されます。  
  
 Sql、リレーショナル データベースとのほとんどの対話が行われるため、 **SQLSetPos**広くサポートされていません。 ただし、ドライバーを簡単にエミュレートできますが構築して実行する**UPDATE**または**DELETE**ステートメント。  
  
 操作を決定する**SQLSetPos**サポートされており、アプリケーションを呼び出す**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または (カーソルの種類) に応じて SQL_STATIC_CURSOR_ATTRIBUTES1 情報オプション。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLSetPos による行セットの行の更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos による行セットの行の削除](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
