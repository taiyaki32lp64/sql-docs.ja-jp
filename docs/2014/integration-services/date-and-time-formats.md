---
title: 日付と時刻の形式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26bd117cb63ccc623ee54f3370e1d07237de9c52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059646"
---
# <a name="date-and-time-formats"></a>日付および時刻の形式
  高速解析は、データを解析するための高速で単純なルーチンのセットです。 高速解析では、日付および時刻のデータ型に対し次の形式がサポートされています。  
  
## <a name="date-data-types"></a>日付データ型  
 高速解析では、次の文字列形式の日付データがサポートされています。  
  
-   先頭の空白文字を含む日付の形式。 たとえば、値 " 2004- 02-03" は有効です。  
  
-   次の表に示す ISO 8601 形式。  
  
    |形式|説明|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> -YYYY-MM-DD|4 桁の年、2 桁の月、および 2 桁の日を表す、基本および拡張形式です。 拡張形式では、日付部分はハイフン (-) で区切られます。|  
    |YYYY-MM|4 桁の年および 2 桁の月を表す、有効桁数を減らした基本および拡張形式です。 拡張形式では、日付部分はハイフン (-) で区切られます。|  
    |YYYY|4 桁の年を表す、有効桁数を減らした形式です。|  
  
 高速解析では、次の形式の日付データはサポートされていません。  
  
-   アルファベットの月の値。 たとえば、日付形式 Oct-31-2003 は無効です。  
  
-   DD-MM-YYYY や MM-DD-YYYY などのあいまいな形式。 たとえば、03-04-1995 や 04-03-1995 の日付は無効です。  
  
-   4 桁の暦年と、その年の日付を 3 桁で表す、基本および拡張の切り捨て形式。たとえば YYYYDDD や YYYY-DDD は無効です。  
  
-   4 桁の年、2 桁の週番号、および 1 桁の曜日番号を表す、基本および拡張の切り捨て形式。たとえば YYYYWwwD や YYYY-Www-D は無効です。  
  
-   年と週を 4 桁の年と 2 桁の週番号で表す、基本および拡張の切り捨て形式。たとえば YYYWww や YYYY-Www は無効です。  
  
 高速解析では、DT_DBDATE としてデータを出力します。 切り捨て形式の日付の値は、埋め込まれます。 たとえば、YYYY は YYYY0101 になります。  
  
 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="time-data-type"></a>時刻データ型  
 高速解析では、次の文字列形式の時刻データがサポートされています。  
  
-   先頭の空白文字を含む時刻の形式。 たとえば、値 " 10:24" は有効です。  
  
-   24 時間形式。 高速解析では、AM および PM の表記はサポートされていません。  
  
-   次の表に示す ISO 8601 時刻形式。  
  
    |形式|説明|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|2 桁の時、2 桁の分、および 2 桁の秒を表す、基本および拡張形式です。 拡張形式では、時刻の部分はコロン (:) で区切られます。|  
    |HHMI<br /><br /> HH:MI|2 桁の時と 2 桁の分を表す、基本および拡張の切り捨て形式です。 拡張形式では、時刻の部分はコロン (:) で区切られます。|  
    |HH|2 桁の時を表す切り捨て形式です。|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|午前 0 時を表す形式です。|  
  
-   次の表に示す、タイム ゾーンを指定する時刻形式。  
  
    |形式|説明|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|ローカル時間を求めるために協定世界時 (UTC) に加算される時間数と分数を示す基本形式と拡張形式。|  
    |-HH:MI<br /><br /> -HHMI|ローカル時間を求めるために協定世界時 (UTC) から減算される時間数と分数を示す基本形式と拡張形式。|  
    |+HH|ローカル時間を求めるために UTC に加算される時間数を示す切り捨て形式。|  
    |-HH|ローカル時間を求めるために UTC から減算される時間数を示す切り捨て形式。|  
    |Z|時間が UTC で表されていることを示す 0 の値。|  
  
     タイム ゾーン要素を含むことのできるすべての時刻および日付/時刻データの形式。 ただし、データが DT_DBTIMESTAMPOFFSET 型以外の場合、タイム ゾーン値は無視されます。 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。  
  
     タイム ゾーン要素を含む形式では、次の例に示すように、時間要素とタイム ゾーン要素の間にスペースはありません。  
  
     HH:MI:SS[+HH:MI]  
  
     上の例の角かっこは、タイム ゾーン値が省略可能であることを示します。  
  
-   次の表に示す、小数部を含む時刻形式。  
  
    |形式|説明|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n は、時間の端数を表す 0 ～ 9999999 の範囲の値です。 角かっこは、この値が省略可能であることを示しています。<br /><br /> たとえば、値 12.750 は 12:45 を示します。|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n は、分の端数を表す 0 ～ 9999999 の範囲の値です。 角かっこは、この値が省略可能であることを示しています。<br /><br /> たとえば、値 1220.500 は 12:20:30 を示します。|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n は、秒の端数を表す 0 ～ 9999999 の範囲の値です。 角かっこは、この値が省略可能であることを示しています。<br /><br /> たとえば、値 122040.250 は 12:20:40.15 を示します。|  
  
    > [!NOTE]  
    >  前の表の時刻形式の区切り文字には、小数点またはコンマを使用できます。  
  
-   次の例に示す、うるう秒を含む時刻値。  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 高速解析では、DT_DBTIME および DT_DBTIME2 として文字列を出力します。 切り捨て形式の時刻値は、埋め込まれます。 たとえば、HH:MI は HH:MM:00.000 になります。  
  
 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="datetime-data-type"></a>日付/時刻データ型  
 高速解析では、次の文字列形式の日付/時刻データがサポートされています。  
  
-   先頭の空白文字を含む形式。 たとえば、値 "  2003-01-10T203910" は有効です。  
  
-   YYYYMMDDT[HHMISS][+HH:MI] などの、大文字 T で区切られた有効な日付形式と有効な時刻形式、および有効なタイム ゾーン形式の組み合わせ。 時刻とタイム ゾーンの値は必須ではありません。 たとえば、"2003-10-14" は有効です。  
  
 高速解析では、期間はサポートされていません。 たとえば、YYYYMMDDThhmmss/YYYYMMDDThhmmss の形式の、開始および終了の日付と時刻で識別される期間は、解析できません。  
  
 高速解析では、DT_DATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET として文字列を出力します。 切り捨て形式の日付/時刻値は、埋め込まれます。 次の表に、欠けている日付および時刻の部分に対して追加される値を示します。  
  
|日付/時刻部分|余白|  
|---------------------|-------------|  
|Seconds|00 が追加されます。|  
|Minutes|00:00 が追加されます。|  
|Hour|00:00:00 が追加されます。|  
|日|月の日付として 01 が追加されます。|  
|Month|年の月として 01 が追加されます。|  
  
 詳細については、「 [Integration Services Data Types](data-flow/integration-services-data-types.md)」を参照してください。  
  
  
