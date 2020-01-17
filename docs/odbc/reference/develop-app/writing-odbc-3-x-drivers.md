---
title: ODBC 3.x ドライバーの記述 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078906"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x ドライバーの作成
次の表は、ODBC 3 関数のサポートを示します。*x*ドライバーおよび ODBC アプリケーションでは、マッピング関数が、ODBC 3 に対して呼び出されたときに、ドライバー マネージャーによってを実行します *。x*ドライバー。  
  
|関数|Supported<br /><br /> で、<br /><br /> ODBC 3。*x*<br /><br /> ドライバーですか。|Supported<br /><br /> で、<br /><br /> ODBC 3。*x*<br /><br /> アプリケーションか。|マップされている/サポートされています<br /><br /> ODBC 3。*x*<br /><br /> ドライバー マネージャー<br /><br /> ODBC 3 の場合。*x*ドライバーですか?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|いいえ|[1]|[はい]|  
|**SQLAllocEnv**|いいえ|[1]|はい|  
|**SQLAllocHandle**|はい|[はい]|いいえ|  
|**SQLAllocStmt**|いいえ|[1]|はい|  
|**SQLBindCol**|はい|[はい]|いいえ|  
|**SQLBindParam**|いいえ|[はい] [2]|はい|  
|**SQLBindParameter**|はい|[はい]|いいえ|  
|**SQLBrowseConnect**|はい|[はい]|いいえ|  
|**SQLBulkOperations**|[はい]|[はい]|いいえ|  
|**SQLCancel**|はい|[はい]|いいえ|  
|**SQLCloseCursor**|はい|[はい]|いいえ|  
|**SQLColAttribute**|はい|[はい]|いいえ|  
|**SQLColAttributes**|No[3]|いいえ|はい|  
|**SQLColumnPrivileges**|はい|[はい]|いいえ|  
|**SQLColumns**|はい|[はい]|いいえ|  
|**SQLConnect**|[はい]|[はい]|いいえ|  
|**SQLCopyDesc**|はい|はい|[はい] [4]|  
|**SQLDataSources**|いいえ|はい|はい|  
|**SQLDescribeCol**|[はい]|[はい]|いいえ|  
|**SQLDescribeParam**|[はい]|[はい]|いいえ|  
|**SQLDisconnect**|はい|[はい]|いいえ|  
|**SQLDriverConnect**|はい|[はい]|いいえ|  
|**SQLDrivers**|いいえ|はい|はい|  
|**SQLEndTran**|[はい]|[はい]|いいえ|  
|**Sqlerror 関数**|いいえ|[1]|はい|  
|**SQLExecDirect**|はい|[はい]|いいえ|  
|**SQLExecute**|[はい]|[はい]|いいえ|  
|**SQLExtendedFetch**|[はい]|いいえ|いいえ|  
|**SQLFetch**|はい|[はい]|いいえ|  
|**SQLFetchScroll**|[はい]|[はい]|いいえ|  
|**SQLForeignKeys**|はい|[はい]|いいえ|  
|**SQLFreeConnect**|いいえ|[はい] [1]|[はい]|  
|**SQLFreeEnv**|いいえ|[はい] [1]|はい|  
|**SQLFreeHandle**|はい|[はい]|いいえ|  
|**SQLFreeStmt**|[はい]|[はい]|いいえ|  
|**SQLGetConnectAttr**|はい|[はい]|いいえ|  
|**SQLGetConnectOption**|[5]|[1]|[はい]|  
|**SQLGetCursorName**|はい|[はい]|いいえ|  
|**SQLGetData**|[はい]|[はい]|いいえ|  
|**SQLGetDescField**|はい|[はい]|いいえ|  
|**SQLGetDescRec**|[はい]|[はい]|いいえ|  
|**SQLGetDiagField**|はい|[はい]|いいえ|  
|**SQLGetDiagRec**|はい|[はい]|いいえ|  
|**SQLGetEnvAttr**|[はい]|[はい]|いいえ|  
|**SQLGetFunctions**|No[6]|[はい]|[はい]|  
|**SQLGetInfo**|はい|[はい]|いいえ|  
|**SQLGetStmtAttr**|はい|[はい]|いいえ|  
|**SQLGetStmtOption**|[5]|[1]|はい|  
|**SQLGetTypeInfo**|はい|[はい]|いいえ|  
|**SQLMoreResults**|はい|[はい]|いいえ|  
|**SQLNativeSql**|[はい]|[はい]|いいえ|  
|**SQLNumParams**|はい|[はい]|いいえ|  
|**SQLNumResultCols**|[はい]|[はい]|いいえ|  
|**SQLParamData**|[はい]|[はい]|いいえ|  
|**SQLParamOptions**|いいえ|いいえ|[はい]|  
|**SQLPrepare**|はい|[はい]|いいえ|  
|**SQLPrimaryKeys**|[はい]|[はい]|いいえ|  
|**SQLProcedureColumns**|はい|[はい]|いいえ|  
|**SQLProcedures**|はい|[はい]|いいえ|  
|**SQLPutData**|はい|[はい]|いいえ|  
|**SQLRowCount**|[はい]|[はい]|いいえ|  
|**SQLSetConnectAttr**|[はい]|[はい]|いいえ|  
|**SQLSetConnectOption**|[5]|[1]|[はい]|  
|**SQLSetCursorName**|はい|[はい]|いいえ|  
|**SQLSetDescField**|はい|[はい]|いいえ|  
|**SQLSetDescRec**|はい|[はい]|いいえ|  
|**SQLSetEnvAttr**|はい|[はい]|いいえ|  
|**SQLSetPos**|[はい]|[はい]|いいえ|  
|**SQLSetParam**|いいえ|いいえ|はい|  
|**SQLSetScrollOption**|はい|[はい]|いいえ|  
|**SQLSetStmtAttr**|はい|[はい]|いいえ|  
|**SQLSetStmtOption**|[5]|[1]|はい|  
|**SQLSpecialColumns**|はい|[はい]|いいえ|  
|**SQLStatistics**|はい|[はい]|いいえ|  
|**SQLTablePrivileges**|はい|[はい]|いいえ|  
|**SQLTables**|はい|[はい]|いいえ|  
|**SQLTransact**|いいえ|[1]|はい|  
  
 [1] この関数は、ODBC 3 で非推奨とされます。*x*します。 ODBC 3。*x*アプリケーションは、この関数を使用する必要があります。 ただし、Open Group、または CLI の ISO 準拠のアプリケーションは、この関数を呼び出すことができます。  
  
 [2] ODBC 3。*x*アプリケーションを使用する必要があります**SQLBindParameter**の代わりに**SQLBindParam**します。 ただし、Open Group、または CLI の ISO 準拠のアプリケーションは、この関数を呼び出すことができます。  
  
 [3] のドライバーの作成者はに注意してください、ODBC 2。*x*で SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE、および SQL_COLUMN_LENGTH をサポートする必要があります列属性**SQLColAttribute**します。  
  
 [4] **SQLCopyDesc**記述子をさまざまなドライバーに属する接続間でコピーするときにドライバー マネージャーによってが部分的に実装します。 ドライバーは、サポートに必要な**SQLCopyDesc**は独自の接続の 2 つの間で。 などの関数**SQLDrivers**、ドライバー マネージャーによってのみ実装されていますが、この一覧に表示されません。  
  
 [特定の状況下で 5]、ドライバーは、この関数をサポートする必要があります。 詳細については、この関数のリファレンス ページを参照してください。  
  
 [6]、ドライバーをサポートするために選択できます**SQLGetFunctions**ドライバーでサポートされる関数のセットは異なる接続から接続する場合。
