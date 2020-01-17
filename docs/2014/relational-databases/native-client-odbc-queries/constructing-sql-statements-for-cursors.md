---
title: カーソルの SQL ステートメントを構築します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], statement construction
- ODBC applications, cursors
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
- statements [ODBC], cursors
ms.assetid: 134003fd-9c93-4f5c-a988-045990933b80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dc86f27ab9e111c5d93c91de65c51da9008ba33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207077"
---
# <a name="constructing-sql-statements-for-cursors"></a>カーソル用の SQL ステートメントの作成
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは、ODBC の仕様で定義されているカーソル機能を実装するためにサーバー カーソルを使用します。 ODBC アプリケーションを使用して、カーソルの動作を制御する[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)別のステートメントの属性を設定します。 次に、属性とその既定値を示します。  
  
|属性|既定|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 これらのオプションは、SQL ステートメントの実行時にデフォルト値に設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の結果セットを実装するためにネイティブ クライアントの ODBC ドライバーがサーバー カーソルを使用できません; 代わりに、既定の結果セットを使用します。 これらのオプションのいずれかが、SQL ステートメントの実行時に既定値から変更された場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは結果セットを実装するためにサーバー カーソルを使用しようとしています。  
  
 既定の結果セットは、すべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをサポートします。 既定の結果セットを使用するときに実行できる SQL ステートメントの種類に制限はありません。  
  
 サーバー カーソルはすべての [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをサポートしているわけではありません。 複数の結果セットを生成する SQL ステートメントはサポートされません。  
  
 次に示す種類のステートメントは、サーバー カーソルではサポートされません。  
  
-   バッチ  
  
     2 つ以上の個別の SQL SELECT ステートメントから構成される SQL ステートメント。次に例を示します。  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   複数の SELECT ステートメントを含むストアド プロシージャ  
  
     複数の SELECT ステートメントを含むストアド プロシージャを実行する SQL ステートメント。 パラメーターまたは変数を設定する SELECT ステートメントも該当します。  
  
-   キーワード  
  
     キーワード FOR BROWSE または INTO を伴う SELECT ステートメント。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、上記の条件のいずれかに該当する SQL ステートメントをサーバー カーソルを使用して実行した場合、サーバー カーソルは暗黙的に既定の結果セットに変換されます。 後**SQLExecDirect**または**SQLExecute**属性は既定の設定に戻して、カーソル、SQL_SUCCESS_WITH_INFO が返されます。  
  
 上記の分類に該当しない SQL ステートメントは、ステートメント属性の設定がどのようであっても実行できます。既定の結果セット、サーバー カーソルを問わず、どちらも正常に機能します。  
  
## <a name="errors"></a>エラー  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 以降のバージョンで複数の結果セットが生成されるステートメントを実行すると、SQL_SUCCESS_WITH INFO および次のメッセージが生成されます。  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 このメッセージが表示、ODBC アプリケーションが呼び出すことができます[SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md)現在のカーソルの設定を決定します。  
  
 サーバー カーソルを使用しているときに、複数の SELECT ステートメントから構成されるプロシージャを実行すると、次のエラーが発生します。  
  
```  
SqlState: 42000  
pfNative: 16937  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               A server cursor is not allowed on a stored procedure  
               with more than one SELECT statement in it. Use a  
               default result set or client cursor.  
```  
  
 サーバー カーソルを使用しているときに、複数の SELECT ステートメントから構成されるバッチを実行すると、次のエラーが発生します。  
  
```  
SqlState: 42000  
pfNative: 16938  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               sp_cursoropen. The statement parameter can only  
               be a single SELECT statement or a single stored   
               procedure.  
```  
  
 ODBC アプリケーションで上記のエラーが発生した場合、カーソルのすべてのステートメント属性を既定値に戻してからステートメントを実行する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [クエリの実行&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
