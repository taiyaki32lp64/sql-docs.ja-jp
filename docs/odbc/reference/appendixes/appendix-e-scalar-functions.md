---
title: '付録 E: スカラー関数 |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb5f16485312979e9fb2ad6b3a95dacb79b695d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996175"
---
# <a name="appendix-e-scalar-functions"></a>付録 E: スカラー関数
ODBC では、この付録の対応するセクションで提供されるこれらの関数型のそれぞれについて詳しい情報のスカラー関数は、次の種類を指定します。 関数の説明には、関連する構文が含まれます。  
  
 この付録には、次のトピックが含まれています。  
  
-   [文字列関数](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [数値関数](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時刻、日付、および間隔の関数](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [システム関数](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [データ型の明示的な変換用関数](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 関数](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC を必要としません戻り値のデータ型のスカラー関数の関数は、データ ソースに固有では多くの場合、ため。 アプリケーションでは、データ型の変換を強制的に可能な限りの CONVERT スカラー関数を使用する必要があります。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC や SQL 92 のスカラー関数  
 この付録でテーブルには、SQL 92 とを連携させる ODBC 3.0 で追加された関数が含まれます。 これらの関数、ODBC で定義されているスカラー関数の特定の型の追加は、各セクションで示されます。  
  
 ODBC および SQL 92、スカラー関数を異なる方法で分類します。 ODBC スカラー関数の引数の型では、分類します。SQL 92 戻り値によって分類を実行します。 たとえば、EXTRACT 関数によって分類される timedate 関数として ODBC では、フィールドの抽出引数が datetime のキーワードで、抽出-変換元の引数が日付時刻または間隔の式であるためです。 Sql-92 は、戻り値が数値であるためその一方で、抽出と数値のスカラー関数として分類します。  
  
 アプリケーションが呼び出すことによって、ドライバーをサポートするスカラー関数を調べる**SQLGetInfo**します。 情報の種類が ODBC とスカラー関数の SQL 92 分類の両方に含まれています。 これらの分類が異なるために、ODBC および SQL 92 に対応していない情報の種類でいくつかのスカラー関数のサポートを示す可能性があります。 たとえば、ODBC での抽出のサポートは、SQL_TIMEDATE_FUNCTIONS 情報の種類。 で示されます。その一方で、抽出、sql-92 でのサポートは、SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 情報の種類で表されます。
