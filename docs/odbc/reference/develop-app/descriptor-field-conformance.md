---
title: 記述子フィールドの適合性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afdb1f18ad641224d13373436dd58f1919a3d280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952346"
---
# <a name="descriptor-field-conformance"></a>記述子フィールドの適合性
次の表では、各 ODBC 記述子のヘッダー フィールド、これは適切に定義されたの準拠レベルを示します。  
  
|関数|準拠レベル|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|(APD、IPR とコア IRD)。レベル 1 (ARD)|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 次の表では、各 ODBC 記述子レコード フィールド、これは適切に定義されたの準拠レベルを示します。  
  
|関数|準拠レベル|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|レベル 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|レベル 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|レベル 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|SQL_DESC_DATETIME_INTERVAL_ コード|[1] のコア|  
|SQL_DESC_DATETIME_INTERVAL_ 精度|[1] のコア|  
|SQL_DESC_DISPLAY_SIZE|Core|  
|SQL_DESC_FIXED_PREC_SCALE|Core|  
|SQL_DESC_INDICATOR_PTR|Core|  
|SQL_DESC_LABEL|レベル 2|  
|SQL_DESC_LENGTH|Core|  
|SQL_DESC_LITERAL_PREFIX|Core|  
|SQL_DESC_LITERAL_SUFFIX|Core|  
|SQL_DESC_LOCAL_TYPE_NAME|Core|  
|SQL_DESC_NAME|Core|  
|SQL_DESC_NULLABLE|Core|  
|SQL_DESC_OCTET_LENGTH|Core|  
|SQL_DESC_OCTET_LENGTH_PTR|Core|  
|SQL_DESC_PARAMETER_TYPE|コア/レベル 2 [2]|  
|SQL_DESC_PRECISION|Core|  
|SQL_DESC_ROWVER|レベル 1|  
|SQL_DESC_SCALE|Core|  
|SQL_DESC_SCHEMA_NAME|レベル 1|  
|SQL_DESC_SEARCHABLE|Core|  
|SQL_DESC_TABLE_NAME|レベル 1|  
|SQL_DESC_TYPE|Core|  
|SQL_DESC_TYPE_NAME|Core|  
|SQL_DESC_UNNAMED|Core|  
|SQL_DESC_UNSIGNED|Core|  
|SQL_DESC_UPDATABLE|Core|  
  
 [これらのレコードのフィールドのサポート 1] は、ドライバーは、該当するデータ型をサポートしている場合にのみ必要です。  
  
 [2] のコア レベルへの準拠、ドライバーは SQL_PARAM_INPUT をサポートする必要があります。 レベル 2 インターフェイスの適合性のドライバーで SQL_PARAM_INPUT_OUTPUT と SQL_PARAM_OUTPUT もサポートする必要があります。
