---
title: チュートリアル:レポートへの縦棒グラフの追加 (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 723e8fe5f657d3b9eda2d6ab73966830a13a3aac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099132"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>チュートリアル:レポートへの縦棒グラフの追加 (レポート ビルダー)
  縦棒グラフでは、カテゴリ別にグループ化された縦棒のセットとして系列が表示されます。 縦棒グラフは次の場合に便利です。  
  
-   時間の経過に伴うデータの変化を示す。  
  
-   複数の系列の相対値を比較する。  
  
-   移動平均を表示して傾向を示す。  
  
 次の図に、これから作成する、移動平均が含まれた縦棒グラフを示します。  
  
 ![rs_TutorialColChartFinished](../../2014/tutorials/media/rs-tutorialcolchartfinished.gif "rs_TutorialColChartFinished")  
  
##  <a name="BackToTop"></a> 学習内容  
 このチュートリアルでは、次の方法を学習します。  
  
1.  [グラフ ウィザードからグラフを作成します。](#Chart)  
  
2.  [グラフの種類を選択します。](#ChartType)  
  
3.  [形式し、水平軸のラベル](#Horizontal)  
  
4.  [凡例を移動します。](#Legend)  
  
5.  [グラフをタイトルします。](#ChartTitle)  
  
6.  [形式し、垂直軸のラベル](#Vertical)  
  
7.  [移動平均を追加します。](#Average)  
  
8.  [レポート タイトルを追加します。](#Title)  
  
9. [レポートを保存します。](#Save)  
  
> [!NOTE]  
>  このチュートリアルでは、ウィザードに関する複数の手順を 1 つにまとめて示します。 レポート サーバーの参照、データ ソースの選択、およびデータセットの作成に関する詳細な手順については、このシリーズの最初のチュートリアルである「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。  
  
 このチュートリアルの推定所要時間:15 分。  
  
## <a name="requirements"></a>必要条件  
 要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/report-builder-tutorials.md) を参照してください。  
  
##  <a name="Chart"></a> 1.グラフ ウィザードからグラフ レポートを作成する  
 **Getting Started** 、埋め込みデータセットを作成、グラフ ウィザードは共有データ ソースを選択し、縦棒グラフを作成 ダイアログ ボックスで、使用します。  
  
> [!NOTE]  
>  このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
#### <a name="to-create-a-new-chart-report"></a>新しいグラフ レポートを作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[プログラム]** 、 **[Microsoft SQL Server 2012 レポート ビルダー]** の順にポイントして、 **[レポート ビルダー]** をクリックします。  
  
     **[作業の開始]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  場合、 **Getting Started** ] ダイアログ ボックスが表示されないから、**レポート ビルダー**ボタン、[**新規**します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[グラフ ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで **[データセットを作成する]** をクリックし、 **[次へ]** をクリックします。  
  
5.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択し、 **[次へ]** をクリックします。 ユーザー名とパスワードの入力が必要な場合があります。  
  
    > [!NOTE]  
    >  適切な権限を持っている限り、選択するデータ ソースは重要ではありません。 データ ソースからはデータを取得しません。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
6.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
7.  次のクエリをクエリ ペインに貼り付けます。  
  
    ```  
    SELECT CAST('2009-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2009-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2009-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2009-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2009-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2009-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2009-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2009-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2009-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2009-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2009-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2009-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2009-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2009-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2009-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2009-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (省略可) [実行] ボタン ( **!** ) をクリックして、グラフの基になるデータを確認します。  
  
9. **[次へ]** をクリックします。  
  
##  <a name="ChartType"></a> 2.グラフの種類を選択する  
 あらかじめ定義されているさまざまなグラフの種類から選択できます。  
  
#### <a name="to-add-a-column-chart"></a>縦棒グラフを追加するには  
  
1.  **[グラフの種類の選択]** ページでは、縦棒グラフが既定のグラフの種類です。 **[次へ]** をクリックします。  
  
2.  **[グラフのフィールドの配置]** ページで、SalesDate フィールドを **[カテゴリ]** にドラッグします。 カテゴリは横軸に表示されます。  
  
3.  Sales フィールドを **[値]** にドラッグします。 販売の合計値の総計が 1 日ごとに集計されるので、 **[値]** ボックスには Sum(Sales) が表示されます。 値は縦軸に表示されます。  
  
4.  **[次へ]** をクリックします。  
  
5.  **スタイルの選択** ページで、スタイル ボックスで、スタイルを選択します。  
  
     スタイルは、フォント スタイル、色、および罫線のスタイルを指定します。 スタイルを選択すると、プレビュー ペインにそのスタイルのグラフのサンプルが表示されます。  
  
6.  **[完了]** をクリックします。  
  
     グラフがデザイン画面に追加されます。  
  
7.  グラフをクリックして、グラフのハンドルを表示します。 グラフの右下隅をドラッグして、グラフのサイズを大きくします。 レポート デザイン画面も、グラフ サイズに合わせて大きくなります。  
  
8.  **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Horizontal"></a> 3.横軸の形式とラベルを設定する  
 既定では、横軸の値が一般的な形式で表示されます。この場合、グラフのサイズに合わせて自動的にスケーリングされます。  
  
#### <a name="to-format-a-date-on-the-horizontal-axis"></a>横軸に表示される日付の書式を変更するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  水平方向の軸を右クリックし、**横軸のプロパティ**します。  
  
3.  クリックして**数**します。  
  
4.  **カテゴリ**、**日付**します。  
  
5.  **[型]** ボックスで **[2000 年 1 月 31 日]** を選択します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [ホーム] タブで **[実行]** をクリックして、レポートをプレビューします。  
  
 選択した日付書式で日付が表示されます。 グラフの横軸を見ると、すべてのカテゴリに対してラベルが表示されているわけではないことがわかります。 既定では、軸の横に収まるラベルだけが表示されます。  
  
 ラベルを回転して間隔を指定することによってラベル表示をカスタマイズできます。  
  
#### <a name="to-rotate-the-axis-labels-and-change-the-display-interval-along-the-horizontal-axis"></a>軸ラベルを回転して横軸の表示間隔を変更するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  横軸のタイトルを右クリックし、をクリックし、 **軸のタイトル**タイトルを削除します。 横軸には日付が表示されるので、タイトルは必要ありません。  
  
3.  横軸を右クリックし、**横軸のプロパティ**します。  
  
4.  **軸のオプション**ページ**軸の範囲と間隔**、型**3**の**間隔**します。 3 日ごとの日付がグラフに表示されるようになります。  
  
5.  クリックして**ラベル**します。  
  
6.  **軸ラベル自動調整オプションを変更**、**自動調整を無効にする**します。  
  
7.  **[ラベルの回転角度]** で **[-90]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     横軸のサンプル テキストが 90 度回転します。  
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
 グラフでは、ラベルが回転して 3 日ごとに表示されています。  
  
##  <a name="Legend"></a> 4.凡例を移動する  
 凡例は、カテゴリと系列データから自動的に作成されます。  
  
#### <a name="to-move-the-legend-below-the-chart-area-of-a-column-chart"></a>凡例を縦棒グラフのグラフ領域の下に移動するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフで凡例を右クリックし、クリックして**凡例のプロパティ**します。  
  
3.  **レイアウトと位置**、異なる位置を選択します。 たとえば、下部中央の位置を選択します。  
  
     凡例をグラフの上または下に配置すると、凡例のレイアウトが縦方向から横方向に変更されます。 **[レイアウト]** ドロップダウン リストから、異なるレイアウトを選択できます。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (省略可) このチュートリアルではカテゴリが 1 つしかないので、凡例は必要ありません。 凡例を削除する凡例を右クリックし、**凡例の削除**します。  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="ChartTitle"></a> 5.グラフのタイトルを設定する  
  
#### <a name="to-change-the-chart-title-above-the-chart-area"></a>グラフ領域の上に表示されるグラフのタイトルを変更するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  単語を選択します。**グラフのタイトル**グラフ、および入力し、次のテキストの上部にあります。**販売注文の合計を格納**します。  
  
3.  **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Vertical"></a> 6.縦軸の形式とラベルを設定する  
 既定では、縦軸の値が一般的な形式で表示されます。この場合、グラフのサイズに合わせて自動的にスケーリングされます。  
  
#### <a name="to-format-as-currency-the-numbers-on-the-vertical-axis"></a>縦軸に表示される数値を通貨形式に変更するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  選択するグラフの側面に沿った縦軸のラベルをダブルクリックします。  
  
3.  リボンの上、**ホーム**] タブで、**数**グループで、[、**通貨**ボタン。 軸ラベルの表示が、通貨形式に変更されます。  
  
4.  リボンで、上、**ホーム**] タブで、**数**グループで、[、**小数点表示桁下げ**が最も近いドルに丸められた数値を表示するボタンを 2 回です。  
  
5.  縦軸を右クリックし、をクリックして**縦軸のプロパティ**します。  
  
6.  クリックして**数**します。 なお**通貨**で既に選択されて、**カテゴリ**ボックスと**小数点**は既に**0** (ゼロ)。  
  
7.  **で値を表示する**ボックスで、**何千も**します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. グラフの側面に沿った縦軸のタイトルを右クリックし、をクリックして**軸のタイトルのプロパティ**します。  
  
10. テキストを置き換える、**タイトルのテキスト**フィールドには、次のテキスト。**売上の合計 (in Thousands)** します。 タイトルの表示形式に関連した各種オプションを指定することもできます。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Average"></a> 7.移動平均を追加します。  
  
#### <a name="to-add-a-moving-average"></a>移動平均を追加するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフをダブルクリックして、 **グラフ データ** ペインを表示します。  
  
3.  右クリックし、 **[sum (sales)]** フィールドを**値**領域、およびクリック**計算系列の追加**します。  
  
4.  **[数式]** で、 **[移動平均]** が選択されていることを確認します。  
  
5.  **[数式パラメーターの設定]** の **[期間]** で、 **[4]** を選択します。  
  
6.  クリックして**境界線**します。  
  
7.  **線の幅**、 **3 pt**します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
 グラフに、4 日ごとに平均値を求めた日付別の売上合計の移動平均を示す線が表示されます。  
  
##  <a name="Title"></a> 8.レポート タイトルを追加する  
  
#### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
3.  型**Sales Chart**を入力し、enter キーを押しながら、 **January to December 2009**ので、次のように見えます。  
  
     **Sales Chart**  
  
     **January to December 2009**  
  
4.  選択**Sales Chart**、 をクリックし、**太字**ボタン、**フォント**セクションで、**ホーム**リボンのタブ。  
  
5.  選択**January to December 2009**、し、**フォント**セクションで、**ホーム** タブで、フォント サイズを設定**10**します。  
  
6.  (省略可能)作成する必要があります、**タイトル**テキスト ボックスの下端の中央をクリックすると、両方向矢印をプルダウンして 2 つの行のテキストに合わせて高さ。  
  
     このタイトルは、レポートの最上部に表示されます。 ページ ヘッダーが定義されていないとき、レポート本文の最上部にあるアイテムがレポート ヘッダーに相当します。  
  
7.  **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Save"></a> 9.レポートを保存する  
  
#### <a name="to-save-the-report"></a>レポートを保存するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  レポート ビルダーのボタンの **[名前を付けて保存]** をクリックします。  
  
3.  **[名前]** に「 **Sales Order Column Chart**」と入力します。  
  
4.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 これで、「レポートへの縦棒グラフの追加」チュートリアルを終了します。 グラフの詳細については、「[グラフ (レポート ビルダーおよび SSRS)](report-design/charts-report-builder-and-ssrs.md)」と「[スパークラインとデータ バー (レポート ビルダーおよび SSRS)](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [チュートリアル&#40;レポート ビルダー&#41;](report-builder-tutorials.md)   
 [SQL Server 2014 のレポート ビルダー](report-builder/report-builder-in-sql-server-2016.md)  
  
  
