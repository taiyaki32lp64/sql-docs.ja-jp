---
title: MDX および DAX での VBA 関数 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 39a0db181f3b1d1a40af1a5fa27ba78366a9d2b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135020"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX および DAX での VBA 関数


  このドキュメントには、交差で使用できるすべての VBA 関数の参照が含まれています[Visual Basic for Applications の関数](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications)MDX でサポートされている; も、一覧では、DAX 言語で同等の機能がある場合に、メモが含まれています.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 関数リファレンス  
  
|関数名|Supported|メモ|  
|-------------------|---------------|-----------|  
|Abs|DAX、MDX||  
|Array|サポートされていません||  
|Asc|MDX のみ||  
|AscW|MDX のみ||  
|Atn|MDX のみ||  
|CallByName|サポートされていません||  
|CBool|MDX のみ||  
|CByte|MDX のみ||  
|CCur|MDX のみ||  
|CDate|MDX のみ||  
|CDbl|MDX のみ||  
|CDec|MDX のみ||  
|Choose|MDX のみ||  
|Chr|MDX のみ||  
|CInt|MDX のみ||  
|CLng|MDX のみ||  
|CLngLng|サポートされていません||  
|CLngPtr|サポートされていません||  
|Command|サポートされていません||  
|Cos|MDX のみ||  
|CreateObject|サポートされていません||  
|CSng|MDX のみ||  
|CStr|MDX のみ||  
|CurDir|サポートされていません||  
|CVar|MDX のみ||  
|CVErr|サポートされていません||  
|date|MDX のみ|**警告**DAX が同じで別の関数を実装する名前は、DATE (Year, Month, Day) 関数は、指定された引数から日付型の値を生成するために使用|  
|DateAdd|MDX のみ|**警告**DAX が同じで別の関数を実装する名前の dateadd (\<日付 >、< number_of_intervals >\<間隔 >) の数で指定された日付をシフトするために使用されている関数の間隔を指定|  
|DateDiff|MDX のみ||  
|DatePart|MDX のみ||  
|DateSerial|MDX のみ||  
|DateValue|DAX、MDX||  
|Day|DAX、MDX||  
|DDB|MDX のみ||  
|Dir|サポートされていません||  
|DoEvents|サポートされていません||  
|Environ|サポートされていません||  
|EOF|サポートされていません||  
|Error|サポートされていません||  
|Exp|DAX、MDX||  
|FileAttr|サポートされていません||  
|FileDateTime|サポートされていません||  
|FileLen|サポートされていません||  
|Assert|サポートされていません|**警告**MDX 実装と同じ名前の別の関数は FILTER (Set_Expression, Logical_Expression) 関数は、指定された引数から検索条件に基づいて、指定されたセットをフィルター処理の結果セットを返します<br /><br /> **警告**DAX が同じで別の関数を実装する名前の FILTER (\<テーブル >、\<フィルター >) 関数は、別のテーブルまたは指定された引数から式のサブセットを表すテーブルを返します。|  
|Fix|MDX のみ||  
|Format (Visual Basic for Applications)|DAX、MDX||  
|FormatCurrency|サポートされていません||  
|FormatDateTime|サポートされていません||  
|FormatNumber|サポートされていません||  
|FormatPercent|サポートされていません||  
|FreeFile|サポートされていません||  
|FV|MDX のみ||  
|GetAllSettings|サポートされていません||  
|GetAttr|サポートされていません||  
|GetObject|サポートされていません||  
|GetSetting|サポートされていません||  
|Hex|MDX のみ||  
|Hour|DAX、MDX||  
|Iif 関数|MDX のみ|**警告**DAX は、名前を持つような関数を実装します。IF (logical_test、value_if_true, value_if_false) 関数。|  
|IMEStatus|サポートされていません||  
|入力|サポートされていません||  
|InputBox|サポートされていません||  
|InStr|MDX のみ||  
|InStrRev|サポートされていません||  
|Int|DAX、MDX||  
|IPmt|MDX のみ||  
|IRR|MDX のみ||  
|IsArray|MDX のみ||  
|IsDateMDX のみ||  
|IsEmpty|MDX のみ||  
|IsError|DAX、MDX||  
|IsMissing|MDX のみ||  
|IsNull|MDX のみ||  
|IsNumeric|MDX のみ||  
|IsObject|サポートされていません||  
|Join|サポートされていません||  
|LBound|サポートされていません||  
|LCase|MDX のみ||  
|Left|DAX、MDX||  
|Len|DAX、MDX||  
|Loc|サポートされていません||  
|LOF|サポートされていません||  
|Log|MDX のみ|**重要な**DAX が同じで別の関数を実装する名前は、LOG (number, base) 関数。 指定された引数から指定されたベースに数値の対数を返します。|  
|LTrim|MDX のみ||  
|MacID|サポートされていません||  
|MacScript|サポートされていません||  
|Mid|DAX、MDX||  
|Minute|DAX、MDX||  
|MIRR|MDX のみ||  
|Month|DAX、MDX||  
|MonthName|サポートされていません||  
|MsgBox|サポートされていません||  
|Now|DAX、MDX||  
|NPer|MDX のみ||  
|NPV|MDX のみ||  
|Oct|MDX のみ||  
|Partition|MDX のみ||  
|Pmt|MDX のみ||  
|PPmt|MDX のみ||  
|PV|MDX のみ||  
|QBColor|MDX のみ||  
|Rate|MDX のみ||  
|Replace|サポートされていません||  
|RGB|MDX のみ||  
|Right|DAX、MDX||  
|Rnd|MDX のみ||  
|Round|DAX、MDX||  
|RTrim|MDX のみ||  
|Second|DAX、MDX||  
|Seek|サポートされていません||  
|Sgn|DAX、MDX||  
|Shell|サポートされていません||  
|Sin|MDX のみ||  
|SLN|MDX のみ||  
|Space|MDX のみ||  
|Spc|サポートされていません||  
|Split|サポートされていません||  
|Sqr|MDX のみ||  
|Str|MDX のみ||  
|StrComp|MDX のみ||  
|StrConv|MDX のみ||  
|String|MDX のみ||  
|StrReverse|サポートされていません||  
|Switch|MDX のみ||  
|SYD|MDX のみ||  
|Tab|サポートされていません||  
|Tan|MDX のみ||  
|Time|サポートされていません||  
|Timer|MDX のみ||  
|TimeSerial|MDX のみ||  
|TimeValue|DAX、MDX||  
|Trim|DAX、MDX||  
|TypeName|MDX のみ||  
|UBound|サポートされていません||  
|UCase|MDX のみ||  
|Val|MDX のみ||  
|VarType|サポートされていません||  
|Weekday|DAX、MDX||  
|WeekdayName|サポートされていません||  
|Year|DAX、MDX||  
  
  
