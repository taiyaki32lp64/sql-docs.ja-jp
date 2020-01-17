---
title: Datetime データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cb92afa9467717b8a589ddbcaee4ab8a5a529f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130091"
---
# <a name="datetime-data-types"></a>Datetime データ型
ODBC で*3.x*、識別子を日付、時刻、および timestamp SQL データ型は、SQL_DATE、SQL_TIME、および SQL_TIMESTAMP から変更された (のインスタンスと **#define** 9、10、および 11 のヘッダー ファイルで) に sql _TYPE_DATE、SQL_TYPE_TIME、および SQL_TYPE_TIMESTAMP (のインスタンスと **#define** 91、92、および 93 のヘッダー ファイルで)、それぞれします。 識別子から変更されている SQL_C_DATE、SQL_C_TIME、および SQL_C_TIMESTAMP SQL_C_TYPE_DATE、SQL_C_TYPE_TIME、SQL_C_TYPE_TIMESTAMP では、それぞれ、対応する C 型とインスタンスの **#define**が変更されました。それに応じて。  
  
 ODBC での SQL の datetime データ型の列のサイズと 10 進数字が返される*3.x*は odbc に返される有効桁数と小数点と同じ*2.x*します。 これらの値は、SQL_DESC_PRECISION および SQL_DESC_SCALE 記述子フィールドの値と異なります。 (詳細については、次を参照してください[列のサイズ、10 進数字、転送オクテット長、および表示サイズ](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)付録 d:。データ型です。)  
  
 これらの変更に影響を与える**SQLDescribeCol**、 **SQLDescribeParam**、および**SQLColAttributes**;**SQLBindCol**、 **SQLBindParameter**、および**SQLGetData**; と**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLStatistics**、および**SQLSpecialColumns**します。  
  
 ODBC *3.x*ドライバーが SQL_ATTR_ODBC_VERSION 環境属性の設定に従って、前の段落で表示されている関数の呼び出しを処理します。 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLSpecialColumns**、および**SQLStatistics**SQL_ATTR_ODBC_VERSION に設定されて SQL_OV_ODBC3、関数の戻り値 SQL_TYPE_DATE、SQL_TYPE_TIME、および SQL_TYPE_TIMESTAMP DATA_TYPE フィールドの場合は、します。 COLUMN_SIZE 列 (によって返される結果セットで**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、および**SQLSpecialColumns**)おおよその数値型のバイナリ有効桁数が含まれています。 NUM_PREC_RADIX 列 (によって返される結果セットで**SQLColumns**、 **SQLGetTypeInfo**、および**SQLProcedureColumns**) 2 の値が含まれています。 COLUMN_SIZE 列には SQL_ATTR_ODBC_VERSION 設定されている場合 SQL_OV_ODBC2、し、関数、戻り値の SQL_DATE、SQL_TIME、および SQL_TIMESTAMP DATA_TYPE フィールドで、おおよその数値型と NUM_PREC_RADIX 列の小数点以下有効桁数が含まれています10 の値が含まれています。  
  
 呼び出しですべてのデータ型を要求するときに**SQLGetTypeInfo**、ODBC で定義されているに、関数によって返される結果セットが SQL_TYPE_DATE、SQL_TYPE_TIME、および SQL_TYPE_TIMESTAMP の両方を格納する*3.x*、SQL_DATE、SQL_TIME、および ODBC で定義されている SQL_TIMESTAMP *2.x*します。  
  
 方法により、ODBC *3.x*ドライバー マネージャーは、日付、時刻、タイムスタンプ データ型、ODBC のマッピングを実行します*3.x*のみ必要なドライバーを認識 **#defines** 91 の 92、入力された日付、時刻、および timestamp C データ型の 93、 *TargetType*の引数**SQLBindCol**と**SQLGetData**または*ValueType*の引数**SQLBindParameter**、必要がありますのみを認識および **#defines** 91 92、および、日付の 93 の時間、および timestamp SQL データ型が、に入力*ParameterType*の引数**SQLBindParameter**または*DataType*の引数**SQLGetTypeInfo**します。 詳細については、次を参照してください。 [Datetime データ型の変更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)します。
