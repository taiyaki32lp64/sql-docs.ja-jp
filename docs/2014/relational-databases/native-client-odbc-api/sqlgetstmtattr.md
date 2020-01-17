---
title: SQLGetStmtAttr |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5604aafbbc8a6d77081e829269955c8b7600f4ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62657811"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはドライバー固有のステートメント属性を公開する SQLGetStmtAttr を拡張します。  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md)はどちらもリストのステートメント属性を読み書きします。 ここでは、読み取り専用のステートメント属性のみを示します。  
  
## <a name="sqlsoptsscurrentcommand"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 コマンド バッチの現在のコマンドを公開します。 バッチ内のコマンドの位置を表す整数を返します。 *ValuePtr*値型は sqllen です。  
  
## <a name="sqlsoptssnocountstatus"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 属性は、NOCOUNT の現在の設定を示すオプションを制御するかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ステートメントによって影響を受ける行の数を報告するときに[SQLRowCount](sqlrowcount.md)が呼び出されます。 *ValuePtr*値型は sqllen です。  
  
|値|説明|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT を OFF にします。 SQLRowCount では、影響を受ける行の数を返します。|  
|SQL_NC_ON|NOCOUNT を ON にします。 影響を受ける行の数が SQLRowCount によって返されないと、0 が返されます。|  
  
 SQLRowCount 0 を返す場合、アプリケーションは SQL_SOPT_SS_NOCOUNT_STATUS をテストする必要があります。 SQL_NC_ON が返された場合、値の 0 SQLRowCount からことを示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が行の数は返されません。 SQL_NC_OFF が返される場合は、NOCOUNT が無効と SQLRowCount から 0 の値は、ステートメントがすべての行に影響しないことを示しますのことを意味します。  
  
 SQL_SOPT_SS_NOCOUNT_STATUS が SQL_NC_OFF のとき、アプリケーションは SQLRowCount の値を表示しない必要があります。 大きなバッチやストアド プロシージャには、複数の SET NOCOUNT ステートメントが含まれていることがあるので、SQL_SOPT_SS_NOCOUNT_STATUS が一定であると想定することはできません。 このオプションには、毎回のでは 0 を返しますをテストする必要があります。  
  
## <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 クエリ通知要求のメッセージ テキストを返します。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr とテーブル値パラメーター  
 SQLGetStmtAttr を呼び出すテーブル値パラメーターを使用する場合は、アプリケーション パラメーター記述子 (APD) の SQL_SOPT_SS_PARAM_FOCUS の値を取得することができます。 SQL_SOPT_SS_PARAM_FOCUS の詳細については、次を参照してください。 [SQLSetStmtAttr](sqlsetstmtattr.md)します。  
  
 テーブル値パラメーターの詳細については、次を参照してください。[テーブル値パラメーター &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLSetStmtAttr 関数](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
