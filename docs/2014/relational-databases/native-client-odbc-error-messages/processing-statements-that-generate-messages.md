---
title: メッセージを生成するステートメントの処理 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11235979a886e82fa09ca1d1a79fa21550965d0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68205699"
---
# <a name="processing-statements-that-generate-messages"></a>メッセージを生成するステートメントの処理
  [!INCLUDE[tsql](../../includes/tsql-md.md)] SET ステートメントのオプション STATISTICS TIME と STATISTICS IO は、実行時間の長いクエリの診断に利用できる情報を取得する場合に使用します。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、クエリ プランを分析するための SHOWPLAN オプションもサポートされています。 ODBC アプリケーションでは、次のステートメントを実行してこれらのオプションを設定できます。  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 SET STATISTICS TIME または SET SHOWPLAN が ON の場合に**SQLExecute**と**SQLExecDirect** SQL_SUCCESS_WITH_INFO が返されます、その時点では、アプリケーションは、SHOWPLAN または統計時の出力を取得できます呼び出して**SQLGetDiagRec** sql_no_data が返されるまでです。 SHOWPLAN データの各行は、次の形式で返されます。  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 では、SHOWPLAN オプションが SHOWPLAN_ALL オプションと SHOWPLAN_TEXT オプションに置き換えられました。これらの両方のオプションでは、一連のメッセージではなく、結果セットとして出力が返されます。  
  
 STATISTICS TIME の各行は、次の形式で返されます。  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 SET STATISTICS IO の出力は、結果セットの最後に到達するまで使用できません。 STATISTICS IO 出力するには、アプリケーション呼び出しを取得する**SQLGetDiagRec**時**SQLFetch**または[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md) sql_no_data が返されます。 STATISTICS IO の出力は、次の形式で返されます。  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>DBCC ステートメントの使用  
 DBCC ステートメントは、結果セットではなく、メッセージとしてデータを返します。 **SQLExecDirect**または**SQLExecute** 、SQL_SUCCESS_WITH_INFO とアプリケーションは、呼び出すことによって出力を取得します。 を返す**SQLGetDiagRec** sql_no_data が返されるまでです。  
  
 たとえば、次のステートメントでは SQL_SUCCESS_WITH_INFO が返されます。  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 呼び出す**SQLGetDiagRec**を返します。  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>PRINT ステートメントと RAISERROR ステートメントの使用  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT ステートメントおよび RAISERROR ステートメントが呼び出すことによってもデータを返す**SQLGetDiagRec**します。 PRINT ステートメントは、SQL_SUCCESS_WITH_INFO、および後続の呼び出しを返す SQL ステートメントの実行を発生**SQLGetDiagRec**を返します、 *SQLState* 01000 します。 重大度が 10 以下の RAISERROR の動作は PRINT と同様です。 重要度レベル 11 以上の RAISERROR の SQL_ERROR を返し、後続の呼び出し実行により**SQLGetDiagRec**返します*SQLState* 42000 します。 たとえば、次のステートメントでは SQL_SUCCESS_WITH_INFO が返されます。  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 呼び出す**SQLGetDiagRec**を返します。  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 次のステートメントからは、SQL_SUCCESS_WITH_INFO が返されます。  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 呼び出す**SQLGetDiagRec**を返します。  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 次のステートメントからは、SQL_ERROR が返されます。  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 呼び出す**SQLGetDiagRec**を返します。  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 呼び出し元のタイミング**SQLGetDiagRec** PRINT または RAISERROR ステートメントからの出力が結果セットに含まれる場合に不可欠です。 呼び出し**SQLGetDiagRec** PRINT または RAISERROR を取得する、SQL_ERROR または SQL_SUCCESS_WITH_INFO ステートメントの直後後の出力を行う必要があります。 この操作は、上記の例のように、1 つの SQL ステートメントのみを実行するときは容易に実行できます。 これらのケースへの呼び出しで**SQLExecDirect**または**SQLExecute** SQL_ERROR または SQL_SUCCESS_WITH_INFO を返しますと**SQLGetDiagRec**しと呼ばれることができます。 SQL ステートメントのバッチの出力を処理するループをコーディングするとき、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャを実行するときは、1 つの SQL ステートメントのみを実行するときほど簡単ではありません。  
  
 この場合、バッチまたはストアド プロシージャで実行される SELECT ステートメントごとに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から結果セットが返されます。 バッチまたはプロシージャに PRINT ステートメントまたは RAISERROR ステートメントが含まれている場合、これらのステートメントの出力は SELECT ステートメントの結果セットと交互に返されます。 バッチまたはプロシージャの最初のステートメントが PRINT または RAISERROR の場合、 **SQLExecute**または**SQLExecDirect** を呼び出す必要があるSQL_SUCCESS_WITH_INFOまたはSQL_ERRORを返し、アプリケーションに返します**SQLGetDiagRec** PRINT または RAISERROR の情報を取得する sql_no_data が返されるまでです。  
  
 PRINT または RAISERROR ステートメントが SELECT ステートメントの場合) など、SQL ステートメントの後に続く場合、PRINT または RAISERROR に関する情報が返される[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md)エラーを含む結果の位置に設定します。 **SQLMoreResults**メッセージの重大度に応じて、SQL_SUCCESS_WITH_INFO または SQL_ERROR を返します。 呼び出すことによってメッセージが取得される**SQLGetDiagRec** sql_no_data が返されるまでです。  
  
## <a name="see-also"></a>関連項目  
 [エラーとメッセージの処理](handling-errors-and-messages.md)  
  
  
