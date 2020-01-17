---
title: 'チュートリアル: レポートへの KPI の追加 (レポート ビルダー) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee2333bc6d369bbc9908198d8cfa2fa18ce23065
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041890"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>チュートリアル: レポートへの KPI の追加 (レポート ビルダー)
この [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] チュートリアルでは、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポートに主要業績評価指標 (KPI) を追加します。  

KPI は、ビジネス上重要で、測定可能な値です。 このシナリオの KPI は、製品サブカテゴリ別の販売集計です。 この KPI の現在の状態を、色、ゲージ、およびインジケーターを使用して表示します。
  
次の図に、ここで作成するレポートと同様のレポートを示します。  
  
![report-builder-kpi-report](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> このチュートリアルでは、ウィザードに関する複数の手順を、データセットの作成とテーブルの作成の 2 つの手順にまとめて示します。 レポート サーバーの参照、データ ソースの選択、データセットの作成、およびウィザードの実行に関する詳細な手順については、このシリーズの最初のチュートリアル (「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」) を参照してください。  
  
このチュートリアルの推定所要時間: 15 分  
  
## <a name="requirements"></a>必要条件  
要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/prerequisites-for-tutorials-report-builder.md) を参照してください。  
  
## <a name="Table"></a>1.テーブルまたはマトリックス ウィザードを使用して表レポートとデータセットを作成する  
このセクションでは、共有データ ソースを選択し、埋め込みデータセットを作成して、データをテーブルに表示します。  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>埋め込みデータセットでテーブルを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで、 **[データセットを作成する]** をクリックします。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。 使用できるデータ ソースがなく、レポート サーバーにもアクセスできない場合は、代わりに埋め込みデータ ソースを使用できます。 詳細については、「[チュートリアル: 基本的な表レポートの作成 (レポート ビルダー)](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。  
  
7.  **[次へ]** をクリックします。  
  
8.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
9. 次のクエリをコピーし、クエリ ペインに貼り付けます。  

    > [!NOTE]  
    > このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. クエリ デザイナーのツール バーで、[実行]\( **!** ) をクリックします。

11. **[次へ]** をクリックします。  
  
## <a name="CompleteWizard"></a>2.ウィザードでデータを整理し、レイアウトを選択する  
テーブルまたはマトリックス ウィザードでは、データを表示するための最初のデザインを提供します。 ウィザードのプレビュー ペインでは、テーブルやマトリックスのデザインを完了する前にデータのグループ化の結果を表示できます。  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>データをグループにまとめてレイアウトを選択するには 
  
1.  [フィールドの配置] ページで、Product を **[値]** にドラッグします。  
  
2.  Quantity を **[値]** にドラッグして Product の下に配置します。  
  
    Quantity は Sum 関数 (数値フィールドを集計するための既定の関数) を使用して集計されます。  
  
3.  Sales を **[値]** にドラッグして Quantity の下に配置します。  
  
    手順 1. ～ 3. で、テーブルに表示するデータが指定されます。  
  
4.  SalesDate を **[行グループ]** にドラッグします。  
  
5.  Subcategory を **[行グループ]** にドラッグして SalesDate の下に配置します。  
  
    手順 4. および 5. で、フィールドの値がまず日付でまとめられ、次にその日付のすべての売上でまとめられます。  
  
6.  **[次へ]** をクリックします。  
  
    レポートを実行すると、テーブルに各日付、日付ごとのすべての注文、および注文ごとのすべての製品、数量、および売上の合計が表示されます。  
  
7.  [レイアウトの選択] ページの **[オプション]** で、 **[小計と総計を表示]** が選択されていることを確認します。  
  
8.  **[ブロック、小計は下]** が選択されていることを確認します。  
  
9. **[グループの展開/折りたたみ]** オプションをオフにします。  
  
    このチュートリアルで作成するレポートでは、ユーザーが親グループ階層を展開して子グループ行および詳細行を表示できるようにするドリル ダウン機能は使用されません。  
  
10. **[次へ]** をクリックします。  
  
11. **[完了]** をクリックします。  
  
      テーブルがデザイン画面に追加されます。 テーブルには 5 列 5 行が含まれています。 行グループ ペインに、SalesDate、Subcategory、および Details の 3 つの行グループが表示されます。 詳細データは、データセット クエリによって取得されるすべてのデータです。 [列グループ] ペインが空です。  
      
      ![report-builder-kpi-row-groups](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. **[実行]** をクリックして、レポートをプレビューします。  
  
テーブルには、特定の日付に販売された製品ごとに製品名、販売数量、および売上合計が表示されます。 このデータがまず販売日でまとめられ、次にサブカテゴリでまとめられます。 

![report-builder-kpi-basic-table](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>日付と通貨の書式を設定する
列の幅を広げ、日付と通貨の書式を設定してみましょう。

1. **[デザイン]** をクリックしてデザイン ビューに戻ります。

2. 製品名には、もっと広い領域が必要かもしれません。 Product 列の幅を広げるには、テーブル全体を選択し、Product 列の上部にある列ハンドルの右端をドラッグします。

3. Ctrl キーを押しながら、 [Sum(Sales)] が格納されている 4 つのセルを選択します。

4. **[ホーム]** タブで、 **[数値]**  >  **[通貨]** の順に選択します。 書式設定された通貨を表示するようにセルが変化します。

   地域設定が英語 (米国) の場合、既定のサンプル テキストは [$12,345.00] です。 通貨値の例が表示されない場合は、 **[数値]** グループで、 **[プレースホルダーのスタイル]**  >  **[サンプルの値]** の順にクリックします。
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (省略可) **[ホーム]** タブの **[数値]** グループで、 **[小数点表示桁下げ]** ボタンを 2 回クリックして、表示されるドルの値にセントの部分が含まれないようにします。

6. [SalesDate] が格納されたセルをクリックします。

6. **[数値]** グループの **[日付]** を選択します。

   セルに、日付の例として [2000/1/31] と表示されます。 

12. **[実行]** をクリックして、レポートをプレビューします。  
 
![report-builder-kpi-format-numbers](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3.背景色を使用して KPI を表示する  
背景色を、レポートの実行時に評価される式に設定することができます。  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>背景色を使用して KPI の現在の状態を表示するには  
  
1.  テーブルで、2 番目の `[Sum(Sales)]` セル (サブカテゴリの売上を表示する小計行) を右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。 

    **[テキスト ボックスのプロパティ]** を表示するには、セル内のテキストではなく、セルが選択されていることを確認します。 
    
    ![report-builder-text-box-properties](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  **[塗りつぶし]** タブで、 **[塗りつぶしの色]** の横にある **[fx]** ボタンをクリックし、 **[式の設定: BackgroundColor]** フィールドに次の式を入力します。  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     これにより、 `[Sum(Sales)]` の集計値が 5000 以上になる各セルの背景色が "黄緑色" に変わります。 2500 ～ 5000 の `[Sum(Sales)]` の値は、"黄色" で表示されます。 2500 未満の値は "赤色" で表示されます。  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  **[実行]** をクリックして、レポートをプレビューします。  
  
サブカテゴリの売上を表示する小計行のセルの背景色が、合計売上の値に応じて赤、黄、または緑になります。  

![report-builder-kpi-colors](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4.ゲージを使用して KPI を表示する  
ゲージは、データセットの単一の値を表示します。 このチュートリアルでは、水平方向の線形ゲージを使用します。このゲージは、その形と単純さにより、テーブルのセルで使用してサイズが小さくなっても読み取りやすいからです。 詳しくは、「 [ゲージ &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)」をご覧ください。  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>ゲージを使用して KPI の現在の状態を表示するには  
  
1.  デザイン ビューに再び切り替えます。  
  
2.  テーブル内の Sales 列の列ハンドルを右クリックし、 **[列の挿入]**  >  **[右]** の順にクリックします。 テーブルに新しい列が追加されます。  

    ![report-builder-kpi-insert-column](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  列見出しに「 **Linear KPI** 」と入力します。  
  
4.  **[挿入]** タブで、 **[データ ビジュアライゼーション]**  >  **[ゲージ]** の順にクリックし、テーブル外部のデザイン画面内をクリックします。   
  
5.  **[ゲージの種類の選択]** ダイアログ ボックスで、最初の線形ゲージの種類として **[水平]** を選択します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    デザイン画面にゲージが追加されます。  
  
7.  レポート データ ペインのデータセットから `Sales` フィールドをゲージにドラッグします。 **ゲージ データ** ペインが開きます。  
  
    `Sales` フィールドをゲージにドロップすると、そのフィールドは、 **[値]** リストに移動し、組み込み Sum 関数を使用して集計されます。  
   
    ![report-builder-kpi-drag-sales-field](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. **[ゲージ データ]** ペインで、 **[LinearPointer1]** の横にある矢印  >  **[ポインターのプロパティ]** の順にクリックします。  
  
10. **[線形ポインターのプロパティ]** ダイアログ ボックスで、 **[ポインター オプション]** タブ、 **[ポインター型]** の順にクリックし、 **[バー]** が選択されていることを確認します。 
 
11. **[OK]** をクリックします。  
  
12. ゲージのスケールを右クリックし、 **[スケールのプロパティ]** をクリックします。  
  
13. **[線形スケールのプロパティ]** ダイアログ ボックスの **[全般]** タブをクリックし、 **[最大]** を 25000 に設定します。  

    > [!NOTE]  
    > 25000 などの定数の代わりに、 **[最大]** オプションの値を動的に計算する式を使用することもできます。 その式では、入れ子になった集計の機能を使用します (例: `=Max(Sum(Fields!Sales.value), "Tablix1")`)。  

14. **[ラベル]** タブで、 **[スケールのラベルを非表示にする]** をオンにします。

15. **[OK]** をクリックします。
  
14. 背景色の式を追加したフィールドの横にある `Subcategory` フィールドの売上高の小計を表示する行で、Linear KPI 列の 2 番目のセルに、テーブル内のゲージをドラッグします。  
  
    > [!NOTE]  
    > 水平方向の線形ゲージがセルに収まるように、列のサイズを変更することが必要な場合があります。 列のサイズを変更するには、テーブルを選択し、列ハンドルをドラッグします。 レポート デザイン画面のサイズが、テーブルが収まるように変更されます。  
  
15. **[実行]** をクリックして、レポートをプレビューします。  
  
    ゲージ内の緑色バーの幅が、KPI の値によって変わります。  
  
![report-builder-linear-kpi](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5.インジケーターを使用して KPI を表示する  
インジケーターは、データ値をひとめでわかるようにするための単純で小さなゲージです。 そのサイズと単純さのために、テーブルやマトリックスでよく使用されます。 詳細については、「[インジケーター (レポート ビルダーおよび SSRS)](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>インジケーターを使用して KPI の現在の状態を表示するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  テーブルにおいて、前回の手順で追加した Linear KPI 列の列ハンドルを右クリックし、 **[列の挿入]**  >  **[右]** の順にクリックします。 テーブルに新しい列が追加されます。  
  
3.  列見出しに「 **Stoplight KPI** 」と入力します。  
  
4.  前回の手順で追加した線形ゲージの横にあるサブカテゴリの小計のセルをクリックします。  
  
5.  **[挿入]** タブで、 **[データ ビジュアライゼーション]** をクリックし、 **[インジケーター]** をダブルクリックします。  
  
6.  **[インジケーターの種類の選択]** ダイアログ ボックスの **[図形]** で、最初の図形の種類として、 **[3 つの信号 (枠なし)]** を選択します。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    新しい Stoplight KPI 列のセルにインジケーターが追加されます。  
  
8.  インジケーターを右クリックし、 **[インジケーターのプロパティ]** をクリックします。  
  
9. **[値と状態]** タブの **[値]** ボックスで、 **[Sum (Sales)]** を選択します。 その他のオプションは変更しないでください。  
  
    既定では、データ領域のデータが同期され、 **Tablix1**という値 (レポートのテーブル データ領域の名前) が **[同期スコープ]** ボックスに表示されます。  
  
    このレポートでは、サブカテゴリの小計のセルに配置したインジケーターのスコープを変更して、SalesDate フィールドのデータが同期されるようにすることもできます。  
  
11. **[OK]** をクリックします。

11. **[実行]** をクリックして、レポートをプレビューします。  

![report-builder-kpi-stoplight](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6.レポート タイトルを追加する  
レポート タイトルは、レポートの最上部に表示されます。 レポート ヘッダーがあれば、そこにレポート タイトルを配置します。レポート ヘッダーを使用しない場合は、レポート本文の一番上のテキスト ボックスに配置します。 このセクションでは、自動的にレポート本文の一番上に配置されるテキスト ボックスを使用します。  
  
テキストの語句や文字のフォントのスタイル、サイズ、および色を変更して、テキストをさらに強調することもできます。 詳細については、「[テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Product Sales KPIs**」と入力し、テキスト ボックスの外側をクリックします。  
  
3.  必要に応じて、 **Product Sales KPI**が含まれているテキスト ボックスを右クリックして **[テキスト ボックスのプロパティ]** をクリックし、[フォント] タブでフォントのスタイル、サイズ、および色を変更します。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Save"></a>7.レポートを保存する  
レポートをレポート サーバーまたは自分のコンピューターに保存します。 レポート サーバーに保存しない場合は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のいくつかの機能 (レポート パーツ、サブレポートなど) が使用できなくなります。  
  
### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に入力されている既定の名前を「 **Product Sales KPI**」に置き換えます。  
  
5.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
> [!NOTE]  
> レポート サーバーにアクセスできない場合は、 **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、コンピューターにレポートを保存してください。  
  
1.  **[名前]** に入力されている既定の名前を「 **Product Sales KPI**」に置き換えます。  
  
2.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  
これで、「レポートへの KPI の追加」チュートリアルを終了します。 詳細については、以下をご覧ください。
*  [ゲージ](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [インジケーター](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
* [レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)
* [SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

