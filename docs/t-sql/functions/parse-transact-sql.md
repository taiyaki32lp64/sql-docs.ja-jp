---
title: PARSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PARSE
- PARSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PARSE function
ms.assetid: 6a2dbf10-f692-471b-9458-24d246963049
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 991d27258b37895ebb2bf54e267fd07fbe87d78e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892498"
---
# <a name="parse-transact-sql"></a>PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で要求されたデータ型に変換された式の結果を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>引数  
 *string_value*  
 指定したデータ型に解析する、書式設定された値を表す **nvarchar**(4000) 値。  
  
 *string_value* は、要求されたデータ型の有効な表現である必要があります。そうでない場合、PARSE でエラーが発生します。  
  
 *data_type*  
 結果に要求されたデータ型を表すリテラル値。  
  
 *culture*  
 *string_value* が書式設定されるカルチャを識別する文字列です (省略可能)。  
  
 *culture* 引数が指定されていない場合は、現在のセッションの言語が使用されます。 この言語は、SET LANGUAGE ステートメントを使用して、暗黙的または明示的に設定されます。 *culture* は、.NET Framework でサポートされている任意のカルチャを受け入れます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で明示的にサポートされている言語に制限されません。 *culture* 引数が有効でない場合は、PARSE でエラーが発生します。  
  
## <a name="return-types"></a>戻り値の型  
 要求されたデータ型に変換された式の結果を返します。  
  
## <a name="remarks"></a>Remarks  
 PARSE への引数として渡される null の値は、2 つの方法で扱われます。  
  
1.  null 定数が渡されると、エラーが発生します。 null の値をカルチャに対応する方法で異なるデータ型に解析することはできません。  
  
2.  実行時に null の値を含んだパラメーターが渡された場合、バッチ全体がキャンセルされないように null が返されます。  
  
 PARSE は、文字列型から日付/時刻型および数値型への変換にのみ使用します。 一般的な型変換では、引き続き CAST または CONVERT を使用します。 文字列値の解析中に一定のパフォーマンス オーバーヘッドが発生することに注意してください。  
  
 PARSE は、.NET Framework の共通言語ランタイム (CLR) の存在に依存しています。  
  
 この関数は、CLR の存在に依存するため、リモート処理は行われません。 CLR が必要な関数をリモート処理すると、リモート サーバー上でエラーが発生します。  
  
 **data_type パラメーターの詳細**  
  
 *data_type* パラメーターの値は、スタイルと共に、次の表に示す型に制限されます。 スタイル情報は、許可するパターンの種類を決定するために提供されます。 スタイルについて詳しくは、.NET Framework のドキュメントで **System.Globalization.NumberStyles** および **DateTimeStyles** 列挙型を参照してください。  
  
|カテゴリ|型|.NET Framework 型|使用されるスタイル|  
|--------------|----------|-------------------------|-----------------|  
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
  
### <a name="a-parse-into-datetime2"></a>A. Datetime2 に解析します。  
  
```  
SELECT PARSE('Monday, 13 December 2010' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-13 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-parse-with-currency-symbol"></a>B. 通貨記号で解析します  
  
```  
SELECT PARSE('€345,98' AS money USING 'de-DE') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
345.98  
  
(1 row(s) affected)  
```  
  
### <a name="c-parse-with-implicit-setting-of-language"></a>C. 暗黙的な言語設定で解析します  
  
```  
-- The English language is mapped to en-US specific culture  
SET LANGUAGE 'English';  
SELECT PARSE('12/16/2010' AS datetime2) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-16 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
  
