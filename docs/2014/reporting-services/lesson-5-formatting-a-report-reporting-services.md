---
title: 'レッスン 5: レポートの書式設定 (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f1acd7bf033ca2170a2a2b0cb1f701606510bf14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108432"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>レッスン 5: レポートの書式設定 (Reporting Services)
  Sales Orders レポートに 1 つのデータ領域といくつかのフィールドを追加した後、日付および通貨のフィールド、および列ヘッダーを書式設定できます。  
  
 このトピックの内容  
  
-   [日付の書式設定します。](#bkmk_format_date)  
  
-   [通貨の書式設定します。](#bkmk_format_currency)  
  
-   [テキストのスタイルおよび列幅を変更します。](#bkmk_change_textstyle)  
  
##  <a name="bkmk_format_date"></a> 日付の書式設定します。  
 日付フィールドには、既定では日付と時刻の情報が表示されます。 このフィールドを書式設定して、日付のみを表示できます。  
  
#### <a name="to-format-a-date-field"></a>日付フィールドを書式設定するには  
  
1.  **[デザイン]** タブをクリックします。  
  
2.  `[Date]` フィールド式が入力されているセルを右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
3.  クリックして**数**、し、**カテゴリ**フィールドで、`Date`します。  
  
4.  **[型]** ボックスで **[2000 年 1 月 31 日]** を選択します。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  レポートをプレビューして `[Date]` フィールドに対する変更を確認し、デザイン ビューに戻ります。  
  
##  <a name="bkmk_format_currency"></a> 通貨の書式設定します。  
 [LineTotal] フィールドには通常の数値が表示されます。 このフィールドを書式設定して、数値を通貨として表示します。  
  
#### <a name="to-format-a-currency-field"></a>通貨フィールドを書式設定するには  
  
1.  `[LineTotal]` フィールド式が入力されているセルを右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
2.  **[数値]** をクリックし、 **[Category]** フィールドで **[通貨]** を選択します。  
  
3.  地域設定が英語 (米国) の場合、既定値は次のようになります。  
  
    -   **小数点以下の桁数 :2**  
  
    -   **負の数値 : ($12345.00)**  
  
    -   **記号 : $ 英語 (米国)**  
  
4.  [ **位取り区切り記号 (,) を使用する]** を選択します。  
  
     " **$12,345.00**" というサンプル テキストが表示されている場合、正しい設定が行われています。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  レポートをプレビューして `[LineTotal]` フィールドに対する変更を確認し、デザイン ビューに戻ります。  
  
##  <a name="bkmk_change_textstyle"></a> テキストのスタイルおよび列幅を変更します。  
 ヘッダー行の書式を変更して、レポートのデータの行と区別することもできます。 最後に、列の幅を調整します。  
  
#### <a name="to-format-header-rows-and-table-columns"></a>ヘッダー行およびテーブル列を書式設定するには  
  
1.  テーブルをクリックし、列ハンドルおよび行ハンドルをテーブルの上部および横に表示します。  
  
     ![デザイン、ヘッダー行および詳細行を持つテーブル](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "デザイン、ヘッダー行および詳細行を持つテーブル")  
  
     テーブルの上と横のグレーのバーは、列および行ハンドルです。  
  
2.  列ハンドルの間の罫線をポイントします。カーソルが 2 方向の矢印の形状に変化します。 列をドラッグして、目的のサイズに変更します。  
  
3.  列ヘッダー ラベルを含む行を選択し、 **[書式]** メニューの **[フォント]** をポイントして **[太字]** をクリックします。  
  
4.  レポートをプレビューするには、 **[プレビュー]** タブをクリックします。次のように表示されます。  
  
     ![列ヘッダーが太字になっているテーブルのプレビュー](../../2014/tutorials/media/rs-basictabledetailsformattedpreview.gif "列ヘッダーが太字になっているテーブルのプレビュー")  
  
5.  **[ファイル]** メニューの **[すべてを保存]** をクリックして、レポートを保存します。  
  
## <a name="next-steps"></a>次の手順  
 ここでは、列ヘッダー、日付値、および通貨値を書式設定しました。 次に、レポートにグループ化および合計を追加します。 「[レッスン 6:グループと合計の追加 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
