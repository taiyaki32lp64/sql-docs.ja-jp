---
title: SQLGetConnectOption (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c17cd473d3c96032817c2b183bf65fe360cf3cdc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053677"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:Partial  
  
 ODBC API 準拠:レベル 1  
  
 接続オプションの現在の設定を返します。 この関数は部分的にサポートされています。ドライバーのすべての値をサポートする、 *fOption*引数の一部でサポートされていません*vParam*の値を*fOption* SQL_TXN_ISOLATION 引数。  
  
 次の表に、これらの引数の Visual FoxPro ODBC ドライバーの実装に固有の動作にのみ**SQLGetConnectOption**します。  
  
|*fOption*|コメント|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|アプリケーションのコミットまたはとのトランザクションをロールバックする必要があります明示的に SQL_AUTOCOMMIT_OFF 場合は、 [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); Visual FoxPro ODBC ドライバーが完了すると、transactable ステートメントを自動的にコミットされません。 ドライバーは、トランザクションを開始するステートメントが transactable の場合。|  
|SQL_CURRENT_QUALIFIER|データベース (.dbc ファイル) の完全修飾名または完全修飾パス 0 個以上のテーブル (.dbf ファイル) を含むディレクトリを指定できます。|  
|SQL_LOGINTIMEOUT|「ドライバーできない」エラーが返されます。|  
|SQL_CURSORS|「ドライバーできない」エラーが返されます。|  
|SQL_PACKET_SIZE|「ドライバーできない」エラーが返されます。|  
|SQL_TXN_ISOLATION|ドライバーでは、SQL_TXN_READ_COMMITTED のみ使用できます。<br /><br /> 次*vParam*はサポートされていません。<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 詳細については、次を参照してください。 [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md)で、 *ODBC プログラマ リファレンス*します。
