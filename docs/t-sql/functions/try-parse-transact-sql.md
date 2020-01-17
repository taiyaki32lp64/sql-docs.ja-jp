---
title: TRY_PARSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_PARSE_TSQL
- TRY_PARSE
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_PARSE function
ms.assetid: 292bac1d-edd8-468c-8ff1-8c7de625bc55
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: 3533d69ebaac7cf535de0e835bdbfdef9c5fbb4b
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152054"
---
# <a name="try_parse-transact-sql"></a>TRY_PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  式の結果を、要求されたデータ型に変換して返します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でキャストに失敗した場合は NULL を返します。 TRY_PARSE は、文字列型から日付/時刻型および数値型への変換にのみ使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TRY_PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>引数  
 *string_value*  
 指定したデータ型に解析する、書式設定された値を表す **nvarchar(4000)** 値。  
  
 *string_value* には、要求されたデータ型の有効な表現を指定する必要があります。そうしないと、TRY_PARSE は NULL を返します。  
  
 *data_type*  
 結果に要求されたデータ型を表すリテラル。  
  
 *culture*  
 *string_value* が書式設定されるカルチャを識別する文字列です (省略可能)。  
  
 *culture* 引数が指定されていない場合は、現在のセッションの言語が使用されます。 この言語は、SET LANGUAGE ステートメントを使用して、暗黙的または明示的に設定されます。 *culture* は、.NET Framework でサポートされている任意のカルチャを受け入れます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で明示的にサポートされている言語に制限されません。 *culture* 引数が有効でない場合は、PARSE でエラーが発生します。  
  
## <a name="return-types"></a>戻り値の型  
 式の結果を、要求されたデータ型に変換して返します。キャストに失敗した場合は、NULL を返します。  
  
## <a name="remarks"></a>Remarks  
 TRY_PARSE は、文字列型から日付/時刻型および数値型への変換にのみ使用します。 一般的な型変換では、引き続き CAST または CONVERT を使用します。 文字列値の解析には一定のパフォーマンス オーバーヘッドがあることに注意してください。  
  
 TRY_PARSE は、.NET Framework の共通言語ランタイム (CLR) の存在に依存しています。  
  
 この関数は、CLR の存在に依存するため、リモート処理は行われません。 CLR が必要な関数をリモート処理すると、リモート サーバー上でエラーが発生します。  
  
 **data_type パラメーターの詳細**  
  
 *data_type* パラメーターの値は、スタイルと共に、次の表に示す型に制限されます。 スタイル情報は、許可するパターンの種類を決定するために提供されます。 スタイルについて詳しくは、.NET Framework のドキュメントで **System.Globalization.NumberStyles** および **DateTimeStyles** 列挙型を参照してください。  
  
|カテゴリ|型|.NET の種類|使用されるスタイル|  
|--------------|----------|---------------|-----------------|  
|数値|BIGINT|Int64|NumberStyles.Number|  
|数値|INT|Int32|NumberStyles.Number|  
|数値|SMALLINT|Int16|NumberStyles.Number|  
|数値|TINYINT|Byte|NumberStyles.Number|  
|数値|Decimal|Decimal|NumberStyles.Number|  
|数値|NUMERIC|Decimal|NumberStyles.Number|  
|数値|FLOAT|Double|NumberStyles.Float|  
|数値|REAL|Single|NumberStyles.Float|  
|数値|SMALLMONEY|Decimal|NumberStyles.Currency|  
|数値|money|Decimal|NumberStyles.Currency|  
|日時|date|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|日時|time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|日時|DATETIME|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|日時|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|日時|datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|日時|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
  
 **culture パラメーターの詳細**  
  
 次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 言語から .NET Framework カルチャへのマッピングを示します。  
  
|完全名|別名|LCID (LCID)|特定のカルチャ|  
|---------------|-----------|----------|----------------------|  
|us_english|English|1033|en-US|  
|Deutsch|German|1031|de-DE|  
|Français|French|1036|fr-FR|  
|Japanese|Japanese|1041|ja-JP|  
|Dansk|Danish|1030|da-DK|  
|Español|Spanish|3082|es-ES|  
|Italiano|Italian|1040|it-IT|  
|Nederlands|Dutch|1043|nl-NL|  
|Norsk|ノルウェー語|2068|nn-NO|  
|Português|Portuguese|2070|pt-PT|  
|Suomi|Finnish|1035|fi-FI|  
|Svenska|Swedish|1053|sv-SE|  
|čeština|Czech|1029|Cs-CZ|  
|magyar|Hungarian|1038|Hu-HU|  
|polski|Polish|1045|Pl-PL|  
|română|Romanian|1048|Ro-RO|  
|hrvatski|Croatian|1050|hr-HR|  
|slovenčina|Slovak|1051|Sk-SK|  
|slovenski|Slovenian|1060|Sl-SI|  
|ελληνικά|Greek|1032|El-GR|  
|български|Bulgarian|1026|bg-BG|  
|русский|Russian|1049|Ru-RU|  
|Türkçe|Turkish|1055|Tr-TR|  
|British|英語 (U.K.)|2057|en-GB|  
|eesti|Estonian|1061|Et-EE|  
|latviešu|Latvian|1062|lv-LV|  
|lietuvių|Lithuanian|1063|lt-LT|  
|Português (Brasil)|Brazilian|1046|pt-BR|  
|繁體中文|Traditional Chinese|1028|zh-TW|  
|한국어|Korean|1042|Ko-KR|  
|简体中文|Simplified Chinese|2052|zh-CN|  
|アラビア語|アラビア語|1025|ar-SA|  
|ไทย|Thai|1054|Th-TH|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-simple-example-of-try_parse"></a>A. TRY_PARSE の簡単な使用例  
  
```  
SELECT TRY_PARSE('Jabberwokkie' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-detecting-nulls-with-try_parse"></a>B. TRY_PARSE で NULL 値を検出する  
  
```  
SELECT  
    CASE WHEN TRY_PARSE('Aragorn' AS decimal USING 'sr-Latn-CS') IS NULL  
        THEN 'True'  
        ELSE 'False'  
END  
AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
True  
  
(1 row(s) affected)  
```  
  
### <a name="c-using-iif-with-try_parse-and-implicit-culture-setting"></a>C. TRY_PARSE と暗黙のカルチャ設定を指定した IIF を使用する  
  
```  
SET LANGUAGE English;  
SELECT IIF(TRY_PARSE('01/01/2011' AS datetime2) IS NULL, 'True', 'False') AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
False  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [PARSE &#40;Transact-SQL&#41;](../../t-sql/functions/parse-transact-sql.md)   
 [変換関数 &#40;Transact-SQL&#41;](../../t-sql/functions/conversion-functions-transact-sql.md)   
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
