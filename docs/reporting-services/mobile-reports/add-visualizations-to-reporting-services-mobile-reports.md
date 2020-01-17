---
title: Reporting Services モバイル レポートへの視覚エフェクトの追加 | Microsoft Docs
ms.date: 09/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 42df96705e680643a9dacca3393e8c9c262c66c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316580"
---
# <a name="add-visualizations-to-reporting-services-mobile-reports"></a>Reporting Services モバイル レポートへの視覚エフェクトの追加
グラフは、データの視覚化における重要な部分です。 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] モバイル レポートで使用可能な、幅広いシナリオに対応した各種グラフについて説明します。 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] には、時間、カテゴリ、および集計という 3 つの基本的なグラフの種類があります。 この 3 つのグラフの種類には、それぞれ対応する比較グラフがあります。比較グラフは 2 つの異なる系列セットを比較するのに便利です。  

## <a name="shared-chart-properties"></a>共有されるグラフ プロパティ

プロパティは、すべてのグラフに適用されるものもあれば、特定のグラフにのみ適用されるものもあります。 ここでは、共有されるプロパティをいくつか紹介します。

### <a name="number-format"></a>数値書式
[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] ではグラフ内の数値にさまざまな書式を割り当てることができます。たとえば、標準、小数点付き/小数点なしの通貨、小数点付き/小数点なしのパーセンテージなどが挙げられます。 グラフの中で、数値書式は軸の注釈や、データ ポイントのポップアップに適用されます。 数値書式は、モバイル レポート全体ではなく、各グラフで個別に設定します。 

* 数値書式を設定するには、 **[レイアウト]** タブを選択し、デザイン画面のグラフを選択し、 **[ビジュアルのプロパティ]** ウィンドウの **[数値書式]** を選択します。 
  
### <a name="legend"></a>凡例
* グラフの凡例を表示するには、 **[レイアウト]** タブを選択し、デザイン画面のグラフを選択し、 **[ビジュアルのプロパティ]** ウィンドウで、 **[凡例の表示]** を **[オン]** に設定します。
  
### <a name="series"></a>系列
グラフに表示される個々のメトリック (値) は、系列と呼ばれます。複数の系列で共通の X 軸と共通の Y 軸を共有できます。 系列を定義するには、データ ビューのデータ プロパティ パネルで 1 つ以上のデータ テーブルとフィールドを選択します。 各フィールドは、グラフの視覚化で独自の色を持つ個々のデータ ポイント系列になります。  

### <a name="change-aggregation"></a>集計の変更 
グラフの数値フィールドにおける既定の集計は合計です。 この値は、平均、カウント、最小、最大、先頭、最後に変更できます。

* **[データ]** タブを選択してから、 **[データ プロパティ]** で、数値フィールドの横にある **[オプション]** を選択し、異なる集計を選択します。

### <a name="set-or-clear-filters"></a>フィルターの設定またはクリア

ナビゲーターを追加してモバイル レポートをフィルター処理する場合は、ナビゲーターでフィルター処理するグラフを決定できます。

1. **[データ]** タブを選択し、 **[データ プロパティ]** で **[オプション]** を選択します。

2. **[フィルター条件]** の下に、オンまたはオフにできるナビゲーターが表示されます。

詳細については、 [「adding navigators to filter a mobile report」](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)(モバイル レポートをフィルター処理するナビゲーターを追加する) を参照してください。
   
## <a name="time-charts"></a>時間グラフ  
  
時間グラフは、 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]で最も基本的なグラフです。 グラフの時間 (および日付) 軸は、データ テーブル内の最初の有効な日付/時刻フィールドに自動的に設定されます。  

![mobile-report-time-chart](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. **[レイアウト]** タブからデザイン画面に **時間グラフ** をドラッグし、そのサイズを変更します。

2. 既定では、積み上げ横棒グラフとなります。 これは、 **[系列の視覚化]** で変更できます。

3. レポートにまだ存在していないデータがグラフで必要な場合は、 **[データ]** タブ、 **[データの追加]** の順に選択して、[Excel または共有データセットからデータを取得](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)します。

3. **[データ プロパティ]** ペインに表示される **[主要な系列]** は **[SimulatedTable]** です。 ボックス内の矢印を選択し、テーブルを選択します。

5. **[データ構造]** を **[列ごと]** に設定した場合 ( **[レイアウト]** タブで、 **[ビジュアルのプロパティ]** ウィンドウを選択)、 **[データ プロパティ]** ウィンドウでは、数値の複数の列を選択することができます。

   **[データ構造]** を **[行ごと]** に設定した場合、 **[データ プロパティ]** ウィンドウで **[系列名フィールド]** を 1 つと数値の列を 1 つ選択できます。
   
詳細については、 [「grouping data by columns or rows」](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)(列または行ごとにデータをグループ化する) を参照してください。
  
## <a name="category-charts"></a>カテゴリ グラフ  
  
時間グラフの場合とは異なり、カテゴリ グラフでは、X 軸で日付/時刻フィールド以外のフィールドでグループ化を行います。 このグループ化は、 *カテゴリ コーディネート*と呼ばれ、数値フィールドではなく文字列フィールドに対して行われる必要があります。

![mobile-report-category-chart](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. **カテゴリ グラフ** を **[レイアウト]** タブからデザイン画面にドラッグし、そのサイズを変更し、必要に応じて [それに関するデータを取得](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)します。

2. **[データ]** タブを選択し、 **[データ プロパティ]** ウィンドウの **[Category Coordinate (カテゴリ コーディネート)]** で、グループ化するテーブルおよびフィールドを選択します。 このフィールドは、結果として作成されるグラフの X 軸で使用されます。

3. **[主要な系列]** で、カテゴリごとに集計するテーブルおよび数値フィールドを選択します。 
  
## <a name="totals-charts"></a>合計グラフ  

![mobile-report-totals-chart](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
合計グラフでは、次の 2 つの個別の処理を行います。 
* 複数の系列を対象とするのでなく、定義された主要な系列の合計のみが提供されます。 
* 列ごと、または行ごとにデータをグループ化するオプションを提供します。 行ごとのグループ化は、フラット化されたデータを処理する場合に便利です。 列ごとにグループ化する場合、カテゴリ列は主要系列プロパティで選択されたフィールドの数によって自動的に決定されるため、主要系列プロパティのみが使用可能です。  

詳細については、 [「grouping data by columns or rows」](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)(列または行ごとにデータをグループ化する) を参照してください。 
  
## <a name="comparison-charts"></a>比較グラフ  
  
時間グラフ、カテゴリ グラフ、および合計グラフは、 *比較グラフ*としても使用できます。 比較グラフでは、主要系列だけでなく、別に 1 つ比較系列を指定することができます。 主要系列と比較系列は、3 種類の方法で表示することができます。

![mobile-report-comparison-time-chart](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. **比較グラフ** (時間グラフ、カテゴリ グラフ、または合計グラフ) の 1 つを **[レイアウト]** タブからデザイン画面にドラッグし、そのサイズを変更し、必要に応じて [それに関するデータを取得](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)します。

2. **[ビジュアルのプロパティ]** ウィンドウの **[系列の視覚化]** で、次のいずれかを選択します。 
   * 棒 vs. 細い棒
   * 折れ線 vs. 棒
   * 棒 vs. ステップ エリア 

比較グラフでは、系列の主要値および比較値に対して同じグラフ色を使用するようにすることができます。

* **[ビジュアルのプロパティ]** ウィンドウで、 **[比較系列上の色の再利用]** を **[オン]** に設定します。

   **[オン]** に設定した場合、主要系列と比較系列の描画の合間にカラー パレットが再起動するため、主要系列と比較系列の関連する値は同じになります。 

   **[オフ]** に設定した場合、比較系列を描画してから主要系列を描画する際にカラー パレットの通常のローテーションが引き続き行われます。これにより、2 つの系列セットの間で色の調和から誤解が生じる可能性が回避されます。  
  
## <a name="pie-and-funnel-charts"></a>円グラフやじょうごグラフ  
  
円グラフやじょうごグラフは、最もシンプルな視覚エフェクトです。 行ごとのデータまたは列ごとのデータを構成することができます。 
* **モバイル レポートの** 円グラフ [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] は、円型、ドーナツ型、または中央に合計を示すドーナツ型とすることができます。 円グラフでは、全体を構成するさまざまな部分の相対的なサイズを示すのに適しています。 スライスが多すぎると、読みにくくなります。
* **じょうごグラフ** は、販売などのプロセスの段階を表示するのによく使用されます。

![mobile-report-funnel-chart](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### <a name="structure-pie-and-funnel-chart-data-by-rows-or-by-columns"></a>円グラフおよびじょうごグラフの行ごとのデータまたは列ごとのデータを構成する
1. **円グラフ** または **じょうごグラフ** を **[レイアウト]** タブからデザイン画面にドラッグし、そのサイズを変更し、必要に応じて [それに関するデータを取得](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)します。
2. **[ビジュアルのプロパティ]** ウィンドウの **[データ構造]** で、次のいずれかを選択します。
   * **列ごと**
   * **行ごと**
3. **[列ごと]** を選択した場合は、 **[データ]** タブを選択し、 **[データのプロパティ]** ウィンドウの **[主要な系列]** で、円グラフまたはじょうごグラフで集計するテーブルとすべてのフィールドを選択します。 生成されるグラフの各領域にはフィールド名のラベルが付けられます。

   **[行ごと]** を選択した場合は、 **[データ]** タブを選択し、 **[データのプロパティ]** ウィンドウの **[カテゴリ列]** で、円グラフでのグループ化およびラベルで使用する値が含まれているテーブルと列を選択します。 主要系列列では、グラフの値に対して数値フィールドを選択します。

詳細については、 [「grouping data by columns or rows」](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)(列または行ごとにデータをグループ化する) を参照してください。 

## <a name="treemaps"></a>ツリーマップ  
  
ツリーマップは、四角形グリッド内のサイズやタイルの色に値を適用することで、メトリックを表示します。 

![mobile-report-group-treemap](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. **ツリーマップ** を **[レイアウト]** タブからデザイン画面にドラッグし、そのサイズを変更し、必要に応じて [それに関するデータを取得](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)します。
2.  **[データ]** タブを選択し、 **[データ プロパティ]** で次の選択を行います。 

     * **[サイズが表すもの]** でタイルのサイズに対して数値フィールドを選択します。
     * **[色が表すもの]** でタイルの色に対して数値フィールドを選択します。 
     * [省略可能] **[カスタム中央値]** : **[カスタム中央値]** は、ビジュアル化の種類が HeatMapWithCustomCenterValue の場合にのみ使用できます。
     
         中央値によって、ボックスの色が決まります。 中央値と比べてよい測定値であるほど、緑色に近くなります。 悪い測定値であるほど、赤色に近くなります。
     
     * [省略可能] 閲覧者がグリッド内のタイルを選択したときにポップアップを表示するには、 **[ポップアップ ラベル]** で 1 つまたは複数のフィールドを選択します。 ツリーマップのポップアップには、テキスト フィールドと数値フィールドの両方を表示できます。  

既定では、ツリーマップは階層構造をとり、タイルをまずカテゴリ別にグループ化し、次にサイズと色別にグループ化します。
* さらに、 **[データ]** タブの **[グループ化]** でテーブルとフィールドを選択します。

グループ化はオフにすることができます。そうすると、サイズと色のみを条件としてタイルは配置されます。 

* **[レイアウト]** タブを選択し、 **[Two-level treemap (2 レベルのツリーマップ)]** を **[オフ]** にします。   

## <a name="waterfall-charts"></a>ウォーターフォール図

ウォーターフォール図は、値の増加または減少とともに累計を示します。 初期値 (純利益など) が、一連の正および負の変化の影響をどのように受けているかを把握するのに役立ちます。

増加を示す棒は緑、減少を示す棒は赤に色分けされるため、増減を簡単に区別できます。 ほとんどの場合、初期値と最終値の棒グラフは 0 から始まり、中間の各値は浮いた棒グラフで示されます。 こうした "見た目" から、ウォーターフォール図はブリッジ図とも呼ばれます。

### <a name="when-to-use-a-waterfall-chart"></a>ウォーターフォール図の使用に適した状況

ウォーターフォール図は以下のような状況に適しています。
* 時系列またはその他のカテゴリにわたって特定の尺度が変化しており、合計値に対して大きく寄与している変化を調べる場合
* 各種の収益源を並べて会社の年益をプロットし、最終的な総利益 (または損失) を示す場合
* 1 年間を通して会社の社員数の移り変わりを示す場合
* 各月に得た金額と消費した金額、および口座の収支の累計を視覚化する場合 

### <a name="create-a-waterfall-chart"></a>ウォーターフォール図の作成

1. **ウォーターフォール図** を **[レイアウト]** タブからデザイン画面にドラッグし、必要に応じてサイズの調整と [データの取得](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)を行います。

    ![mobile-report-waterfall-chart-icon](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  **[データ]** タブをクリックし、 **[データのプロパティ]** ペインで、データから **[Category Coordinate]** (カテゴリ座標) のカテゴリ フィールドと **[主要な系列]** の数値フィールドを選択します。 

    ![mobile-report-waterfall-data](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. **[レイアウト]** タブをクリックして、ウォーターフォール図のプレビューを確認します。

   ![mobile-report-waterfall-chart](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   2 月、6 月、7 月などの損失が出た月は赤色で示されています。 
   9 月、10 月、11 月などの利益が出た月は緑色で示されています。 

## <a name="see-also"></a>参照 
* [Maps in SQL Server mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのナビゲーター](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services モバイル レポートのデータ グリッド](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Reporting Services モバイル レポートのゲージ](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  

