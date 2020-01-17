---
title: 数値と日付の書式設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.placeholderproperties.number.f1
- "10127"
- sql13.rtp.rptdesigner.textboxproperties.number.f1
- "10130"
- "10286"
- sql13.rtp.rptdesigner.serieslabelproperties.number.f1
- "10285"
- sql13.rtp.rptdesigner.axisproperties.number.f1
ms.assetid: 6de1a725-9f06-4708-be26-2d55e442e344
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2802da2b5b227f3cdb4e4ea3bfa59ca15f5d8d2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576085"
---
# <a name="formatting-numbers-and-dates-report-builder-and-ssrs"></a>数値と日付の書式設定 (レポート ビルダーおよび SSRS)
  データ領域の数値と日付の書式を設定するには、対応するデータ領域の **[プロパティ]** ダイアログ ボックスの **[数値]** ページを使用します。  
  
 テキスト ボックスのレポート アイテム内の書式文字列を指定するには、書式を設定するアイテムを選択して右クリックし、 **[テキスト ボックスのプロパティ]** を選択してから **[数値]** をクリックする必要があります。 テーブルまたはマトリックスのセルは個別のテキスト ボックスであるため、同じ方法でテーブル データ領域またはマトリックス データ領域の個別のセルを書式設定できます。  
  
 グラフ データ領域では、通常、カテゴリ軸 (x 軸) に日付が示され、値軸 (y 軸) に値が示されます。 グラフの書式を指定するには、軸を右クリックし、 **[軸のプロパティ]** を選択します。 値軸では、数値の書式しか指定できません。 詳細については、「[グラフの軸ラベルの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
 ゲージのデータ領域で書式を指定するには、ゲージのスケールを右クリックし、 **[放射状のスケールのプロパティ]** または **[線形スケールのプロパティ]** を選択します。  
  
> [!NOTE]  
>  目的の書式設定オプションがグレー表示されている場合、その書式設定オプションと、データ ソースに設定されているフィールドのデータ型に互換性がないことを示します。 たとえば、フィールドに格納されているデータが数値であっても、フィールドのデータ型が文字列である場合、通貨型や 10 進数型などの数値データ書式設定オプションを適用できません。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="considerations-for-formatting-numbers-and-dates"></a>数値および日付の書式設定に関する注意点  
 レポートの数値および日付の書式を設定する前に、次のことを考慮してください。  
  
-   既定では、数値の書式はクライアント コンピューターのカルチャ設定を反映して設定されます。 数値の表示方法を指定するために書式設定の文字列を使用すると、レポートを参照するユーザーの地域に関係なく、一貫した書式を指定できます。  
  
-   **[数値]** ページで指定された書式は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 標準の数値書式設定文字列のサブセットです。 ダイアログ ボックスに表示されないカスタム書式を使用して数値や日付の書式を設定するには、数値または日付の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 書式設定文字列を使用します。 カスタム書式設定文字列の詳細については、MSDN のトピック「 [型の書式設定](https://go.microsoft.com/fwlink/?LinkId=112024) 」を参照してください。  
  
-   カスタム書式設定文字列が指定されている場合、既定のカルチャ固有の設定よりも優先度が高くなります。 たとえば、カスタム書式設定文字列 "#,###" を設定して、数値 1234 を 1,234 と表すとします。 これは、米国のユーザーとヨーロッパのユーザーで意味が異なる場合があります。 カスタム書式設定を指定する前に、レポートを参照する異なるカルチャのユーザーに対して選択した書式設定がどのような影響を与えるか考慮するようにしてください。  
  
-   指定した書式設定文字列が正しくない場合、書式設定されたテキストは、書式設定をオーバーライドするリテラル文字列として解釈されます。  
  
-   同じテキスト ボックスで数字と文字が混在するテキストの書式を設定する場合、プレースホルダーを使用して、テキストの数値以外の部分とは別に数値の書式を設定します。 詳細については、「 [テキストとプレースホルダーの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)をクリックする必要があります。 テキスト ボックスで Format プロパティについて指定された書式設定文字列が正しくない場合、書式設定文字列は無視されます。 グラフまたはゲージで Format プロパティについて指定された書式設定文字列が正しくない場合、指定した書式設定文字列は文字列として解釈され、書式設定は適用されません。  
  
-   **[カテゴリ]** の **[通貨]** をクリックして、 **[値の表示単位]** をオンにすると、 **[千]** 、 **[百万]** 、または **[十億]** を選択し、財務上の形式を使用して数値を表示できます。 たとえば、フィールド値が 1,789,905,394 の場合、 **[十億]** を選択して、小数点以下桁数を 2 桁に指定すると、レポートに表示される値は 1.78 です。  
  
## <a name="see-also"></a>参照  
 [テキストとプレースホルダーの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [線、色、および画像の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [日付または通貨として軸ラベルを書式設定する &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [ゲージのスケールの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
