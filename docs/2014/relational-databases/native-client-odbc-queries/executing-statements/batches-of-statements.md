---
title: ステートメントのバッチ |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8951469279e5c3577aef355e339397b329bb5d63
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206775"
---
# <a name="batches-of-statements"></a>ステートメントのバッチ
  バッチの[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントに渡される 1 つの文字列に組み込まれている、セミコロン (;) で区切られた 2 つ以上のステートメントが含まれています**SQLExecDirect**または[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)します。 以下に例を示します。  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 バッチでは、通常、ネットワーク トラフィックが削減されるので、複数のステートメントを個別に送信するよりも効率的になる可能性があります。 使用[SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)を次の結果セットの現在の結果セットが終了したら位置指定します。  
  
 行セットのサイズが 1 になっている、順方向専用かつ読み取り専用のカーソルの既定値に ODBC カーソル属性が設定されている場合は、常にバッチを使用できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対してサーバー カーソルを使用しているときにバッチを実行すると、サーバー カーソルが暗黙的に既定の結果セットに変換されます。 **SQLExecDirect**または**SQLExecute**呼び出すと、SQL_SUCCESS_WITH_INFO を返す**SQLGetDiagRec**を返します。  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>関連項目  
 [ステートメントを実行する&#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
