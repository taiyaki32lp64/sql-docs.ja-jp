---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3724c25854bd98a98b077fb59897ba4da250aee1
ms.sourcegitcommit: 73dc08bd16f433dfb2e8406883763aabed8d8727
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68329290"
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

この関数は、*startdate* と *enddate* で指定された 2 つの日付間の差を、指定された *datepart* 境界の数で (符号付き多倍長整数値として) 返します。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のあらゆるデータ型と関数に関する概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引数  
*datepart*  
*startdate* と *enddate* の差を求めるときの単位に使用する要素を指定します。

> [!NOTE]
> `DATEDIFF_BIG` では、ユーザー定義変数からの、または引用符で囲まれた文字列としての *datepart* 値は受け入れられません。

この表には、有効な *datepart* 引数名と省略形をすべて一覧表示しています。
  
|*datepart* 名| *datepart* 省略形|  
|---|---|
|**year**|**yy、yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy、y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi、n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  

> [!NOTE]
> 特定の各 *datepart* 名と、その *datepart* 名の省略形では、同じ値が返されます。

*startdate*  
次のいずれかの値に解決できる式。

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

*date* の場合、`DATEDIFF_BIG` では、列式、式、文字列リテラル、ユーザー定義の変数が受け入れられます。 文字列リテラル値は **datetime** に解決する必要があります。 あいまいさの問題を排除するために、4 桁の西暦を使用してください。 `DATEDIFF_BIG` では、*enddate* から *startdate* が減算されます。 こうしたあいまいさを排除するため、4 桁の西暦を使用してください。 2 桁の西暦については、「[two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。
  
*enddate*  
「*startdate*」をご覧ください。
  
## <a name="return-type"></a>戻り値の型  
符号付き **bigint**  
  
## <a name="return-value"></a>戻り値  
*datepart* により設定された境界に表示された、*startdate* と *enddate* の間の **bigint** 差を返します。
  
**bigint** の範囲外の戻り値 (-9,223,372,036,854,775,808 から 9,223,372,036,854,775,807) の場合、`DATEDIFF_BIG` はエラーを返します。 **int** を返すため **minute** 以上の精度でオーバーフローする可能性がある `DATEDIFF` とは異なり、`DATEDIFF_BIG` は **nanosecond** の精度を使用する場合にのみオーバーフローする可能性があります。この場合、*enddate* と *startdate* の差は 292 年以上、3 か月、10 日、23 時間、47 分、および 16.8547758 秒です。
  
*startdate* と *enddate* の両方に時刻値のみが割り当てられており、*datepart* が時刻の *datepart* でない場合、`DATEDIFF_BIG` は 0 を返します。
  
`DATEDIFF_BIG` では、戻り値を計算する際に、*startdate* または *enddate* のタイム ゾーン オフセット要素を使用しません。
  
[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) の精度は分単位までなので、*startdate* または *enddate* に **smalldatetime** 値を使用した場合、`DATEDIFF_BIG` では、戻り値で秒とミリ秒が常に 0 に設定されます。
  
日付データ型の変数に時刻値のみが割り当てられている場合、`DATEDIFF_BIG` では、欠落している日付要素の値が既定値である `1900-01-01` に設定されます。 時刻データ型または日付データ型の変数に日付値のみが割り当てられている場合、`DATEDIFF_BIG` では、欠落している時刻要素の値が既定値である `00:00:00` に設定されます。 *startdate* または *enddate* のいずれか一方が時刻要素のみで、もう一方が日付要素のみであった場合、`DATEDIFF_BIG` では、欠落している時刻要素と日付要素がそれぞれの既定値に設定されます。
  
*startdate* と *enddate* で異なる日付データ型が使用されており、一方の時刻要素の数または秒の小数部の有効桁数が、もう一方のデータ型を超えている場合、`DATEDIFF_BIG` では、欠落している要素が 0 に設定されます。
  
## <a name="datepart-boundaries"></a>datepart の差
次の各ステートメントには、すべて同じ *startdate* と *enddate* の値が指定されています。 これらの日付は隣接しており、時間的な差は 1 マイクロ秒 (0.0000001 秒) です。 各ステートメントにおける *startdate* と *enddate* の差は、どの要素をとっても、*datepart* の 1 単位分となるように配慮されています。 いずれのステートメントも 1 を返します。 *startdate* と *enddate* の年の値は異なるが、カレンダー週の値が同じである場合、`DATEDIFF_BIG` では、*datepart* **week** に対して 0 を返します。

```sql
SELECT DATEDIFF_BIG(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
`DATEDIFF_BIG` は、`SELECT <list>`、`WHERE`、`HAVING`、`GROUP BY`、`ORDER BY` 句で使用します。
  
`DATEDIFF_BIG` は、文字列リテラルを **datetime2** 型として暗黙的にキャストします。 つまり、`DATEDIFF_BIG` では、日付が文字列として渡される場合、YDM 形式がサポートされません。 文字列を明示的にキャストする必要があります、 **datetime** または **smalldatetime** YDM 形式を使用する型。
  
`SET DATEFIRST` を指定しても、`DATEDIFF_BIG` には何の影響もありません。 `DATEDIFF_BIG` では、週の最初の曜日として常に日曜日を使用し、関数が決定的な方法で動作するようにします。

*enddate* と *startdate* の差として **bigint** の範囲を超える値が返された場合、`DATEDIFF_BIG` は **nanosecond** の精度でオーバーフローする可能性があります。
  
## <a name="examples"></a>使用例 
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>startdate と enddate に列を指定する  
この例では、*startdate* パラメーターと *enddate* パラメーターの引数として、各種の式を使用しています。 テーブルの 2 つの列に日付を格納し、両者の差を日単位で計算しています。
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF_BIG(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  

### <a name="finding-difference-between-startdate-and-enddate-as-date-parts-strings"></a>startdate と enddate の差を日付部分の文字列として検索する

```sql
DECLARE @date1 DATETIME2, @date2 DATETIME2, @result VARCHAR(100)
DECLARE @years BIGINT, @months BIGINT, @days BIGINT, @hours BIGINT, @minutes BIGINT, @seconds BIGINT, @milliseconds BIGINT

SET @date1 = '0001-01-01 00:00:00.00000000'
SET @date2 = '2018-12-12 07:08:01.12345678'

SELECT @years = DATEDIFF(yy, @date1, @date2)
IF DATEADD(yy, -@years, @date2) < @date1 
SELECT @years = @years-1
SET @date2 = DATEADD(yy, -@years, @date2)

SELECT @months = DATEDIFF(mm, @date1, @date2)
IF DATEADD(mm, -@months, @date2) < @date1 
SELECT @months=@months-1
SET @date2= DATEADD(mm, -@months, @date2)

SELECT @days=DATEDIFF(dd, @date1, @date2)
IF DATEADD(dd, -@days, @date2) < @date1 
SELECT @days=@days-1
SET @date2= DATEADD(dd, -@days, @date2)

SELECT @hours=DATEDIFF(hh, @date1, @date2)
IF DATEADD(hh, -@hours, @date2) < @date1 
SELECT @hours=@hours-1
SET @date2= DATEADD(hh, -@hours, @date2)

SELECT @minutes=DATEDIFF(mi, @date1, @date2)
IF DATEADD(mi, -@minutes, @date2) < @date1 
SELECT @minutes=@minutes-1
SET @date2= DATEADD(mi, -@minutes, @date2)

SELECT @seconds=DATEDIFF(s, @date1, @date2)
IF DATEADD(s, -@seconds, @date2) < @date1 
SELECT @seconds=@seconds-1
SET @date2= DATEADD(s, -@seconds, @date2)

SELECT @milliseconds=DATEDIFF(ms, @date1, @date2)

SELECT @result= ISNULL(CAST(NULLIF(@years,0) AS VARCHAR(10)) + ' years,','')
     + ISNULL(' ' + CAST(NULLIF(@months,0) AS VARCHAR(10)) + ' months,','')    
     + ISNULL(' ' + CAST(NULLIF(@days,0) AS VARCHAR(10)) + ' days,','')
     + ISNULL(' ' + CAST(NULLIF(@hours,0) AS VARCHAR(10)) + ' hours,','')
     + ISNULL(' ' + CAST(@minutes AS VARCHAR(10)) + ' minutes and','')
     + ISNULL(' ' + CAST(@seconds AS VARCHAR(10)) 
          + CASE WHEN @milliseconds > 0 THEN '.' + CAST(@milliseconds AS VARCHAR(10)) 
               ELSE '' END 
          + ' seconds','')

SELECT @result
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 

```
2017 years, 11 months, 11 days, 7 hours, 8 minutes and 1.123 seconds
```   

より密接に関連する例については、「[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)」を参照してください。
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
