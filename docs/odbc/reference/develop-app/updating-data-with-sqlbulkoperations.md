---
title: SQLBulkOperations によるデータの更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d1aa9b3300cba78f34e876a8501dbaaa421390a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091661"
---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations によるデータの更新
アプリケーションへの呼び出しで、データ ソースの基になるテーブルでの一括更新、削除、fetch、または挿入操作を実行できます**SQLBulkOperations**します。 呼び出す**SQLBulkOperations**を構築して、SQL ステートメントの実行に代わる便利な方法です。 位置指定更新をサポートして、データ ソースが配置されている SQL ステートメントをサポートしていない場合にも ODBC ドライバーことができます。 関数呼び出しを使用してデータベースの完全なアクセスを実現するためのパラダイムの一部になります。  
  
 **SQLBulkOperations**は現在の行セットを操作しへの呼び出し後にのみ使用することができます**SQLFetch**または**SQLFetchScroll**します。 アプリケーションでは、更新、削除、またはそのブックマークをキャッシュすることで更新する行を指定します。 ドライバーは、新しいデータを更新する行または行セットのバッファーから、基になるテーブルに挿入する新しいデータを取得します。  
  
 使用される行セット サイズ**SQLBulkOperations**への呼び出しで設定されて**SQLSetStmtAttr**で、*属性*引数 sql_attr_row_array_size を指定します。 異なり**SQLSetPos**への呼び出し後にのみ新しい行セット サイズを使用する**SQLFetch**または**SQLFetchScroll**、 **SQLBulkOperations**を使用して、呼び出しの後の新しい行セット サイズ**SQLSetStmtAttr**します。  
  
 Sql、リレーショナル データベースとのほとんどの対話が行われるため、 **SQLBulkOperations**広くサポートされていません。 ただし、ドライバーを簡単にエミュレートできますが構築して実行する**UPDATE**、**DELETE**、または**INSERT**ステートメント。  
  
 操作を決定する**SQLBulkOperation**サポートされており、アプリケーションを呼び出す**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または (カーソルの種類) に応じて SQL_STATIC_CURSOR_ATTRIBUTES1 情報オプション。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLBulkOperations を使ったブックマークによる行の更新](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations を使ったブックマークによる行の削除](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations による行の挿入](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations による行のフェッチ](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
