---
title: 軸の間隔の指定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ecee87ddf31314b8e54c98148ab0570db08a1caf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578497"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>軸の間隔の指定 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] ページ分割されたレポートで軸の間隔を設定して、グラフのカテゴリ (x) 軸に表示するラベル数と目盛り数を変更する方法について説明します。
 
値軸 (通常は y 軸) では、軸の間隔により、グラフのデータ ポイントに一貫性のある基準が提供されます。 

ただし、カテゴリ軸 (通常は x 軸) では、軸の間隔の自動調整によって、カテゴリの軸ラベルが表示されないことがあります。 軸の Interval プロパティで、必要な間隔の数を指定できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、実行時に、結果セットのデータに基づいて間隔の数が計算されます。 軸の間隔を計算する方法の詳細については、「 [グラフの軸ラベルの書式設定](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  

サンプル データを使って軸の間隔を設定するには、「[チュートリアル: レポートへの縦棒グラフの追加 (レポート ビルダー)](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)」を参照してください。
  
> [!NOTE]  
>  カテゴリ軸は、通常、横軸 (X 軸) です。 ただし、横棒グラフの場合は、縦軸 (Y 軸) です。  
>
> このトピックで対象としない内容:
>-   カテゴリ軸の日付値または時刻値。 既定では、 **DateTime** 値は日として表示されます。 月や時間間隔など、別の日時間隔を指定できます。 詳細については、「 [日付または通貨として軸ラベルを書式設定する](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)」を参照してください。  
>-  円グラフ、ドーナツ グラフ、じょうごグラフ、ピラミッド グラフなど、軸のないグラフ。 
  
## <a name="to-show-all-the-category-labels-on-the-x-axis"></a>X 軸のすべてのカテゴリのラベルを表示するには  

この縦棒グラフでは、横軸のラベル間隔が自動に設定されています。

![report-builder-column-chart-preview-x-axis-interval-auto](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-auto.png)
  
1.  カテゴリ軸を右クリックし、 **[横軸のプロパティ]** をクリックします。   

    ![report-builder-column-chart-x-axis-labels](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-labels.png)
  
2.  **[横軸のプロパティ]** ダイアログ ボックスの **[軸のオプション]** タブで、 **[間隔]** を **1** に設定して、すべてのカテゴリ グループ ラベルを表示します。 X 軸でカテゴリ グループのラベルを 1 つおきに表示するには、 **2**と入力します。 

     ![report-builder-column-chart-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-interval-one.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    以上の操作で、縦棒グラフにすべての横軸のラベルが表示されました。

    ![report-builder-column-chart-preview-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-one.png)
  
    > [!NOTE]  
    >  軸の間隔を設定すると、ラベルの自動調整機能は無効になります。 軸の間隔に値を指定すると、カテゴリ軸のカテゴリ数によって、予期しないラベル付け動作が発生する場合があります。  

## <a name="change-the-label-interval-in-properties-pane"></a>プロパティ ペインでラベルの間隔を変更する

プロパティ ペインでラベルの間隔を設定することもできます。

1.  レベル デザイン ビューでグラフをクリックし、横軸ラベルを選択します。

3. プロパティ ペインで、LabelInterval を **1**に設定します。

    ![report-builder-column-chart-set-label-interval](../../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    グラフはデザイン ビューで同じに見えます。 
    
5.  **[実行]** をクリックして、レポートをプレビューします。

    ![report-builder-column-chart-label-interval-one-preview](../../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    これでグラフにすべてのラベルが表示されました。
  
## <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>軸の可変間隔の計算を有効にするには  

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の既定では、軸の間隔は自動に設定されます。この手順では、既定値に設定を戻す方法について説明します。 
  
1.  変更するグラフ軸を右クリックし、 **[軸のプロパティ]** をクリックします。 
  
2.  **[横軸のプロパティ]** ダイアログ ボックスの **[軸のオプション]** タブで、 **[間隔]** を **[自動]** に設定して、すべてのカテゴリ グループ ラベルを表示します。軸に収まる最適な数のカテゴリ ラベルがグラフに表示されます。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [データ領域内のデータの並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [[軸のプロパティ] ダイアログ ボックス、[軸のオプション] &#40;レポート ビルダーおよび SSRS&#41;](https://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
 [対数スケールの指定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [セカンダリ軸へのデータのプロット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
