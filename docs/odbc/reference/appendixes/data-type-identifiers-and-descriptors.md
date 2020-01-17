---
title: データ型識別子と記述子 |Microsoft Docs
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 748f2452d20b618ae0011e2e1ac4e24af098ac06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019048"
---
# <a name="data-type-identifiers-and-descriptors"></a>データ型識別子と記述子
データの種類の一覧を[SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)と[C データ型](../../../odbc/reference/appendixes/c-data-types.md)前のセクションでは「簡潔な」のデータ型。各識別子は、1 つのデータ型を参照します。 Id とデータ型の間、一対一で対応します。 すべてのケースでは、1 つの値を使用して、データ型を識別するために、記述子がではなく行うただし。 場合によっては、"verbose"のデータ型と型サブコード使用します。 Datetime と間隔のデータ型を除くすべてのデータ型の詳細な型の識別子は、簡潔なタイプ識別子と同じと SQL_DESC_DATETIME_INTERVAL_CODE の値は 0 にします。 Datetime と間隔のデータ型のただし、(SQL_DATETIME または SQL_INTERVAL) の詳細な型に格納 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE で簡潔な型が格納されているされ SQL_DESC_DATETIME_INTERVAL_CODE に簡潔な各種のサブコードが格納されています。 これらのフィールドのいずれかを設定すると、他に影響します。 これらのフィールドの詳細については、次を参照してください。、 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)関数の説明。  
  
 一部のデータ型の SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE またはフィールドを設定すると、SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_LENGTH、SQL_DESC_PRECISION、および SQL_DESC_SCALE フィールドはデータの該当する場合の既定値に自動的に設定します。入力します。 詳細については、の SQL_DESC_TYPE フィールドの説明を参照してください。 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。 既定値の設定のいずれかの情報が適切でない場合、アプリケーションへの呼び出しを通じて記述子フィールドに明示的に設定する必要があります**SQLSetDescField**します。  
  
 次の表は、簡潔なタイプ識別子、詳細な型の識別子、および各 datetime と SQL の間隔、および C 型識別子の型のサブコードを示します。 SQL_DESC_TYPE と SQL_DESC_DATETIME_INTERVAL_CODE フィールドに同じマニフェスト定数 (実装記述子) での SQL データ型と (アプリケーションでの C データ型の両方がある datetime と間隔のデータ型のこの表に示すよう記述子)。  
  
|SQL の簡潔な型|簡潔な C 型|詳細な型|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
