---
title: SQLBulkOperations を使ったブックマークによる行の削除 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a34f96dd7f5c2f0e2ac4bbb3feae06ea4856a248
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076816"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations を使ったブックマークによる行の削除
ブックマークで行を削除するときに**SQLBulkOperations**データ ソースのテーブルの 1 つまたは複数の選択した行を削除します。 行は、バインドされたブックマーク列内のブックマークによって識別されます。  
  
 使ったブックマークによる行を削除する**SQLBulkOperations**アプリケーションは、次を実行します。  
  
1.  取得し、削除するすべての行のブックマークをキャッシュします。 ブックマークは配列に格納されている 1 つ以上のブックマークが存在し、列方向のバインドを使用した場合1 つ以上のブックマークが存在し、行方向のバインドを使用した場合、それらのブックマークは、行の構造体の配列に格納されます。  
  
2.  ブックマークの数、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性を設定し、ブックマークの値、または列 0 へのブックマークの配列を含むバッファーをバインドします。  
  
3.  呼び出し**SQLBulkOperations**で*操作*SQL_DELETE_BY_BOOKMARK に設定します。
