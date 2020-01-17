---
title: 'レッスン 5 : レポートの書式設定 (Reporting Services) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8bf8b6814f7989a904507cd89fbea397b8b6930
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105927"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>レッスン 5 : レポートの書式設定 (Reporting Services)

Sales Orders レポートに 1 つのデータ領域といくつかのフィールドを追加した後、日付および通貨のフィールド、および列ヘッダーを書式設定できます。

## <a name="bkmk_format_date"></a>日付の書式設定

Date フィールド式には、既定では日付と時刻の情報が表示されます。 このフィールドを書式設定して、日付のみを表示できます。

1. **[デザイン]** タブを選択します。
2. `[Date]` フィールド式があるセルを右クリックし、 **[テキスト ボックスのプロパティ]** を選択します。
3. **[数値]** を選択し、 **[カテゴリ]** フィールドで **[日付]** を選択します。
4. **[型]** ボックスで **[2000 年 1 月 31 日]** を選択します。
5. **[OK]** を選択して書式を適用します。
6. レポートをプレビューして `[Date]` フィールド書式に対する変更を確認し、デザイン ビューに戻ります。

## <a name="bkmk_format_currency"></a>通貨の書式設定

[LineTotal] フィールド式には通常の数値が表示されます。 これを書式設定して、数値を通貨として表示することができます。

1. `[LineTotal]` 式があるセルを右クリックし、 **[テキスト ボックスのプロパティ]** を選択します。
2. 左端の列リスト ボックスから **[数値]** を選択し、 **[カテゴリ]** リストボックスから **[通貨]** を選択します。
3. 地域設定が英語 (米国) の場合、 **[型]** リスト ボックスの既定値は次のようになります。
    - **小数点以下の桁数 : 2**
    - **負の数値 : ($12345.00)**
    - **記号 : $ 英語 (米国)**
4. [ **位取り区切り記号 (,) を使用する]** を選択します。 " **$12,345.00**" というサンプル テキストが表示されている場合、正しい設定が行われています。
5. **[OK]** を選択して書式を適用します。
6. レポートをプレビューして `[LineTotal]` 式の列に対する変更を確認し、デザイン ビューに戻ります。  

## <a name="bkmk_change_textstyle"></a>テキスト スタイルおよび列幅の変更

ヘッダー行を強調表示し、データ列の幅を調整することで、レポートに他の書式追加することができます。

### <a name="to-format-header-rows-and-table-columns"></a>ヘッダー行およびテーブル列を書式設定するには

1. テーブルを選択し、列および行ハンドルをテーブルの上部および横に表示します。 テーブルの上と横のグレーのバーは、列および行ハンドルです。

2. 列ハンドルの間の罫線をポイントします。カーソルが 2 方向の矢印の形状に変化します。 列をドラッグして、目的のサイズに変更します。
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. 列ヘッダー ラベルを含む行を選択し、 **[書式]** メニューから **[フォント]**  >  **[太字]** を選択します。

4. レポートをプレビューします。 次のように表示されます。

    ![列ヘッダーが太字になっているテーブルのプレビュー](media/rs-basictabledetailsformattedpreview.png "列ヘッダーが太字になっているテーブルのプレビュー")  

5. **[ファイル]** メニューから **[すべてを保存]** をクリックしてレポートを保存します。

## <a name="next-steps"></a>次の手順

このレッスンでは、列ヘッダーとフィールド式の書式を正常に設定しました。 次に、レポートにグループおよび合計を追加します。 「[レッスン 6: グループと合計の追加 &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)」に進みます。

## <a name="see-also"></a>参照

[数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
