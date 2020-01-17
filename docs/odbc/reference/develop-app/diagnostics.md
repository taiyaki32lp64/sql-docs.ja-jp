---
title: 診断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd6640c0dc06d9e957176717ef26aa3e444ffa9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022519"
---
# <a name="diagnostics"></a>診断
ODBC の関数は、次の2つの方法で診断情報を返します。 リターンコードは、関数の全体的な成功または失敗を示し、診断レコードは関数に関する詳細情報を提供します。 少なくとも1つの診断レコード-ヘッダーレコード-関数が成功した場合でも返されます。  
  
 診断情報は、ハードコーディングされた SQL ステートメントでの無効なハンドルや構文エラーなどのプログラミングエラーをキャッチするために、開発時に使用されます。 実行時には、ユーザーが入力した SQL ステートメントのデータの切り捨て、アクセス違反、構文エラーなどの実行時エラーと警告をキャッチするために使用されます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [リターン コード](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [診断レコード](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [SQLGetDiagRec および SQLGetDiagField の使用](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [SQLGetDiagRec および SQLGetDiagField の実装](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [診断処理の例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
