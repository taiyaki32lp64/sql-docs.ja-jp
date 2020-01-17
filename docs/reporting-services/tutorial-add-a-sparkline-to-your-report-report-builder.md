---
title: 'チュートリアル: レポートへのスパークラインの追加 (レポート ビルダー) | Microsoft Docs'
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4dbe5d5afdf507f3edfd68135aa8ee14aee5ae08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043182"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>チュートリアル: レポートへのスパークラインの追加 (レポート ビルダー)

[!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)]のこのチュートリアルでは、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポート内にスパークライン グラフを含む基本的なテーブルを作成します。   
  
スパークラインとデータ バーは、小さい領域で多くの情報を伝達する小さい単純なグラフで、多くの場合、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] レポートで使用されます。 次の図に、ここで作成するレポートと同様のレポートを示します。  
  
![report-builder-sparkline-final](../reporting-services/media/report-builder-sparkline-final.png)  
     
このチュートリアルの推定所要時間: 30 分。  
  
## <a name="requirements"></a>必要条件  
要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。  
  
## <a name="CreateTable"></a>1.テーブルを使用したレポートを作成する  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで、 **[データセットを作成する]**  >  **[次へ]** の順に選択します。 **[データ ソースへの接続の選択]** ページが開きます。  
  
    > [!NOTE]  
    > このチュートリアルでは、特定のデータは必要ありません。SQL Server データベースへの接続だけが必要です。 **[データ ソース接続]** の一覧に既にデータ ソース接続が表示されている場合は、データ ソース接続を選択して手順 10 に進みます。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
5.  **[新規作成]** をクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
6.  **[名前]** に、データ ソースの名前として「 **Product Sales**」と入力します。  
  
7.  **[接続の種類の選択]** で、 **[Microsoft SQL Server]** が選択されていることを確認します。  
  
8.  **[接続文字列]** に次のテキストを入力します。  
  
    `Data Source\=<servername>`  
  
    式 `<servername>`には、たとえば Report001 など、SQL Server データベース エンジンのインスタンスがインストールされているコンピューターを指定します。 レポート データは SQL Server のデータベースから抽出されるのではないので、データベース名を含める必要はありません。 指定したサーバー上の既定のデータベースを使用して、クエリが解析されます。  
  
9. **[資格情報]** をクリックします。 外部データ ソースへのアクセスに必要な資格情報を入力します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    **[データ ソースへの接続の選択]** ページに戻ります。  
  
11. データ ソースに接続できることを確認するために、 **[接続テスト]** をクリックします。  
  
    "接続が正常に作成されました" というメッセージが表示されます。  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. **[次へ]** をクリックします。  
  
## <a name="Query"></a>2.テーブル ウィザードでクエリおよびテーブル レイアウトを作成する  
レポートでは、クエリが事前に定義された共有データセットを使用するか、そのレポートでのみ使用する埋め込みデータセットを作成できます。 このチュートリアルでは、埋め込みデータセットを作成します。  
  
> [!NOTE]  
> このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-query-and-table-layout-in-the-table-wizard"></a>テーブル ウィザードでクエリおよびテーブル レイアウトを作成するには 
  
1.  **[クエリのデザイン]** ページでは、リレーショナル クエリ デザイナーが開きます。 このチュートリアルでは、テキスト ベースのクエリ デザイナーを使用します。  
  
2.  **[テキストとして編集]** をクリックします。 テキスト ベースのクエリ デザイナーは、クエリ ペインと結果ペインで構成されています。  
  
3.  [!INCLUDE[tsql](../includes/tsql-md.md)] [クエリ] **ボックスに、次の** クエリを貼り付けます。  
  
    ```  
    SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  クエリ デザイナーのツール バーで、[実行]\( **!** ) をクリックします。  
  
    **SalesDate**、 **Subcategory**、 **Product**、 **Sales**、および **Quantity**の各フィールドを取得するクエリが実行され、結果セットが表示されます。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[フィールドの配置]** ページで、 **Sales** を **[値]** にドラッグします。  
  
    **Sales** は Sum 関数を使用して集計されます。 値は [Sum(Sales)] です。  
  
7.  **Product** を **[行グループ]** にドラッグします。  
  
8.  **SalesDate** を **[列グループ]** にドラッグします。  

    ![report-builder-sparkline-arrange-fields](../reporting-services/media/report-builder-sparkline-arrange-fields.png)
  
9. **[次へ]** をクリックします。  
  
10. **[レイアウトの選択]** ページの **[オプション]** で、 **[小計と総計を表示]** が選択されていることを確認します。  
  
    ウィザードのプレビュー ペインに、3 行を含むテーブルが表示されます。 レポートを実行すると、各行は次のように表示されます。  
  
    *  1 行目はテーブルで 1 回表示され、列見出しを示します。  
  
    *  2 行目は製品ごとに 1 回表示され、製品名、1 日あたりの合計、および行の合計を示します。  
  
    *  3 行目はテーブルで 1 回表示され、総計を示します。  
    
    ![report-builder-sparkline-choose-layout](../reporting-services/media/report-builder-sparkline-choose-layout.png)
  
11. **[次へ]** をクリックします。  
  
12. **[完了]** をクリックします。  
  
14. テーブルがデザイン画面に追加されます。 テーブルには 3 列および 5 行が含まれています。  
  
    グループ化ペインを確認します。 グループ化ペインが表示されない場合、 **[表示]** メニューの **[グループ化]** をクリックします。 行グループ ペインに行グループ **Product**が表示されます。 列グループ ペインに列グループ **SalesDate**が表示されます。 詳細データは、データセット クエリによって取得されるすべてのデータです。  
    
    ![report-builder-sparkline-grouping-pane](../reporting-services/media/report-builder-sparkline-grouping-pane.png)
  
15. **[実行]** をクリックして、レポートをプレビューします。  

### <a name="FormatCurrency"></a>2a. データに通貨の書式を設定する  
既定では、 **Sales** フィールドの集計データは通常の数値として表示されます。 このフィールドを書式設定して、数値を通貨として表示します。 書式設定したテキスト ボックスおよびプレースホルダー テキストのサンプル値を表示するには、 **[プレースホルダーのスタイル]** の設定を切り替えます。  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  **SalesDate** 列の 2 行目 (列見出しの次の行) のセルをクリックします。 Ctrl キーを押しながら、 `[Sum(Sales)]`を含むすべてのセルを選択します。 

    ![report-builder-select-sum-sales](../reporting-services/media/report-builder-select-sum-sales.png) 
  
3.  **[ホーム]** タブの **[数値]** グループで、 **[通貨]** をクリックします。 書式設定された通貨を表示するようにセルが変化します。  

    ![report-builder-placeholder-currency](../reporting-services/media/report-builder-placeholder-currency.png)
  
    地域設定が英語 (米国) の場合、既定のサンプル テキストは **[$12,345.00]** です。 通貨値の例が表示されない場合は、 **[数値]** グループで、 **[プレースホルダーのスタイル]**  >  **[サンプルの値]** の順にクリックします。  
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)
   
### <a name="FormatDates"></a>2b. (オプション) データに日付の書式を設定する  
既定では、 **SalesDate** フィールドには日付と時刻の情報が表示されます。 このフィールドを書式設定して、日付のみを表示できます。  
  
1.  `[SalesDate]`が格納されたセルをクリックします。  
  
3.  **[ホーム]** タブで、 **[数値]** グループ **[日付]** の順に選択します。  
  
    セルに、日付の例として **[2000/1/31]** と表示されます。
     
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
**SalesDate** の値は既定の日付形式で表示され、 **Sales** の集計値は通貨の形式で表示されます。   
  
## <a name="Sparkline"></a>3.スパークラインを追加する    
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  テーブルの合計列を選択します。  
  
3.  右クリックして表示される **[列の挿入]** を選択してから、 **[左]** をクリックします。  

    ![report-builder-add-column-left](../reporting-services/media/report-builder-add-column-left.png)
  
4.  新しい列の `[Product]` 行のセルを右クリックし、 **[挿入]**  >  **[スパークライン]** の順にクリックします。  

    ![report-builder-insert-sparkline](../reporting-services/media/report-builder-insert-sparkline.png)
  
5.  **[スパークラインの種類を選択]** で、 **[列]** 行の最初のスパークラインが選択されていることを確認してから、 **[OK]** をクリックします。  
  
6.  スパークラインをクリックして、グラフ データ ペインを表示します。  
  
7.  [値] ボックスのプラス記号 (+) をクリックしてから、 **Sales**をクリックします。 

    ![report-builder-sparkline-values](../reporting-services/media/report-builder-sparkline-values.png) 
  
    **Sales** フィールドの値がスパークラインの値になります。  
  
8.  [カテゴリ グループ] ボックスのプラス記号 (+) をクリックしてから、 **SalesDate**をクリックします。  
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
    スパークライン グラフ内のバーが揃っていないことに注目してください。 データの 2 行目のバーは 4 本しかないので、バーが 6 本ある最初の行のバーよりも太くなっています。 1 日あたりの各製品の値を比較できません。 整列する必要があります。  
  
    また、どの行も、最も高いバーが行の高さになっています。 各行の最大値は同じではないので、誤解を招きます。たとえば、Budget Movie-Maker の最大の値は 10,400 ドルですが、Slim Digital の最大の値は 26,576 ドルで 2 倍以上あります。 ところが、これらの 2 つの行の最も高いバーはほぼ同じ高さになっています。 すべてのスパークラインで、同じスケールを使用する必要があります。  
  
     ![report-builder-sparkline-misaligned](../reporting-services/media/report-builder-sparkline-misaligned.png)
  
## <a name="AlignSparklines"></a>4.スパークラインを垂直方向および水平方向に揃える  
スパークラインは、測定方法が異なると、読み取りにくくなります。 各スパークラインの縦軸と横軸は、残りのスパークラインと一致させる必要があります。  
   
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  スパークラインを右クリックし、 **[縦軸のプロパティ]** をクリックします。  
  
3.  **[軸を整列する]** チェック ボックスをオンにします。 Tablix1 は、リスト内の唯一のオプションです。  
  
     このオプションによって、各スパークラインのバーの高さが相対的に設定されます。 
  
4.  **[OK]** をクリックします。  
  
5.  スパークラインを右クリックし、 **[横軸のプロパティ]** をクリックします。  
  
6.  **[軸を整列する]** チェック ボックスをオンにします。 Tablix1 は、リスト内の唯一のオプションです。 
  
    このオプションによって、各スパークラインのバーの幅が相対的に設定されます。 あるスパークラインで他のスパークラインよりバーの数が少ない場合は、そのスパークラインのデータがない位置は空白のスペースになります。  
  
7.  **[OK]** をクリックします。  
  
8.  **[実行]** をクリックして、レポートをもう一度プレビューします。  
  
これで、各スパークライン内のすべてのバーが、他のスパークライン内のバーと揃えられ、高さが相関的になりました。  
  
![report-builder-sparkline-aligned](../reporting-services/media/report-builder-sparkline-aligned.png)
  
## <a name="Width"></a>7.(オプション) 列幅を変更する  
テーブルの各セルには、既定でテキスト ボックスが含まれます。 テキスト ボックスは、ページを表示するときにテキストに合わせて垂直方向に拡張されます。 表示されるレポートでは、各行がその行で最も高いテキスト ボックスの高さに拡張されます。 デザイン画面の行の高さは、表示されるレポートの行の高さには影響しません。  
  
各行の垂直方向の領域を小さくするには、列の幅を広げ、列で想定されるテキスト ボックスの内容が 1 行に収まるようにします。  
  
### <a name="to-change-the-width-of-columns"></a>列の幅を変更するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  テーブルをクリックし、灰色のバーをテーブルの上部および横に表示します。 これらは、列および行のハンドルです。
  
3.  列ハンドルの間の罫線をポイントします。カーソルが 2 方向の矢印の形状に変化します。 たとえば、製品名が 1 行に表示されるように **Product** 列をドラッグします。  
  
4.  **[実行]** をクリックし、レポートをプレビューして、列の幅が十分に広くなったかどうかを確認します。  
  
## <a name="Title"></a>8.(オプション) レポート タイトルを追加する  
レポート タイトルは、レポートの最上部に表示されます。 レポート ヘッダーがあれば、そこにレポート タイトルを配置します。レポート ヘッダーを使用しない場合は、レポート本文の一番上のテキスト ボックスに配置します。 このチュートリアルでは、自動的にレポート本文の一番上に配置されるテキスト ボックスを使用します。  
  
テキストの語句や文字のフォントのスタイル、サイズ、および色を変更して、テキストをさらに強調することもできます。 詳細については、「[テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Sales by Date**」と入力し、テキスト ボックスの外側をクリックします。  
  
3.  **Product Sales**を含むテキスト ボックスを選択します。  
  
4.  [ホーム] タブで、 **[フォント]** グループ、 **[色]** の順に進み、 **[青緑]** を選択します。  
  
7.  **[太字]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>9.レポートを保存する  
レポートをレポート サーバーまたは自分のコンピューターに保存します。 レポート サーバーに保存しない場合は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のいくつかの機能 (レポート パーツ、サブレポートなど) が使用できなくなります。  
  
### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に入力されている既定の名前を「 **Product Sales**」に置き換えます。  
  
5.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **[名前]** に入力されている既定の名前を「 **Product Sales**」に置き換えます。  
  
4.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  

これで、スパークライン グラフを使ったテーブル レポートを作成するチュートリアルを終了します。 スパークラインの詳細については、「[スパークラインとデータ バー](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)」を参照してください。  
  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md) 
[SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
