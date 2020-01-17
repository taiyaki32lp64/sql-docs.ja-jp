---
title: チュートリアル:レポートへのスパークラインの追加 (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a543182d5c367be9cc1be875f05c1ab5d4c9bfcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099042"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>チュートリアル:レポートへのスパークラインの追加 (レポート ビルダー)
  このチュートリアルでは、サンプルの売上データに基づいて基本的なテーブル レポートを作成してから、テーブルのセルにスパークライン グラフを追加します。  
  
 このチュートリアルで作成するレポートについては、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] レポート ビルダーのサンプル レポートに発展版が含まれています。 このサンプル レポートおよびその他のダウンロードの詳細については、次を参照してください。[レポート ビルダーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=184851)します。 次の図に、ここで作成するレポートと同様のサンプル レポートを示します。  
  
 ![rs_SparklineMatrixTutorial](../../2014/tutorials/media/rs-sparklinematrixtutorial.gif "rs_SparklineMatrixTutorial")  
  
 ビデオ[方法。スパーク ラインをテーブル (レポート ビルダー ビデオ) で作成](https://technet.microsoft.com/bi/ff871942.aspx)スパーク ラインと同様のレポートを作成する方法を示しています。  
  
##  <a name="BackToTop"></a> 学習内容  
 このチュートリアルでは、次の方法を学習します。  
  
 1. [レポート テーブルを作成します。](#CreateTable)  
  
 2. [テーブルまたはマトリックス ウィザードでクエリを作成します。](#Query)  
  
 3. [テーブルにスパーク ラインを追加します。](#Sparkline)  
  
 4. [スパーク ラインを垂直方向および水平方向に揃える](#AlignSparklines)  
  
### <a name="other-optional-steps"></a>その他のオプションの手順  
 5. [データに通貨の形式](#FormatCurrency)  
  
 6. [データに日付の書式](#FormatDates)  
  
 7. [列幅を変更します。](#Width)  
  
 8. [レポート タイトルを追加します。](#Title)  
  
 9. [レポートを保存します。](#Save)  
  
 このチュートリアルの推定所要時間:30 分。  
  
## <a name="requirements"></a>必要条件  
 要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/report-builder-tutorials.md)」を参照してください。  
  
##  <a name="CreateTable"></a> 1.テーブルを使用したレポートを作成する  
  
#### <a name="to-create-a-report"></a>レポートを作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[プログラム]** 、 **[Microsoft SQL Server 2012 レポート ビルダー]** の順にポイントして、 **[レポート ビルダー]** をクリックします。  
  
     **Getting Started**  ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  場合、 **Getting Started** ] ダイアログ ボックスが表示されないから、**レポート ビルダー**ボタン、[**新規**します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで **[データセットを作成する]** を選択し、 **[次へ]** をクリックします。 **[データ ソースへの接続の選択]** ページが開きます。  
  
    > [!NOTE]  
    >  このチュートリアルでは、特定のデータは必要ありません。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] データベースへの接続だけが必要です。 **[データ ソース接続]** の一覧に既にデータ ソース接続が表示されている場合は、データ ソース接続を選択して手順 10 に進みます。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
5.  **[新規作成]** をクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
6.  **[名前]** に、データ ソースの名前として「 **Product Sales**」と入力します。  
  
7.  **[接続の種類の選択]** で、 **[Microsoft SQL Server]** が選択されていることを確認します。  
  
8.  **[接続文字列]** に次のテキストを入力します。  
  
     **データ ソース =\<servername >**  
  
     式\<servername >、たとえば report001 など、SQL Server データベース エンジンのインスタンスがインストールされているコンピューターを指定します。 レポート データは SQL Server のデータベースから抽出されるのではないので、データベース名を含める必要はありません。 指定したサーバー上の既定のデータベースを使用して、クエリが解析されます。  
  
9. **[資格情報]** をクリックします。 外部データ ソースへのアクセスに必要な資格情報を入力します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     **[データ ソースへの接続の選択]** ページに戻ります。  
  
11. データ ソースに接続できることを確認するために、 **[接続テスト]** をクリックします。  
  
     "接続が正常に作成されました" というメッセージが表示されます。  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. **[次へ]** をクリックします。  
  
##  <a name="Query"></a> 2.テーブル ウィザードでクエリを作成する  
 レポートでは、クエリが事前に定義された共有データセットを使用するか、そのレポートでのみ使用する埋め込みデータセットを作成できます。 このチュートリアルでは、埋め込みデータセットを作成します。  
  
> [!NOTE]  
>  このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
#### <a name="to-create-a-query"></a>クエリを作成するには  
  
1.  **[クエリのデザイン]** ページでは、リレーショナル クエリ デザイナーが開きます。 このチュートリアルでは、テキスト ベースのクエリ デザイナーを使用します。  
  
2.  **[テキストとして編集]** をクリックします。 テキスト ベースのクエリ デザイナーは、クエリ ペインと結果ペインで構成されています。  
  
3.  [!INCLUDE[tsql](../includes/tsql-md.md)] [クエリ] **ボックスに、次の** クエリを貼り付けます。  
  
    ```  
    SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2010-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  クエリ デザイナーのツール バーで、[実行]\( **!** ) をクリックします。  
  
     **SalesDate**、 **Subcategory**、 **Product**、 **Sales**、および **Quantity**の各フィールドを取得するクエリが実行され、結果セットが表示されます。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[フィールドの配置]** ページで、 **Sales** を **[値]** にドラッグします。  
  
     **Sales** は Sum 関数を使用して集計されます。 値は [Sum(Sales)] です。  
  
7.  **Product** を **[行グループ]** にドラッグします。  
  
8.  **SalesDate** を **[列グループ]** にドラッグします。  
  
9. **[次へ]** をクリックします。  
  
10. **[レイアウトの選択]** ページの **[オプション]** で、 **[小計と総計を表示]** が選択されていることを確認します。  
  
     ウィザードのプレビュー ペインに、3 行を含むテーブルが表示されます。 レポートを実行すると、各行は次のように表示されます。  
  
    1.  1 行目はテーブルで 1 回表示され、列見出しを示します。  
  
    2.  2 行目は製品ごとに 1 回表示され、製品名、1 日あたりの合計、および行の合計を示します。  
  
    3.  3 行目はテーブルで 1 回表示され、総計を示します。  
  
11. **[次へ]** をクリックします。  
  
12. **[スタイルの選択]** ページの **スタイル** ペインで、 **[スレート]** を選択します。  
  
     プレビュー ペインにそのスタイルのテーブルのサンプルが表示されます。  
  
13. **[完了]** をクリックします。  
  
14. テーブルがデザイン画面に追加されます。 テーブルには 3 列および 5 行が含まれています。  
  
     グループ化ペインを確認します。 グループ化ペインが表示されない場合、 **[表示]** メニューの **[グループ化]** をクリックします。 行グループ ペインには 1 つの行グループ**Product** が表示されます。 列グループ ペインには 1 つ列グループ**SalesDate** が表示されます。 詳細データは、データセット クエリによって取得されるすべてのデータです。  
  
15. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Sparkline"></a> 3.スパークラインを追加する  
  
#### <a name="to-add-a-sparkline-chart-to-a-table"></a>テーブルにスパークライン グラフを追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  テーブルの合計列を選択します。  
  
3.  右クリックして表示される **[列の挿入]** を選択してから、 **[左]** をクリックします。  
  
4.  新しい列で、[Product] 行で右クリックして、**挿入**リボン タブをクリックして**スパーク ライン**します。  
  
5.  最初のスパーク ラインの確認、**列**行が選択されているし、順にクリックします**OK**します。  
  
6.  スパークラインをクリックして、グラフ データ ペインを表示します。  
  
7.  プラス記号をクリックします (+) は、[値] ボックスにサインインし、をクリックし、 **Sales**します。  
  
     **Sales** フィールドの値がスパークラインの値になります。  
  
8.  プラス記号をクリックします (+) は、カテゴリ グループ ボックスにサインインし、をクリックし、 **SalesDate**します。  
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
     テーブルの各行にスパークライン グラフがありますが、正しくないことに注意してください。 グラフ内のバーが揃っていません。 データの 2 行目のバーは 4 本しかないので、バーが 6 本ある最初の行のバーよりも太くなっています。 1 日あたりの各製品の値を比較できません。 グラフ内のバーは揃っている必要があります。  
  
     また、どの行も、最も高いバーの高さがその行の高さに合わせられています。 これは、誤解を行ごとの最大値が等しくないためです。 予算ムービー メーカーの最大値は $10,400、が、Slim Digital の最大値は 26,576 ドルより 2 倍よりもします。 ところが、これらの 2 つの行の最も高いバーはほぼ同じ高さになっています。 こちらも他のスパークラインに合わせて修正する必要があります。  
  
     ![rs_SprklineMtrxUnaligndBars](../../2014/tutorials/media/rs-sprklinemtrxunaligndbars.gif "rs_SprklineMtrxUnaligndBars")  
  
##  <a name="AlignSparklines"></a> 4.スパークラインを垂直方向および水平方向に揃える  
 スパーク ラインでは、すべてを使用していない測定方法が異なると、読み取り困難です。 各スパークラインの縦軸と横軸は、残りのスパークラインと一致させる必要があります。  
  
#### <a name="to-set-alignment-for-the-sparklines-in-the-table"></a>テーブル内のスパークラインの配置を設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  スパークラインを右クリックし、 **[縦軸のプロパティ]** をクリックします。  
  
3.  **[軸を整列する]** チェック ボックスをオンにします。  
  
     一覧に Tablix1 が表示されます。 これが唯一のオプションです。 このオプションによって、各スパークラインのバーの高さが相対的に設定されます。  
  
4.  **[OK]** をクリックします。  
  
5.  スパークラインを右クリックし、 **[横軸のプロパティ]** をクリックします。  
  
6.  **[軸を整列する]** チェック ボックスをオンにします。  
  
     一覧に Tablix1 が表示されます。 これが唯一のオプションです。 このオプションによって、各スパークラインのバーの幅が相対的に設定されます。 あるスパークラインで他のスパークラインよりバーの数が少ない場合は、そのスパークラインのデータがない位置は空白のスペースになります。  
  
7.  **[OK]** をクリックします。  
  
8.  **[実行]** をクリックして、レポートをもう一度プレビューします。  
  
 今度は、すべてのバーが他の行のバーと揃っています。  
  
##  <a name="FormatCurrency"></a> 5.(オプション) データに通貨の書式を設定する  
 既定では、 **Sales** フィールドの集計データは通常の数値として表示されます。 このフィールドを書式設定して、数値を通貨として表示します。 書式設定したテキスト ボックスおよびプレースホルダー テキストのサンプル値を表示するには、 **[プレースホルダーのスタイル]** の設定を切り替えます。  
  
#### <a name="to-format-a-currency-field"></a>通貨フィールドを書式設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  2 行目 (列の見出し行) の下のセルをクリックして、 **SalesDate**列とが含まれているすべてのセルを選択するドラッグ`[Sum(Sales)]`します。  
  
3.  **[ホーム]** タブの **[数値]** グループで、 **[通貨]** ボタンをクリックします。 書式設定された通貨を表示するようにセルが変化します。  
  
     地域設定が英語 (米国) の場合、既定のサンプル テキストは **[$12,345.00]** です。 通貨値の例が表示されない場合はクリックして**プレース ホルダーのスタイル**で、**番号**グループ化、およびクリックして**サンプル値**。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
 集計値が**Sales**を通貨として表示します。  
  
##  <a name="FormatDates"></a> 6.(オプション) データに日付の書式を設定する  
 既定では、 **SalesDate** フィールドには日付と時刻の情報が表示されます。 このフィールドを書式設定して、日付のみを表示できます。  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>日付フィールドの書式を既定の書式に設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  `[SalesDate]`が格納されたセルをクリックします。  
  
3.  リボンの上、**ホーム** タブで、**数**グループの選択 ドロップダウン リストから**日付**。  
  
     セルに、日付の例として **[2000/1/31]** と表示されます。 日付の例が表示されない場合は、 **[数値]** グループの **[プレースホルダーのスタイル]** をクリックし、 **[サンプルの値]** をクリックします。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
 **SalesDate**値が既定の日付形式で表示します。  
  
##  <a name="Width"></a> 7.(オプション) 列幅を変更する  
 テーブルの各セルには、既定でテキスト ボックスが含まれます。 テキスト ボックスは、ページを表示するときにテキストに合わせて垂直方向に拡張されます。 表示されるレポートでは、各行がその行で最も高いテキスト ボックスの高さに拡張されます。 デザイン画面の行の高さは、表示されるレポートの行の高さには影響しません。  
  
 各行の垂直方向の領域を小さくするには、列の幅を広げ、列で想定されるテキスト ボックスの内容が 1 行に収まるようにします。  
  
#### <a name="to-change-the-width-of-columns"></a>列の幅を変更するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  テーブルをクリックし、列ハンドルおよび行ハンドルをテーブルの上部および横に表示します。  
  
     テーブルの上と横のグレーのバーは、列および行ハンドルです。  
  
3.  列ハンドルの間の罫線をポイントします。カーソルが 2 方向の矢印の形状に変化します。 列をドラッグして、目的のサイズに変更します。 たとえば、列を広げます**製品**製品名は 1 つの行が表示されるようにします。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Title"></a> 8.(オプション) レポート タイトルを追加する  
 レポート タイトルは、レポートの最上部に表示されます。 レポート ヘッダーがあれば、そこにレポート タイトルを配置します。レポート ヘッダーを使用しない場合は、レポート本文の一番上のテキスト ボックスに配置します。 このチュートリアルでは、自動的にレポート本文の一番上に配置されるテキスト ボックスを使用します。  
  
 テキストの語句や文字のフォントのスタイル、サイズ、および色を変更して、テキストをさらに強調することもできます。 詳細については、「[テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)」を参照してください。  
  
#### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Product Sales**」と入力し、テキスト ボックスの外側をクリックします。  
  
3.  **Product Sales** が含まれているテキスト ボックスを右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
4.  **[テキスト ボックスのプロパティ]** ダイアログ ボックスで、 **[フォント]** をクリックします。  
  
5.  **[サイズ]** ボックスの一覧の **[18pt]** を選択します。  
  
6.  **色**一覧で、**茶色**します。  
  
7.  **[太字]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> 9.レポートを保存する  
 レポートをレポート サーバーまたは自分のコンピューターに保存します。 レポート サーバーに保存しない場合は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のいくつかの機能 (レポート パーツ、サブレポートなど) が使用できなくなります。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
     "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に入力されている既定の名前を「 **Product Sales**」に置き換えます。  
  
5.  **[保存]** をクリックします。  
  
 レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
#### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **[名前]** に入力されている既定の名前を「 **Product Sales**」に置き換えます。  
  
4.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 これで、スパークライン グラフを使ったテーブル レポートを作成するチュートリアルを終了します。 スパークラインの詳細については、[「スパークラインとデータ バー (レポート ビルダーおよび SSRS)」](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md) を参照してください。  
  
## <a name="see-also"></a>参照  
 [チュートリアル&#40;レポート ビルダー&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 のレポート ビルダー](report-builder/report-builder-in-sql-server-2016.md)  
  
  
