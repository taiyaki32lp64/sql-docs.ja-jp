---
title: 日付、時刻、および間隔を扱う関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae10946be501adb16fdda5fa9f053e389eea4bed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070081"
---
# <a name="time-date-and-interval-functions"></a>時刻、日付、および間隔を扱う関数
次の表には、ODBC スカラー関数のセットに含まれている日付と時刻の関数が一覧表示します。 どの日付と時刻の関数が呼び出すことによってドライバーによってサポートされているアプリケーションを調べる**SQLGetInfo**で、*情報の種類*SQL_TIMEDATE_FUNCTIONS の。  
  
 として表される引数*timestamp_exp* 、もう 1 つのスカラー関数の結果の列の名前を指定できますまたは*ODBC 時刻-エスケープ*、 *ODBC の日付のエスケープ*、または*ODBC タイムスタンプ エスケープ*SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、SQL_TYPE_DATE、または SQL_TYPE_TIMESTAMP と基になるデータ型を表す可能性があります。  
  
 として表される引数*date_exp* 、もう 1 つのスカラー関数の結果の列の名前を指定できますまたは*ODBC の日付のエスケープ*または*ODBC タイムスタンプ エスケープ*、どこで、基になるデータ型は、SQL_CHAR、SQL_VARCHAR、SQL_TYPE_DATE、または SQL_TYPE_TIMESTAMP として表すことができます。  
  
 として表される引数*time_exp* 、もう 1 つのスカラー関数の結果の列の名前を指定できますまたは*ODBC 時刻-エスケープ*または*ODBC タイムスタンプ エスケープ*、どこで、基になるデータ型は、SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、または SQL_TYPE_TIMESTAMP として表すことができます。  
  
 CURRENT_DATE や CURRENT_TIME、CURRENT_TIMESTAMP timedate スカラー関数、sql-92 とを連携させる ODBC 3.0 で追加されました。  
  
|関数|説明|  
|--------------|-----------------|  
|**CURRENT_DATE( )** (ODBC 3.0)|現在の日付を返します。|  
|**CURRENT_TIME [(** *時間精度* **)]** (ODBC 3.0)|現在のローカル時間を返します。 *時間精度*引数は、戻り値の秒の有効桁数を決定します。|  
|**CURRENT_TIMESTAMP**<br /> **[(** *タイムスタンプ精度* **)]** (ODBC 3.0)|タイムスタンプの値として、現在の日付と現地時刻を返します。 *タイムスタンプ精度*引数は、タイムスタンプの秒の有効桁数を決定します。|  
|**CURDATE( )** (ODBC 1.0)|現在の日付を返します。|  
|**CURTIME ()** (ODBC 1.0)|現在のローカル時間を返します。|  
|**DAYNAME(** *date_exp* **)** (ODBC 2.0)|(たとえば、Sunday ~ Saturday または Sun 1 日のデータ ソースに固有の名前を含む文字列を返しますです。 \- Sat. ドイツ語を使ったデータ ソースの英語版、または Sonntag ~ 場合を使用するデータ ソース) 用の日の部分の*date_exp*します。|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|月のフィールドに基づき、月の通算日を返す*date_exp* 1 ~ 31 の範囲の整数値として。|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|週に基づく週の通算日を返す*date_exp*の範囲の整数値として 1 ~ 7、ここで、1 は日曜日を表します。|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|[Year] フィールドに基づき、年の通算日を返す*date_exp* 1 ~ 366 の範囲の整数値として。|  
|**抽出 (** *フィールドの抽出 FROM* *抽出ソース* **)** (ODBC 3.0)|返します、*フィールドの抽出*の部分、*抽出ソース*します。 *抽出ソース*引数は、datetime または間隔の式。 *フィールドの抽出*引数には、次のキーワードのいずれかを指定できます。<br /><br /> 年、月 1 日 1 時間分の 1 秒<br /><br /> 返される値の有効桁数は、実装で定義します。 小数点以下桁数は、0 2 つ目が指定されていない場合、スケールの秒の小数部の有効桁数よりも小さいか、*抽出ソース*フィールド。|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|時間フィールドに基づいて時間を返します*time_exp*として 0 ~ 23 の範囲の整数値。|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|分単位のフィールドに基づいて分が返されます*time_exp*として 0 ~ 59 の範囲の整数値。|  
|**月 (** *date_exp* **)** (ODBC 1.0)|月のフィールドに基づき、月を返します*date_exp* 1 ~ 12 の範囲の整数値として。|  
|**MONTHNAME(** *date_exp* **)** (ODBC 2.0)|月の部分を (たとえば、January ~ December または英語を使用するデータ ソースの 12 月で 1 月またはドイツ語を使ったデータ ソースの Dezember を通じて Januar) 月のデータ ソースに固有の名前を含む文字列を返します*date_exp*します。|  
|**() を今すぐ**(ODBC 1.0)|現在の日付と時刻のタイムスタンプ値を返します。|  
|**四半期 (** *date_exp* **)** (ODBC 1.0)|における四半期を返します*date_exp*の範囲の整数値として 1 ~ 4、1 を表す年 1 月 1 日 ~ 3 月 31 日。|  
|**2 番目 (** *time_exp* **)** (ODBC 1.0)|2 番目のフィールドに基づく秒を返します。 *time_exp*として 0 ~ 59 の範囲の整数値。|
|**TIMESTAMPADD (** *間隔*、 *integer_exp*、 *timestamp_exp* **)** (ODBC 2.0)|加算したタイムスタンプを返す*integer_exp*間隔の種類の*間隔*に*timestamp_exp*します。 有効な値の*間隔*は、次のキーワード。<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> 予期されています<br /><br /> 秒の小数部は、2 つ目の 10億で表現されます。 たとえば、次の SQL ステートメントは、各従業員や自分の 1 年間の契約応当日の名前を返します。<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 場合*timestamp_exp*が時間の値と*間隔*日、週、月、四半期、または年の日付部分を指定します*timestamp_exp*する前に、現在の日付に設定されています。結果として得られるタイムスタンプを計算します。<br /><br /> 場合*timestamp_exp*は日付の値と*間隔*小数部を指定します秒、秒、分、または時間単位の時間部分*timestamp_exp*する前に 0 に設定されています。結果として得られるタイムスタンプを計算します。<br /><br /> アプリケーションは、データ ソースを呼び出すことによってサポートされる間隔を決定します。 **SQLGetInfo** SQL_TIMEDATE_ADD_INTERVALS オプションを使用します。|  
|**TIMESTAMPDIFF (** *間隔*、 *timestamp_exp1*、 *timestamp_exp2* **)** (ODBC 2.0)|整数型の間隔の数を返します*間隔*される*timestamp_exp2*がより大きい*timestamp_exp1*します。 有効な値の*間隔*は、次のキーワード。<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> 予期されています<br /><br /> 秒の小数部は、2 つ目の 10億で表現されます。 たとえば、次の SQL ステートメントは、自分が採用されて年の数と各従業員の名前を返します。<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> タイムスタンプのいずれかの式が時刻値の場合と*間隔*タイムスタンプの差を計算する前に、現在の日付に設定する日、週、月、四半期、または年間、そのタイムスタンプの日付部分を指定します。<br /><br /> タイムスタンプのいずれかの式が日付値の場合と*間隔*小数部を指定します、タイムスタンプの差を計算する前に、そのタイムスタンプの時刻部分が 0 に設定されて秒、秒、分、または時間、します。<br /><br /> アプリケーションは、データ ソースを呼び出すことによってサポートされる間隔を決定します。 **SQLGetInfo** SQL_TIMEDATE_DIFF_INTERVALS オプションを使用します。|  
|**週 (** *date_exp* **)** (ODBC 1.0)|週のフィールドに基づき、年の週を返します*date_exp* 1 ~ 53 の範囲の整数値として。|  
|**年 (** *date_exp* **)** (ODBC 1.0)|[Year] フィールドに基づき、年を返します*date_exp*整数値として。 範囲は、データ ソースに依存します。|
