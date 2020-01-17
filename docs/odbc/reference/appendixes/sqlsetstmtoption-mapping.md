---
title: SQLSetStmtOption のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc4ed430b301f2b191c0586c0a54af19a2d2d526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091669"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption のマッピング
アプリケーションを呼び出すと**SQLSetStmtOption** ODBC を通じて*3.x*ドライバーへの呼び出し  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 次のようになります。  
  
-   場合*fOption*ドライバー マネージャーの呼び出し、文字列、あるステートメントの ODBC で定義された属性を示します  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   場合*fOption*ドライバー マネージャーの呼び出し、32 ビット整数値を返すステートメントの ODBC で定義された属性を示します  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   場合*fOption*ドライバー定義ステートメント属性、ドライバー マネージャーの呼び出しを示します  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 上記の 3 つのケース、 **StatementHandle**引数の値に設定されて*hstmt*、*属性*引数の値に設定されて*fOption*、および*ValuePtr*引数として値に設定されて*vParam*します。  
  
 有効な値を渡す必要がある、ドライバー マネージャーでは、文字列または 32 ビット整数の値には、ドライバーの定義済みのステートメント属性が必要かどうかがわからない、ため、 *StringLength*の引数**SQLSetStmtAttr**. ドライバーがドライバーの定義済みのステートメント属性の特別な意味が定義されているを使用して呼び出される必要がある場合**SQLSetStmtOption**、それをサポートする必要があります**SQLSetStmtOption**します。  
  
 アプリケーションを呼び出す場合**SQLSetStmtOption** odbc ドライバー固有のステートメントのオプションを設定する*3.x*ドライバーとオプションは、ODBC で定義された*2.x*のバージョン、ドライバーでは、ODBC でのオプションには、新しいマニフェスト定数を定義するか*3.x*ドライバー。 古いのマニフェスト定数への呼び出しで使用する場合**SQLSetStmtOption**、ドライバー マネージャーが呼び出す**SQLSetStmtAttr**で、 *StringLength*引数は 0 に設定します。  
  
 アプリケーションを呼び出すと**SQLSetStmtAttr** odbc SQL_UB_ON SQL_ATTR_USE_BOOKMARKS に設定する*3.x*ドライバー、SQL_ATTR_USE_BOOKMARKS ステートメントの属性が SQL_UB_FIXED に設定します。 SQL_UB_ON は、SQL_UB_FIXED として同じ定数です。 ドライバー マネージャーは、ドライバーを通じて SQL_UB_FIXED を渡します。 ODBC で SQL_UB_FIXED が非推奨とされました*3.x*が ODBC *3.x*ドライバーは ODBC と連動するように実装する必要があります*2.x*固定長のブックマークを使用するアプリケーション。  
  
 ODBC の*3.x*ドライバー、ドライバー マネージャーは不要になったかどうかを確認します*オプション*SQL_STMT_OPT_MIN と SQL_STMT_OPT_MAX、間、または SQL_CONNECT_OPT_DRVR_START よりも大きい。
