---
title: ステートメントの実行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d95226e9d895bf78e15176744f651b7e830a1a10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901344"
---
# <a name="executing-a-statement"></a>ステートメントの実行
によって、データベース エンジンとそれを定義するには、(準備)、コンパイル時にに応じて、ステートメントを実行する 4 つの方法はあります。  
  
-   **直接実行**アプリケーションは、SQL ステートメントを定義します。 準備され、1 つの手順で実行時に実行します。  
  
-   **準備実行**アプリケーションは、SQL ステートメントを定義します。 これにより、準備は、別の手順で実行時に実行します。 ステートメントは、1 回だけ準備し、複数回実行できます。  
  
-   **プロシージャ**アプリケーションを定義し、コンパイル、または開発での複数の SQL ステートメントは、時間し、手順として、データ ソースでこれらのステートメントを格納します。 プロシージャが実行時に 1 つまたは複数回実行されます。 アプリケーションでは、カタログ関数を使用して、使用可能なストアド プロシージャを列挙できます。  
  
-   **カタログ関数**ドライバー開発者は、定義済みの結果セットを返す関数を作成します。 通常、この関数は定義済みの SQL ステートメントを送信するか、この目的で作成したプロシージャを呼び出します。 関数は実行時に 1 つまたは複数回実行されます。  
  
 特定のステートメント (そのステートメント ハンドルで識別される) になる可能性が任意の回数実行します。 別の SQL ステートメントのさまざまなステートメントを実行することができますか、同じ SQL ステートメントを繰り返し実行することができます。 たとえば、次のコードが、同一ステートメント ハンドルを使用 (*hstmt1*) を取得し、Sales データベースにテーブルを表示します。 次に、ユーザーが選択されているテーブルで列を取得するには、このハンドルを再利用します。  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 次のコードを繰り返し、同じステートメントのテーブルから行を削除を実行する単一のハンドルを使用する方法を示しています。  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 ドライバーの数、ステートメントの割り当ては、高価なタスク、通常は既存のステートメントと新規の割り当てを解放することよりも効率的ではこの方法で、同じステートメントを再利用します。 ステートメントで結果セットを作成するアプリケーションは、設定、ステートメントの前に結果の上にカーソルを閉じるように注意してくださいである必要があります。詳細については、次を参照してください。[カーソルを閉じる](../../../odbc/reference/develop-app/closing-the-cursor.md)します。  
  
 ステートメントを再利用も、一部のドライバーに一度にアクティブにできるステートメントの数の制限を回避するためにアプリケーションを強制的にします。 「アクティブ」の正確な定義は、個々 のドライバーが、多くの場合、準備または実行されたすべてのステートメントを参照し、まだ使用可能な結果です。 後など、**挿入**ステートメントが準備された、一般的にはアクティブにすると見なされます後、**選択**ステートメントが実行されると、カーソルが開いたまま、通常と見なされます。アクティブです。後に、 **CREATE TABLE**ステートメントが実行された、一般的にアクティブにも考慮されません。  
  
 アプリケーションは、呼び出すことによって、一度に 1 つの接続でアクティブにできるステートメントの数を決定します。 **SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES オプションを使用します。 アプリケーションは、データ ソースに複数の接続を開くことでこの制限よりもアクティブなステートメントを使用できます。接続できるので高価なただし、パフォーマンスに影響を検討してください。  
  
 アプリケーションは、SQL_ATTR_QUERY_TIMEOUT ステートメント属性で実行するためのステートメントに割り当てられた時間の量を制限できます。 データ ソースには、結果セットが返される前に、タイムアウト期間が経過すると、SQL ステートメントを実行する関数は、SQLSTATE HYT00 を返します (タイムアウトになりました)。 既定では、タイムアウトはありません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [直接実行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [準備実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [手順](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL ステートメントのバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [カタログ関数の実行](../../../odbc/reference/develop-app/executing-catalog-functions.md)
