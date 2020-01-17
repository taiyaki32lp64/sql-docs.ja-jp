---
title: 非同期モードと発生。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a4ec4e5d7575fdf5d915c8209999e1285fa79aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144323"
---
# <a name="asynchronous-mode-and-sqlcancel"></a>非同期モードと SQLCancel
  ODBC 関数には、同期して動作する関数と非同期に動作する関数があります。 アプリケーションでは、ステートメント ハンドルまたは接続ハンドルのいずれかに対して非同期動作を有効にすることができます。 オプションが接続ハンドル用に設定されている場合、接続ハンドルのすべてのステートメント ハンドルに影響します。 アプリケーションで次のステートメントを使用すると、非同期動作を有効または無効にすることができます。  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 アプリケーションが同期モードで ODBC 関数を呼び出した場合、サーバーでのコマンドの実行が完了したことがドライバーに通知されるまでは、ドライバーからアプリケーションに制御が戻りません。  
  
 非同期動作の場合は、ドライバーからサーバーにコマンドを送信する前でも、ドライバーからアプリケーションに直ちに制御が戻ります。 ドライバーは、リターン コードを SQL_STILL_EXECUTING に設定します。 アプリケーションでは他の作業を実行できます。  
  
 アプリケーションでコマンドが完了したかどうかをテストするときは、ドライバーに対して同じ関数を同じパラメーターを指定して呼び出します。 ドライバーがサーバーからまだ応答を受け取っていない場合、SQL_STILL_EXECUTING が再び返されます。 アプリケーションでは、リターン コードが SQL_STILL_EXECUTING 以外になるまで、定期的にコマンドをテストする必要があります。 アプリケーションで他のリターン コードを受け取ると、それが SQL_ERROR であっても、コマンドが完了したことがわかります。  
  
 コマンドが長時間未完了になることがあります。 呼び出すことによって実行可能アプリケーションの応答を待つことがなく、コマンドをキャンセルする場合は、**発生**同じステートメントでは、未解決のコマンドとして処理します。 これだけの時間は、**発生**使用する必要があります。 いくつかのプログラマを使用して、**発生**とそれらの処理が途中の結果を設定し、結果セットの残りの部分をキャンセルします。 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)または[手段](../../native-client-odbc-api/sqlclosecursor.md)、未処理の結果セットの残りの部分にキャンセルを使用する必要があります**発生**。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client ODBC ドライバー アプリケーションの作成](creating-a-driver-application.md)  
  
  
