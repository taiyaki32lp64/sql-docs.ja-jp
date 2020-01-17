---
title: チュートリアル:レポートへの KPI の追加 (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a1b158b6fc504a0917e0c268846da93be3aa59b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098976"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>チュートリアル:レポートへの KPI の追加 (レポート ビルダー)
  主要業績評価指標 (KPI) は、ビジネス上重要な測定可能値です。 このチュートリアルでは、レポートに KPI を追加する方法を説明します。 このシナリオの KPI は、製品サブカテゴリ別の販売集計です。 この KPI の現在の状態を、色、ゲージ、およびインジケーターを使用して表示します。  
  
 次の図に、ここで作成するレポートを示します。  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="BackToTop"></a> 学習内容  
 このチュートリアルでは、テーブルのセルの背景色をセルの値に基づいて設定することによって KPI を追加する方法、ゲージおよびインジケーターを追加して構成する方法、 およびテーブルのセルの背景色を設定する式を作成する方法を学習します。  
  
 このチュートリアルでは以下の手順について説明します。  
  
1.  [テーブルまたはマトリックス ウィザードから、テーブル レポートとデータセットを作成します。](#Table)  
  
2.  [データを整理し、レイアウトを選択して、テーブルまたはマトリックス ウィザードからスタイル](#CompleteWizard)  
  
3.  [背景色を使用して KPI を表示します。](#BackgroundColors)  
  
4.  [ゲージを使用して、KPI を表示します。](#Gauge)  
  
5.  [インジケーターを使用して、KPI を表示します。](#Indicator)  
  
6.  [レポート タイトルを追加します。](#Title)  
  
7.  [レポートを保存します。](#Save)  
  
> [!NOTE]  
>  このチュートリアルでは、ウィザードに関する複数の手順を、データセットの作成とテーブルの作成の 2 つの手順にまとめて示します。 レポート サーバーの参照、データ ソースの選択、データセットの作成、およびウィザードの実行に関する詳細な手順については、このシリーズの最初のチュートリアルである「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。  
  
 このチュートリアルの推定所要時間:15 分。  
  
## <a name="requirements"></a>必要条件  
 要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/report-builder-tutorials.md)」を参照してください。  
  
##  <a name="Table"></a> 1.テーブルまたはマトリックス ウィザードを使用して表レポートとデータセットを作成する  
 **Getting Started**ダイアログ ボックスで、共有データ ソースを選択して、埋め込みデータセットを作成、テーブルにデータを表示します。  
  
> [!NOTE]  
>  このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
#### <a name="to-create-a-new-table"></a>新しいテーブルを作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[プログラム]** 、 **[Microsoft SQL Server 2012 レポート ビルダー]** の順にポイントして、 **[レポート ビルダー]** をクリックします。  
  
     **[作業の開始]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  場合、 **Getting Started**  ダイアログ ボックスが表示されない、レポート ビルダーのボタン クリックして**新規**します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  データセットのページの選択、**データセットを作成する**します。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。 使用できるデータ ソースがなく、レポート サーバーにもアクセスできない場合は、代わりに埋め込みデータ ソースを使用できます。 詳細については、「[チュートリアル:基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。  
  
7.  **[次へ]** をクリックします。  
  
8.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
9. 次のクエリをコピーし、クエリ ペインに貼り付けます。  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. **[次へ]** をクリックします。  
  
##  <a name="CompleteWizard"></a> 2.データを整理し、レイアウトを選択して、テーブルまたはマトリックス ウィザードからスタイル  
 ウィザードを使用して、データを表示する最初のデザインを作成します。 ウィザードのプレビュー ペインでは、テーブルやマトリックスのデザインを完了する前にデータのグループ化の結果を表示できます。  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>グループにデータを整理するには、レイアウトとスタイルを選択します  
  
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
  
11. [スタイルの選択] ページのスタイル ペインで、スタイルを選択します。  
  
     先ほどの図の完成したレポートでは、[オーシャン] スタイルが使用されています。  
  
12. **[完了]** をクリックします。  
  
     テーブルがデザイン画面に追加されます。 テーブルには 5 列 5 行が含まれています。 [行グループ] ウィンドウには 3 つの行グループが表示されます。SalesDate、Subcategory、Details です。 詳細データは、データセット クエリによって取得されるすべてのデータです。  
  
13. **[実行]** をクリックして、レポートをプレビューします。  
  
 テーブルには、特定の日付に販売された製品ごとに製品名、販売数量、および売上合計が表示されます。 このデータがまず販売日でまとめられ、次にサブカテゴリでまとめられます。  
  
##  <a name="BackgroundColors"></a> 3.背景色を使用して KPI を表示する  
 背景色を、レポートの実行時に評価される式に設定することができます。  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>背景色を使用して KPI の現在の状態を表示するには  
  
1.  表内のセルを右クリックして 2 つ下から、`[Sum(Sales)]`セル (小計行サブカテゴリの売上を表示する)、およびクリック**テキスト ボックスのプロパティ**します。  
  
2.  **入力**、 をクリックして、 **fx**横に、**塗りつぶしの色**オプションし、次の式を入力、**式の設定。BackgroundColor** フィールド。  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 これにより、`[Sum(Sales)]` の集計値が 5000 以上になる各セルの背景色が、"ライム" という緑の網掛けを使用した緑色に変わります。 2500 ～ 5000 の `[Sum(Sales)]` の値は、黄色で表示されます。 2500 未満の値は赤色で表示されます。  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  **[実行]** をクリックして、レポートをプレビューします。  
  
 サブカテゴリの売上を表示する小計行のセルの背景色が、合計売上の値に応じて赤、黄、または緑になります。  
  
##  <a name="Gauge"></a> 4.ゲージを使用して KPI を表示する  
 ゲージは、データセットの単一の値を表示します。 このチュートリアルでは、水平方向の線形ゲージを使用します。このゲージは、その形と単純さにより、テーブルのセルで使用してサイズが小さくなっても読み取りやすいからです。 詳しくは、「 [ゲージ &#40;レポート ビルダーおよび SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)」をご覧ください。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>ゲージを使用して KPI の現在の状態を表示するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  テーブルの列ハンドルを右クリックし、前の手順で変更して、セルへのポイント**列の挿入**、順にクリックします**右**します。 テーブルに新しい列が追加されます。  
  
3.  型**KPI**列見出し。  
  
4.  **挿入**] タブで、**データ領域**グループで、[**ゲージ**、デザイン画面にテーブル外部の順にクリックします。 **[ゲージの種類の選択]** ダイアログ ボックスが表示されます。  
  
5.  クリックして**線形**します。 最初の線形ゲージの種類、**水平**が選択されています。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     デザイン画面にゲージが追加されます。  
  
7.  レポート データ ペインからゲージに Sales をドラッグします。 Sales をゲージにドラッグすると、ゲージ データ ペインが開きます。  
  
8.  Sales を削除、**値**一覧。  
  
     フィールドをゲージにドロップすると、組み込み Sum 関数を使用してフィールドが集計されます。  
  
9. ゲージのポインターを右クリックし、をクリックして**ポインターのプロパティ**します。  
  
10. **ポインター型**、**バー**します。 これにより、ポインターがマーカーからバーに変更され、テーブルにゲージを追加したときに見やすくなります。  
  
11. クリックして**ポインターの塗りつぶし**します。 **2 番目の色、** 選択**黄色**します。 グラデーションの塗りつぶしパターンが白から黄色に変更されます。  
  
12. ゲージのスケールを右クリックし、 **[スケールのプロパティ]** をクリックします。  
  
13. 設定、**最大**オプションを 25000 にします。  
  
    > [!NOTE]  
    >  25000 などの定数の代わりに、 **[最大]** オプションの値を動的に計算する式を使用することもできます。 その式では、入れ子になった集計の機能を使用します (例: `=Max(Sum(Fields!Sales.value), "Tablix1")`)。  
  
14. ゲージを、テーブル内の挿入した列の、サブカテゴリの売上を表示する小計行の 3 番目のセルにドラッグします。  
  
    > [!NOTE]  
    >  水平方向の線形ゲージがセルに収まるように、列のサイズを変更する必要があります。 列のサイズを変更するには、列ヘッダーをクリックし、ハンドルを使用してセルの横方向と縦方向のサイズを変更します。  
  
15. **[実行]** をクリックして、レポートをプレビューします。  
  
     ゲージ内のバーの幅が、KPI の値によって変わります。  
  
16. (省略可) オーバーフローを処理する最大ピンを追加して、スケールの最大値を超える任意の値が常に最大ピンを参照できるようにします。  
  
    1.  プロパティ ペインを開きます。  
  
    2.  [スケール] をクリックします。 線形スケールのプロパティがプロパティ ペインに表示されます。  
  
    3.  **スケールのピン**カテゴリで、展開、 **[maximumpin]** ノード。  
  
    4.  設定、**を有効にする**プロパティを`True`します。 スケールの最大値の後にピンが表示されます。  
  
    5.  設定**BorderColor**に`Lime`します。  
  
17. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Indicator"></a> 5.インジケーターを使用して KPI を表示する  
 インジケーターは、データ値をひとめでわかるようにするための単純で小さなゲージです。 そのサイズと単純さのために、テーブルやマトリックスでよく使用されます。 詳細については、「[インジケーター (レポート ビルダーおよび SSRS)](report-design/indicators-report-builder-and-ssrs.md)」を参照してください。  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>インジケーターを使用して KPI の現在の状態を表示するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  テーブルの列ハンドルを右クリックし、前の手順で変更して、セルへのポイント**列の挿入**、順にクリックします**右**します。 テーブルに新しい列が追加されます。  
  
3.  型**KPI**列見出し。  
  
4.  サブカテゴリの小計のセルをクリックします。  
  
5.  **挿入** タブで、**データ領域**グループで、ダブルクリックして**インジケーター。**  
  
     **[インジケーターの種類の選択]** ダイアログ ボックスが表示されます。  
  
6.  クリックして**図形**します。 最初の図形の種類、 **3 つの信号 (枠なし)、** が選択されています。  
  
     このチュートリアルではこのインジケーターを使用します。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     インジケーターがデザイン画面に追加されます。  
  
8.  インジケーターを右クリックし、 **[インジケーターのプロパティ]** をクリックします。  
  
9. クリックして**値と状態**します。  
  
10. 値のドロップダウン リストで選択 **[sum (sales)]** がその他のオプションを変更しません。  
  
     既定では、データ領域のデータが同期され、 **Tablix1**という値 (レポートのテーブル データ領域の名前) が **[同期スコープ]** ボックスに表示されます。  
  
     このレポートでは、サブカテゴリの小計のセルに配置したインジケーターのスコープを変更して、SalesDate フィールドのデータが同期されるようにすることもできます。  
  
11. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Title"></a> 6.レポート タイトルを追加する  
 レポート タイトルは、レポートの最上部に表示されます。 レポート ヘッダーがあれば、そこにレポート タイトルを配置します。レポート ヘッダーを使用しない場合は、レポート本文の一番上のテキスト ボックスに配置します。 その場合は、自動的にレポート本文の一番上に配置されるテキスト ボックスを使用します。  
  
 テキストの語句や文字のフォントのスタイル、サイズ、および色を変更して、テキストをさらに強調することもできます。 詳細については、「[テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)」を参照してください。  
  
#### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  型**Product Sales KPI**、テキスト ボックスの外側をクリックします。  
  
3.  必要に応じて、[を含むテキスト ボックスを右クリックして**Product Sales KPI**、] をクリックして**テキスト ボックスのプロパティ**、し、[フォント] タブのフォントのスタイル、サイズと色を選択します。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Save"></a> 7.レポートを保存する  
 レポートをレポート サーバーまたは自分のコンピューターに保存します。 レポート サーバーに保存しない場合は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のいくつかの機能 (レポート パーツ、サブレポートなど) が使用できなくなります。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
     "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に入力されている既定の名前を「 **Product Sales KPI**」に置き換えます。  
  
5.  **[保存]** をクリックします。  
  
 レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
#### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
> [!NOTE]  
>  レポート サーバーにアクセスできない場合は、 **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、コンピューターにレポートを保存してください。  
  
1.  **[名前]** に入力されている既定の名前を「 **Product Sales KPI**」に置き換えます。  
  
2.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 これで、「レポートへの KPI の追加」チュートリアルを終了します。 詳細については、ゲージ (レポート ビルダー) を参照してください。[インジケーター&#40;レポート ビルダーおよび SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)します。  
  
## <a name="see-also"></a>参照  
 [チュートリアル&#40;レポート ビルダー&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 のレポート ビルダー](report-builder/report-builder-in-sql-server-2016.md)  
  
  
