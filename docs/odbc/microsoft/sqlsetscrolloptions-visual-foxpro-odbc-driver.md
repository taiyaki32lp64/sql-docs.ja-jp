---
title: SQLSetScrollOptions (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3746d9cea2ce5ffb7d03424d7cda4fa1889aabc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905380"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:Partial  
  
 ODBC API 準拠:レベル 2  
  
 ステートメント ハンドルに関連付けられているカーソルの動作を制御するオプションを設定*hstmt*します。  
  
 Visual FoxPro ODBC ドライバーのみ SQL_CONCUR_READ_ONLY; をサポートしていますサポートされていません、 *fConcurrency* SQL_CONCUR_ROWVER の値します。 ドライバーは SQL_KEYSET_SIZE、SQL_CURSOR_DYNAMIC、および SQL_CURSOR_KEYSET_DRIVEN を警告 ODBC_01S02 SQL_SCROLL_STATIC に変換します。  
  
 詳細については、次を参照してください。 [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)で、 *ODBC プログラマ リファレンス*します。
