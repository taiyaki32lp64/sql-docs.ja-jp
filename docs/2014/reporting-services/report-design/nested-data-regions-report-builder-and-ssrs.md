---
title: 入れ子になったデータ領域 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 15c2bc9b-428a-47ac-9630-8dde925d0595
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 293bfe1f270d32bc64d4344c5363a0be2cd74b84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105522"
---
# <a name="nested-data-regions-report-builder-and-ssrs"></a>入れ子になったデータ領域 (レポート ビルダーおよび SSRS)
  グラフなどのデータ領域をマトリックスなどの別のデータ領域に挿入して入れ子化することができます。この方法は通常、データの要約を簡潔に表示する場合や、視覚的な表示およびテーブルやマトリックスの表示を行う場合に使用します。  
  
 たとえば、販売店を行、四半期を列として販売注文をまとめたマトリックス ( *Tablix*とも呼ばれる) では、全販売店の売り上げをテーブルやグラフにまとめてコーナー セルに追加できます。グラフを表の列ヘッダーに追加すると、全売り上げに対してその列の販売店が貢献した売り上げの割合を示すこともできます。  
  
 ![rs_NestedDataRegion](../media/rs-nesteddataregion.gif "rs_NestedDataRegion")  
  
 この図では、コーナー セルの円グラフと行のスパークライン グラフが、入れ子になったデータ領域です。  
  
 入れ子になったデータ領域は、親のデータ領域と同じレポート データセットに基づくように定義されています。 別のデータセットに基づくデータ領域を入れ子にすることはできません。 別のデータセットのデータを表示するには詳細レポートまたはサブレポートを使用します。 詳細については、「 [ドリルスルー、ドリルダウン、サブレポート、および入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](drillthrough-drilldown-subreports-and-nested-data-regions.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-scope-for-a-nested-data-region"></a>入れ子データ領域のスコープについて  
 入れ子データ領域のデータのスコープは、それが親データ領域のどこに配置されているかによって自動的に定義されます。 たとえば、Tablix コーナー セルに入れ子になっているグラフのデータ スコープは、Tablix データ領域に関連付けられているデータセットですが、データセット、Tablix データ領域、およびグラフ データ領域に対するフィルターも適用されます。 Tablix セルに入れ子になっている Tablix のデータ スコープは、そのセルが所属する行と列のグループ フィルターを適用したスコープに制限されることを除き、コーナー セルの場合と同じです。 スコープの詳細については、「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
 次の一覧は Tablix セルでのスコープを領域別に説明したものです。  
  
-   **Tablix コーナー** スコープは Tablix データ領域にリンクされたデータ領域のデータ。ただし、データセットと外側の Tablix に対するフィルターおよび並べ替え式が適用されます。  
  
-   **Tablix 列グループ** 最も内側の列グループのデータ。ただし、データセット、外側の Tablix、およびその列グループに対するフィルターおよび並べ替え式が適用されます。  
  
-   **Tablix 行グループ** 最も内側の行グループのデータ。ただし、データセット、外側の Tablix、およびその行グループに対するフィルターおよび並べ替え式が適用されます。  
  
-   **Tablix 本体** 最も内側の行グループと列グループが重なる部分のデータ。ただし、データセット、外側の Tablix、およびその行グループと列グループに対するフィルターおよび並べ替え式が適用されます。  
  
 詳細については、「[Tablix データ領域部分 &#40;レポート ビルダーおよび SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="nesting-a-chart-sparkline-or-data-bar-in-a-tablix"></a>Tablix にグラフ、スパークライン、データ バーを挿入するには  
 Tablix 列のグループ ヘッダー行またはグループ フッター行にグラフ (スパークラインとデータ バーを含む) を追加するとき、あるいは Tablix 本体のセルにグラフを追加するとき、グラフに渡されるデータはそのセル用のサブセットに制限されます。 既定では、Tablix セルにグラフを追加すると、グラフの寸法はそのセルを満たす大きさになります。  
  
> [!NOTE]  
>  Tablix セル内のグラフのサイズを制御するには、まずグラフを長方形に入れて、その長方形を Tablix セルに入れます。  
  
 既定では、グラフの凡例の色はグラフ シリーズの中のデータ点の色によって決まります。 同じカテゴリのデータに同じ色が使用されるように、入れ子になっているグラフ データ領域の色を制御するには、ユーザー定義の色を使用して、そのデータに並べ替え式を設定する必要があります。 詳細については、「[複数の図形グラフでの色の統一 &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)」と「[データ領域内のデータの並べ替え &#40;レポート ビルダーおよび SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="nesting-a-gauge-or-an-indicator-in-a-tablix"></a>Tablix にゲージまたはインジケーターを挿入するには  
 主要業績評価指標 (KPI) を表示するために、表、マトリックス、またはリストの中でゲージまたはインジケーターを入れ子にすることができます。 表の中にゲージまたはインジケーターを配置すると、それらは Tablix の各行でレンダリングされます。 Tablix へのインジケーターの追加の詳細については、「[インジケーター &#40;レポート ビルダーおよび SSRS&#41;](indicators-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="adding-a-gauge-to-a-tablix"></a>Tablix へのゲージの追加  
 Tablix データ領域にゲージを追加するには次の 2 つの方法があります。  
  
-   Tablix セルの内部をクリックし、ゲージを挿入する。 **[ゲージの種類の選択]** ダイアログ ボックスが表示されます。 ゲージの種類を選択すると、選択された Tablix セル内にゲージのデータ領域が配置されます。 通常は、ゲージのレイアウトを調整するために Tablix のサイズを変更する必要があります。  
  
-   表の外でクリックしてゲージを挿入する。 **[ゲージの種類の選択]** ダイアログ ボックスが表示されます。 ゲージの種類を選択したら、ゲージのデータ領域がレポートの左上に配置されます。 データを追加してこのゲージのレイアウトを調整したら、それをドラッグ アンド ドロップで Tablix セルの中に配置します。  
  
 グラフの場合と同様、ゲージに渡されるデータセットのスコープはそのセルのデータのサブセットに制限されます。 ゲージが Tablix セル内に配置されたとき、ゲージで集計されるデータは常に 1 行分のデータのみです。  
  
 Tablix 内のデータがグループ化されていても、Tablix 内に入れ子になっているゲージのデータ領域で自動的にはそのグループ化が継承されません。 ゲージに Tablix と同じ情報を表示するには、同じグループ化の式をゲージに追加する必要があります。 たとえば、Tablix のデータが製品ごとにグループ化されている場合、ゲージにも製品ごとのグループ化の式を追加しなければ同じデータは表示されません。 詳細については、「[ゲージ &#40;レポート ビルダーおよび SSRS&#41;](gauges-report-builder-and-ssrs.md)」と「[データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
 ゲージの目盛りに表示される最大値と最小値を指定する必要があります。 ゲージの最大値を指定するために `=Max!MyField.Value`のような式を使用できます。 ただし、この式はそのセルのデータ スコープ内でのみ評価されるので、個々のゲージの実際の最大値は Tablix のすべての行で同じになりません。 このことにより、Tablix 内のゲージ間の比較はわかりにくいものになります。 代わりに、静的な値を最大値に指定することもできます。 Tablix 内のすべての行でこの最大値がゲージに表示されます。 詳細については、「[ゲージへの最小値または最大値の設定 &#40;レポート ビルダーおよび SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)」を参照してください。  
  
 ゲージに表示されるデータが大きすぎる場合は、表示される数値の桁数を減らすために目盛りの縮尺を指定できます。 縮尺を指定するには、目盛りを右クリックして **[スケールのプロパティ]** を選択します。 **[スケールのプロパティ]** ダイアログ ボックスが開いたら、 **[乗数]** の値を指定します。  
  
## <a name="nesting-a-table-or-matrix-and-a-chart-in-a-list"></a>リストに表またはマトリックスとグラフを挿入するには  
 リストに複数のデータ領域を入れ子にするには、まず長方形を追加し、その後でその長方形に複数のデータ領域を追加します。  
  
 リストのデータ領域にグループを定義できます。さらに Tablix とグラフを追加して同じデータの異なったビューを提供できます。 それには、埋め込まれた Tablix とグラフに同じグループ化と並べ替えの式を定義する必要があります。 Tablix とグラフは親となるリストのデータ領域のデータを使用するように定義されています。  
  
> [!NOTE]  
>  既定では、デザイン画面にリスト データ領域を追加すると、そのリストには詳細行が含まれています。 この既定動作を変更して、詳細行を取り除き、グループ行を追加できます。 詳細については、「[Tablix データ領域の柔軟性について &#40;レポート ビルダーおよび SSRS&#41;](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
 詳細については、「[グループについて &#40;レポート ビルダーおよび SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)」と「[テーブル、マトリックス、または一覧の追加、移動、または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [ゲージ (レポート ビルダーおよび SSRS)](gauges-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [レポート アイテムの書式設定 (レポート ビルダーおよび SSRS)](formatting-report-items-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへの KPI の追加 &#40;レポート ビルダー&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [ゲージのスケールの書式設定 (レポート ビルダーおよび SSRS)](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
