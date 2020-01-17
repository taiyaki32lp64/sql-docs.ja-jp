---
title: 列のサイズ、転送オクテット長、10 進数字の表示のサイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8d7f1b8ec5647a34b09f0636fc8fcc2ad070f72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019239"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>列のサイズ、10 進数字は、転送オクテット長、および ODBC のサイズを表示
データ型は、特性は、その列 (またはパラメーター) のサイズ、10 進桁数、長さ、およびサイズを表示します。 次の ODBC 関数では、データ ソースの SQL ステートメント内のパラメーターまたは SQL データ型をこれらの属性を返します。 各 ODBC 関数では、次のように、これらの属性の別のセットを返します。  
  
-   **SQLDescribeCol**列について説明しますが、列のサイズと 10 進数の桁を返します。  
  
-   **SQLDescribeParam**パラメーターについて説明しますが、パラメーターのサイズと 10 進数の桁を返します。 **SQLBindParameter** SQL ステートメントのパラメーターのサイズと 10 進数字のパラメーターを設定します。  
  
-   カタログ関数**SQLColumns**、 **SQLProcedureColumns**、および**SQLGetTypeInfo**テーブル、結果セット、またはプロシージャのパラメーターの列の属性を返すとデータ ソース内のデータ型のカタログ属性。 **SQLColumns** (など、ベース テーブル、ビュー、またはシステム テーブル) の指定したテーブルに列のサイズ、10 進数字、および列の長さを返します。 **SQLProcedureColumns**プロシージャで列のサイズ、10 進数字、および列の長さを返します。 **SQLGetTypeInfo**データ ソースの列の最大サイズと SQL のデータ型の最小値と最大 10 進数字を返します。  
  
 列のこれらの関数によって返される値またはパラメーターのサイズは"precision"として ODBC 2 で定義されているに対応します。*x*します。 ただし、値、必ずしも対応しません SQL_DESC_PRECISION またはその他の任意の 1 つの記述子フィールドで返される値。 "Scale"として ODBC 2 で定義されているに対応する 10 進数の数字も同様です。*x*します。 SQL_DESC_SCALE またはその他の 1 つ記述子フィールドで返される値は必ずしも対応しませんが、データ型に応じて異なる記述子フィールドから取得します。 詳細については、次を参照してください。[列サイズ](../../../odbc/reference/appendixes/column-size.md)と[10 進数字](../../../odbc/reference/appendixes/decimal-digits.md)します。  
  
 同様に、転送オクテット長の値は、SQL_DESC_LENGTH からは提供されません。 すべての文字やバイナリ型の記述子フィールドの SQL_DESC_OCTET_LENGTH から取得します。 その他の種類には、この情報を保持する記述子フィールドはありません。  
  
 すべてのデータ型の表示サイズの値は、SQL_DESC_DISPLAY_SIZE、1 つの記述子フィールドの値に対応します。  
  
 記述子フィールドは、結果セットの特性を記述します。 記述子フィールドには、ステートメントの実行前にデータの有効な値はありません。 列の値のサイズを 10 進数字とによって返されるサイズを表示**SQLColumns**、 **SQLProcedureColumns**、および**SQLGetTypeInfo**、他に戻り、渡すデータ ソースのカタログ内に存在するテーブルの列と、データ型などのデータベース オブジェクトの特性。 同様に、その結果セットで**SQLColAttribute**列のサイズ、10 進数字、およびデータ ソースの列の転送オクテット長を返しますこれらの値は必ずしも SQL_DESC_PRECISION、sql _ の値と同じです。DESC_SCALE、および SQL_DESC_OCTET_LENGTH 記述子フィールド。  
  
 これらの記述子フィールドの詳細については、次を参照してください。 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。  
  
 関連項目:  
  
-   [列サイズ](../../../odbc/reference/appendixes/column-size.md)  
-   [10 進数字](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [転送オクテット長](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [表示サイズ](../../../odbc/reference/appendixes/display-size.md)
