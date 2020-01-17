---
title: ヘッダー ファイル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d20f2535038b13eac0b8d5ca20dfa77bfc12588
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139029"
---
# <a name="header-files"></a>ヘッダー ファイル
Sql.h ヘッダー ファイルには、主要な ODBC インターフェイスへの準拠レベルの機能のプロトタイプが含まれています。 Sqlext.h ヘッダー ファイルには、レベル 1 およびレベル 2 API の適合性レベルで機能のプロトタイプが含まれています。 Sqltypes.h ヘッダー ファイルには、型の定義と、SQL データ型のインジケーターが含まれています。  
  
 すべてを含むヘッダー ファイル、 **#define**ODBCVER、アプリケーション、ドライバーは ODBC のさまざまなバージョン用にコンパイルするのに設定できます。  
  
 ヘッダー ファイルには開いてグループ CLI と ISO CLI でアラインするにはへの呼び出しで使用される情報の種類のエイリアスが含まれて**SQLGetInfo**します。 次の表には、「ODBC 名」列はで情報の種類を ODBC の名前を示します。 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)します。 列「ヘッダー ファイル内の別名」では、ISO CLI と開いているグループ CLI で使用される名前を示します。 これらのマニフェスト名の実際の数値は、ODBC と標準の Cli の両方で同じです。 これらの別名には、ODBC を使用してコンパイルするには、標準に準拠したアプリケーションまたはドライバーが有効にする*3.x*ヘッダー ファイル。  
  
 これらの別名には、名前がわかりやすくなるように、ODBC 名での省略形の拡張が含まれます。 "OUTER_JOIN"に"MULTIPLE"、"OJ"を「トランザクションです」に「トランザクション」に、"MAX"を"MAXIMUM"、"LEN"に"LENGTH"、"MULT"に拡張します。  
  
|ODBC の名前|ヘッダー ファイル内の別名|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
