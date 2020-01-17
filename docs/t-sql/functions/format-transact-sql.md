---
title: FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: fd44673ce62d74349e83b09b020c9e20ab6957de
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155799"
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

指定した形式とオプションのカルチャを使用して書式設定された値を返します。 文字列としての日付/時刻と数値のロケール依存の書式指定には FORMAT 関数を使用します。 一般的なデータ型変換では、引き続き CAST または CONVERT を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>引数

 *value*  
 書式設定がサポートされているデータ型の式。 有効な型の一覧については、以下の「解説」のセクションにある表を参照してください。  
  
 *format*  
 **nvarchar** 書式パターン。  
  
 *format* 引数には、有効な .NET Framework 形式文字列を、標準形式文字列 ("C" や "D" など) として、または日付と数値に対するカスタム文字のパターン ("MMMM DD, yyyy (dddd)" など) として含める必要があります。 複合書式設定はサポートされていません。 これらの書式設定パターンの詳細については、一般的な文字列の書式設定、カスタム日付/時刻書式、およびカスタム数値書式に関する .NET Framework ドキュメントを参照してください。 最初にトピック「[型の書式設定](https://go.microsoft.com/fwlink/?LinkId=211776)」を参照することをお勧めします。  
  
 *culture*  
 カルチャを指定する省略可能な **nvarchar** 引数です。  
  
 *culture* 引数が指定されていない場合は、現在のセッションの言語が使用されます。 この言語は、SET LANGUAGE ステートメントを使用して、暗黙的または明示的に設定されます。 *culture* は、引数として .NET Framework でサポートされている任意のカルチャを受け入れます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で明示的にサポートされている言語に制限されません。 *culture* 引数が有効でない場合は、FORMAT でエラーが発生します。  
  
## <a name="return-types"></a>戻り値の型

 **nvarchar** または null  
  
 戻り値の長さは *format* によって決まります。  
  
## <a name="remarks"></a>Remarks

 *valid* でない *culture* 以外のエラーの場合、FORMAT は NULL を返します。 たとえば、*format* に指定された値が無効な場合は NULL を返します。  

 FORMAT 関数は非決定的です。
  
 FORMAT は、.NET Framework の共通言語ランタイム (CLR) の存在に依存しています。  
  
 この関数は、CLR の存在に依存するため、リモート処理を行うことはできません。 CLR が必要な関数をリモート処理すると、リモート サーバー上でエラーが発生する可能性があります。  
  
 FORMAT は、コロンとピリオドをエスケープする必要がある CLR の書式規則に依存しています。 そのため、書式設定文字列 (2 番目のパラメーター) にコロンまたはピリオドが含まれ、入力値 (最初のパラメーター) が **time** データ型の場合、コロンまたはピリオドを円記号でエスケープする必要があります。 「[D. 時刻データ型を使用する FORMAT](#ExampleD)」を参照してください。  
  
 *value* 引数の許容データ型の一覧を、.NET Framework にマッピングした同等の型と共に、次の表に示します。  
  
|カテゴリ|型|.NET の種類|  
|--------------|----------|---------------|  
|数値|BIGINT|Int64|  
|数値|INT|Int32|  
|数値|SMALLINT|Int16|  
|数値|TINYINT|Byte|  
|数値|Decimal|SqlDecimal|  
|数値|NUMERIC|SqlDecimal|  
|数値|FLOAT|Double|  
|数値|REAL|Single|  
|数値|SMALLMONEY|Decimal|  
|数値|money|Decimal|  
|日時|date|DateTime|  
|日時|time|TimeSpan|  
|日時|DATETIME|DateTime|  
|日時|smalldatetime|DateTime|  
|日時|datetime2|DateTime|  
|日時|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-simple-format-example"></a>A. シンプルな FORMAT 例

 次の例では、さまざまなカルチャ用にフォーマットされたシンプルな日付を返します。  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. カスタムの書式指定文字列を使用する FORMAT

 次の例では、カスタム書式を指定して数値を書式設定する方法を示します。 この例では、現在の日付が 2012 年 9 月 27 日であることを前提としています。 これらのカスタム書式およびその他のカスタム書式の詳細については、「[カスタム数値書式設定文字列](https://msdn.microsoft.com/library/0c899ak8.aspx)」を参照してください。  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. 数値型を使用する FORMAT

 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの **Sales.CurrencyRate** テーブルから 5 行を返します。 列 **EndOfDateRate** は、**money** 型としてテーブルに格納されます。 この例では、書式設定されずに返された列を、.NET の数値書式、一般書式、および通貨の書式の種類を指定して書式設定します。 これらの数値書式およびその他の数値書式の詳細については、「[標準数値書式設定文字列](https://msdn.microsoft.com/library/dwhawy9k.aspx)」を参照してください。  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 この例では、ドイツのカルチャ de (de-de) を指定します。  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
### <a name="ExampleD"></a> D. 時刻データ型を使用する FORMAT

 `.` と `:` がエスケープされていないため、FORMAT は NULL を返します。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 `.` と `:` はエスケープされているため、FORMAT から書式設定された文字列が返されます。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  

FORMAT からは、AM または PM が指定され、書式設定された現在時刻が返されます。

```sql
SELECT FORMAT(SYSDATETIME(), N'hh:mm tt'); -- returns 03:46 PM
SELECT FORMAT(SYSDATETIME(), N'hh:mm t'); -- returns 03:46 P
```

FORMAT からは指定の時刻が AM で返されます。

```sql
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm tt') -- returns 01:00 AM
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm t')  -- returns 01:00 A
```

FORMAT からは指定の時刻が PM で返されます。

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm tt') -- returns 02:00 PM
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm t') -- returns 02:00 P
```
  
FORMAT からは指定の時刻が 24 時間形式で返されます。

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'HH:mm') -- returns 14:00
```
  
## <a name="see-also"></a>参照

 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
