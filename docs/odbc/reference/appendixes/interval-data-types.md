---
title: Interval データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a42c8767228c75d3b7b0da308d739516875cf966
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947554"
---
# <a name="interval-data-types"></a>Interval データ型
間隔は、2 つの日付と時刻の差として定義されます。 間隔は、2 つの方法の 1 つで表現されます。 1 つは、*年-月*単位、年と月を表す整数の間隔を表す間隔。 もう 1 つは、*日付と時刻*日、分、および秒単位の間隔を表す間隔。 これら 2 種類の間隔は、個別か月間のさまざまな日数があるため、混在させることはできません。  
  
 間隔は、一連のフィールドで構成されます。 フィールド間の暗黙的な順序。 たとえば、年月の間隔で年か早い方を 1 か月後に。 同様に、1 日 ~ 分間隔では、フィールドは、注文日、時、分では。 間隔の種類の最初のフィールドと呼ばれる、*先頭*フィールド、または*上位*フィールド。 最後のフィールドと呼ばれる、*末尾*フィールド。  
  
 先頭のフィールドは、すべての間隔で、構成のグレゴリオ暦カレンダーのルールによって制限はありません。 たとえば、1 分間の時間間隔の時間フィールド制限はありませんは通常、0 から 23 (包括) の間で指定します。 その後、その先頭フィールドの後続のフィールドには、グレゴリオ暦の通常の制約に従ってください。 詳細については、次を参照してください。[グレゴリオ暦の制約](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)、この付録で後述します。  
  
 13 interval SQL データ型と 13 interval C データ型があります。 間隔の C データ型のそれぞれは、間隔のデータを含む SQL_INTERVAL_STRUCT、同じ構造を使用します。 (詳細については、次のセクションを参照してください[C Interval 構造体](../../../odbc/reference/appendixes/c-interval-structure.md)。)。SQL データ型の詳細については、次を参照してください。 [SQL データ型](../../../odbc/reference/appendixes/sql-data-types.md)C のデータ型の詳細についてを参照してください。 [C データ型](../../../odbc/reference/appendixes/c-data-types.md)します。  
  
|型識別子|クラス|説明|  
|---------------------|-----------|-----------------|  
|[MONTH]|年月|2 つの日付間の月の数。|  
|[YEAR]|年月|2 つの日付間の年の数。|  
|YEAR_TO_MONTH|年月|年と 2 つの日付間の月の数。|  
|[DAY]|日付と時刻|2 つの日付までの日数の数。|  
|[HOUR]|日付と時刻|日付/時刻の 2 つの間の時間数。|  
|[MINUTE]|日付と時刻|日付/時刻の 2 つの間隔を分単位の数。|  
|[SECOND]|日付と時刻|日付/時刻の 2 つの間の秒数。|  
|DAY_TO_HOUR|日付と時刻|日付/時刻の 2 つの間の日数/時間数。|  
|DAY_TO_MINUTE|日付と時刻|2 つの日、時間と分の日付/時刻。|  
|DAY_TO_SECOND|日付と時刻|日/時間/分/秒間に 2 つの日付/時刻。|  
|HOUR_TO_MINUTE|日付と時刻|日付/時刻の 2 つの分単位の時間数。|  
|HOUR_TO_SECOND|日付と時刻|2 つの時間、分/秒の日付/時刻。|  
|MINUTE_TO_SECOND|日付と時刻|分/秒間に 2 つの日付/時刻。|  
  
 このセクションでは、次のトピックを扱います。  
  
-   [C Interval 構造体](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Interval データ型の精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Interval データ型の長さ](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Interval のリテラル](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Interval データ型での既定の先頭有効桁数と秒小数部分のオーバーライド](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
