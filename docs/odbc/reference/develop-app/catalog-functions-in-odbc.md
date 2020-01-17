---
title: ODBC のカタログ関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8cd46fbc8f633ef31f00fa60ced885f9455f185
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062729"
---
# <a name="catalog-functions-in-odbc"></a>ODBC のカタログ関数
ODBC には、次のカタログ関数が含まれています。  
  
|関数|説明|  
|--------------|-----------------|  
|**SQLTables**|データ ソースのカタログ、スキーマ、テーブル、またはテーブル型の一覧を返します。|  
|**SQLColumns**|1 つまたは複数のテーブルの列の一覧を返します。|  
|**SQLStatistics**|1 つのテーブルに関する統計情報の一覧を返します。 そのテーブルに関連付けられているインデックスの一覧を返します。|  
|**SQLSpecialColumns**|1 つのテーブル内の行を一意に識別する列の一覧を返します。 自動的に更新されるテーブルの列の一覧を返します。|  
|**SQLPrimaryKeys**|1 つのテーブルの主キーを構成する列の一覧を返します。|  
|**SQLForeignKeys**|1 つのテーブルまたはその他の 1 つのテーブルを参照するテーブルの外部キーの一覧で、外部キーの一覧を返します。|  
|**SQLTablePrivileges**|1 つまたは複数のテーブルに関連付けられた権限の一覧を返します。|  
|**SQLColumnPrivileges**|1 つのテーブル内 1 つまたは複数の列に関連付けられている権限の一覧を返します。|  
|**SQLProcedures**|データ ソース内には、プロシージャの一覧を返します。|  
|**SQLProcedureColumns**|1 つのプロシージャの結果セットでは、入力と出力パラメーター、戻り値、および列の一覧を返します。|  
|**SQLGetTypeInfo**|データ ソースでサポートされている SQL データ型の一覧を返します。 通常、これらのデータ型で使用**CREATE TABLE**と**ALTER TABLE**ステートメント。|  
  
 **SQLTables**、 **SQLColumns**、 **SQLStatistics**、および**SQLSpecialColumns**開いてグループ CLI、およびに準拠して**SQLGetTypeInfo** 92 CLI ISO に準拠している、ほとんどのドライバーによって実装されます。 ODBC 準拠のレベルは、残りのカタログ関数です。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [カタログ関数によって返されるデータ](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [スキーマ ビュー](../../../odbc/reference/develop-app/schema-views.md)
