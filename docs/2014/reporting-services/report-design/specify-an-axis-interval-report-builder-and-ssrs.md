---
title: 軸の間隔の指定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9d862ac509af3936a9f09cadd01667cbe81a679c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104848"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>軸の間隔の指定 (レポート ビルダーおよび SSRS)
  軸の間隔により、軸上のラベルおよび付随する目盛りの数が定義されます。 値軸では、軸の間隔により、グラフ上のデータ ポイントに一貫性のある基準が提供されます。 ただしカテゴリ軸では、この機能により、軸ラベルなしでカテゴリが表示されることがあります。 軸の Interval プロパティで、必要な間隔の数を指定できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、実行時に、結果セットのデータに基づいて間隔の数が計算されます。 軸の間隔を計算する方法の詳細については、「[グラフの軸ラベルの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
 このトピックは、カテゴリ軸の日付または時刻の値には適用されません。 既定では、`DateTime` 値は日として表示されます。 月や期間など、別の日付または期間を指定するには、軸ラベルの書式を設定し、`DateTime` 型ではなく `String` 型のインスタンスが表示されるように軸を設定する必要があります。 また、Interval プロパティを設定する必要があります。 詳細については、「[日付または通貨として軸ラベルを書式設定する &#40;レポート ビルダーおよび SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)」を参照してください。  
  
 このトピックは、円グラフ、ドーナツ グラフ、じょうごグラフ、ピラミッド グラフなど、軸のないグラフには当てはまりません。  
  
> [!NOTE]  
>  カテゴリ軸は、通常、横軸 (X 軸) です。 ただし、横棒グラフの場合は、縦軸 (Y 軸) です。  
  
 異なる軸の間隔を指定するグラフについては、サンプル レポートに例が含まれています。 このサンプル レポートおよびその他のサンプル レポートをダウンロードする方法の詳細については、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][レポート ビルダーおよびレポート デザイナーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=198283)に関するページを参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>X 軸のすべてのカテゴリのラベルを表示するには  
  
1.  カテゴリ軸を右クリックし、 **[軸のプロパティ]** をクリックします。 **[軸のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **軸のオプション**設定`Interval`に**1**します。 すべてのカテゴリ グループのラベルが表示されます。 X 軸でカテゴリ グループのラベルを交互に表示する場合は、「 **2**」と入力します。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  軸の間隔が設定されている場合、ラベルの自動調整機能は無効になります。 軸の間隔に値を指定すると、カテゴリ軸のカテゴリ数によって、予期しないラベル付け動作が発生する場合があります。  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>軸の可変間隔の計算を有効にするには  
  
1.  変更するグラフ軸を右クリックし、 **[軸のプロパティ]** をクリックします。 **[軸のプロパティ]** ダイアログ ボックスが表示されます。  
  
2.  **軸のオプション**設定`Interval`に**自動**します。軸に収まる最適な数のカテゴリ ラベルがグラフに表示されます。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS)](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [データ領域内のデータの並べ替え (レポート ビルダーおよび SSRS)](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [[軸のプロパティ] ダイアログ ボックス、[軸のオプション] &#40;レポート ビルダーおよび SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [対数スケールの指定 &#40;レポート ビルダーおよび SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [セカンダリ軸へのデータのプロット &#40;レポート ビルダーおよび SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
