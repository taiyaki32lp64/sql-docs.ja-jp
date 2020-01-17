---
title: チュートリアル:自由形式のレポートの作成 (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 332c67f47c8096cbeb5a94c4e2a288cd532038cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098948"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>チュートリアル:自由形式のレポートの作成 (レポート ビルダー)
  このチュートリアルでは、フォーム レターのような SSRS 自由形式レポートを作成する方法を説明します。 レポート アイテムを配置して、テキスト ボックス、画像、その他のデータ領域が含まれるフォームを作成できます。  
  
 このチュートリアルで作成するレポートは、このチュートリアルに含まれているサンプルの売上データに基づいています。 このレポートでは、販売区域ごとに情報をまとめて、各区域の販売責任者の名前と売上情報の概要を表示します。 自由形式レポートでは、一覧データ領域を基盤として使用し、画像を使用した装飾用のパネル、データが挿入された静的テキスト、詳細情報を表示するテーブル、および必要に応じて概要情報を表示する円グラフと縦棒グラフを追加します。  
  
##  <a name="BackToTop"></a> 学習内容  
 このチュートリアルでは、次の方法を学習します。  
  
-   [空のレポート、データ ソース、およびデータセットを作成します。](#BlankReport)  
  
-   [追加し、一覧の構成](#List)  
  
-   [グラフィックスを追加します。](#Graphics)  
  
-   [自由形式テキストを追加します。](#Text)  
  
-   [詳細を表示するテーブルを追加します。](#Table)  
  
-   [データを書式設定](#Format)  
  
-   [レポートを保存します。](#Save)  
  
### <a name="other-optional-steps"></a>その他のオプションの手順  
  
-   [レポートの領域に行を追加します。](#Line)  
  
-   [概要データの視覚化を追加します。](#Visualization)  
  
 このチュートリアルの推定所要時間:20 分  
  
## <a name="requirements"></a>必要条件  
 要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/report-builder-tutorials.md)」を参照してください。  
  
##  <a name="BlankReport"></a> 1.空のレポート、データ ソース、およびデータセットを作成する  
  
> [!NOTE]  
>  このチュートリアルでは、レポートが外部のデータ ソースを必要としないように、クエリにデータ値が含まれています。 この種の内部データは学習に使用する目的に役立ちますが、そのためクエリが長くなっています。 .  
  
#### <a name="to-create-a-blank-report"></a>空のレポートを作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[プログラム]** 、 **[Microsoft SQL Server 2012 レポート ビルダー]** の順にポイントして、 **[レポート ビルダー]** をクリックします。  
  
    > [!NOTE]  
    >  **[作業の開始]** ダイアログ ボックスが表示されます。 表示されない場合は、レポート ビルダーのボタンの **[新規作成]** をクリックします。  
  
2.  **[作業の開始]** ダイアログ ボックスの左ペインで **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[空のレポート]** をクリックします。  
  
#### <a name="to-create-a-new-data-source"></a>新しいデータ ソースを作成するには  
  
1.  レポート データ ペインで、 **[新規作成]** をクリックし、 **[データ ソース]** をクリックします。  
  
2.  `Name`ボックスに、入力します。「**ListDataSource**」と入力します。  
  
3.  **[レポートに埋め込まれた接続を使用する]** をクリックします。  
  
4.  接続の種類が Microsoft SQL Server であることを確認したら **[接続文字列]** ボックスに次のように入力します。**Data Source = \<servername>**  
  
     \<サーバー名 >、たとえば report001 など、SQL Server データベース エンジンのインスタンスがインストールされているコンピューターを指定します。 レポート データは SQL Server のデータベースから抽出されるのではないので、データベース名を含める必要はありません。 指定したサーバー上の既定のデータベースを使用して、クエリが解析されます。  
  
5.  **[資格情報]** をクリックし、SQL Server データベース エンジンのインスタンスとの接続に必要な資格情報を入力します。  
  
6.  **[OK]** をクリックします。  
  
#### <a name="to-create-a-new-dataset"></a>新しいデータセットを作成するには  
  
1.  レポート データ ペインで、 **[新規作成]** をクリックし、 **[データセット]** をクリックします。  
  
2.  `Name`ボックスに、入力します。 **[Listdataset]。**  
  
3.  **[レポートに埋め込まれたデータセットを使用します]** をクリックし、データ ソースが **ListDataSource**であることを確認します。  
  
4.  クエリの種類に **[テキスト]** が選択されていることを確認してから、 **[クエリ デザイナー]** をクリックします。  
  
5.  **[テキストとして編集]** をクリックします。  
  
6.  次のクエリをコピーし、クエリ ペインに貼り付けます。  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  [実行] アイコンをクリックしてクエリを実行します。  
  
     クエリの結果が、レポートに表示できるデータになります。  
  
     ![クエリ デザイナー](../../2014/tutorials/media/tutorial-querydesigner.png "クエリ デザイナー")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="List"></a> 2.一覧を追加および構成する  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] には、テーブル、マトリックス、リストという 3 つのデータ領域テンプレートがあります。 これらのテンプレートはすべて、tablix データ領域に基づいています。  
  
 このチュートリアルでは、リストを使用して、ニュースレターのようなレポートに、販売区域の販売情報を表示します。 情報は、区域ごとにグループ化されます。 区域ごとのデータをグループ化する新しい行グループを追加し、組み込みの詳細行グループを削除します。 リスト テンプレートは、自由形式レポートを作成するのに最適です。 詳細については、次を参照してください。[一覧&#40;レポート ビルダーおよび SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)します。  
  
> [!NOTE]  
>  このレポートでは、用紙サイズを Letter (8.5 X11) にし、余白を 1 インチとします。 縦が 9 インチまたは横が 6 1/2 インチよりも大きいレポート ページでは、空のページが生成される可能性があります。  
  
#### <a name="to-add-a-list"></a>一覧を追加するには  
  
1.  リボンの **[挿入]** タブの **[データ領域]** で **[一覧]** をクリックし、レポート本文内に一覧をドラッグします。 リストの高さを 7 インチ、幅を 6.25 インチにします。  
  
2.  一覧内をクリックし、一覧の先頭を右クリックし、 **[Tablix のプロパティ]** をクリックします。  
  
     ![追加一覧](../../2014/tutorials/media/tutorial-addinglistwithnumbers.png "追加一覧")  
  
3.  **[データセット名]** ドロップダウン リストの **[ListDataset]** を選択します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  一覧内を右クリックし、 **[四角形のプロパティ]** をクリックします。  
  
     ![四角形のプロパティ コマンド](../../2014/tutorials/media/tutorial-rectanglepropertiescommand.png "四角形のプロパティ コマンド")  
  
6.  **[全般]** タブで **[後に改ページを追加する]** チェック ボックスをオンにします。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>新しい行グループを追加し、詳細グループを削除するには  
  
1.  行グループ ペインで、詳細グループを右クリックし、 **[グループの追加]** をポイントして **[親グループ]** をクリックします。  
  
     ![親グループ コマンド](../../2014/tutorials/media/tutorial-parentgroupcommand.png "親グループ コマンド")  
  
2.  ドロップダウン リストの `[Territory].` を選択します。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     一覧に列が追加されます。 この列には、`[Territory].` セルが格納されます。  
  
4.  一覧の Territory 列を右クリックし、 **[列の削除]** をクリックします。  
  
     ![列の削除](../../2014/tutorials/media/tutorial-deletecolumnscommand.png "列の削除")  
  
5.  **[列のみの削除]** をクリックします。  
  
     ![列の削除 ダイアログ ボックス](../../2014/tutorials/media/tutorial-deletecolumnsdialog.png "列の削除 ダイアログ ボックス")  
  
6.  行グループ ペインで、 **[詳細]** グループを右クリックし、 **[グループの削除]** をクリックします。  
  
     ![詳細グループの削除](../../2014/tutorials/media/tutorial-deletedetailsgroup.png "詳細グループの削除")  
  
7.  **[グループのみを削除]** をクリックします。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Graphics"></a> 3.グラフィックスを追加する  
 一覧データ領域を使用する利点の 1 つは、表形式のレイアウトに制限されずに、四角形やテキスト ボックスなどのレポート アイテムをどこにでも追加できることです。 ここでは、グラフィック (任意の色で塗りつぶされた四角形) を追加して、レポートの体裁を整えます。  
  
#### <a name="to-add-graphic-elements-to-the-report"></a>レポートにグラフィック要素を追加するには  
  
1.  **挿入** タブ、リボンのをクリックして**四角形**リストの左上隅を四角形をドラッグします。 四角形のサイズを縦 7 インチ、横 1 インチにします。  
  
2.  四角形を右クリックし、 **[四角形のプロパティ]** をクリックします。  
  
3.  **[塗りつぶし]** タブをクリックします。  
  
4.  **[塗りつぶしの色]** ドロップ ダウン リストの **[その他の色]** をクリックし、 **[濃い灰色]** を選択します。  
  
     ![塗りつぶしの色を選択します](../../2014/tutorials/media/tutorial-selectfillcolorwithnumbers.png "選択の塗りつぶしの色。")  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
 レポートの左側に、ダーク グレー色の四角形からなる縦長のグラフィックが追加されています。  
  
##  <a name="Text"></a> 4.自由形式テキストを追加する  
 テキスト ボックスには、各レポート ページに繰り返し表示される静的テキストとデータ フィールドが含まれます。  
  
#### <a name="to-add-text-to-the-report"></a>テキストをレポートに追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  リボンの **[挿入]** タブにある **[テキスト ボックス]** をクリックし、一覧の左上隅、以前追加した四角形の内部にテキスト ボックスをドラッグします。 テキスト ボックスのサイズを縦 3 インチ、横 5 インチにします。  
  
3.  テキスト ボックスの上部にカーソルを置き、次のように入力します。「**Newsletter for**」と入力します。  
  
     ![ニュースレターの見出しテキストの追加](../../2014/tutorials/media/tutorial-newsletterfor.png "ニュースレターの見出しテキストの追加")  
  
    > [!NOTE]  
    >  for の後に必ずスペースを入れてください。 このスペースによって、入力したテキストと次の手順で追加するフィールドが分けられます。  
  
4.  Territory フィールドをテキスト ボックスにドラッグし、手順 3. で入力したテキストの後に配置します。  
  
     ![Territorial フィールドの追加](../../2014/tutorials/media/tutorial-addterritorialfield.png "追加 Territorial フィールド")  
  
5.  すべてのテキストを選択して右クリックし、 **[テキストのプロパティ]** をクリックします。  
  
6.  **[フォント]** タブをクリックします。  
  
7.  **[フォント]** ボックスの一覧の **[Times New Roman]** 、 **[サイズ]** ボックスの一覧の **[20 pt]** 、および **[色]** ボックスの一覧の **[赤]** を選択します。  
  
     ![テキスト プロパティ](../../2014/tutorials/media/tutorial-textpropertieswithnumbers.png "テキストのプロパティ")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 手順 3 で入力したテキストの下にカーソルを置いて、次のように入力します。**こんにちは**します。  
  
    > [!NOTE]  
    >  「Hello」の後に必ずスペースを入れてください。 このスペースによって、入力したテキストと次の手順で追加するフィールドが分けられます。  
  
10. FullName フィールドをテキスト ボックスにドラッグして、手順 9. で入力したテキストの後に配置し、コンマ (,) を入力します。  
  
     ![完全な名前のフィールドの追加](../../2014/tutorials/media/tutorial-addfullnamefield.png "完全な名前の追加フィールド")  
  
11. 手順 9. および 10. で追加したテキストを選択して右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
12. **[フォント]** タブをクリックします。  
  
13. **[フォント]** ボックスの一覧の **[Times New Roman]** 、 **[サイズ]** ボックスの一覧の **[16 pt]** 、および **[色]** ボックスの一覧の **[黒]** を選択します。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 手順 9. ～ 13. で追加したテキストの下にカーソルを置き、次の "意味不明" のテキストをコピーして貼り付けます。  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
    Nulla facilisi. Proin ligula enim, porta ut tincidunt id, adipiscing sit amet eros. Ut purus sem, bibendum et vulputate sit amet, facilisis eget magna. Sed aliquam erat non erat eleifend hendrerit. Ut a ligula est, sit amet eleifend enim. Ut et nisl enim, sit amet adipiscing augue. Vivamus eu arcu ac libero posuere elementum. Integer condimentum bibendum venenatis. Integer odio tellus, feugiat in pellentesque semper, interdum nec sem. Sed cursus euismod sem, ut elementum sapien placerat vel.   
    ```  
  
16. 手順 15. で追加したテキストを選択して右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
17. **[フォント]** タブをクリックします。  
  
18. **[フォント]** ボックスの一覧の **[Arial]** 、 **[サイズ]** ボックスの一覧の **[10 pt]** 、および **[色]** ボックスの一覧の **[黒]** を選択します。  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![ニュースレター テキストの追加](../../2014/tutorials/media/tutorial-newslettertext.png "ニュースレター テキストの追加")  
  
20. 手順 15 で貼り付けたテキストの下にカーソルを置いて、次のように入力します。**これで、売上合計**します。  
  
    > [!NOTE]  
    >  of の後に必ずスペースを入れてください。 このスペースによって、入力したテキストと次の手順で追加するフィールドが分けられます。  
  
21. Sales フィールドをテキスト ボックスにドラッグして、手順 20. で入力したテキストの後に配置し、感嘆符 (!) を入力します。  
  
22. Sales フィールドを強調表示で、フィールドを右クリックし をクリックし、**式**します。  
  
23. [式] ボックスの式を変更して、次のように Sum 関数を指定します。  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![売上フィールドに式を追加](../../2014/tutorials/media/tutorial-addexpressiontosalesfield.png "売上フィールドに式を追加")  
  
25. 手順 20. ～ 23. で追加したテキストを選択して右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
26. **[フォント]** タブをクリックします。  
  
27. **[フォント]** ボックスの一覧の **[Times New Roman]** 、 **[サイズ]** ボックスの一覧の **[16 pt]** 、および **[色]** ボックスの一覧の **[赤]** を選択します。  
  
28. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
29. `[Sum(Sales)]` を選択し、 **[ホーム]** タブの **[数値]** グループで、 **[通貨]** ボタンをクリックします。  
  
     ![追加の通貨記号](../../2014/tutorials/media/tutorial-addcurrencysymbol.png "通貨記号の追加")  
  
30. "クリックしてタイトルを追加" というテキストが含まれているテキスト ボックスを右クリックし、 **[削除]** をクリックします。  
  
31. リスト ボックスを選択し、方向キーを使用して、リスト ボックスをページの先頭に移動します。  
  
32. **[実行]** をクリックして、レポートをプレビューします。  
  
 レポートに静的テキストが表示され、各レポート ページには特定の販売区域についてのデータが含まれています。 売上には通貨の書式が適用されます。  
  
 ![ニュースレターのプレビュー](../../2014/tutorials/media/tutorial-newsletters.png "ニュースレターのプレビュー")  
  
##  <a name="Table"></a> 5.売上の詳細情報を表示するテーブルを追加する  
 テーブルまたはマトリックスの新規作成ウィザードを使用して、自由形式レポートにテーブルを追加します。 ウィザードの完了後、合計を表示する行を手動で追加します。  
  
#### <a name="to-add-a-table"></a>テーブルを追加するには  
  
1.  リボンの **[挿入]** タブの **[データ領域]** で **[テーブル]** をクリックし、 **[テーブル ウィザード]** をクリックします。  
  
2.  [データセットの選択] ページで、 **[ListDataset]** をクリックします。  
  
3.  **[次へ]** をクリックします。  
  
4.  **[フィールドの配置]** ページで、 **[使用できるフィールド]** から Product フィールドを **[値]** にドラッグします。  
  
5.  SalesDate、Quantity、および Sales についても、手順 4. を実行します。 Product の下に SalesDate を、SalesDate の下に Quantity を、SalesDate の下に Sales を配置します。  
  
6.  **[次へ]** をクリックします。  
  
7.  **[レイアウトの選択]** ページで、テーブルのレイアウトを確認します。  
  
     テーブルはごく単純です。 5 つの列から成り、行グループや列グループは含まれていません。 グループがないため、グループに関連するレイアウト オプションは使用できません。 このチュートリアルでは後ほど、テーブルを手動で更新して合計が表示されるようにします。  
  
8.  **[次へ]** をクリックします。  
  
9. **[スタイルの選択]** ページの **スタイル** ペインで、 **[スレート]** を選択します。  
  
10. **[完了]** をクリックします。  
  
11. テーブルをレッスン 4 で追加したテキスト ボックスの下にドラッグします。  
  
    > [!NOTE]  
    >  テーブルが一覧内に配置されていることを確認してください。  
  
12. テーブルが選択されていることを確認してから、行グループ ペインで詳細を右クリックし、 **[合計の追加]** をポイントして **[後]** をクリックします。  
  
     ![レポート合計の追加](../../2014/tutorials/media/tutorial-addtotal.png "レポート合計の追加")  
  
13. **[実行]** をクリックして、レポートをプレビューします。  
  
 レポートに、売上の詳細情報と合計が入力されたテーブルが表示されます。  
  
 ![レポート内の売上合計](../../2014/tutorials/media/tutorial-reportsalestotals.png "レポート内の Sales totals")  
  
##  <a name="Format"></a> 6.データの書式を設定する  
 数値データの書式を通貨にし、日付の書式を日付と時刻のみに設定します。  
  
#### <a name="to-format-fields-table"></a>フィールド テーブルの書式を設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  `[Sum(SalesSales)]` が格納されているテーブルのセルをクリックし、 **[ホーム]** タブの **[数値]** グループで、 **[通貨]** ボタンをクリックします。  
  
     ![合計売り上げ高を通貨記号を追加](../../2014/tutorials/media/tutorial-sumsales-currencysymbol.png "合計売り上げ高を通貨記号の追加")  
  
3.  `[SalesDate]` が格納されているセルをクリックし、 **[数値]** グループで、ドロップダウン リストから **[日付]** を選択します。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
 レポートには書式が設定されたデータが表示され、読みやすくなりました。  
  
 ![レポート内の売上合計を書式設定](../../2014/tutorials/media/tutorial-reportsalestotals-formatted.png "レポート内の売上合計を書式設定")  
  
##  <a name="Save"></a> 7.レポートを保存する  
 レポートは、レポート サーバー、SharePoint ライブラリ、またはコンピューターに保存することができます。 また、レポートは Word や PDF など各種形式にエクスポートできます。そのためには、レポートを実行し、 **[エクスポート]** メニューから形式を選択します。  
  
 このチュートリアルでは、レポートをレポート サーバーに保存します。 レポート サーバーにアクセスできない場合は、レポートをコンピューターに保存してください。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
     "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  `Name`、既定の名前を**SalesInformationByTerritory**します。  
  
5.  **[保存]** をクリックします。  
  
 レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
#### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  `Name`、既定の名前を**SalesInformationByTerritory**します。  
  
4.  **[保存]** をクリックします。  
  
##  <a name="Line"></a> 8.(省略可) レポートの領域を区切る線を追加する  
 レポートの編集領域と詳細領域を区切る線を追加します。  
  
#### <a name="to-add-a-line"></a>罫線を追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  リボンの **[挿入]** タブの **[レポート アイテム]** で、 **[線]** をクリックします。  
  
3.  レッスン 4 で追加した自由形式のテキスト ボックスの下に線を引きます。  
  
4.  線をクリックします。  
  
5.  **[ホーム]** タブをクリックします。  
  
6.  **[罫線]** の領域で幅を **[4 1/2]** pt に、色を **[赤]** に指定します。  
  
     ![レポートに行を追加](../../2014/tutorials/media/tutorial-reportwithline.png "レポートに行を追加")  
  
##  <a name="Visualization"></a> 9.(省略可) 概要データのビジュアル表現を追加する  
 四角形を利用して、レポートの表示方法を制御できます。 四角形の内側に円グラフや縦棒グラフを配置することで、レポートを思いどおりに表示できます。  
  
#### <a name="to-add-a-rectangle"></a>四角形を追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  リボンの **[挿入]** タブの **[レポート アイテム]** で **[四角形]** をクリックし、一覧内でテーブルの右側に四角形をドラッグします。 四角形のサイズを横 2 インチ、縦 4 インチにします。  
  
3.  四角形とテーブルの上部を揃えます。  
  
#### <a name="to-add-a-pie-chart"></a>円グラフを追加するには  
  
1.  リボンの **[挿入]** タブの **[データの視覚エフェクト]** で **[グラフ]** をクリックし、 **[グラフ ウィザード]** をクリックします。  
  
2.  [データセットの選択] ページで **[ListDataset]** をクリックし、 **[次へ]** をクリックします。  
  
3.  **[円]** をクリックし、 **[次へ]** をクリックします。  
  
4.  [グラフのフィールドの配置] ページで、Product を **[カテゴリ]** にドラッグします。  
  
5.  数量をドラッグして**値**、順にクリックします**次**します。  
  
6.  **[スタイルの選択]** ページの **スタイル** ペインで、 **[スレート]** を選択します。  
  
7.  **[完了]** をクリックします。  
  
8.  レポートの左上隅に表示されているグラフのサイズを変更し、縦 1 1/2 インチ、横 2 インチにします。  
  
9. 四角形の内側にグラフをドラッグします。  
  
     ![円グラフの追加](../../2014/tutorials/media/tutorial-addpiechart.png "円グラフの追加")  
  
10. グラフのタイトルを右クリックし、 **[タイトルのプロパティ]** をクリックします。  
  
11. **グラフのタイトルのプロパティ**ダイアログ ボックスのタイトルのテキストの種類。「**Product Quantities Sold**」と入力します。  
  
12. **[フォント]** タブで、 **[サイズ]** ボックスの一覧の **[10 pt]** をクリックします。  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-column-chart"></a>縦棒グラフを追加するには  
  
1.  リボンの **[挿入]** タブの **[データの視覚エフェクト]** で **[グラフ]** をクリックし、 **[グラフ ウィザード]** をクリックします。  
  
2.  **[データセットの選択]** ページで、 **[ListDataset]** をクリックし、 **[次へ]** をクリックします。  
  
3.  **[列]** をクリックし、 **[次へ]** をクリックします。  
  
4.  グラフのフィールドの配置 ページで、Product フィールドをドラッグして**カテゴリ**します。  
  
5.  Sales を **[値]** にドラッグして、 **[次へ]** をクリックします。  
  
     値は縦軸に表示されます。  
  
6.  **[スタイルの選択]** ページの **スタイル** ペインで、 **[スレート]** を選択します。  
  
7.  **[完了]** をクリックします。  
  
     縦棒グラフがレポートの左上隅に追加されます。  
  
8.  グラフのサイズを横 2 インチ、縦 2 インチに変更します。  
  
9. 四角形の内側で円グラフの下にグラフをドラッグします。  
  
     ![縦棒グラフの追加](../../2014/tutorials/media/tutorial-addcolumnchart.png "縦棒グラフの追加")  
  
10. グラフのタイトルを右クリックし、 **[タイトルのプロパティ]** をクリックします。  
  
11. **グラフのタイトルのプロパティ**ダイアログ ボックスのタイトルのテキストの種類。「**Product Sales**」と入力します。  
  
12. **[フォント]** タブで、 **[サイズ]** ボックスの一覧の **[10pt]** をクリックし、 **[OK]** をクリックします。  
  
13. 縦棒グラフで、縦軸を右クリックし、 **[軸のタイトルの表示]** チェック ボックスをオフにします。  
  
14. 横軸についても、手順 13. 繰り返します。  
  
15. 凡例を右クリックして **[凡例の削除]** をクリックします。  
  
    > [!NOTE]  
    >  軸のタイトルと凡例を削除すると、グラフのサイズが小さい場合に、グラフが見やすくなります。  
  
 ![グラフのタイトルを変更したり軸のタイトルを削除したり](../../2014/tutorials/media/tutorial-columnchart-newtitle-noaxistitle.png "グラフのタイトルを変更して、軸のタイトルの削除")  
  
#### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>四角形の内側にグラフが配置されていることを確認するには  
  
1.  このレッスンの前の手順で追加した四角形をクリックします。  
  
     プロパティ ペインで `Name` プロパティに四角形の名前が表示されます。  
  
     ![四角形の名前](../../2014/tutorials/media/tutorial-rectanglename.png "四角形の名前")  
  
2.  円グラフをクリックします。  
  
3.  **プロパティ**ウィンドウで、いることを確認、`Parent`プロパティに四角形の名前が含まれています。  
  
     ![円グラフのプロパティを親](../../2014/tutorials/media/tutorial-piechart-parentproperty.png "円グラフのプロパティの親")  
  
4.  縦棒グラフをクリックし、手順 2. および 3. を繰り返します。  
  
    > [!NOTE]  
    >  グラフが四角形の内側にない場合、表示レポートでグラフはいっしょに表示されません。  
  
#### <a name="to-make-the-charts-the-same-size"></a>グラフのサイズを揃えるには  
  
1.  円グラフをクリックし、Ctrl キーを押しながら縦棒グラフをクリックします。  
  
2.  両方のグラフが選択されている状態で **[レイアウト]** をポイントし **[同じ幅に揃える]** をクリックします。  
  
     ![グラフの幅を同じ](../../2014/tutorials/media/tutorial-makechartssamewidth.png "同じグラフの幅を行う")  
  
    > [!NOTE]  
    >  最初にクリックしたアイテムの幅が、選択されたすべてのアイテムの幅になります。  
  
3.  **[実行]** をクリックして、レポートをプレビューします。  
  
 レポートに、円グラフと縦棒グラフで概要データが表示されます。  
  
 ![SSRS チュートリアル、自由形式レポート](../../2014/tutorials/media/tutorial-reportfinal.png "SSRS チュートリアル、自由形式のレポート")  
  
## <a name="more-information"></a>詳細情報  
 リストの詳細については、次を参照してください[テーブル、マトリックス、および一覧&#40;レポート ビルダーおよび SSRS&#41;](report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)、[一覧&#40;レポート ビルダーおよび SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)、 [Tablix のデータ。領域部分&#40;レポート ビルダーおよび SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md)、および[Tablix データ領域のセル、行、および列&#40;レポート ビルダー&#41;と SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)します。  
  
 クエリ デザイナーの詳細については、「[クエリ デザイナー (レポート ビルダー)](../../2014/reporting-services/query-designers-report-builder.md)」と「[テキストベースのクエリ デザイナーのユーザー インターフェイス (レポート ビルダー)](report-data/text-based-query-designer-user-interface-report-builder.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [チュートリアル&#40;レポート ビルダー&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 のレポート ビルダー](report-builder/report-builder-in-sql-server-2016.md)  
  
  
