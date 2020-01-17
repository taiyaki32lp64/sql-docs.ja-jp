---
title: SQLSetStmtOption (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905337"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:レベル 1  
  
 ステートメント ハンドルに関連するオプションを設定*hstmt*します。  
  
|*fOption*|指定できる値|コメント|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|これを設定しようとした場合*fOption*ドライバーは、エラーを返します。"Driver できない"。 Visual FoxPro は、非同期実行をサポートしていません。|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN または構造体、または結果に列がバインドされるバッファーのインスタンスの長さを示す 32 ビット値。||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Visual FoxPro にタイムスタンプに基づく行のバージョン管理があるないために、ドライバーは、SQL_CONCUR_ROWVER を許可しません。|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|ドライバーでは、SQL_CURSOR_KEYSET_DRIVEN または SQL_CURSOR_DYNAMIC; は許可しません参照してください[SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md)詳細についてはします。|  
|SQL_KEYSET_SIZE|エラー:"Driver できません。"|Visual FoxPro は、キーセット カーソル モデルをサポートしていません。|  
|SQL_MAX_LENGTH|0|これを設定しようとした場合*fOption*値、ドライバー エラーが返されます「ドライバーに対応していない」。|  
|SQL_MAX_ROWS|0|これを設定しようとした場合*fOption*値、ドライバー エラーが返されます「ドライバーに対応していない」。|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|これを設定しようとした場合*fOption*値、ドライバー エラーが返されます「ドライバーに対応していない」。|  
|SQL_RETRIEVE_DATA|SQL_RD_ON、SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 に 4,294,967,296||  
|SQL_SIMULATE_CURSOR|エラー:"Driver できません。"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 詳細については、次を参照してください。 [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)で、 *ODBC プログラマ リファレンス*します。
