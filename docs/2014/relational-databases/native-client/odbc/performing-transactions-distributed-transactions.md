---
title: 分散トランザクションを実行します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa5c6b607fa7523380950ecd89f9cae20ffc6f21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228952"
---
# <a name="performing-distributed-transactions"></a>分散トランザクションの実行
  Microsoft 分散トランザクション コーディネーター (MS DTC) により、アプリケーションで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の複数のインスタンスにトランザクションを分散できるようになります。 また、Open Group DTP XA 標準に準拠するトランザクション マネージャーによって管理されるトランザクションに参加させることもできます。  
  
 通常、すべてのトランザクション管理コマンドは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを経由してサーバーに送信されます。 アプリケーションを呼び出すことによってトランザクションを開始する[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)自動コミット モードをオフにします。 次に、アプリケーションがトランザクションと呼び出しを構成する更新プログラムを実行します[SQLEndTran](../../native-client-odbc-api/sqlendtran.md)した状態または SQL_ROLLBACK オプションを使用します。  
  
 MS DTC を使用している場合ただし、MS DTC がトランザクション マネージャーとアプリケーションを使用して、不要になった**sqlendtran を呼び出してと**。  
  
 分散トランザクションに参加しているときに 2 番目の分散トランザクションに参加すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは元の分散トランザクションへの参加を解除して、新しいトランザクションに参加します。 詳細についてを参照してください[DTC プログラマーズ リファレンス](https://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)。  
  
## <a name="see-also"></a>参照  
 [トランザクションを実行する&#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
