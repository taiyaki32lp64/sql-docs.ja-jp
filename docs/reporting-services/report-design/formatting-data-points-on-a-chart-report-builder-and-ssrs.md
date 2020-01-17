---
title: グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10248"
- sql13.rtp.rptdesigner.serieslabelproperties.general.f1
ms.assetid: 08ec3818-f63a-4e89-b52c-750e47f48b85
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0481f39c0c047f401914e2c710a1f52c393bc335
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580334"
---
# <a name="formatting-data-points-on-a-chart-report-builder-and-ssrs"></a>グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートで、データ ポイントは、グラフにおける最小単位のエンティティです。 図形以外のグラフのデータ ポイントは、そのグラフの種類に応じて表されます。 たとえば、線系列は 1 つまたは複数の連続したデータ ポイントで構成されます。 図形グラフのデータ ポイントは、個々のスライスやセグメントによって表され、これらのスライスやセグメントがグラフ全体を形成します。 たとえば、円グラフでは、それぞれのピースがデータ ポイントです。 詳細については、「 [グラフの種類 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)」を参照してください。  
  
 1 つまたは複数のデータ ポイントが系列を形成します。 既定では、すべての書式設定オプションが系列のすべてのデータ ポイントに適用されます。 個々のデータ ポイントのプロパティを指定するには、実行時にデータセットに基づいて個々のデータ ポイントを書式設定するフィールドまたは式を系列で指定します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-tooltips-and-drillthrough-actions-to-data-points"></a>データ ポイントへのツールヒントおよびドリルスルー アクションの追加  
 各データ ポイントにツールヒントを追加するには、系列に対して **ToolTip** プロパティの値を設定します。 ツールヒントを表示すると、ユーザーは、グループ名、データ ポイントの値、系列の合計値に対するデータ ポイントの比率など、データ ポイントに関連する情報を確認できます。 詳細については、「 [系列へのツールヒントの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)」を参照してください。  
  
 系列のデータ ポイントにドリルスルー アクションを指定して、他のレポートや URL を表示することもできます。 クリックされたデータ ポイントに関する情報を表示するためのパラメーターを渡すこともできます。 詳細については、「[レポートへのドリルスルー アクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="highlighting-individual-data-points-in-a-series"></a>系列の個々のデータ ポイントの強調表示  
 図形以外のグラフでは、Color プロパティの式を指定すると、個々のデータ ポイントを強調表示できます。 たとえば、 `MyField` という名前の系列内の最大値を、他のデータ ポイントと異なる色で強調表示するには、次のような式を指定します。  
  
 `=Iif(Fields!MyField.Value >= Max(Fields!MyField.Value, "MyDataSet"), "Red", "Green")`  
  
 この例では、 `MyField` の最大値は赤色になり、その他のすべてのデータ ポイントは緑色になります。 系列で **Fill** プロパティを使用して系列の色を指定する場合、パレットで指定された色をオーバーライドします。 詳細については、「 [グラフの系列の色の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)をクリックします。  
  
## <a name="positioning-data-point-labels-on-a-chart"></a>グラフへのデータ ポイント ラベルの配置  
 すべての種類のグラフで、グラフを右クリックして **[データ ラベルの表示]** を選択すると、データ ポイント ラベルを表示できます。 データ ポイント ラベルの位置は、グラフの種類に応じて指定されます。  
  
-   横棒グラフの場合、 **BarLabelStyle** カスタム属性を使用してデータ ポイント ラベルの位置を指定できます。 外側、左、中央、および右の 4 つの位置から選択できます。 バーのラベル スタイルが外側に設定されている場合、ラベルは、グラフ領域内に収まる範囲でバーの外側に配置されます。 バーの外側でグラフ領域内にラベルを配置できない場合、ラベルはバーの内側に配置されます。  
  
-   円グラフの場合、 **PieLabelStyle** カスタム属性を使用してデータ ポイント ラベルの位置を指定できます。 円グラフの周囲にデータ ポイント ラベルを配置する場合は、円グラフのサイズ、円グラフと対応する凡例の間の空間、ラベルのサイズなど、多くの点を考慮する必要があります。 詳細については、「 [円グラフの外側へのデータ ポイント ラベルの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)」を参照してください。  
  
-   ピラミッド グラフやじょうごグラフの場合、 **FunnelLabelStyle** および **PyramidLabelStyle** カスタム属性を使用してデータ ポイント ラベルの位置を指定できます。 グラフの種類としてピラミッドまたはじょうごを選択した場合、これらの属性は **プロパティ** ペインで設定できます。  
  
-   積み上げグラフの場合、データ ポイント ラベルは常に系列の内側に配置され、系列ラベルの **Position** プロパティは無視されます。  
  
-   その他の種類のグラフでは、系列ラベルの **Position** プロパティを使用してデータ ポイント ラベルの位置を指定できます。 既定では、ラベルが重ならないように、データ ポイント ラベルの位置が自動的に計算されます。 **Position**プロパティの値を設定すると、すべてのデータ ポイント ラベルが同じように配置され、ラベルが重なり合う場合があります。 データ ポイントの数が少ない場合にのみ、Position プロパティを使用してください。  
  
 詳細については、「[グラフへのラベルの配置 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/position-labels-in-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="adding-keywords-for-data-point-labels-tooltips-and-legend-text"></a>データ ポイント ラベル、ツールヒント、および凡例テキストへのキーワードの追加  
 大文字と小文字の区別があるグラフに固有のキーワードを使用すると、グラフ内に存在する項目を表すことができます。 これらのキーワードは、ツールヒント、カスタムの凡例テキスト、データ ポイント ラベルのプロパティにのみ適用されます。 多くの場合、グラフ キーワードには同等の簡単な式がありますが、キーワードを入力する方がすばやく簡単です。 グラフ キーワードの一覧は次のとおりです。  
  
|グラフ キーワード|[説明]|適用可能なグラフの種類|同等の簡単な式の例|  
|-------------------|-----------------|------------------------------|------------------------------------------------|  
|#VALY|データ ポイントの Y 値|All|`=Fields!MyDataField.Value`|  
|#VALY2|データ ポイントの Y 値の 2 番目の値|範囲、バブル|なし|  
|#VALY3|データ ポイントの Y 値の 3 番目の値|株価、ローソク足|なし|  
|#VALY4|データ ポイントの Y 値の 4 番目の値|株価、ローソク足|なし|  
|#SERIESNAME|系列名|All|なし|  
|#LABEL|データ ポイント ラベル|All|なし|  
|#AXISLABEL|軸データ ポイント ラベル|図形|`=Fields!MyDataField.Value`|  
|#INDEX|データ ポイントのインデックス|All|なし|  
|#PERCENT|データ ポイントの Y 値の比率|All|`=FormatPercent(Fields!MyDataField.Value/Sum(Fields!MyDataField.Value, "MyDataSet"),2)`|  
|#TOTAL|系列のすべての Y 値の合計|All|`=Sum(Fields!MyDataField.Value)`|  
|#LEGENDTEXT|凡例項目のテキストに対応するテキスト|All|なし|  
|#AVG|系列内のすべての Y 値の平均|All|`=Avg(Fields!MyDataField.Value)`|  
|#MIN|系列内のすべての Y 値の最小値|すべて|`=Min(Fields!MyDataField.Value)`|  
|#MAX|系列内のすべての Y 値の最大値|All|`=Max(Fields!MyDataField.Value)`|  
|#FIRST|系列内のすべての Y 値の最初の値|All|`=First(Fields!MyDataField.Value)`|  
  
 キーワードを書式設定するには、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 書式設定文字列をかっこで囲みます。 たとえば、ツールヒントでデータ ポイントの値を小数点以下 2 桁の数値として指定するには、書式設定文字列 "N2" を中かっこで囲みます。たとえば、系列の **ToolTip** プロパティで "#VALY{N2}" のようになります。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 書式設定文字列の詳細については、MSDN の「 [型の書式設定](https://go.microsoft.com/fwlink/?LinkId=112024) 」を参照してください。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の数値を書式設定する方法については、「[数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)」を参照してください。  
  
 グラフにキーワードを追加する方法の詳細については、「[系列へのツールヒントの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)」、「[凡例アイテムのテキストの変更 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)」を参照してください。  
  
## <a name="increasing-readability-in-a-chart-with-multiple-data-points"></a>複数のデータ ポイントを持つグラフを読みやすくする  
 グラフに複数の系列が表示されると、グラフ データ ポイントがわかりにくくなることがあります。 複数の系列をグラフに追加する場合は、グラフの各系列を効率よく見分ける方法を検討してください。 詳細については、「 [グラフ上の複数の系列 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md):  
  
 便宜上、図形グラフを使用している場合は、データ フィールドとカテゴリ フィールドをそれぞれ 1 つだけ追加するようにしてください。 詳細については、「[図形グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)」を参照してください。 グラフに複数のデータ フィールドとカテゴリ フィールドが必要な場合は、グラフの種類を変更することを検討してください。 系列を右クリックし、 **[グラフの種類の変更]** をクリックします。  
  
## <a name="inserting-data-point-markers"></a>データ ポイント マーカーの挿入  
 データ ポイント マーカーは、系列の各データ ポイントを目立たせるための視覚インジケーターです。 散布図の場合、個々のデータ ポイントの形状とサイズを示すためにマーカーが使用されます。 マーカーのサイズはグラフの種類に基づいて指定されます。 マーカーのサイズ、色、またはスタイルは変更できます。 範囲グラフおよび図形グラフ、サブタイプの積み上げグラフには、マーカーを使用できません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [系列へのツールヒントの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [円グラフの外側へのデータ ポイント ラベルの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)  
  
 [円グラフへのパーセンテージの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [日付または通貨として軸ラベルを書式設定する &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [チュートリアル: レポートへの円グラフの追加 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
