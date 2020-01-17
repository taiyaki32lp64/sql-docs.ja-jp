---
title: SQLGetStmtAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 198c3c8e5752aebc58726b2e7478632adf2c1bd0
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786289"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、ドライバー固有のステートメント属性を公開するために SQLGetStmtAttr が拡張されます。  
  
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)には、読み取りと書き込みの両方のステートメント属性が一覧表示されます。 ここでは、読み取り専用のステートメント属性のみを示します。  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 コマンド バッチの現在のコマンドを公開します。 バッチ内のコマンドの位置を表す整数を返します。 *Valueptr*値の型は SQLLEN です。  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 SQL_SOPT_SS_NOCOUNT_STATUS 属性は、NOCOUNT オプションの現在の設定を示します。これは、 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)が呼び出されたときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がステートメントの影響を受ける行の数を報告するかどうかを制御します。 *Valueptr*値の型は SQLLEN です。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT を OFF にします。 SQLRowCount は、影響を受けた行数を返します。|  
|SQL_NC_ON|NOCOUNT を ON にします。 影響を受ける行の数は SQLRowCount によって返されず、戻り値は0です。|  
  
 SQLRowCount が0を返す場合、アプリケーションは SQL_SOPT_SS_NOCOUNT_STATUS をテストする必要があります。 SQL_NC_ON が返された場合、SQLRowCount の値が0の場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって行数が返されなかったことを示します。 SQL_NC_OFF が返された場合は、NOCOUNT が無効になっていることを意味し、SQLRowCount からの値が0の場合は、ステートメントが行に影響していないことを示します。  
  
 SQL_SOPT_SS_NOCOUNT_STATUS が SQL_NC_OFF 場合、アプリケーションには SQLRowCount の値が表示されません。 大きなバッチやストアド プロシージャには、複数の SET NOCOUNT ステートメントが含まれていることがあるので、SQL_SOPT_SS_NOCOUNT_STATUS が一定であると想定することはできません。 このオプションは、SQLRowCount が0を返すたびにテストする必要があります。  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 クエリ通知要求のメッセージ テキストを返します。  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr とテーブル値パラメーター  
 SQLGetStmtAttr を呼び出すと、テーブル値パラメーターを操作するときに、アプリケーションパラメーター記述子 (APD) の SQL_SOPT_SS_PARAM_FOCUS の値を取得できます。 SQL_SOPT_SS_PARAM_FOCUS の詳細については、「 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)」を参照してください。  
  
 テーブル値パラメーターの詳細については、「[テーブル値パラメーター &#40;の&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLSetStmtAttr 関数](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
