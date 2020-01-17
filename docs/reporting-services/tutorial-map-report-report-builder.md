---
title: 'チュートリアル: マップ レポート (レポート ビルダー) | Microsoft Docs'
ms.date: 08/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4db47bde02745ddc554f17e1f951c836c1542cc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041671"
---
# <a name="tutorial-map-report-report-builder"></a>チュートリアル: マップ レポート (レポート ビルダー)
この [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] チュートリアルでは、地図を背景として、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポートのデータを表示するときに使用できるマップ機能について学習できます。 
  
マップは、空間データに基づいています。空間データは通常、ポイント、線、および多角形で構成され (郡の輪郭を表す多角形、道路を表す線、市区町村の場所を表すポイントなど)、 種類ごとに異なるマップ レイヤーにマップ要素のセットとして表示されます。  
  
マップ要素の表示を変化させるには、マップ要素をデータセットの分析データに対応付ける値を持つフィールドを指定します。 色やサイズなどのプロパティをデータの範囲に基づいて変化させるルールを定義することもできます。  

![report-builder-map-final-map-only](../reporting-services/media/report-builder-map-final-map-only.png)
  
このチュートリアルでは、New York 州の郡にある店舗の場所を表示するマップ レポートを作成します。  
   
> [!NOTE]  
> このチュートリアルでは、ウィザードに関する複数の手順を、データセットの作成とテーブルの作成の 2 つの手順にまとめて示します。 レポート サーバーの参照、データ ソースの選択、データセットの作成、およびウィザードの実行に関する詳細な手順については、このシリーズの最初のチュートリアル (「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」) を参照してください。  
  
このチュートリアルの推定所要時間: 30 分。  
  
## <a name="requirements"></a>必要条件  
このチュートリアルでは、Bing マップの背景をサポートするようにレポート サーバーが構成されている必要があります。 詳細については、「 [マップ レポートのサポートを計画する](https://msdn.microsoft.com/5ddc97a7-7ee5-475d-bc49-3b814dce7e19)」を参照してください。 

その他の要件については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。  
  
## <a name="Map"></a>1.マップ ウィザードを使用して多角形レイヤーを含むマップを作成する  
このセクションでは、マップをマップ ギャラリーからレポートに追加します。 このマップには、New York 州の郡を表示するレイヤーが含まれています。 各郡の図形は、マップ ギャラリーのマップに埋め込まれている空間データに基づく多角形です。  
  
### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>新しいレポートでマップ ウィザードを使用してマップを追加するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[マップ ウィザード]** をクリックします。  
  
4.  **[空間データのソースを選択]** ページで、 **[マップ ギャラリー]** が選択されていることを確認します。  
  
6.  [マップ ギャラリー] ボックスで、 **[USA]** の **[州を郡ごと]** を展開し、 **[New York]** をクリックします。  
  
    [マップ プレビュー] ペインに、New York の郡マップが表示されます。  
    
    ![report-builder-map-ny-counties](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  **[次へ]** をクリックします。  
  
8.  **[空間データとマップ ビューのオプションを選択]** ページで、既定値をそのまま使用し、 **[次へ]** をクリックします。 
 
    既定では、マップ ギャラリーのマップ要素は自動的にレポート定義に埋め込まれます。  
  
9. **[マップの視覚エフェクトを選択]** ページで、 **[基本マップ]** が選択されていることを確認し、 **[次へ]** をクリックします。  
  
11. **[配色テーマとデータの視覚エフェクトを選択]** ページで、 **[ラベルの表示]** チェック ボックスをオンにします。  
  
12. **[単色マップ]** チェック ボックスがオンになっている場合はオフにします。  
  
13. **[データ フィールド]** ドロップダウン リストで **#COUNTYNAME**をクリックします。 ウィザードの [マップ プレビュー] ペインに次のアイテムが表示されます。  
  
    -   " **マップのタイトル**" というテキストを含むタイトル。  
  
    -   New York の郡を表示するマップ。各郡は異なる色で表示され、郡の領域に収まる場所に郡の名前が表示されます。  
  
    -   タイトルとアイテム 1 ～ 5 の一覧を含む凡例。  
  
    -   値 0 ～ 160 および色なしを含むカラー スケール。  
  
    -   キロメートル (km) およびマイル (mi) を表示する距離スケール。  
    
    ![report-builder-map-choose-color-theme](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. **[完了]** をクリックします。  
  
    デザイン画面にマップが追加されます。  
  
13. "マップのタイトル" テキストを選択して、「**Sales by Store**」と入力し、Enter キーを押します。  

15. マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。 **[マップ レイヤー]** ペインには、レイヤーの種類が **[埋め込み]** である 1 つの多角形レイヤー PolygonLayer1 が表示されます。 各郡は、このレイヤー上の埋め込みマップ要素となります。  
  
    > [!NOTE]  
    > **[マップ レイヤー]** ペインが表示されない場合は、現在のビューの外に表示されている可能性があります。 デザイン ビュー ウィンドウの下部にあるスクロール バーを使用して、ビューを変更してください。 **[表示]** タブで **[レポート データ]** オプションをオフにして、デザイン画面の領域を広げることもできます。   

15. PolygonLayer1 の横の矢印を選択し、 **[多角形のプロパティ]** をクリックします。

16. **[フォント]** タブで、色を **[ディム グレー]** に変更します。

17. **[ホーム]** タブで **[実行]** をクリックして、レポートをプレビューします。  
  
    ![report-builder-map-first-preview](../reporting-services/media/report-builder-map-first-preview.png)
  
表示されたレポートには、マップのタイトル、マップ、および距離スケールが表示されています。 郡はマップの多角形レイヤーにあります。 各郡は多角形で、カラー パレットからそれぞれ異なる色が割り当てられていますが、色はデータとは関連付けられていません。 距離スケールには、距離がキロメートル単位とマイル単位の両方で表示されます。  
  
マップの凡例とカラー スケールは、各郡に分析データが関連付けられていないため、まだ表示されません。 このチュートリアルで後ほど分析データを追加します。  
  
## <a name="PointLayer"></a>2.店舗の場所を表示するマップのポイント レイヤーを追加する  
このセクションでは、マップ レイヤー ウィザードを使用して、店舗の場所を表示するポイント レイヤーを追加します。  
  
> [!NOTE]  
> このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>SQL Server 空間クエリに基づいてポイント レイヤーを追加するには  
  
1.  **[実行]** タブで **[デザイン]** をクリックして、デザイン ビューに戻ります。  
  
2.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。 ツールバーの **[レイヤーの新規作成]** ボタン ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard") をクリックします。 

    ![report-builder-map-new-layer-wizard-icon](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  **[空間データのソースを選択]** ページで、 **[SQL Server 空間クエリ]** を選択し、 **[次へ]** をクリックします。  
  
4.  **[SQL Server 空間データを含むデータセットの選択]** ページで、 **[SQL Server 空間データを含む新しいデータセットの追加]**  >  **[次へ]** の順にクリックします。  
  
5.  **[SQL Server 空間データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。  

    > [!NOTE]  
    > 適切な権限を持っている限り、選択するデータ ソースは重要ではありません。 データ ソースからはデータを取得しません。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
6.  **[次へ]** をクリックします。  
  
7.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
8.  次のテキストをコピーし、クエリ ペインに貼り付けます。  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. クエリ デザイナーのツール バーで、 **[実行]** ( **!** ) をクリックします。  
  
    この結果セットには、消費者向けの商品を販売している New York 州内の店舗を表す 7 つの列が含まれています。 一覧を次に示します。わかりにくいものには説明を付けています。 
    *   **StoreKey**: 店舗の識別子。  
    *   **StoreName**。
    *   **SellingArea**: 製品の展示に使用できる面積。範囲は 455 ～ 1125 平方フィートです。
    *   **City**。
    *   **County**。
    *   **Sales**: 総売上。 
    *   **SpatialLocation**: 緯度と経度による位置。 

    ![report-builder-map-design-query](../reporting-services/media/report-builder-map-design-query.png) 
  
10. **[次へ]** をクリックします。  
  
    DataSet1 という名前のレポート データセットが作成されます。 ウィザードを完了したら、レポート データ ペインにフィールド コレクションが表示されます。  
  
11. **[空間データとマップ ビューのオプションを選択]** ページで、 **[空間フィールド]** が **SpatialLocation** であり、 **[レイヤーの種類]** が **[ポイント]** であることを確認します。 このページの他の項目は、既定の設定をそのまま使用します。  
  
    マップ ビューに、各店舗の場所を示す円が表示されます。  
  
12. **[次へ]** をクリックします。  
  
13. [マップの視覚エフェクトの選択] ページで、マップの種類として、データに基づきサイズが変化するマーカーを表示する **[バブル マップ]** をクリックします。 **[次へ]** をクリックします。  
  
14. **[分析データセットの選択]** ページで [DataSet1] をクリックし、 **[次へ]** をクリックします。 このデータセットには、新しいポイント レイヤーに表示される分析データと空間データの両方が含まれています。   
  
16. **[配色テーマとデータの視覚エフェクトを選択]** ページで、 **[バブルのサイズを使用してデータを表示する]** チェック ボックスをオンにします。  
  
17. **[データ フィールド]** で `[Sum(SellingArea)]` を選択して、商品の展示のために確保されている面積に応じてバブルのサイズを変化させます。  
  
18. **[ラベルの表示]** チェック ボックスをオンにし、 **[データ フィールド]** で `[City]`を選択します。

18. **[完了]** をクリックします。  
  
    マップ レイヤーがレポートに追加されます。 凡例には、SellingArea の値に基づくバブルのサイズが表示されます。  
  
 19. マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。 **[マップ レイヤー]** ペインに、空間データ ソースの種類が **DataRegion**である新しいレイヤー PointLayer1 が表示されます。  
  
19. 凡例のタイトルを追加します。 凡例では、 **タイトル**テキストを選択して、「 **Display Area (sq. ft.)** 」と入力し、ENTER キーを押します。  
  
21. **[マップ レイヤー]** ペインで、PointLayer1 の横の矢印をクリックし、 **[ポイントのプロパティ]** をクリックします。  

    ![report-builder-map-point-properties](../reporting-services/media/report-builder-map-point-properties.png)
  
22. **[フォント]** タブで、スタイルを **[太字]** 、サイズを **[10pt]** にします。

    ![report-builder-map-point-properties-font](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. **[全般]** タブで、 **[位置]** に **[下詰め]** を選択します。

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. **[実行]** をクリックして、レポートをプレビューします。  

    ![report-builder-map-city-names](../reporting-services/media/report-builder-map-city-names.png)
  
    マップには、New York 州にある店舗の場所が表示されます。 各店舗のマーカーのサイズは展示面積に基づいています。 展示面積の 5 つの範囲が自動的に計算されます。


  
## <a name="LineLayer"></a>3.ルートを表示するマップの線レイヤーを追加する  
マップ レイヤー ウィザードを使用して、2 つの店舗間のルートを表示するマップ レイヤーを追加します。 このチュートリアルではパスを 3 つの店舗の場所から作成しますが、 ビジネス アプリケーションでは店舗間の最適なルートにすることができます。  
  
### <a name="to-add-a-line-layer-to-map"></a>マップに線レイヤーを追加するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。 ツールバーの **[レイヤーの新規作成]** ボタン ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard") をクリックします。  
  
3.  **[空間データのソースを選択]** ページで、 **[SQL Server 空間クエリ]** を選択し、 **[次へ]** をクリックします。  
  
4.  **[SQL Server 空間データを含むデータセットの選択]** ページで、 **[SQL Server 空間データを含む新しいデータセットの追加]** をクリックし、 **[次へ]** をクリックします。  
  
5.  **[SQL Server 空間データ ソースへの接続の選択]** で、最初の手順で使用したデータ ソースを選択します。  
  
6.  **[次へ]** をクリックします。  
  
7.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。 クエリ デザイナーがテキスト ベース モードに切り替わります。  
  
8.  クエリ ペインに次のテキストを貼り付けます。  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. **[次へ]** をクリックします。  
  
    3 つの店舗を接続するパスがマップに表示されます。  
  
10. **[空間データとマップ ビューのオプションを選択]** ページで、 **[空間フィールド]** が **Route** であり、 **[レイヤーの種類]** が **[線]** であることを確認します。 他の項目は既定の設定をそのまま使用します。  
  
    マップ ビューに、New York 州の北部にある店舗から New York 州の南部にある店舗へのパスが表示されます。  
  
11. **[次へ]** をクリックします。  
  
12. **[マップの視覚エフェクトを選択]** ページで、 **[基本線マップ]** をクリックし、 **[次へ]** をクリックします。  
  
13. **[配色テーマとデータの視覚エフェクトを選択]** で、 **[単色マップ]** オプションを選択します。 選択したテーマに基づく 1 つの色でパスが表示されます。  
  
14. **[完了]** をクリックします。  

    ![report-builder-map-line](../reporting-services/media/report-builder-map-line.png)
  
     マップに、空間データ ソースの種類が **DataRegion**である新しい線レイヤーが表示されます。 この例では、空間データがデータセットから得られますが、線に分析データは関連付けられていません。  

## <a name="adjust-the-zoom"></a>ズームの調整
1. New York の州全体が表示されない場合は、ズームを調整できます。 選択したマップで、[プロパティ] ペインに **[MapViewport]** のプロパティが表示されます。 

15. **[ビュー]** セクションを展開し、 **[ビュー]** を展開して、 **[Zoom]** プロパティを表示します。 **125**に設定します。 

    ![report-builder-map-zoom](../reporting-services/media/report-builder-map-zoom.png)

      これはズーム比です。 125% で州全体が表示されます。
  
## <a name="TileLayer"></a>4.Bing Maps のタイル背景を追加する  
このセクションでは、Bing Maps のタイル背景を表示するマップ レイヤーを追加します。  
  
1.  デザイン ビューに切り替えます。  
  
2.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。 ツールバーの **[レイヤーの追加]** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer") をクリックします。  
  
3.  ドロップダウン リストで、 **[タイル レイヤー]** をクリックします。  
  
    **[マップ レイヤー]** ペインの最後のレイヤーは TileLayer1 です。 既定では、タイル レイヤーには道路地図スタイルが表示されます。  
  
    > [!NOTE]  
    > ウィザードでも、 **[空間データとマップ ビューのオプションを選択]** ページでタイル レイヤーを追加できます。 そのためには、 **[このマップ ビューに Bing Maps の背景を追加する]** を選択します。 表示されるレポートのタイルの背景では、現在のマップ ビューポートの中心およびズーム レベルに基づいて Bing Maps のタイルが表示されます。  
  
4.  TileLayer1 の横の矢印をクリックし、 **[タイトルのプロパティ]** をクリックします。  
  
5.  **[全般]** タブの **[種類]** で、 **[航空写真]** を選択します。 航空写真ビューには、テキストは含まれません。  

    ![report-builder-map-bing-aerial](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Transparent"></a>5.レイヤーを透明にする  
このセクションでは、レイヤー上のアイテムが別のレイヤーを通して見えるように、レイヤーの順序と透明度を、目的の効果が得られるように調整します。 作成した最初のレイヤー PolygonLayer1 から開始します。 
  
1.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。  
  
3.  PolygonLayer1 の横の矢印をクリックし、 **[レイヤー データ]** をクリックします。 **[マップの多角形レイヤーのプロパティ]** ダイアログ ボックスが表示されます。  
  
4.  **[表示]** タブの **[透明度 (パーセント)]** に、「 **30**」と入力します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     デザイン画面に郡が半透明で表示されます。  

    ![report-builder-map-transparency](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="Vary"></a>6.郡の色を売上に基づいて変化させる  
レポート プロセッサにより、マップ ウィザードの最後のページで選択したテーマに基づいてカラー パレットから色値が自動的に割り当てられるため、多角形レイヤー上の各郡は異なる色で表示されます。  
  
このセクションでは、各郡の店舗売上の範囲に特定の色を関連付ける色ルールを指定します。 赤、黄、緑の各色は、売上高が相対的に高い、中程度、または低いことを示します。 カラー スケールを通貨形式に変更します。 新しい凡例に年間売上高の範囲を表示します。 店舗のない郡については、どの色も使用しないことで、関連付けられたデータがないことを示します。  
  
### <a name="Relationship"></a>6a. 空間データと分析データの間にリレーションシップを構築する  
分析データに基づいて郡の図形を色分けするには、まず分析データを空間データに関連付けておく必要があります。 このチュートリアルでは、郡の名前を使用してデータを対応させます。 
  
1.  デザイン ビューに切り替えます。  
  
2.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。  
  
3.  PolygonLayer1 の横の矢印をクリックし、 **[レイヤー データ]** をクリックします。 **[マップの多角形レイヤーのプロパティ]** ダイアログ ボックスが表示されます。  
  
4.  **[分析データ]** タブの **[分析データセット]** で、[DataSet1] を選択します。 このデータセットは、郡の空間データ クエリを作成したときにウィザードによって作成されたものです。  
  
6.  **[対応付けるフィールド]** で、 **[追加]** をクリックします。 新しい行が追加されます。  
  
7.  **[空間データセットから]** で、[COUNTYNAME] をクリックします。  
  
8.  **[分析データセットから]** で、[County] をクリックします。  

    ![report-builder-map-county-colors](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. レポートをプレビューします。  

    ![report-builder-map-county-highlight](../reporting-services/media/report-builder-map-county-highlight.png)
  
空間データ ソースおよび分析データセットから対応フィールドを指定することで、レポート プロセッサではマップ要素に基づいて分析データをグループ化できます。 データバインド マップ要素には、指定した値の適切な対応が含まれています。  
  
店舗がある各郡には、ウィザードで選択したスタイルのカラー パレットに基づく色が割り当てられています。 その他の郡は灰色になります。  
  
### <a name="ColorRules"></a>6b. 多角形の色ルールを指定する  
各郡の色を店舗売上に基づいて変化させるルールを作成するには、範囲の値、その範囲内で表示する部分範囲の数、および使用する色を指定する必要があります。  
  
#### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>データが関連付けられているすべての多角形の色ルールを指定するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  PolygonLayer1 の横の矢印をクリックし、 **[多角形の色のルール]** をクリックします。 **[マップの色のルールのプロパティ]** ダイアログ ボックスが表示されます。 色ルールのオプションとして **[色パレットを使用してデータを表示する]** が選択されています。 このオプションは、ウィザードによって設定されたものです。  
  
3.  **[色の範囲を使用してデータを表示する]** を選択します。 パレット オプションが、開始色、中間色、および終了色のオプションで置き換えられます。  
  
4.  郡の売上高について値の範囲を定義します。 **[データ フィールド]** のドロップダウン リストで `[Sum(Sales)]`を選択します。  
  
5.  通貨が 1,000 単位で表示されるようにするために、式を次のように変更します。 `=Sum(Fields!Sales.Value)/1000`  
  
6.  **[最初の色]** を **[赤]** に変更します。  
  
7.  **[最後の色]** を **[緑]** に変更します。  
  
    **[赤]** は低い売上高、 **[黄]** は中程度の売上高、 **[緑]** は高い売上高を表します。 レポート プロセッサでは、これらの値と、 **[分布]** ページで選択したオプションに基づいて、色の範囲が計算されます。  
    
    ![report-builder-map-county-color-rules](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  **[分布]** をクリックします。  
  
9. 分布の種類が **[最適]** であることを確認します。 手順 5 の式の場合、最適な分布では、各範囲のアイテム数と各範囲の大きさとのバランスが取れるような部分範囲に値が分布されます。  
  
10. このページの他のオプションについては、既定の値をそのまま使用します。 最適な分布タイプを選択した場合は、レポートを実行すると部分範囲の数が計算されます。  
  
11. **[凡例]** をクリックします。  
  
12. **[カラー スケールのオプション]** で、 **[カラー スケールに表示]** が選択されていることを確認します。  
  
13. **[この凡例に表示]** のドロップダウン リストで、空白行を選択します。 ここでは、色の範囲をカラー スケールだけで表示します。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. レポートをプレビューします。

    ![report-builder-map-county-color-rule-preview](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    カラー スケールには、赤、橙、黄、緑の 4 色が表示されます。 各色は、郡別の売上に基づいて自動的に計算された売上範囲を表しています。  
  
### <a name="ColorScale"></a>6c. カラー スケールのデータを通貨形式に変更する  
既定では、一般的な形式がデータに適用されますが、 このセクションでは、形式をカスタマイズします。  
  
1. デザイン ビューに切り替えます。  

2. カラー スケールを選択します。 **[ホーム]** タブの **[数値]** セクションで、 **[通貨]** をクリックします。  
  
4.  **[数値]** セクションで、 **[小数点表示桁下げ]** ボタンを 2 回クリックします。  
  
    カラー スケールで、各範囲の年間売上高が通貨形式で表示されます。  
  
### <a name="NewLegend"></a>6d. 凡例のタイトルの追加   
  
1.  カラー スケールが選択された状態で、[プロパティ] ペインに **[MapColorScale]** のプロパティが表示されます。 
  
2. [タイトル] セクションを展開し、[Caption] プロパティに「 **Sales (Thousands)** 」と入力します。

3. [TextColor] プロパティを変更 **[White]** に変更します。  

    ![report-builder-map-color-scale-title](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  レポートをプレビューします。  
  
店舗と売上が関連付けられている郡が、色のルールに従って表示されます。 売上が関連付けられていない郡の色はありません。  
  
### <a name="NoData"></a>6f. データがない郡の色を変更する  
レイヤー上のすべてのマップ要素の既定の表示オプションを設定することができます。 これらの表示オプションよりも色ルールが優先されます。  
  
#### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>レイヤー上のすべての要素に対して表示プロパティを設定するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。  
  
3.  PolygonLayer1 の下向き矢印をクリックし、 **[多角形のプロパティ]** をクリックします。 

     ![report-builder-map-polygon-layer-properties](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     **[マップの多角形のプロパティ]** ダイアログ ボックスが表示されます。 このダイアログ ボックスで設定した表示オプションは、ルールに基づく表示オプションが適用される前にレイヤー上のすべての多角形に適用されます。  
  
4.  **[塗りつぶし]** タブで、塗りつぶしのスタイルが **[純色]** になっていることを確認します。グラデーションやパターンはすべての色に適用されます。  
  
6.  **[色]** で **[薄いスチール ブルー]** を選択します。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  レポートをプレビューします。  
  
データが関連付けられていない郡が灰色 - 青で表示されます。 分析データが関連付けられている郡のみが、色のルールで指定した **[赤]** から **[緑]** の範囲の色で表示されます。  
  
## <a name="CustomPoint"></a>7.カスタム ポイントを追加する  
このセクションでは、まだ開店していない新しい店舗を表すために、マーカーの種類に **[星]** を使用してポイントを指定します。  
  
1.  デザイン ビューに切り替えます。  
  
2.  マップをダブルクリックして **[マップ レイヤー]** ペインを表示します。 ツールバーの **[レイヤーの追加]** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer") をクリックし、 **[ポイント レイヤー]** をクリックします。  
  
    新しいポイント レイヤーがマップに追加されます。 既定では、ポイント レイヤーの空間データの種類は **[埋め込み]** になります。  
  
3.  PointLayer2 の矢印をクリックし、 **[ポイントの追加]** をクリックします。  
  
4.  マップ ビューポートにポインターを移動します。 カーソルが十字に変化します。  
  
5.  マップ上でポイントを追加する場所をクリックします。 このチュートリアルでは、オネイダ郡内の場所をクリックします。 レイヤー上のクリックした場所に、円で示されるポイントが追加されます。 既定では、ポイントが選択された状態になります。  

    ![report-builder-map-custom-point](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  追加したポイントを右クリックし、 **[埋め込みポイントのプロパティ]** をクリックします。  
  
7.  **[このレイヤーのポイント オプションをオーバーライドする]** を選択します。 ダイアログ ボックスに追加のページが表示されます。 ここで設定したオプションは、レイヤーまたは色ルールの表示オプションよりも優先されます。  

    ![report-builder-map-custom-point-general](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  **[マーカー]** タブで、 **[マーカーの種類]** に **[星]** を選択します。  

10. **[マーカー サイズ]** を **[18pt]** に変更します。
  
3.  **[ラベル]** タブで、 **[ラベルの文字]** に「 **New Store**」と入力します。  
  
5.  **[位置]** で **[上]** をクリックします。  

13. **[フォント]** タブで、フォントのサイズを **[10pt]** 、スタイルを **[太字]** にします。

    ![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  レポートをプレビューします。  
  
店舗の場所の上にラベルが表示されます。  

![report-builder-map-custom-point-new-store](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="CenterView"></a>8.マップの中心の変更およびサイズの変更   
このセクションでは、マップの中心を変更する方法、およびズーム レベルを変更する別の方法について説明します。  
 
1.  デザイン ビューに切り替えます。  

1.  マップを選択して右クリックし、 **[ビューポートのプロパティ]** をクリックします。  
  
2.  **[中心とズーム]** タブで、 **[ビューの中心とズーム レベルを設定する]** オプションが選択されていることを確認します。  

4. **[ズーム レベル (パーセント)]** を **[125]** に設定します。
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  マップをクリックし、目的の場所が中心になるようにドラッグします。  
  
6.  マウス ホイールを使用してズーム レベルを変更することもできます。  
  
7.  レポートをプレビューします。  
  
デザイン ビューでは、デザイン画面やビューのマップはサンプル データに基づいています。 表示されたレポートでは、指定したビューがマップ ビューの中心になります。  
  
## <a name="Title"></a>9.レポート タイトルを追加する  
  
1.  デザイン ビューに切り替えます。
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Sales in New York Stores** 」と入力し、テキスト ボックスの外側をクリックします。  
  
このタイトルは、レポートの最上部に表示されます。 ページ ヘッダーが定義されていない場合は、レポート本文の最上部にあるアイテムがレポート ヘッダーに相当します。  
  
## <a name="Save"></a>10.レポートを保存する  
  
1.  デザイン ビューまたはプレビューで、 **[ファイル]** メニューの **[名前を付けて保存]** をクリックします。
 
3.  **[名前]** に、「 **Store Sales in New York**」と入力します。  

3. ローカル コンピューターまたは [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] サーバーに保存します。
  
4. **[保存]** をクリックします。 

レポート サーバーに保存した場合は、レポート サーバーで表示できます。

![report-builder-map-in-portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## <a name="next-steps"></a>Next Steps  
これで、レポートにマップを追加する方法のチュートリアルは終了です。  
  
詳細については、「[マップ &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)  
[SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[マップ ウィザードおよびマップ レイヤー ウィザードのページ &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[ルールおよび分析データを使用した多角形、線、およびポイントの表示の変更 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  

