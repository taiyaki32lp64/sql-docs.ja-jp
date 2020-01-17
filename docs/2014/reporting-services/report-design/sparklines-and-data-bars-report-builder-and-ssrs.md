---
title: スパークラインとデータ バー (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.sparklines.f1
- "10544"
ms.assetid: b287436b-fa48-4970-a1a7-1dbcb86e7411
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 28b981dfe725a42228f287bc7a02df836030f3d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104963"
---
# <a name="sparklines-and-data-bars-report-builder-and-ssrs"></a>スパークラインとデータ バー (レポート ビルダーおよび SSRS)
  スパークラインとデータ バーは、小さい領域で多くの情報を伝達する小さい単純なグラフで、多くの場合、インライン テキストが含まれています。 スパークラインとデータ バーはテーブルやマトリックスでよく使用されます。 その効果は、それらを個々に表示するのではなく、同時に上下に表示して簡単に比較できることにあります。 この機能によって、他の値と動作の異なる行である外れ値を把握しやすくなります。 これらは小さいですが、各スパークラインは長期にわたる複数のデータ ポイントを表す場合が多く、 データ バーは複数のデータ ポイントを表すこともできますが、通常は 1 つのデータ ポイントのみを示します。 各スパークラインは通常 1 つの系列を表します。 スパークラインをテーブル内の詳細グループに追加することはできません。 スパークラインは集計データを表示するため、グループに関連付けられているセル内に含める必要があります。 スパークラインとデータ バーには、カテゴリ、系列、および値という同じ基本グラフ要素がありますが、凡例、軸線、ラベル、目盛りはありません。  
  
 ![rs_SparklineExample](../media/rs-sparklineexample.gif "rs_SparklineExample")  
  
 スパークラインをすぐに使用するには、「[チュートリアル:レポートへのスパークラインの追加 &#40;レポート ビルダー&#41;](../tutorial-add-a-sparkline-to-your-report-report-builder.md)」とビデオ「[方法:テーブルにスパークラインを作成する方法](https://go.microsoft.com/fwlink/?LinkId=197092)」と「[レポート ビルダーのスパークライン、横棒グラフ、およびインジケーター](https://technet.microsoft.com/bi/video/ff877165)」をご覧ください。  
  
> [!NOTE]  
>  親テーブル、マトリックス、または一覧を含むスパークラインとデータ バーは、レポート パーツとしてレポートとは別にパブリッシュできます。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="KindsofSparklines"></a> スパークラインの種類  
 スパークラインの種類は、通常のグラフの場合とほぼ同じ数だけ作成できます。 一般に、3D スパークラインは作成できません。 以下の完全なグラフをスパークラインにすることができます。  
  
-   [縦棒グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md):縦棒グラフ、積み上げ縦棒グラフ、および 100% 積み上げ縦棒グラフ。  
  
-   [折れ線グラフ &#40;レポート ビルダーおよび SSRS&#41;](line-charts-report-builder-and-ssrs.md):3D 折れ線グラフを除くすべてのグラフ。  
  
-   [面グラフ &#40;レポート ビルダーおよび SSRS&#41;](area-charts-report-builder-and-ssrs.md):3D 面グラフを除くすべてのグラフ。  
  
-   [円グラフ &#40;レポート ビルダーおよび SSRS&#41;](pie-charts-report-builder-and-ssrs.md):ドーナツ グラフ (平坦なグラフと 3D, グラフの両方)。じょうごグラフやピラミッド グラフなどの他の形状のグラフは表示できません。  
  
-   [範囲グラフ &#40;レポート ビルダーおよび SSRS&#41;](range-charts-report-builder-and-ssrs.md):株価、ローソク足、エラー バー、および箱ひげ図の各グラフ。  
  
##  <a name="DataBars"></a> データ バー  
 データ バーは、一般的な横棒グラフのように複数のデータ ポイントを表すことができますが、通常は 1 つのデータ ポイントを表します。 また、カテゴリのない複数の系列を含んでいる場合や、系列グループを含んでいる場合もあります。  
  
 ![rs_DataBars](../media/rs-databars.gif "rs_DataBars")  
  
 積み上げデータ バーを使用したこの例では、各データ バー (ここでは 1 つしか表示していません) は、複数のデータ ポイントを示しています。 たとえば、バーの 3 色の異なる色が、3 つの優先レベルのタスクを表し、バーの長さは各ユーザーに割り当てられたタスクの合計数を表すことができます。 100% 積み上げデータ バーを代わりに作成した場合、各バーはセル全体を示し、色の違いで各優先度レベルがそれぞれ全体の何パーセントを占めているかを表します。  
  
 以下の完全なグラフをデータ バーにすることができます。  
  
-   [横棒グラフ &#40;レポート ビルダーおよび SSRS&#41;](bar-charts-report-builder-and-ssrs.md):横棒グラフ、積み上げ横棒グラフ、および 100% 積み上げ横棒グラフ。  
  
-   [縦棒グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md):縦棒グラフ、積み上げ縦棒グラフ、および 100% 積み上げ縦棒グラフ。 縦棒グラフはスパークラインまたはデータ バーのどちらにも変換できます。  

##  <a name="AlignDatainTableMatrix"></a> テーブルまたはマトリックス内でのスパークライン データの整列  
 スパークラインをテーブルまたはマトリックスに挿入する場合、通常は、各スパークラインのデータ ポイントを対象の列にある他のスパークラインのデータ ポイントに揃えることが重要です。 そうしないと、異なる行内のデータを比較することが難しくなります。 たとえば、社内の複数の販売員の月ごとの売上データを比較する場合は、月を揃えます。 従業員が 4 月に欠勤した場合、その従業員の 4 月分のデータはありません。 その月は空白にし、後続の月のデータを他の従業員のデータと揃えて表示することができます。 これを行うには、横軸を揃えます。 詳細については、「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」のスパーク ラインに関するセクションと、「[テーブル内のグラフまたはマトリックスでのデータの整列 &#40;レポート ビルダーおよび SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)」を参照してください。  
  
 同様に、行全体を比較できるようにするには、データを縦に揃える必要があります。つまり、1 つのスパークラインまたはデータ バーにある棒または折れ線の高さが、他のすべてのスパークラインまたはデータ バーにある棒と折れ線の高さに相対的である必要があります。 そうしないと、行を他の行と比較することはできません。  
  
 ![rs_SparklineAlignData](../media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 次の画像には、各従業員の毎日の売り上げが縦棒グラフで示されています。 売り上げのない日にはグラフが空白になり、後続の日が整列されていることに注意してください。 これは、横方向の配置の例を示しています。 また、一部の従業員では、各縦棒が短く、縦棒がセルの最上部に届いていません。 これは、縦方向の配置の例を示しています。そうでない場合、高い縦棒のない行では、短い縦棒がセル全体の高さまで拡張されます。  

##  <a name="UnderstandScope"></a> スパークラインまたはデータ バーに渡されるデータについて  
 スパークラインまたはデータ バーをテーブルまたはマトリックスに追加する場合、この操作をあるデータ領域を別のデータ領域に *入れ子にする* といいます。 入れ子とは、スパークラインまたはデータ バーに渡されたデータが、テーブルまたはマトリックスを構成するデータセットと、テーブルまたはマトリックス内の配置場所によって制御されることを指します。 詳細については、「 [入れ子になったデータ領域 &#40;レポート ビルダーおよび SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="ConvertSparklinetoChart"></a> スパークラインまたはデータ バーの完全なグラフへの変換  
 スパークラインとデータ バーはグラフの一種であるため、完全なグラフの機能を使用する必要がある場合は、それらを右クリックし、 **[完全なグラフに変換]** をクリックすると、完全なグラフに変換できます。 この変換を行うと、軸の線、ラベル、目盛り、および凡例が自動的に追加されます。  
  
> [!NOTE]  
>  1 回のクリックで、完全なグラフをスパークラインまたはデータ バーに変換することはできません。 しかし、スパークラインまたはデータ バーにないグラフ要素をすべて削除すれば、完全なグラフからスパークラインまたはデータ バーを作成できます。  

##  <a name="HowTo"></a> 操作方法に関するトピック  
 [スパークラインとデータ バーの追加 &#40;レポート ビルダーおよび SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
 [テーブル内のグラフまたはマトリックスでのデータの整列 &#40;レポート ビルダーおよび SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
### <a name="other-how-to-topics-for-charts"></a>グラフの使用法に関するその他のトピック  
 スパークラインとデータ バーはグラフの一種であるため、次に紹介するグラフの使用法に関するトピックにも役立つ関連情報が記載されています。  
  
 [レポートへのグラフの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
 [空のポイントをグラフに追加&#40;レポート ビルダーおよび SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
 [グラフの余白の追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [グラフの種類の変更 &#40;レポート ビルダーおよび SSRS&#41;](change-a-chart-type-report-builder-and-ssrs.md)  
  
 [パレットを使用したグラフの色の定義 &#40;レポート ビルダーおよび SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [系列へのツールヒントの表示 &#40;レポート ビルダーおよび SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [対数スケールの指定 &#40;レポート ビルダーおよび SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
 [軸の間隔の指定 &#40;レポート ビルダーおよび SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [複数の図形グラフでの色の統一 &#40;レポート ビルダーおよび SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [チュートリアル: レポートにスパーク ラインを追加&#40;レポート ビルダー&#41;](../tutorial-add-a-sparkline-to-your-report-report-builder.md)   
 [スパーク ライン、横棒グラフ、およびレポート ビルダー (ビデオ) インジケーター](https://technet.microsoft.com/bi/video/ff877165)   
 [方法:(ビデオ) テーブルにスパーク ラインを作成します。](https://go.microsoft.com/fwlink/?LinkId=197092)  
