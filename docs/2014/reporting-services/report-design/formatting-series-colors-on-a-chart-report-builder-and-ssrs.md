---
title: グラフの系列の色の書式設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10245"
- "10252"
- sql12.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql12.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 445e6d2ccaba0d03de9f25d770ac22f35b628778
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105768"
---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>グラフの系列の色の書式設定 (レポート ビルダーおよび SSRS)
  Reporting Services にはグラフ用にいくつかの組み込みパレットが用意されていますが、カスタム パレットを定義することもできます。 既定では、グラフは、組み込みを使用して**BrightPastel**各系統に色パレット。 これらの色は、凡例にも表示されます。 複数の系統をグラフに追加すると、グラフでは、パレットで定義されている色の順序で系統に色が割り当てられます。  
  
 パレットにある色の数より系統の数が多い場合、グラフで色が再利用され、2 つの系統で同じ色が使用される場合があります。 このような状態は、各データ ポイントにパレットから色が割り当てられる、図形グラフを使用する場合に頻繁に起こります。 混同を避けるために、グラフの系列数と少なくとも同じ数の色を使用してカスタム パレットを定義してください。  
  
 新しいパレットを選択することも、プロパティ ペインからカスタム パレットを定義することもできます。 詳細については、「[パレットを使用したグラフの色の定義 &#40;レポート ビルダーおよび SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>組み込みパレットの使用  
 Reporting Services には、定義済みの組み込みパレットの一覧が用意されています。この組み込みパレットを使用して、グラフの系統に設定する色を定義できます。 すべての組み込みパレットには、10 ～ 16 色の値が含まれています。 組み込みパレットを拡張してさらに色を追加することはできません。このため、17 色以上が必要な場合は、カスタム パレットを定義する必要があります。  
  
 レポートを印刷する場合、 **[グレースケール]** パレットの使用を検討してください。 このパレットでは、白と黒の影を使用してグラフの各系統を表します。  
  
 以前のバージョンの Reporting Services では、[既定] という名前のパレットが既定のグラフ パレットとして使用されていました。 既定のグラフ パレットは同じ名前で維持され、一貫性が保たれています。 グラフは、[既定] パレットを使用してシームレスにアップグレードされますが、アップグレード後は名前を変更するようにしてください。  
  
## <a name="using-custom-palettes"></a>カスタム パレットの使用  
 グラフに独自の色を適用する場合は、カスタム パレットを使用します。 カスタム パレットを使用すると、グラフに表示される順序で独自の色を追加できます。 カスタム パレットは、グラフの系列の数がデザイン時に不明な場合に特に役立ちます。 詳細については、「[パレットを使用したグラフの色の定義 &#40;レポート ビルダーおよび SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="using-a-color-fill-on-each-series"></a>各系統での塗りつぶしの使用  
 グラフの各系統に色を指定して、グラフに独自の色を定義することもできます。 この操作を行うには、 **[系列のプロパティ]** ダイアログ ボックスを開き、 **Color** プロパティを **[塗りつぶし]** に設定します。 この方法により、定義されたすべてのパレットがオーバーライドされます。 一般的に、データセットの系統の数はレポート処理の段階まで不明な場合があるため、カスタム パレットを使用して独自の色を定義することをお勧めします。  
  
 この方法は、式を基に系統の色を条件に応じて設定する場合に最も適しています。  詳細については、「 [グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS)](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)をクリックします。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [複数の図形グラフでの色の統一 &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
 [パレットを使用したグラフの色の定義 &#40;レポート ビルダーおよび SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [ストリップ ラインの追加によるグラフのデータの強調表示 &#40;レポート ビルダーおよび SSRS&#41;](highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [グラフへの傾斜、エンボス、およびテクスチャのスタイルの追加 &#40;レポート ビルダーおよび SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [グラフの凡例の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](chart-legend-formatting-report-builder.md)  
  
  
