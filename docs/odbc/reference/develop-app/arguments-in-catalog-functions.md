---
title: カタログ関数の引数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 649c00f1db486dab4a996138be4e26b0e270fbae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106293"
---
# <a name="arguments-in-catalog-functions"></a>カタログ関数の引数
すべてのカタログ関数では、アプリケーションが返されるデータのスコープを制限する引数を受け取ります。 最初と 2 つ目の呼び出しなど**SQLTables** 3 番目の呼び出しは、Orders テーブルに関する情報を返すときに、すべてのテーブルに関する情報を含む結果セットを返す、次のコード。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 カタログ関数の文字列引数が 4 つの種類に分類されます。 通常の引数 (OA)、パターンの引数 (PV) の値、id の引数 (ID)、および値リストの引数 (ボリューム ライセンス)。 ほとんどの文字列引数は、SQL_ATTR_METADATA_ID ステートメント属性の値に応じて、2 つのさまざまな種類のいずれかの指定できます。 次の表では、各カタログ関数の引数の一覧し、SQL_ATTR_METADATA_ID の値を SQL_TRUE または SQL_FALSE の引数の型について説明します。  
  
|関数|引数|ときに、型 sql _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE になります|ときに、型 sql _<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID ID の ID の ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID ID の ID の ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID の ID の ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID の ID の ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID ID の ID の ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID の ID の ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID の ID の ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID の ID の ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID の ID の ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV ボリューム ライセンス|ID ID の ID のボリューム ライセンス|  
  
 このセクションでは、次のトピックを扱います。  
  
-   [通常の引数](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [パターン値の引数](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [識別子の引数](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [値リストの引数](../../../odbc/reference/develop-app/value-list-arguments.md)
