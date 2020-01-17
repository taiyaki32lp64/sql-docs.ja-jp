---
title: 明示的なデータ型変換関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6982f7b7caa71abc08c5b84ef1bb6211dcadaecd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913610"
---
# <a name="explicit-data-type-conversion-function"></a>データ型の明示的な変換用関数
SQL データ型の定義では、明示的なデータ型の変換を指定します。  
  
 明示的なデータ型の変換関数の ODBC 構文では、変換は制限されません。 1 つのデータ型の別のデータ型への特定の変換の有効性は、各ドライバー固有の実装によって決定されます。 ドライバーは、ネイティブの構文に ODBC 構文を変換として拒否される ODBC 構文では有効ですが、データ ソースでサポートされていない変換のします。 ODBC 関数**SQLGetInfo**、変換 (SQL_CONVERT_BIGINT、SQL_CONVERT_BINARY、SQL_CONVERT_INTERVAL_YEAR_MONTH、具合) などのオプションは、データ ソースでサポートされている変換について照会する方法を提供します.  
  
 形式、**変換**関数は。  
  
 **変換 (** _value_exp_、 _data_type_ **)**  
  
 指定された値を返します*value_exp*を指定した変換*data_type*ここで、 *data_type*は、次のキーワードの 1 つです。  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 明示的なデータ型の変換関数の ODBC 構文は、変換形式の仕様をサポートしていません。 明示的な形式の仕様は、基になるデータ ソースでサポートされていますが場合、ドライバーが既定値を指定または形式の仕様を実装する必要があります。  
  
 引数*value_exp*列名、または指定できます、もう 1 つのスカラー関数、または数値の結果の文字列リテラル。 以下に例を示します。  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 CURDATE スカラー関数の出力を文字列に変換します。  
  
 ODBC からの戻り値のデータ型を必要としませんので、スカラー関数 (関数は、データ ソースに固有では多くの場合) ため、アプリケーションは、データ型の変換を強制的に可能な限りの CONVERT スカラー関数を使用する必要があります。  
  
 次の 2 つの例の使用方法を示します、**変換**関数。 これらの例は、型 SQL_SMALLINT の EMPNO 列および SQL_CHAR 型の EMPNAME 列で、従業員をという名前のテーブルの存在を想定しています。  
  
 場合は、アプリケーションは、次の SQL ステートメントを指定します。  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 用のドライバーでは、SQL ステートメントを変換します。  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server 用のドライバーでは、SQL ステートメントを変換します。  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 場合は、アプリケーションは、次の SQL ステートメントを指定します。  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 用のドライバーでは、SQL ステートメントを変換します。  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server 用のドライバーでは、SQL ステートメントを変換します。  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 用のドライバーでは、SQL ステートメントに変換します。  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
