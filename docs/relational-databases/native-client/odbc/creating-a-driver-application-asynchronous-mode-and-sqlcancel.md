---
title: 非同期モードと SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e49e9cd9fdf9b4aeeaad4480a222914aaeb607e3
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787781"
---
# <a name="creating-a-driver-application---asynchronous-mode-and-sqlcancel"></a>ドライバー アプリケーションの作成 - 非同期モードと SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
  
 コマンドが長時間未完了になることがあります。 アプリケーションが応答を待たずにコマンドをキャンセルする必要がある場合は、未解決のコマンドと同じステートメントハンドルを使用して**SQLCancel**を呼び出すことによって、この操作を行うことができます。 これは、 **SQLCancel**を使用する必要がある唯一の時間です。 一部のプログラマは、結果セットを使用して一部の処理を行ったときに、結果セットの残りの部分を取り消す必要がある場合に、 **SQLCancel**を使用します。 **SQLCancel**ではなく、未処理の結果セットの残りの部分を取り消すには、 [Sqlmoreresults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)または[sqlcloセキュリティー](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)を使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client ODBC ドライバー アプリケーションの作成](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
