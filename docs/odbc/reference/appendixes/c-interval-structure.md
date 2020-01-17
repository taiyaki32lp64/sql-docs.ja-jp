---
title: C Interval 構造体 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3387b4fa48eb1a04102daadcc08f971765d7ca2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037785"
---
# <a name="c-interval-structure"></a>C Interval 構造体
表示される間隔の C データ型の[C データ型](../../../odbc/reference/appendixes/c-data-types.md)セクションでは、同じ構造を使用して、データの間隔を含めることができます。 ときに**SQLFetch**、 **SQLFetchScroll**、または**SQLGetData**が呼び出されると、ドライバー SQL_INTERVAL_STRUCT 構造にデータを返す、によって指定された値を使用して、C データ型のアプリケーション (への呼び出しで**SQLBindCol**、 **SQLGetData**、または**SQLBindParameter**) SQL_INTERVAL_STRUCT の内容を解釈するには、し、設定、 *interval_type*を構造体のフィールド、 *enum* C 型に対応する値。 ドライバーの読み取りを行わないことに注意してください、 *interval_type*間隔の種類を決定するフィールド; SQL_DESC_CONCISE_TYPE 記述子フィールドの値を取得します。 アプリケーションの値を設定する場合でも、ドライバーが、SQL_INTERVAL_STRUCT の内容を解釈する APD SQL_DESC_CONCISE_TYPE フィールドに適用することによって指定された値を使用パラメーターのデータ構造体を使用すると、ときに、 *interval_type*フィールドを別の値。  
  
 この構造体の定義は次のとおりです。  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 *Interval_type*和集合にどのような構造が保持されているアプリケーションに、SQL_INTERVAL_STRUCT のフィールドを示し、構造体のメンバーは関連することもできます。 *Interval_sign*フィールドには SQL_FALSE 値フィールドの先頭の間隔が署名されていない場合は SQL_TRUE の場合、先頭のフィールドが負の値。 先頭フィールド自体の値は、常に署名済みの値に関係なく、 *interval_sign*します。 *Interval_sign*フィールドは符号ビットとして機能します。
