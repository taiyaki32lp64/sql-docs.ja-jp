---
title: カーソル オプション (ODBC) の設定 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48389a3b537461a89bcf5c8bcbc646d3417939c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200346"
---
# <a name="set-cursor-options-odbc"></a>カーソル オプションの設定 (ODBC)
  カーソル オプションを設定するには、呼び出す[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)を設定または[SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md)カーソル動作を制御するステートメント オプションを取得します。  
  
|*属性*|指定対象|  
|-----------------|---------------|  
|SQL_ATTR_CURSOR_TYPE|カーソルの種類。順方向専用、静的、動的、キーセット ドリブンのいずれか|  
|SQL_ATTR_CONCURRENCY|コンカレンシー制御オプション。読み取り専用、ロック、タイムスタンプを使用するオプティミスティック、値を使用するオプティミスティックのいずれか|  
|SQL_ATTR_ROW_ARRAY_SIZE|フェッチごとに取得される行数|  
|SQL_ATTR_CURSOR_SENSITIVITY|他の接続によるカーソル行の更新を、カーソルで表示するかしないか|  
|SQL_ATTR_CURSOR_SCROLLABLE|カーソルを前後にスクロール可能|  
  
 これらの属性の既定値 (順方向専用、読み取り専用、行セット サイズ 1) では、サーバー カーソルを使用しません。 サーバー カーソルを使用するには、少なくともこれらの属性のいずれかを既定値以外に設定する必要があります。また、実行するステートメントを、単一の SELECT ステートメントか、単一の SELECT ステートメントを含むストアド プロシージャにする必要があります。 サーバー カーソルを使用する場合、SELECT ステートメントは、サーバー カーソルでサポートされていない句を使用できません。COMPUTE、COMPUTE BY、FOR BROWSE および INTO です。  
  
 SQL_ATTR_CURSOR_TYPE および SQL_ATTR_CONCURRENCY を設定するか、SQL_ATTR_CURSOR_SENSITIVITY と SQL_ATTR_CURSOR_SCROLLABLE を設定して使用するカーソルの種類を制御できます。 カーソルの動作を指定するこの 2 つの方法を組み合わせて実行しないでください。  
  
## <a name="example"></a>例  
 次のサンプルでは、ステートメント ハンドルを割り当て、行のバージョンに基づくオプティミスティック コンカレンシーを使用する動的カーソルを種類として設定してから、SELECT を実行します。  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_DYNAMIC, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQLPOINTER)SQL_CONCUR_ROWVER, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, SELECT au_lname FROM authors", SQL_NTS);  
```  
  
## <a name="example"></a>例  
 次のサンプルでは、ステートメント ハンドルを割り当て、スクロール可能な反映型カーソルを設定してから、SELECT を実行します。  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
  
// Set the cursor options and execute the statement.  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SCROLLABLE, SQLPOINTER)SQL_SCROLLABLE, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SENSITIVITY, SQLPOINTER)SQL_INSENSITIVE, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, select au_lname from authors", SQL_NTS);  
```  
  
## <a name="see-also"></a>参照  
 [クエリを実行方法に関するトピック&#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
