---
title: 数値関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e744d3de177197923540fc3101c58dcbb4d3490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990729"
---
# <a name="numeric-functions"></a>数値関数
次の表では、ODBC スカラー関数のセットに含まれている数値の関数について説明します。 呼び出して**SQLGetInfo**で、*情報の種類*する数値関数は、ドライバーによってサポート SQL_NUMERIC_FUNCTIONS のアプリケーションを判断できます。  
  
 すべての数値関数の戻り値のデータ型、ABS 以外に使用できます ROUND、TRUNCATE、記号、FLOOR、関数と CEILING、同じデータの値を返すは、入力パラメーターとして入力します。  
  
 として表される引数*numeric_exp* 、もう 1 つのスカラー関数の結果の列の名前を指定できます、*数値 litera*SQL_NUMERIC、sql _ として基になるデータ型を表すことができます、l10 進数、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、使用できます、SQL_REAL、または SQL_DOUBLE します。  
  
 として表される引数*float_exp* 、もう 1 つのスカラー関数の結果の列の名前を指定できます、*数値リテラル*として使用できます、基になるデータ型を表すことができます。  
  
 として表される引数*integer_exp* 、もう 1 つのスカラー関数の結果の列の名前を指定できます、*数値リテラル*SQL_TINYINT、sql _ として基になるデータ型を表すことが、SMALLINT、SQL_INTEGER、または SQL_BIGINT します。  
  
 CURRENT_DATE や CURRENT_TIME、CURRENT_TIMESTAMP スカラー関数は、SQL 92 とを連携させる ODBC 3.0 で追加されました。  
  
|関数|説明|  
|--------------|-----------------|  
|**ABS (** _numeric_exp_ **)** (ODBC 1.0)|絶対値を返します*numeric_exp*します。|  
|**ACOS (** _float_exp_ **)** (ODBC 1.0)|アーク コサインを返します*float_exp*ラジアンの角度で表されます。|  
|**ASIN (** _float_exp_ **)** (ODBC 1.0)|アークサインを返します*float_exp*ラジアンの角度で表されます。|  
|**ATAN (** _float_exp_ **)** (ODBC 1.0)|アーク タンジェントを返します*float_exp*ラジアンの角度で表されます。|  
|**ATAN2 (** _float_exp1_、 _float_exp2_ **)** (ODBC 2.0)|アーク タンジェントを返します、 *x*と*y*によって指定された座標*float_exp1*と*float_exp2*、それぞれの角度で、ラジアンで表されます。|  
|**CEILING (** _numeric_exp_ **)** (ODBC 1.0)|大きいまたは等しい最小整数を返します*numeric_exp*します。 戻り値は入力パラメーターと同じデータ型です。|  
|**COS (** _float_exp_ **)** (ODBC 1.0)|コサインを返します*float_exp*ここで、 *float_exp*ラジアンを角度のことです。|  
|**COT (** _float_exp_ **)** (ODBC 1.0)|コタンジェントを返します*float_exp*ここで、 *float_exp*ラジアンを角度のことです。|  
|**度 (** _numeric_exp_ **)** (ODBC 2.0)|変換された度の数を返します*numeric_exp*ラジアン。|  
|**EXP (** _float_exp_ **)** (ODBC 1.0)|指数値を返します*float_exp*します。|  
|**FLOOR (** _numeric_exp_ **)** (ODBC 1.0)|等しいまたはそれより小さい最大整数を返します*numeric_exp*します。 戻り値は入力パラメーターと同じデータ型です。|  
|**ログ (** _float_exp_ **)** (ODBC 1.0)|自然対数を返します*float_exp*します。|  
|**LOG10 (** _float_exp_ **)** (ODBC 2.0)|底が 10 を返します。 対数*float_exp*します。|  
|**MOD (** _integer_exp1_、 _integer_exp2_ **)** (ODBC 1.0)|(剰余) の残りの部分を返します*integer_exp1*で割った値*integer_exp2*します。|  
|**PI()** (ODBC 1.0)|Π の定数値を浮動小数点値として返します。|  
|**電源 (** _numeric_exp_、 _integer_exp_ **)** (ODBC 2.0)|値を返します*numeric_exp*のべき乗に*integer_exp*します。|  
|**ラジアン (** _numeric_exp_ **)** (ODBC 2.0)|変換されたラジアン単位の数を返します*numeric_exp*度。|  
|**RAND(** [*integer_exp*] **)**  (ODBC 1.0)|使用して、ランダムな浮動小数点値を返します*integer_exp*省略可能なシード値として。|  
|**ROUND (** _numeric_exp_、 _integer_exp_ **)** (ODBC 2.0)|返します*numeric_exp*に丸められます*integer_exp*小数点の右側に配置します。 場合*integer_exp*が負の値、 *numeric_exp*に丸められます&#124; *integer_exp* &#124;小数点の左側に配置します。|  
|**サインイン (** _numeric_exp_ **)** (ODBC 1.0)|符号を示すインジケーターを返す*numeric_exp*します。 場合*numeric_exp*が 0、-1 未満ですが返されます。 場合*numeric_exp*が 0 に等しい、0 が返されます。 場合*numeric_exp*はゼロより大きく、1 が返されます。|  
|**SIN (** _float_exp_ **)** (ODBC 1.0)|サインを返します*float_exp*ここで、 *float_exp*ラジアンを角度のことです。|  
|**SQRT (** _float_exp_ **)** (ODBC 1.0)|平方根を返します*float_exp*します。|  
|**TAN (** _float_exp_ **)** (ODBC 1.0)|タンジェントを返します*float_exp*ここで、 *float_exp*ラジアンを角度のことです。|  
|**TRUNCATE(** _numeric_exp_, _integer_exp_ **)**  (ODBC 2.0)|返します*numeric_exp*に切り捨てられます*integer_exp*小数点の右側に配置します。 場合*integer_exp*が負の値、 *numeric_exp*に切り捨てられます&#124; *integer_exp* &#124;小数点の左側に配置します。|
