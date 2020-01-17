---
title: 非推奨の関数のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 307f0f54434fdcb4ebb19c38256a7a04f4a5c46d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990716"
---
# <a name="mapping-deprecated-functions"></a>非推奨の関数のマッピング
このセクションには、どのように非推奨の関数がについて説明します、ODBC によってマップされます*3.x* ODBC の旧バージョンとの互換性を保証するために、ドライバー マネージャー *3.x* ODBC で使用されるドライバー *2.x*アプリケーション。 ドライバー マネージャーは、アプリケーションのバージョンに関係なく、このマッピングを実行します。 ODBC の各*2.x*関数は、次の一覧は、対応する ODBC にマップされて*3.x*関数、ODBC で呼び出されると*3.x*ドライバー、ODBC *3.x*ドライバーは ODBC を実装する必要はありません*2.x*関数。  
  
 リスト内のマッピングは、ドライバーは ODBC ときにトリガーされる*3.x*ドライバーとドライバーがマップされる関数をサポートしていません。  
  
 次の表に、ODBC で導入された機能がすべての重複*3.x*します。  
  
|ODBC *2.x*関数|ODBC *3.x*関数|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**Sqlerror 関数**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt**で、*オプション*SQL_DROP の|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] この関数は、ODBC には存在しなかった場合でも*2.x*、Open Group と ISO 標準になっています。  
  
 [2] これは、ODBC 1.0 関数です。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQLAllocConnect のマッピング](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [SQLAllocEnv のマッピング](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [SQLAllocStmt のマッピング](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [SQLBindParam のマッピング](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [SQLColAttributes のマッピング](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [SQLError のマッピング](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [SQLFreeConnect のマッピング](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [SQLFreeEnv のマッピング](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [SQLFreeStmt のマッピング](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [SQLGetConnectOption のマッピング](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [SQLGetStmtOption のマッピング](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [SQLInstallTranslator のマッピング](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [SQLParamOptions のマッピング](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [SQLSetConnectOption のマッピング](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [SQLSetParam のマッピング](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [SQLSetScrollOptions のマッピング](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [SQLSetStmtOption のマッピング](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [SQLTransact のマッピング](../../../odbc/reference/appendixes/sqltransact-mapping.md)
