---
title: 日付と時刻のデータ型および関数
description: 日付と時刻のデータ型および関数に関する記事へのリンクです。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azure-sqldw-latest||= azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: a7beec472b0f4b70662c364081641b6ea91be507
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75256091"
---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>日付と時刻のデータ型および関数 (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

このトピックの次のセクションでは、すべての [!INCLUDE[tsql](../../includes/tsql-md.md)] 日付と時刻のデータ型および関数について説明します。
-   [日付および時刻のデータ型](#DateandTimeDataTypes)  
-   [日付と時刻の関数](#DateandTimeFunctions)  
    -   [システムの日付と時刻値を返す関数](#GetSystemDateandTimeValues)  
    -   [日付と時刻の要素を返す関数](#GetDateandTimeParts)  
    -   [要素から日付と時刻の値を返す関数](#fromParts)  
    -   [日付と時刻の差の値を返す関数](#GetDateandTimeDifference)  
    -   [日付と時刻の値を変更する関数](#ModifyDateandTimeValues)  
    -   [セッションの形式の関数を設定または返す関数](#SetorGetSessionFormatFunctions)  
    -   [日付と時刻の値を検証する関数](#ValidateDateandTimeValues)  
-   [日付と時刻に関連したトピック](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a> 日付および時刻のデータ型
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のデータ型を次の表に示します。
  
|データ型|Format|Range|精度|ストレージ サイズ (バイト)|ユーザー定義の 1 秒未満の秒の有効桁数|タイム ゾーン オフセット|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 ～ 23:59:59.9999999|100 ナノ秒|3 から 5 まで|はい|いいえ|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01 ～ 31.12.99|1 日|3|いいえ|いいえ|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01 から 2079-06-06|1 分|4|いいえ|いいえ|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01 から 9999-12-31|0.00333 秒|8|いいえ|いいえ|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 から 9999-12-31 23:59:59.9999999|100 ナノ秒|6 ～ 8|はい|いいえ|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|0001-01-01 00:00:00.0000000 から 9999-12-31 23:59:59.9999999 (UTC)|100 ナノ秒|8 ～ 10|はい|はい|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) データ型は、日付または時刻のデータ型ではありません。 **timestamp** は、**rowversion** の非推奨のシノニムです。  
  
##  <a name="DateandTimeFunctions"></a> 日付と時刻関数  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 日付と時刻の関数を次の表に示します。 決定性の詳細については、「[決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。
  
###  <a name="GetSystemDateandTimeValues"></a> システムの日付と時刻値を返す関数 
[!INCLUDE[tsql](../../includes/tsql-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターのオペレーティング システムから、システムのすべての日付値と時刻値を取得します。
  
#### <a name="higher-precision-system-date-and-time-functions"></a>高精度のシステム日付/時刻関数  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、GetSystemTimeAsFileTime() Windows API を使用して日付と時刻の値を取得します。 精度は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューター ハードウェアおよび Windows のバージョンによって異なります。 この API の精度は 100 ナノ秒で固定されます。 精度を確認するには、GetSystemTimeAdjustment() Windows API を使用します。
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターの日付と時刻を含む、**datetime2(7)** 値を返します。 戻り値には、タイム ゾーン オフセットは含まれません。|**datetime2(7)**|非決定的|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターの日付と時刻を含む、**datetimeoffset(7)** 値を返します。 戻り値にはタイム ゾーン オフセットが含まれます。|**datetimeoffset(7)**|非決定的|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターの日付と時刻を含む、**datetime2(7)** 値を返します。 この関数は、日付と時刻を UTC 時刻 (世界協定時刻) として返します。|**datetime2(7)**|非決定的|  
  
#### <a name="lower-precision-system-date-and-time-functions"></a>低精度のシステム日付/時刻関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターの日付と時刻を含む、**datetime** 値を返します。 戻り値には、タイム ゾーン オフセットは含まれません。|**datetime**|非決定的|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターの日付と時刻を含む、**datetime** 値を返します。 戻り値には、タイム ゾーン オフセットは含まれません。|**datetime**|非決定的|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているコンピューターの日付と時刻を含む、**datetime** 値を返します。 この関数は、日付と時刻を UTC 時刻 (世界協定時刻) として返します。|**datetime**|非決定的|  
  
###  <a name="GetDateandTimeParts"></a> 日付と時刻の要素を返す関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *date* )|指定された日付の指定された *datepart* を表す文字列を返します。|**nvarchar**|非決定的|   
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *date* )|指定された *date* の指定された *datepart* を表す整数を返します。|**int**|非決定的|  
|[DAY](../../t-sql/functions/day-transact-sql.md)|DAY ( *date* )|指定された *date* の日の部分を表す整数を返します。|**int**|決定的|  
|[MONTH](../../t-sql/functions/month-transact-sql.md)|MONTH ( *date* )|指定された *date* の月の部分を表す整数を返します。|**int**|決定的|  
|[YEAR](../../t-sql/functions/year-transact-sql.md)|YEAR ( *date* )|指定された *date* の年の部分を表す整数を返します。|**int**|決定的|  
  
###  <a name="fromParts"></a> 要素から日付と時刻の値を返す関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS  ( *year*, *month*, *day* )|返します、 **日付** 指定された年、月、および日の値です。|**date**|決定的|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *precision*)|指定された有効桁数を使用して、指定された日付と時刻を表す **datetime2** 値を返します。|**datetime2(** _precision_ **)**|決定的|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *milliseconds*)|返します、 **datetime** 指定した日付と時刻の値です。|**datetime**|決定的|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *hour_offset*, *minute_offset*, *precision*)|指定されたオフセットおよび有効桁数を使用して、指定された日付と時刻を表す **datetimeoffset** 値を返します。|**datetimeoffset(** _precision_ **)**|決定的|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute* )|返します、 **smalldatetime** 指定した日付と時刻の値です。|**smalldatetime**|決定的|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS  ( *hour*, *minute*, *seconds*, *fractions*, *precision* )|指定された有効桁数を使用して、指定された時刻を表す **time** 値を返します。|**time(** _precision_ **)**|決定的|  
  
###  <a name="GetDateandTimeDifference"></a> 日付と時刻の差の値を返す関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|指定された 2 つの日付間の差を、日付または時刻の *datepart* の境界の数値で返します。|**int**|決定的|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|指定された 2 つの日付間の差を、日付または時刻の *datepart* の境界の数値で返します。|**bigint**|決定的|  
  
###  <a name="ModifyDateandTimeValues"></a> 日付と時刻の値を変更する関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *number* , *date* )|指定された *date* の指定された *datepart* に期間を加えた新しい **datetime** の値を返します。|*date* 引数のデータ型|決定的|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH  ( *start_date* [, *month_to_add* ] )|オプションのオフセットを使用して、指定された日付を含んでいる月の最後の日付を返します。|戻り値の型は、*start_date* 引数型、または **date** データ型です。|決定的|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCHOFFSET (*DATETIMEOFFSET* , *time_zone*)|SWITCHOFFSET は、DATETIMEOFFSET 値のタイム ゾーン オフセットを変更し、UTC 値を保持します。|*DATETIMEOFFSET* の小数部の有効桁数を持つ **datetimeoffset**|決定的|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expression* , *time_zone*)|TODATETIMEOFFSET では、datetime2 値が datetimeoffset 値に変換されます。 *TODATETIMEOFFSET* は、datetime2 値を、指定された time_zone のローカル時刻で解釈します。|*datetime* 引数の小数部の有効桁数を持つ **datetimeoffset**|決定的|  
  
###  <a name="SetorGetSessionFormatFunctions"></a> セッションの形式の関数を設定または返す関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|現在のセッションにおける、SET DATEFIRST の現在の値を返します。|**tinyint**|非決定的|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *number* &#124; **\@** _number_var_ }|週の最初の曜日を 1 から 7 の数値で設定します。|適用なし|適用なし|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *format* &#124; **@** _format_var_ }|**datetime** 型または **smalldatetime** 型のデータを入力する場合の日付要素 (月、日、年) の順番を設定します。|適用なし|適用なし|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|現在使用している言語の名前を返します。 @@LANGUAGE は、日付または時刻の関数ではありません。 ただし、言語設定は日付関数の出力に影響します。|適用なし|適用なし|  
|[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE { [ N ] **'** _language_ **'** &#124; **\@** _language_var_ }|セッションおよびシステム メッセージの言語環境を設定します。 SET LANGUAGE は日付または時刻の関数ではありません。 ただし、言語設定は日付関数の出力に影響します。|適用なし|適用なし|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [ [ **@language =** ] **'** _language_ **'** ]|サポートされているすべての言語の日付形式に関する情報を返します。 **sp_helplanguage** は、日付または時刻のストアド プロシージャではありません。 ただし、言語設定は日付関数の出力に影響します。|適用なし|適用なし|  
  
###  <a name="ValidateDateandTimeValues"></a> 日付と時刻の値を検証する関数
  
|Function|構文|戻り値|戻り値のデータ型|決定性|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expression* )|**datetime** または **smalldatetime** の入力式の日付値または時刻値が有効であるかどうかを調べます。|**int**|ISDATE は、CONVERT 関数と共に使用され、CONVERT スタイル パラメーターが指定されており、スタイルが 0、100、9、または 109 と等しくない場合にのみ決定的関数になります。|  
  
##  <a name="DateandTimeRelatedTopics"></a> 日付と時刻に関連したトピック 
  
|トピック|[説明]|  
|-----------|-----------------|  
|[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|文字列リテラルとその他の日時形式間の、日付と時刻の値の変換に関する情報を提供します。|  
|[国際化に対応した Transact-SQL ステートメントの記述](../../relational-databases/collations/write-international-transact-sql-statements.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用するデータベースやデータベース アプリケーションをある言語から別の言語に移行する、または複数の言語をサポートするためのガイドラインを提供します。|  
|[ODBC スカラー関数 &#40;Transact-SQL&#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで使用できる ODBC スカラー関数に関する情報を提供します。 これには、ODBC の日付および時刻の関数が含まれます。|  
|[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|タイム ゾーンの変換を提供します。|  
  
## <a name="see-also"></a>参照
[関数](../../t-sql/functions/functions.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
