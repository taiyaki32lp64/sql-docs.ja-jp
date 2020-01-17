---
title: 'チュートリアル: レポートへの縦棒グラフの追加 (レポート ビルダー) | Microsoft Docs'
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 55a74bcd165fd06d55eccd6afa718ccd775c7faf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041400"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>チュートリアル: レポートへの縦棒グラフの追加 (レポート ビルダー)
このチュートリアルでは、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポートを作成します。レポートには、カテゴリでグループ化された一連の縦棒として連続を表示する棒グラフを含めます。 

縦棒グラフは次に役立ちます。  
  
-   時間の経過に伴うデータの変化を示す。  
-   複数の系列の相対値を比較する。  
-   移動平均を表示して傾向を示す。  
  
次の図に、これから作成する、移動平均が含まれた縦棒グラフを示します。  
  
![レポート-ビルダー-列のグラフのチュートリアル](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> このチュートリアルでは、ウィザードに関する複数の手順を 1 つにまとめて示します。 レポート サーバーの参照、データ ソースの選択、データセットの作成に関する詳細な手順については、このシリーズの最初のチュートリアル (「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」) を参照してください。  
  
このチュートリアルの推定所要時間: 15 分  
  
## <a name="requirements"></a>必要条件  
要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/prerequisites-for-tutorials-report-builder.md) を参照してください。  
  
## <a name="Chart"></a>1.グラフ ウィザードからグラフ レポートを作成する  
このセクションでは、グラフ ウィザードを使用して埋め込みデータセットを作成し、共有データ ソースを選択して、縦棒グラフを作成します。  
  
> [!NOTE]  
> このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-chart-report"></a>グラフ レポートを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[グラフ ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで **[データセットを作成する]** をクリックし、 **[次へ]** をクリックします。  
  
5.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択し、 **[次へ]** をクリックします。 ユーザー名とパスワードの入力が必要な場合があります。  
  
    > [!NOTE]  
    > 適切な権限を持っている限り、選択するデータ ソースは重要ではありません。 データ ソースからはデータを取得しません。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
6.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
7.  次のクエリをクエリ ペインに貼り付けます。  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (省略可) [実行] ボタン ( **!** ) をクリックして、グラフの基になるデータを確認します。  
  
9. **[次へ]** をクリックします。  
  
## <a name="ChartType"></a>2.グラフの種類を選択する  
事前定義されたグラフの種類から選択し、ウィザードの完了後にグラフを修正できます。  
  
### <a name="to-add-a-column-chart"></a>縦棒グラフを追加するには  
  
1.  **[グラフの種類の選択]** ページでは、縦棒グラフが既定のグラフの種類です。 **[次へ]** をクリックします。  
  
2.  **[グラフのフィールドの配置]** ページで、SalesDate フィールドを **[カテゴリ]** にドラッグします。 カテゴリは横軸に表示されます。  
  
3.  Sales フィールドを **[値]** にドラッグします。 販売の合計値の総計が 1 日ごとに集計されるので、 **[値]** ボックスには Sum(Sales) が表示されます。 値は縦軸に表示されます。  
  
4.  **[次へ]** をクリックします。  
 
6.  **[完了]** をクリックします。  
  
    グラフがデザイン画面に追加されます。 新しい縦棒グラフは主要なデータのみを示すことに注意してください。 凡例に Sales Date A、Sales Date B と示されています。これから完成したレポートの姿がわかります。 
    
    ![report-builder-column-chart-1-design-view](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  グラフをクリックして、グラフのハンドルを表示します。 グラフの右下隅をドラッグして、グラフのサイズを大きくします。 レポート デザイン画面も、グラフ サイズに合わせて大きくなります。  
  
8.  **[実行]** をクリックして、レポートをプレビューします。  

    ![report-builder-column-chart-1-preview](../reporting-services/media/report-builder-column-chart-1-preview.png)

グラフの横軸を見ると、すべてのカテゴリに対してラベルが表示されているわけではないことがわかります。 既定では、軸の横に収まるラベルだけが表示されます。 
  
## <a name="Horizontal"></a>3.横軸に表示される日付の書式を変更する  
既定では、横軸の値が一般的な形式で表示されます。この場合、グラフのサイズに合わせて自動的にスケーリングされます。  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  横軸を右クリックし、 **[横軸のプロパティ]** をクリックします。  
  
3.  **[数値]** タブの **[カテゴリ]** で **[日付]** を選択します。  
  
5.  **[型]** ボックスで **[2000 年 1 月 31 日]** を選択します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [ホーム] タブで **[実行]** をクリックして、レポートをプレビューします。  
  
選択した日付書式で日付が表示されます。 グラフの横軸を見ると、すべてのカテゴリに対してラベルが表示されているわけではありません。 

![report-builder-column-chart-2-preview](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
ラベルを回転して間隔を指定することによってラベル表示をカスタマイズできます。  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4.横軸の軸ラベルを回転させる  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  横軸のタイトルを右クリックし、 **[軸のタイトルの表示]** をクリックしてタイトルを削除します。 横軸には日付が表示されるので、タイトルは必要ありません。  
  
3.  横軸を右クリックし、 **[横軸のプロパティ]** をクリックします。  
  
5.  **[ラベル]** タブの **[軸ラベル自動調整のオプションを変更します]** で **[自動調整を無効にする]** を選択します。  
  
7.  **[ラベルの回転角度]** で **[-90]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    横軸のサンプル テキストが 90 度回転します。  
    
    ![report-builder-column-chart-rotate-x-axis](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
グラフでラベルが回転します。  

![report-builder-column-chart-rotate-x-axis-preview](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="Legend"></a>5.凡例を移動する  
凡例は、カテゴリと系列データから自動的に作成されます。 凡例を縦棒グラフのグラフ領域の下に移動できます。  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフの凡例を右クリックし、 **[凡例のプロパティ]** をクリックします。  
  
3.  **[レイアウトと位置]** で、異なる位置を選択します。 たとえば、中央下を選択します。  
  
    凡例をグラフの上または下に配置すると、凡例のレイアウトが縦方向から横方向に変更されます。 **[レイアウト]** ボックスの一覧で異なるレイアウトを選択できます。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (省略可) このチュートリアルではカテゴリが 1 つしかないので、凡例は必要ありません。 削除するには、凡例を右クリックして **[凡例の削除]** をクリックします。  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="ChartTitle"></a>6.グラフのタイトルを設定する  
    
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフ上部の **[グラフのタイトル]** というテキストを選択し、「 **Store Sales Order Totals**」と入力します。  
  
3.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Vertical"></a>7.縦軸の形式とラベルを設定する  
既定では、縦軸の値が一般的な形式で表示されます。この場合、グラフのサイズに合わせて自動的にスケーリングされます。   
  
1.  レポート デザイン ビューに切り替えます。  
  
2. グラフの側面にある縦軸のラベルをクリックして選択します。  
  
3.  **[ホーム]** タブの **[数値]** グループで、 **[通貨]** ボタンをクリックします。 軸ラベルの表示が、通貨形式に変更されます。  
  
4.  **[小数点表示桁下げ]** ボタンを 2 回クリックします。数値が最も近いドルに丸められて表示されます。  
  
5.  縦軸を右クリックし、 **[縦軸のプロパティ]** をクリックします。  
  
6.  **[数値]** タブの **[カテゴリ]** ボックスでは **[通貨]** が既に選択されており、 **[小数点以下桁数]** は **[0]** (ゼロ) になっています。  
  
7.  **[値の表示単位]** を確認します。 **[千]** が既に選択されています。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 縦軸を右クリックし、 **[軸のタイトルの表示]** をクリックします。 

10. 縦軸のタイトルを右クリックし、 **[軸のタイトルのプロパティ]** をクリックします。  
  
10. **[タイトルのテキスト]** フィールドのテキストを「 **Sales Total (in Thousands)** 」に置き換えます。 タイトルの表示形式に関連した各種オプションを指定することもできます。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. **[実行]** をクリックして、レポートをプレビューします。  

    ![report-builder-column-chart-format-y-axis](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8.横軸 (x) にすべてのラベルを表示する

x 軸では一部のラベルのみが表示されています。 このセクションでは、プロパティ ペインでプロパティを設定し、ラベルをすべて表示します。

1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフをクリックし、横軸ラベルを選択します。

3. プロパティ ペインで、LabelInterval を 1 に設定します。

    ![report-builder-column-chart-set-label-interval](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    グラフはデザイン ビューで同じに見えます。 
    
5.  **[実行]** をクリックして、レポートをプレビューします。

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    これでグラフにすべてのラベルが表示されました。
  
## <a name="Average"></a>9.計算系列で移動平均を追加する  

移動平均は、一定期間にわたって計算される、系列内のデータの平均です。 移動平均で傾向を特定できます。
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフをダブルクリックして、 **グラフ データ** ペインを表示します。  
  
3.  **[値]** 領域の **[Sum(Sales)]** フィールドを右クリックし、 **[計算系列の追加]** をクリックします。  

     ![report-builder-column-chart-add-calculated-series](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  **[数式]** で、 **[移動平均]** が選択されていることを確認します。  
  
5.  **[数式パラメーターの設定]** の **[期間]** で、 **[4]** を選択します。  
  
6.  **[罫線]** タブの **[線の幅]** で **[3pt]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
グラフに、4 日ごとに平均値を求めた日付別の売上合計の移動平均を示す線が表示されます。 グラフに移動平均を追加する方法の詳細は、 [グラフへの移動平均の追加](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)に関する記事をご覧ください。 

![report-builder-column-chart-moving-average](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="Title"></a>10.レポート タイトルを追加する  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
3.  「 **Sales Chart**」と入力して Enter キーを押し、さらに「 **January to December 2015**」と入力します。次のように表示されます。  
  
    **Sales Chart**  
  
    **January to December 2015**  
  
4.  **[Sales Chart]** を選択し、 **[ホーム]** タブの **[フォント]** セクションで **[太字]** を選択します。  
  
5.  **[January to December 2015]** を選択し、 **[ホーム]** タブの **[フォント]** セクションでフォント サイズを **[10]** に設定します。  
  
6.  (省略可) 2 行のテキストに合わせて、 **[タイトル]** テキスト ボックスの高さを高くする必要が生じる場合もあります。 下端の中央をクリックするとき、両方向矢印のところでプルダウンします。 場合によっては、タイトルが重ならないようにグラフの上部をドラッグする必要があります。  
  
    このタイトルは、レポートの最上部に表示されます。 ページ ヘッダーが定義されていないとき、レポート本文の最上部にあるアイテムがレポート ヘッダーに相当します。  
  
7.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Save"></a>11.レポートを保存する  
  
### <a name="to-save-the-report"></a>レポートを保存するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  レポート ビルダーのボタンの **[名前を付けて保存]** をクリックします。  

    コンピューターまたはレポート サーバーに保存できます。
  
3.  **[名前]** に「 **Sales Order Column Chart**」と入力します。  
  
4.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  
これで、「レポートへの縦棒グラフの追加」チュートリアルを終了します。 グラフの詳細については、「[グラフ (レポート ビルダーおよび SSRS)](../reporting-services/report-design/charts-report-builder-and-ssrs.md)」と「[スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
-    [レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md) 
-    [SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

