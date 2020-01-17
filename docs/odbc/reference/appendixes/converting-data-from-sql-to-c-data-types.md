---
title: SQL から C データ型にデータを変換する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95a44698c12abf0de64c8d6f7d316e9156dc139c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019109"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>SQL から C データ型へのデータ変換
アプリケーションを呼び出すと**SQLFetch**、 **SQLFetchScroll**、または**SQLGetData**ドライバーは、データ ソースからデータを取得します。 かどうか、必要に応じて、データ変換から変換で指定されたデータ型には、ドライバーによってを取得するデータ型、 *TargetType*引数**SQLBindCol**または**SQLGetData します。** 最後に、によって示される場所にデータを格納、 *TargetValuePtr*引数**SQLBindCol**または**SQLGetData** (および、ARD の SQL_DESC_DATA_PTR フィールド)。  
  
 次の表は、ODBC SQL からサポートされている変換にデータ型を ODBC C データ型を示します。 塗りつぶされた円は、SQL データ型の既定の変換を示します (をデータが変換されるときに、C データ型の値*TargetType* SQL_C_DEFAULT が)。 白抜きの円では、サポートされている変換を示します。  
  
 ODBC の*3.x* odbc 作業アプリケーション*2.x*ドライバー、ドライバー固有のデータ型がサポートされていない可能性がありますから変換します。  
  
 変換後のデータの形式は、Windows® 国設定の影響を受けません。  
  
 次のセクションでの表では、ドライバーまたはデータ ソースがデータ ソースから取得されたデータに変換する方法について説明しますドライバーがサポートする ODBC SQL データ型からすべての ODBC C データ型への変換をサポートするために必要です。 テーブルの最初の列の特定の ODBC SQL データ型の有効な入力値を一覧表示、 *TargetType*引数**SQLBindCol**と**SQLGetData**します。 2 番目の列を使用して多くの場合、テストの結果を一覧表示、 *BufferLength*引数で指定された**SQLBindCol**または**SQLGetData**へのドライバーを実行します。データを変換できるかどうかを決定します。 3 番目と 4 番目の列で指定されたバッファーに配置された値の一覧、各結果に対して、 *TargetValuePtr*と*StrLen_or_IndPtr*で指定された引数**SQLBindCol**または**SQLGetData**後、ドライバーが、データを変換しようとしています。 (、 *StrLen_or_IndPtr*引数、ARD の SQL_DESC_OCTET_LENGTH_PTR フィールドに対応します)。最後の列の一覧の各結果によって返される SQLSTATE **SQLFetch**、 **SQLFetchScroll**、または**SQLGetData**します。  
  
 場合、 *TargetType*引数**SQLBindCol**または**SQLGetData**しない指定の ODBC SQL データ型の表に示した ODBC C データ型の識別子を含む**SQLFetch**、 **SQLFetchScroll**、または**SQLGetData** SQLSTATE 07006 が返されます (制限付きのデータ型は属性の違反)。 場合、 *TargetType*引数には、ドライバー固有の SQL データ型から ODBC C データ型への変換を指定する識別子が含まれ、ドライバーでは、この変換はサポートされていない**SQLFetch**、**SQLFetchScroll**、または**SQLGetData** SQLSTATE HYC00 を返します (省略可能な機能が実装されていません)。  
  
 テーブルには表示されません、ドライバーで指定したバッファーの SQL_NULL_DATA を返します、 *StrLen_or_IndPtr*引数 SQL のデータ値が NULL の場合。 使用の詳細については*StrLen_or_IndPtr*データを取得するは、複数の呼び出しが行われるを参照してください、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)関数の説明。 文字数が返される SQL のデータが文字データに変換されると、 \* *StrLen_or_IndPtr* null 終了バイトには含まれません。 場合*TargetValuePtr* null ポインターの場合は、 **SQLGetData** SQLSTATE HY009 を返します (null ポインターの無効な使用)、 **SQLBindCol**、バインドは解除され、列。  
  
 次の用語と規則は、テーブルで使用されます。  
  
-   **データのバイト長**で返される使用可能な C データのバイト数は、**TargetValuePtr*アプリケーションに返される前に、データは切り捨てられますかどうか。 文字列データは、これに null 終端文字のための領域は含まれません。  
  
-   **バイトの長さを文字**文字形式でデータを表示するために必要なバイト数の合計です。 これは、セクションでは C データ型ごとに定義されている[表示サイズ](../../../odbc/reference/appendixes/display-size.md)バイト長の文字が文字では、表示サイズ、(バイト単位) がある点が、します。  
  
-   単語*斜体*関数の引数または SQL 文法の要素を表します。 文法要素の構文を参照してください[付録 c:。SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQL c: から文字](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL c: から数値](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL c: からビット](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL c: からバイナリ](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL c: から日付](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL c: からGUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL c: から時間](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL c: からタイムスタンプ](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL c: から年月の間隔](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL c: から日付と時刻の間隔](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL から C へのデータ変換の例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
