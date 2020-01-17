---
title: 暗黙のカーソル変換 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e62604404c83e7780d50438a485910e5af4d4f05
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784374"
---
# <a name="implicit-cursor-conversions-odbc"></a>暗黙のカーソル変換 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  アプリケーションでは、 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を使用してカーソルの種類を要求した後、要求された種類のサーバーカーソルでサポートされていない SQL ステートメントを実行できます。 **Sqlexecute**または**SQLExecDirect**を呼び出すと SQL_SUCCESS_WITH_INFO が返され、 **SQLGetDiagRec**はを返します。  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 アプリケーションでは、SQL_CURSOR_TYPE に設定された**SQLGetStmtOption**を呼び出すことによって現在使用されているカーソルの種類を特定できます。 カーソルの種類の変換は、1 つのステートメントにのみ適用されます。 次の**SQLExecDirect**または**sqlexecute**は、元のステートメントのカーソル設定を使用して実行されます。  
  
## <a name="see-also"></a>参照  
 [カーソルプログラミングの&#40;詳細 ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
