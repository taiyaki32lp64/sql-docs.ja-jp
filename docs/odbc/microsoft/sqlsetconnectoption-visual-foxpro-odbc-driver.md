---
title: SQLSetConnectOption (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 398d098615a0453cb016286867836388fd817540
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631790"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート: 部分  
  
 レベル 1 の ODBC API 準拠:  
  
 接続の側面を制御するオプションを設定します。 この関数が部分的にサポートされています: ドライバーのすべての値をサポートする、 *fOption*引数の一部でサポートされていません*vParam*の値を*fOption*引数SQL_TXN_ISOLATION します。  
  
 次の表に、これらの引数の Visual FoxPro ODBC ドライバーの実装に固有の動作にのみ**SQLSetConnectOption**します。  
  
|*fOption*|コメント|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|アプリケーションのコミットまたはとのトランザクションをロールバックする必要があります明示的に SQL_AUTOCOMMIT_OFF 場合は、 [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC ドライバーが完了すると、transactable ステートメントを自動的にコミットされません。 ドライバーは、トランザクションを開始するステートメントが transactable の場合。|  
|SQL_CURRENT_QUALIFIER|完全修飾すること[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)名または 0 個以上含むディレクトリへの完全修飾パス[テーブルを無料](../../odbc/microsoft/visual-foxpro-terminology.md)します。|  
|SQL_LOGINTIMEOUT|"Driver できない"エラーが返されます。|  
|SQL_CURSORS|"Driver できない"エラーが返されます。|  
|SQL_PACKET_SIZE|"Driver できない"エラーが返されます。|  
|SQL_TXN_ISOLATION|ドライバーでは、SQL_TXN_READ_COMMITTED のみ使用できます。<br /><br /> 次*vParam*はサポートされていません。<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 詳細については、次を参照してください。 [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)で、 *ODBC プログラマ リファレンス*します。
