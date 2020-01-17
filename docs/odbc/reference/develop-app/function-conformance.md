---
title: 関数への準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45eb427b660496430334633b5d43ee8989211c0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069755"
---
# <a name="function-conformance"></a>関数の適合性
次の表では、これが適切に定義されている各 ODBC 関数の準拠レベルを示します。  
  
|関数|準拠レベル|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|[1] のコア|  
|**SQLBrowseConnect**|レベル 1|  
|**SQLBulkOperations**|レベル 1|  
|**SQLCancel**|[1] のコア|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|[1] のコア|  
|**SQLColumnPrivileges**|レベル 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|[1] のコア|  
|**SQLDescribeParam**|レベル 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|[1] のコア|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|[1] のコア|  
|**SQLForeignKeys**|レベル 2|  
|**SQLFreeHandle**|Core|  
|**SQLFreeStmt**|Core|  
|**SQLGetConnectAttr**|Core|  
|**SQLGetCursorName**|Core|  
|**SQLGetData**|Core|  
|**SQLGetDescField**|Core|  
|**SQLGetDescRec**|Core|  
|**SQLGetDiagField**|Core|  
|**SQLGetDiagRec**|Core|  
|**SQLGetEnvAttr**|Core|  
|**SQLGetFunctions**|Core|  
|**SQLGetInfo**|Core|  
|**SQLGetStmtAttr**|Core|  
|**SQLGetTypeInfo**|Core|  
|**SQLMoreResults**|レベル 1|  
|**SQLNativeSql**|Core|  
|**SQLNumParams**|Core|  
|**SQLNumResultCols**|Core|  
|**SQLParamData**|Core|  
|**SQLPrepare**|Core|  
|**SQLPrimaryKeys**|レベル 1|  
|**SQLProcedureColumns**|レベル 1|  
|**SQLProcedures**|レベル 1|  
|**SQLPutData**|Core|  
|**SQLRowCount**|Core|  
|**SQLSetConnectAttr**|[2] のコア|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|[1] のコア|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|[2] のコア|  
|**SQLSetPos**|レベル 1 [1]|  
|**SQLSetStmtAttr**|[2] のコア|  
|**SQLSpecialColumns**|[1] のコア|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|レベル 2|  
|**SQLTables**|Core|  
  
 [この関数の 1] 重要な機能は、適合性の高いレベルでのみ利用します。  
  
 [2] を既定以外の値に特定の属性を設定すると、準拠のレベルに依存します。 詳細については、次のセクションを参照してください。[属性の適合性](../../../odbc/reference/develop-app/attribute-conformance.md)します。
