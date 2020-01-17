---
title: テキスト ファイルの形式 (テキスト ファイル ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 51619902398f0e3d0a8307a0c76a40ab898ce88d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912441"
---
# <a name="text-file-format-text-file-driver"></a>テキスト ファイルの形式 (テキスト ファイル ドライバー)
テキストの ODBC ドライバーでは、両方の区切りと固定幅テキスト ファイルをサポートします。 テキスト ファイルは、省略可能なヘッダー行と 0 個以上のテキスト行で構成されます。  
  
 ヘッダー行は、同じ形式を使用してテキスト ファイルの他の行として、テキストの ODBC ドライバーは、ヘッダー行エントリをデータではなく、列名として解釈します。  
  
 区切られたテキスト行には区切り記号で区切られた 1 つまたは複数のデータ値が含まれています。 コンマ、タブ、または独自の区切り記号。 同じ区切り記号は、ファイル全体で使用する必要があります。 Null データ値は、それらの間のデータの行の 2 つの区切り記号で示されていません。 区切られたテキスト行内の文字の文字列を二重引用符で囲むことができます ("")。 区切られた値の前後に空白は行われません。  
  
 固定幅テキスト行の場合は、各データ項目の幅は、スキーマで指定されます。 空白では、null データ値が示されます。  
  
 テーブルは、255 個のフィールドの最大数に制限されます。 フィールド名は 64 文字に制限されていますし、フィールド幅は 32,766 文字に制限されます。 レコードは、65,000 バイトに制限されます。  
  
 1 人のユーザーに対してのみ、テキスト ファイルを開くことができます。 複数のユーザーがサポートされていません。  
  
 次の文章では、プログラマにとっては、書き込まれるには、テキストの ODBC ドライバーで読み取ることができるテキスト ファイルの形式を定義します。  
  
|Format|表現|  
|------------|--------------------|  
|非斜体|文字に示すように入力する必要があります。|  
|*斜体*|文法で定義されている引数|  
|角かっこ ()|省略可能な項目|  
|中かっこ ({})|相互に排他的な選択肢の一覧|  
|垂直バー (&#124;)|個別に相互に排他的な選択|  
|省略記号 (...)|1 つまたは複数回繰り返すことができる項目|  
  
 テキスト ファイルの形式です。  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  固定幅テキスト ファイル内の各列の幅は、Schema.ini ファイルで指定されます。  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  カスタム区切りテキスト ファイルの区切り記号は、Schema.ini ファイルで指定されます。  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  区切られたファイルの場合、NULL は、2 つの区切り記号の間のデータがありませんによって表されます。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  固定幅ファイルの場合は、null 値はスペースで表されます。
