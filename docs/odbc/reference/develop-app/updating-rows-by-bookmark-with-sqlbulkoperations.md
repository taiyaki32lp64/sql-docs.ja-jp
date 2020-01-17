---
title: SQLBulkOperations を使ったブックマークによる行の更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9b10037883ef9cfa4051195270e6477c5cc04ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091622"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations を使ったブックマークによる行の更新
ブックマークで行を更新するときに**SQLBulkOperations**データ ソースのテーブルの 1 つまたは複数の行を更新します。 行は、バインドされたブックマーク列内のブックマークによって識別されます。 バインドされた各列 (列の長さ/インジケーター バッファーの値が SQL_COLUMN_IGNORE) を除くアプリケーションのバッファーでデータを使用して、行が更新されます。 バインドされていない列は更新されません。  
  
 使ったブックマークによる行を更新する**SQLBulkOperations**アプリケーション。  
  
1.  取得し、更新するすべての行のブックマークをキャッシュします。 ブックマークは配列に格納されている 1 つ以上のブックマークが存在し、列方向のバインドを使用した場合1 つ以上のブックマークが存在し、行方向のバインドを使用した場合、それらのブックマークは、行の構造体の配列に格納されます。  
  
2.  ブックマークの数、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性を設定し、ブックマークの値、または列 0 へのブックマークの配列を含むバッファーをバインドします。  
  
3.  行セットのバッファーでは、新しいデータ値を配置します。 長い形式のデータを送信する方法については**SQLBulkOperations**を参照してください[長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)します。  
  
4.  必要に応じて、各列の長さ/インジケーター バッファーの値を設定します。 これは、SQL_NTS またはデータのバイト長のバイナリのバッファーを NULL に設定する列の SQL_NULL_DATA バインドされている列のデータのバイト長の文字列のバッファーにバインドされている列です。  
  
5.  SQL_COLUMN_IGNORE に更新されませんが、それらの列の長さ/インジケーター バッファーの値を設定します。 アプリケーションは、この手順をスキップし、既存のデータを再送信、これは非効率的とが切り詰められました。 読み取られたときにデータ ソースに値を送信するリスクがあります。  
  
6.  呼び出し**SQLBulkOperations**で、*操作*引数 SQL_UPDATE_BY_BOOKMARK に設定します。  
  
 更新プログラムとして、データ ソースに送信されるすべての行をアプリケーション バッファーは有効な行のデータが必要です。 行の状態配列が維持されている場合、フェッチすることによってアプリケーション バッファーが入力されているし、行の状態値が SQL_ROW_DELETED、SQL_ROW_ERROR、または sql_row_norow であって場合は、無効なデータは、データ ソースに誤って送信でした。
