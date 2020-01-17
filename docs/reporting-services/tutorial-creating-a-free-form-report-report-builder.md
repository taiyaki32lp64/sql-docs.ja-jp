---
title: 'チュートリアル: 自由形式のレポートの作成 (レポート ビルダー) | Microsoft Docs'
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 567abd4423f546f853abea4caa5c944ce9d8ccdb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66499565"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>チュートリアル: 自由形式のレポートの作成 (レポート ビルダー)
このチュートリアルでは、ニュースレターとして機能する、ページ分割されたレポートを作成します。 各ページには、固定テキスト、概要ビジュアル、詳細サンプル セールス データが表示されます。

![report-builder-free-form-report-complete](../reporting-services/media/report-builder-free-form-report-complete.png)

このレポートでは、販売区域ごとに情報をまとめて、各区域の販売責任者の名前と売上情報の概要を表示します。 自由形式レポートでは、まず、基盤として一覧データ領域から開始し、画像を使用した装飾用のパネル、データが挿入された固定テキスト、詳細情報を表示するテーブルを追加し、必要に応じて、概要情報を表示する円グラフと縦棒グラフを追加します。  
  
このチュートリアルの推定所要時間 : 20 分  
  
## <a name="requirements"></a>必要条件  
要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。  
  
## <a name="BlankReport"></a>1.空のレポート、データ ソース、およびデータセットを作成する  
  
> [!NOTE]  
> このチュートリアルでは、外部のデータ ソースが必要ないようにクエリにデータ値が含まれています。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-blank-report"></a>空のレポートを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。 
 
3.  右ペインで、 **[空のレポート]** をクリックします。  
  
### <a name="to-create-a-new-data-source"></a>新しいデータ ソースを作成するには  
  
1.  レポート データ ペインで、 **[新規作成]**  >  **[データ ソース]** をクリックします。  
  
2.  **[名前]** ボックスに「 **ListDataSource**」と入力します。  
  
3.  **[レポートに埋め込まれた接続を使用する]** をクリックします。  
  
4.  接続の種類が Microsoft SQL Server であることを確認したら、 **[接続文字列]** ボックスに「**Data Source = \<servername>** 」と入力します。  
  
    **\<servername>** には、たとえば Report001 など、SQL Server データベース エンジンのインスタンスがインストールされているコンピューターを指定します。 このレポートのデータは SQL Server のデータベースから抽出されるのではないので、データベース名を含める必要はありません。 指定したサーバー上の既定のデータベースを使用し、クエリが解析されます。  
  
5.  **[資格情報]** をクリックし、SQL Server データベース エンジンのインスタンスとの接続に必要な資格情報を入力します。  
  
6.  **[OK]** をクリックします。  
  
### <a name="to-create-a-new-dataset"></a>新しいデータセットを作成するには  
  
1.  レポート データ ペインで、 **[新規作成]**  >  **[データセット]** をクリックします。  
  
2.  **[名前]** ボックスに「 **ListDataset**」と入力します。  
  
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
  
7.  **[実行]** アイコン (!) をクリックしてクエリを実行します。  
  
    クエリの結果が、レポートに表示できるデータになります。  
  
    ![report-builder-free-form-tutorial-data](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="List"></a>2.一覧を追加および構成する  
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、一覧データ領域は自由形式レポートを作成するのに最適です。 表やマトリックスと同様に、これは *tablix* データ領域に基づきます。 詳細については、「 [一覧がある請求書とフォームを作成する](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)」を参照してください。  
  
ニュースレターのように書式設定されたレポートで販売区域ごとの売上情報を表示するには、一覧を使用します。 情報は、区域ごとにグループ化されます。 区域ごとのデータをグループ化する新しい行グループを追加し、組み込みの詳細行グループを削除します。  
  
### <a name="to-add-a-list"></a>一覧を追加するには  
  
1.  **[挿入]** タブで、 **[データ領域]**  >  **[一覧]** の順に選択します。 

2. レポート本文 (タイトル領域とフッター領域の間) をクリックし、ドラッグしてリスト ボックスを作成します。 リスト ボックスの高さを 7 インチ、幅を 6.25 インチにします。 正確なサイズを得るには、 **[プロパティ]** ペインの **[位置]** で、 **[幅]** プロパティと **[高さ]** プロパティに値を入力します。
  
    > [!NOTE]  
    > このレポートでは、用紙サイズを Letter (8.5 X11) にし、余白を 1 インチとします。 縦が 9 インチより大きいか、横が 6.5 インチよりも大きいリスト ボックスでは、空のページが生成される可能性があります。  
  
2.  リスト ボックス内をクリックし、一覧の一番上にあるバーを右クリックし、 **[Tablix のプロパティ]** をクリックします。  
  
    ![report-builder-free-form-tablix-properties](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  **[データセット名]** ドロップダウン リストの **[ListDataset]** を選択します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  一覧内を右クリックし、 **[四角形のプロパティ]** をクリックします。  
  
6.  **[全般]** タブで **[後に改ページを追加する]** チェック ボックスをオンにします。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>新しい行グループを追加し、詳細グループを削除するには  
  
1.  行グループ ペインで、詳細グループを右クリックし、 **[グループの追加]** をポイントして **[親グループ]** をクリックします。  
  
    ![report-builder-free-form-add-parent-group](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  **[グループ化]** 一覧で、次を選択します。 `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    セル `[Territory]` を含む列が一覧に追加されます。
  
4.  一覧の Territory 列を右クリックし、 **[列の削除]** をクリックします。  
  
    ![report-builder-free-form-delete-columns](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  **[列のみの削除]** を選択します。  
  
6.  行グループ ペインで、 **[詳細]** グループを右クリックし、 **[グループの削除]** をクリックします。  
   
7.  **[グループのみを削除]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Graphics"></a>3.グラフィック要素を追加する  
一覧データ領域の利点の 1 つは、表形式のレイアウトに制限されずに、四角形やテキスト ボックスなどのレポート アイテムをどこにでも追加できることです。 ここでは、グラフィック (任意の色で塗りつぶされた四角形) を追加して、レポートの体裁を整えます。  
  
### <a name="to-add-graphic-elements-to-the-report"></a>レポートにグラフィック要素を追加するには  
  
1.  **[挿入]** タブで **[四角形]** を選択します。 

2. 一覧の左上隅をクリックし、ドラッグして高さ 7 インチ、幅 3.5 インチの四角形を作成します。 ここでも、正確なサイズを得るには、 **[プロパティ]** ペインの **[位置]** で、 **[幅]** と **[高さ]** に値を入力します。
  
2.  四角形を右クリックし、 **[四角形のプロパティ]** をクリックします。  
  
3.  **[塗りつぶし]** タブをクリックします。  
  
4.  **[塗りつぶしの色]** で **[淡い灰色]** を選択します。  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
次の画像のように、レポートの左側に、淡い灰色の四角形からなる縦長のグラフィックが追加されています。  
  
![report-builder-free-form-gray-rectangle](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="Text"></a>4.自由形式テキストを追加する  
テキスト ボックスを追加し、各レポート ページに繰り返し表示される固定テキストとデータ フィールドを表示できます。  
  
### <a name="to-add-text-to-the-report"></a>テキストをレポートに追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **[挿入]** タブの **[テキスト ボックス]** をクリックします。 先に追加した四角形の内側で、一覧の左上隅をクリックし、ドラッグして幅が約 3.45 インチ、高さが約 5 インチのテキスト ボックスを作成します。  
  
3.  テキスト ボックスにカーソルを合わせ、「 **Newsletter for** 」と入力します。 "for" という単語の後にスペースを入れ、次の手順で追加するフィールドとテキストを分離します。   
  
    ![ニュースレターの見出しテキストの追加](../reporting-services/media/tutorial-newsletterfor.png "ニュースレターの見出しテキストの追加")  
  
4.  [レポート データ] ペインの ListDataSet からテキスト ボックスに `[Territory]` フィールドをドラッグし、"Newsletter for " の後に置きます。  
  
    ![report-builder-free-form-territory-field](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  テキストと `[Territory]` フィールドを選択します。  
  
6.  **[ホーム]** タブで **[フォント]** を選択し、次を選択します。 
  
    *  **Segoe Semibold**
    *  **20 pt**
    *  **トマト**  
  
9. 手順 3 で入力したテキストの下にカーソルを置き、「 **Hello** 」と入力します。「Hello」の後にスペースを入力し、次の手順で追加するフィールドとテキストを分離します。  
 
10. [レポート データ] ペインの ListDataSet からテキスト ボックスに `[FullName]` フィールドをドラッグし、"Hello " の後に置きます。それからコンマ (,) を入力します。  
   
11. 前の手順で追加したテキストを選択します。
  
12. **[ホーム]** タブで **[フォント]** を選択し、次を選択します。 
  
    *  **Segoe Semibold**
    *  **16 pt**
    *  **黒**  
   
15. 手順 9. ～ 13. で追加したテキストの下にカーソルを置き、次の意味のないテキストをコピーして貼り付けます。  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. 追加したテキストを選択します。  
  
17.  **[ホーム]** タブで **[フォント]** を選択し、次を選択します。 
  
      *  **Segoe UI**
      *  **10 pt**
      *  **黒**  
 
20. テキスト ボックスの中にカーソルを置き、意味のないテキストの下に「 **Congratulations on your total sales of**」と入力します。この文章の後にスペースを入力し、次の手順で追加するフィールドとテキストを分離します。 
  
21. Sales フィールドをテキスト ボックスにドラッグし、前の手順で入力したテキストの後に配置し、感嘆符 (!) を入力します。  

25. テキストとたった今追加したフィールドを選択します。  
  
17.  **[ホーム]** タブで **[フォント]** を選択し、次を選択します。 
  
      *  **Segoe Semibold**
      *  **16 pt**
      *  **黒**  
  
22. `[Sales]` フィールドだけを選択し、右クリックし、 **[式]** をクリックします。  
  
23. **[式]** ボックスの式を変更し、次のように Sum 関数を指定します。  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![report-builder-free-form-text-box](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. `[Sum(Sales)]` を選択したまま、 **[ホーム]** タブで **[数値]** グループ、 **[通貨]** の順に選択します。  
  
30. "クリックしてタイトルを追加" というテキストが含まれているテキスト ボックスを右クリックし、 **[削除]** をクリックします。  
  
31. リスト ボックスを選択します。 2 つの両方向矢印を選択し、ページの上部に移動します。  

    ![report-builder-drag-list](../reporting-services/media/report-builder-drag-list.png)
  
32. **[実行]** をクリックして、レポートをプレビューします。  
  
レポートに静的テキストが表示され、各レポート ページには特定の販売区域についてのデータが含まれています。 売上には通貨の書式が適用されます。  
  
![report-builder-newsletter-page-preview](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="Table"></a>5.売上の詳細情報を表示するテーブルを追加する  
テーブルまたはマトリックスの新規作成ウィザードを使用して、自由形式レポートにテーブルを追加します。 ウィザードの完了後、合計を表示する行を手動で追加します。  
  
### <a name="to-add-a-table"></a>テーブルを追加するには  
  
1.  **[挿入]** タブで、 **[データ領域]** 領域を選択し、 **[テーブル]**  >  **[テーブル ウィザード]** を選択します。  
  
2.  **[データセットの選択]** ページで、 **[ListDataset]**  >  **[次へ]** をクリックします。  
  
4.  **[フィールドの配置]** ページで、 **[使用できるフィールド]** から Product フィールドを **[値]** にドラッグします。  
  
5.  SalesDate、Quantity、Sales にも手順 3 を実行します。 Product の下に SalesDate を、SalesDate の下に Quantity を、SalesDate の下に Sales を配置します。  
  
6.  **[次へ]** をクリックします。  
  
7.  **[レイアウトの選択]** ページで、テーブルのレイアウトを確認します。  
  
    テーブルは単純で、5 列、行なし、列グループなしです。 グループがないため、グループに関連するレイアウト オプションは使用できません。 このチュートリアルでは後ほど、テーブルを手動で更新して合計が表示されるようにします。  
  
8.  **[次へ]** をクリックします。  
  
9. **[完了]** をクリックします。  
  
11. テーブルをレッスン 4 で追加したテキスト ボックスの下にドラッグします。  
  
    > [!NOTE]  
    > テーブルがリスト ボックスの内側、かつ、灰色の四角形の内側に入っているようにします。  
  
12. テーブルが選択されている状態で、 **[行グループ]** ペインで **[詳細]**  >  **[合計の追加]**  >  **[後]** をクリックします。  
  
    ![report-builder-free-form-table-totals](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. Product 列のセルを選択し、「 **Total**」と入力します。

    ![report-builder-free-form-type-total](../reporting-services/media/report-builder-free-form-type-total.png)

12. [SalesDate] フィールドを選択します。 **[ホーム]** タブで **[数値]** を選択し、 **[既定]** を **[日付]** に変更します。

13. [Sum(Sales)] フィールドを選択します。 **[ホーム]** タブで **[数値]** を選択し、 **[既定]** を **[通貨]** に変更します。

**[実行]** をクリックして、レポートをプレビューします。  
  
レポートに、売上の詳細情報と合計が入力されたテーブルが表示されます。  
  
![report-builder-free-form-with-table](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="Save"></a>6.レポートを保存する  
レポートは、レポート サーバー、SharePoint ライブラリ、またはコンピューターに保存することができます。  
  
このチュートリアルでは、レポートをレポート サーバーに保存します。 レポート サーバーにアクセスできない場合は、レポートをコンピューターに保存してください。  
  
### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に表示されている既定の名前を「 **SalesInformationByTerritory**」に変更します。  
  
5.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **[名前]** に表示されている既定の名前を「 **SalesInformationByTerritory**」に変更します。  
  
4.  **[保存]** をクリックします。  
  
## <a name="Line"></a>7.(省略可) レポートの領域を区切る線を追加する  
レポートの編集領域と詳細領域を区切る線を追加します。  
  
### <a name="to-add-a-line"></a>罫線を追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **[挿入]** タブで **[レポート アイテム]**  >  **[線]** を選択します。  
  
3.  レッスン 4 で追加したテキスト ボックスの下に線を引きます。  
  
4.  線をクリックし、 **[ホーム]** タブの **[罫線]** で次のように選択します。
     * **[幅]** に **[3]** pt を選択します。
     * **[色]** に **[トマト]** を選択します。  
  
## <a name="Visualization"></a>8.(省略可) 概要データのビジュアル表現を追加する  
四角形を利用して、レポートの表示方法を制御できます。 四角形の内側に円グラフや縦棒グラフを配置することで、レポートを思いどおりに表示できます。  
  
### <a name="to-add-a-rectangle"></a>四角形を追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **[挿入]** タブで **[レポート アイテム]**  >   **[四角形]** を選択します。 リスト ボックスの内側にある四角形をテーブルの右にドラッグし、幅が約 2.25 インチ、高さが約 7.9 インチの四角形を作成します。  
  
3.  しい四角形が選択されている状態で、[プロパティ] ペインで、 **BorderColor LightGrey**、 **BorderStyle Solid**、 **BorderWidth 2 pt**に設定します。 

4. 四角形とテーブルの上部を揃えます。  
  
## <a name="to-add-a-pie-chart"></a>円グラフを追加するには  
  
1.  **[挿入]** タブで、 **[データ ビジュアライゼーション]**  >  **[グラフ]**  >  **[グラフ ウィザード]** を選択します。  
  
2.  **[データセットの選択]** ページで、 **[ListDataset]**  >  **[次へ]** をクリックします。  
  
3.  **[円]**  >  **[次へ]** をクリックします。  
  
4.  [グラフのフィールドの配置] ページで、Product を **[カテゴリ]** にドラッグします。  
  
5.  Quantity を **[値]** にドラッグし、 **[次へ]** をクリックします。  
  
6.  **[完了]** をクリックします。  
  
8.  レポートの左上隅に表示されているグラフのサイズを変更し、幅を約 2.25 インチ、高さを約 3.6 インチにします。  
  
9. 四角形の内側にグラフをドラッグします。  
   
10. グラフ タイトルを選択し、「 **Product Quantities Sold**」と入力します。  
  
12. **[ホーム]** タブで **[フォント]** を選択し、タイトルを次のように設定します。
    * **[フォント]** **Segoe UI Semibold**」を参照してください。
    * **サイズ** **12 pt**」を参照してください。
    * **[色]** **黒**」を参照してください。  

13. 凡例を右クリックし、 **[凡例のプロパティ]** をクリックします。

14. **[全般]** タブの **[凡例の位置]** で、一番下の中丸を選択します。 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. 必要に応じて、ドラッグしてグラフ領域を大きくします。

     ![report-builder-free-form-pie](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>縦棒グラフを追加するには  
  
1.  **[挿入]** タブで、 **[データ ビジュアライゼーション]**  >  **[グラフ]**  >  **[グラフ ウィザード]** を選択します。  
  
2.  **[データセットの選択]** ページで、 **[ListDataset]** をクリックし、 **[次へ]** をクリックします。  
  
3.  **[列]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[グラフのフィールドの配置]** ページで、Product フィールドを **[カテゴリ]** にドラッグします。  
  
5.  Sales を **[値]** にドラッグして、 **[次へ]** をクリックします。  
  
    値は縦軸に表示されます。  
  
6.  **[完了]** をクリックします。  
  
    縦棒グラフがレポートの左上隅に追加されます。  
  
8.  グラフのサイズを変更し、幅を約 2.25 インチに、高さを約 4 インチにします。  
  
9. 四角形の内側で円グラフの下にグラフをドラッグします。  
   
10. グラフ タイトルを選択し、「 **Product Sales**」と入力します。  
  
12. **[ホーム]** タブで **[フォント]** を選択し、タイトルを次のように設定します。
    * **[フォント]** **Segoe UI Semibold**」を参照してください。
    * **サイズ** **12 pt**」を参照してください。
    * **[色]** **黒**」を参照してください。  
  
15. 凡例を右クリックして **[凡例の削除]** をクリックします。  
  
    > [!NOTE]  
    > 凡例を削除すると、小さいグラフが読みやすくなります。  
  
    ![report-builder-free-form-column](../reporting-services/media/report-builder-free-form-column.png)

12. グラフ軸を選択し、 **[ホーム]** タブで **[数値]** 、 **[通貨]** の順に選択します。

13. **[小数点表示桁下げ]** を 2 回選択します。数値にドルだけ表示され、セントは表示されません。      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>四角形の内側にグラフが配置されていることを確認するには  

レポート ページの他のアイテムのコンテナーとして四角形を利用できます。 コンテナーとして四角形を利用する方法の詳細は [ここ](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)で確認できます。
  
1.  このレッスンで作成し、グラフを追加した四角形を選択します。  
  
    プロパティ ペインで **Name** プロパティに四角形の名前が表示されます。  
  
    ![report-builder-free-form-rectangle-name](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  円グラフをクリックします。  
  
3.  **[プロパティ]** ペインで、 **Parent** プロパティに四角形の名前が表示されていることを確認します。  
  
     ![report-builder-free-form-pie-parent](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  縦棒グラフをクリックし、手順 3 を繰り返します。  
  
    > [!NOTE]  
    > グラフが四角形の内側にない場合、表示レポートでグラフはいっしょに表示されません。  
  
### <a name="to-make-the-charts-the-same-size"></a>グラフのサイズを揃えるには  
  
1.  円グラフを選択し、Ctrl キーを押しながら縦棒グラフを選択します。  
  
2.  両方のグラフを選択した状態で、 **[レイアウト]**  >  **[同じ幅に揃える]** をクリックします。  
  
    > [!NOTE]  
    > 最初にクリックしたアイテムの幅が、選択されたすべてのアイテムの幅になります。  
  
3.  **[実行]** をクリックして、レポートをプレビューします。  
  
レポートに、円グラフと縦棒グラフで概要データが表示されます。  
  

  
## <a name="next-steps"></a>Next Steps  
これで、自由形式のレポートを作成する方法のチュートリアルは終了です。  
  
一覧の詳細については、次を参照してください。 
* [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [一覧がある請求書とフォームを作成する](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [Tablix データ領域のセル、行、および列 (レポート ビルダーおよび SSRS)](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
クエリ デザイナーの詳細については、「[クエリ デザイン ツール (SSRS)](report-data/query-design-tools-ssrs.md)」と「[テキストベースのクエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md) 
  

