---
title: ODBC のトランザクション。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ade18b71fa83c7acbb16cb7facd19dd3de61a2e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63143321"
---
# <a name="transactions-in-odbc"></a>ODBC でのトランザクション
  ODBC のトランザクションは接続レベルで管理されます。 アプリケーションはトランザクションの完了時に、その接続のすべてのステートメント ハンドルで完了したすべての作業を、コミットまたはロールバックします。 コミットするトランザクションをロールバックするか、アプリケーションを呼び出す必要があります[sqlendtran を呼び出してと](../../native-client-odbc-api/sqlendtran.md)COMMIT または ROLLBACK ステートメントを送信する代わりにします。  
  
 アプリケーションを呼び出す[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)のトランザクションを管理する 2 つの ODBC のモードを切り替えます。  
  
-   自動コミット モード  
  
     各ステートメントは、正常に完了したときに自動的にコミットされます。 自動コミット モードで実行するときは、他のトランザクション管理関数は必要ありません。  
  
-   手動コミット モード  
  
     呼び出すことによって、明示的に停止されるまで、同じトランザクションで実行されるすべてのステートメントが含まれる**sqlendtran を呼び出してと**。  
  
 自動コミット モードは、ODBC の既定のトランザクション モードです。 までオート コミット ・ モードでは、接続が行われると、 **SQLSetConnectAttr**を自動コミット モードの設定を手動コミット モードに切り替えると呼ばれます。 アプリケーションが自動コミットを無効にすると、次にデータベースに送信されるステートメントでトランザクションが開始されます。 その後、トランザクションがアプリケーション呼び出しまで有効になります**SQLEndTran**した状態または SQL_ROLLBACK オプションを使用します。 後にデータベースに送信されたコマンド**sqlendtran を呼び出してと**次のトランザクションを開始します。  
  
 手動コミット モードから自動コミット モードに切り替えると、ドライバーは接続で現在開かれているすべてのトランザクションをコミットします。  
  
 ODBC アプリケーションで BEGIN TRANSACTION、COMMIT TRANSACTION、ROLLBACK TRANSACTION などの Transact-SQL トランザクション ステートメントを使用すると、ドライバーの動作が不確定になる可能性があるので、このような Transact-SQL トランザクション ステートメントは使用しないでください。 ODBC アプリケーションする必要があります自動コミット モードで実行し、トランザクション管理関数やステートメントを使用して、または手動コミット モードで実行されず、ODBC を使用して、 **sqlendtran を呼び出してと**関数がコミットまたはトランザクションをロールバックします。  
  
## <a name="see-also"></a>参照  
 [トランザクションを実行する&#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
