---
title: LANGUAGE と FORMAT_STRING formated_value |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a116be708dd714a48d1cc936a08350237ca98ddf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074398"
---
# <a name="language-and-formatstring-on-formatedvalue"></a>FORMATED_VALUE の LANGUAGE と FORMAT_STRING
  FORMATTED_VALUE プロパティは、セルの VALUE、FORMAT_STRING、および LANGUAGE の各プロパティの相互作用に基づいて構築されます。 このトピックではそのしくみについて説明します。  
  
## <a name="value-formatstring-language-properties"></a>VALUE プロパティ、FORMAT_STRING プロパティ、LANGUAGE プロパティ  
 これらのプロパティを組み合わせて使用するための準備として、次の表に各プロパティの概要を示します。  
  
 VALUE  
 書式設定されていないセルの値。  
  
 FORMAT_STRING  
 FORMATTED_VALUE プロパティを生成するためにセルの値に適用される書式設定テンプレート  
  
 LANGUAGE  
 ローカライズされたバージョンの FORMATTED_VALUE を生成するために FORMAT_STRING と共に適用されるロケールの指定  
  
## <a name="formattedvalue-constructed"></a>FORMATTED_VALUE の構築  
 FORMATTED_VALUE プロパティは、FORMAT_STRING プロパティで指定されている書式設定テンプレートを VALUE プロパティの値に適用することによって構築されます。 また、書式設定値が `named formatting literal` の場合は、LANGUAGE プロパティで指定されている言語の用法に従って FORMAT_STRING の出力が変更されます。 名前付き書式設定リテラルはすべてローカライズできるように定義されています。 たとえば `"General Date"` はローカライズ可能な指定ですが、 `"YYYY-MM-DD hh:nn:ss",` は、言語の指定に関係なくこの定義のとおりに日付を表示するように指定するテンプレートです。  
  
 FORMAT_STRING のテンプレートと LANGUAGE の指定が競合している場合は、FORMAT_STRING のテンプレートが LANGUAGE の指定をオーバーライドします。 たとえば、FORMAT_STRING="$ #0"、LANGUAGE=1034 (スペイン)、VALUE=123.456 の場合、書式設定テンプレートの値が言語の指定よりもオーバーライドされるため、FORMATTED_VALUE="€ 123" (予想される書式) ではなく FORMATTED_VALUE="$ 123" になります。  
  
### <a name="examples"></a>使用例  
 以下の例は、LANGUAGE と FORMAT_STRING を組み合わせて使用した場合に得られる出力を示しています。  
  
 1 つ目の例は数値の書式設定の例で、2 つ目の例は日付と時刻の値の書式設定の例です。  
  
 それぞれの例について多次元式 (MDX) コードが示されています。  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して上の MDX クエリをロケール 1033 のサーバーとクライアントで実行すると、結果 (置き換え後) は次のようになります。  
  
|Member|FORMATTED_VALUE|説明|  
|------------|----------------------|-----------------|  
|A|$5,040.00|FORMAT_STRING が `Currency` に設定され、LANGUAGE が `1033`に設定されています (システム ロケール値から継承)。|  
|B|€5.040,00|FORMAT_STRING が `Currency` に設定され (A から継承)、LANGUAGE が明示的に `1034` (スペイン) に設定されています。したがって、ユーロ記号が使用され、小数点と桁の区切り文字も変わっています。|  
|c|$5.040,00|FORMAT_STRING が `$#,##0.00` に設定されて、A から継承された Currency がオーバーライドされています。LANGUAGE は明示的に `1034` (スペイン) に設定されています。 FORMAT_STRING プロパティで通貨記号が明示的に $ に設定されているため、FORMATTED_VALUE には $ 記号が付いています。 一方、 `.` (ドット) と `,` (コンマ) はそれぞれ小数点区切り文字と桁区切り文字のプレースホルダーであるため、言語の指定の影響を受けます。したがって、小数点と桁の区切り文字がローカライズされた出力が生成されています。|  
|D|5.04E+03|FORMAT_STRING が `Scientific` に設定され、LANGUAGE が `1033`に設定されています (システム ロケール値から継承)。したがって、小数点区切り文字が `.` (ドット) になっています。|  
|E|5,04E+03|FORMAT_STRING が `Scientific` に設定され、LANGUAGE が明示的に `1034,` に設定されています。したがって、小数点区切り文字が `,` (コンマ) になっています。|  
|F|50.40%|FORMAT_STRING が `Percent` に設定され、LANGUAGE が `1033`に設定されています (システム ロケール値から継承)。したがって、小数点区切り文字が `.` (ドット) になっています。<br /><br /> VALUE が 5040 から 0.5040 に変更されたことに注意してください。|  
|G|50,40%|FORMAT_STRING が `Percent`に設定され (F から継承)、LANGUAGE が明示的に `1034` に設定されています。したがって、小数点区切り文字が `,` (コンマ) になっています。<br /><br /> VALUE が F の値から継承されていることに注意してください。|  
|H|いいえ|FORMAT_STRING が `YES/NO`に設定され、VALUE が 0 に設定され、LANGUAGE が明示的に `1034`に設定されています。英語の NO とスペイン語の NO は変わらないため、FORMATTED_VALUE には目に見える違いはありません。|  
|I|SI|FORMAT_STRING が `YES/NO`に設定され、VALUE が 59 に設定され、LANGUAGE が明示的に `1034`に設定されています。YES/NO の書式設定の定義ではゼロ (0) 以外の値はすべて YES になり、ここでは言語がスペイン語に設定されているため、FORMATTED_VALUE は SI になります。|  
|J|Desactivado|FORMAT_STRING が `ON/OFF`に設定され、VALUE が 0 に設定され、LANGUAGE が明示的に `1034`に設定されています。ON/OFF の書式設定の定義では値がゼロ (0) と等しい場合は OFF になり、ここでは言語がスペイン語に設定されているため、FORMATTED_VALUE は Desactivado になります。|  
|K|Activado|FORMAT_STRING が `ON/OFF`に設定され、VALUE が -312 に設定され、LANGUAGE が明示的に `1034`に設定されています。ON/OFF の書式設定の定義ではゼロ (0) 以外の値はすべて ON になり、ここでは言語がスペイン語に設定されているため、FORMATTED_VALUE は Activado になります。|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して上の MDX クエリをロケール 1033 のサーバーとクライアントで実行すると、結果 (置き換え後) は次のようになります。  
  
|Member|FORMATTED_VALUE|説明|  
|------------|----------------------|-----------------|  
|A|3/12/1959 6:30:00 AM|FORMAT_STRING が CDate() 式によって暗黙的に `General Date` に設定され、LANGUAGE が `1033` (英語) に設定されています (システム ロケール値から継承)。|  
|B|Thursday, March 12, 1959|FORMAT_STRING が明示的に `Long Date` に設定され、LANGUAGE が `1033` (英語) に設定されています (システム ロケール値から継承)。|  
|c|12/03/1959 6:30:00|FORMAT_STRING が明示的に `General Date` に設定され、LANGUAGE が明示的に `1034` (スペイン語) に設定されています。<br /><br /> 月と日の位置が米国の書式スタイルとは逆になっていることに注意してください。|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING が明示的に `Long Date` に設定され、LANGUAGE が明示的に `1034` (スペイン語) に設定されています。<br /><br /> 月と曜日がスペイン語になっていることに注意してください。|  
|E|1959/03/12 6:30:00|FORMAT_STRING が明示的に `General Date` に設定され、LANGUAGE が明示的に `1041` (日本語) に設定されています。<br /><br /> 日付の書式が "年/月/日 時:分:秒" になったことに注意してください。|  
|F|1959年3月12日|FORMAT_STRING が明示的に `Long Date` に設定され、LANGUAGE が明示的に `1041` (日本語) に設定されています。|  
|G|6:30:00 AM|FORMAT_STRING が明示的に `Long Time` に設定され、LANGUAGE が `1033` (英語) に設定されています (システム ロケール値から継承)。|  
|H|06:30|FORMAT_STRING が明示的に `Short Time` に設定され、LANGUAGE が `1033` (英語) に設定されています (システム ロケール値から継承)。|  
|I|6:30:00|FORMAT_STRING が明示的に `Long Time` に設定され、LANGUAGE が明示的に `1034` (スペイン語) に設定されています。|  
|J|06:30|FORMAT_STRING が明示的に `Short Time` に設定され、LANGUAGE が明示的に `1034` (スペイン語) に設定されています。|  
|K|6:30:00|FORMAT_STRING が明示的に `Long Time` に設定され、LANGUAGE が明示的に `1041` (日本語) に設定されています。|  
|L|06:30|FORMAT_STRING が明示的に `Short Time` に設定され、LANGUAGE が明示的に `1041` (日本語) に設定されています。|  
  
## <a name="see-also"></a>参照  
 [FORMAT_STRING の内容 (MDX)](mdx-cell-properties-format-string-contents.md)   
 [セル プロパティの使用 (MDX)](mdx-cell-properties-using-cell-properties.md)   
 [プロパティ値の作成および使用&#40;MDX&#41;](../../creating-and-using-property-values-mdx.md)   
 [MDX クエリの基礎 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
