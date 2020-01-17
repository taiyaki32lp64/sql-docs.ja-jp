---
title: 'チュートリアル: レポートへの円グラフの追加 (レポート ビルダー) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b25a2f955ddd630c7093a1dc82a22c2cd0ba41b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041262"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>チュートリアル: レポートへの円グラフの追加 (レポート ビルダー)
このチュートリアルでは、Reporting Services の改ページ調整されたレポートに円グラフを作成します。 パーセンテージを追加し、小さいスライスを 1 つのスライスに結合します。

円グラフおよびドーナツ グラフは、データを全体に対する比率として表示します。 これらのグラフには軸はありません。 円グラフに数値フィールドを追加すると、それぞれの値の全体に占める比率が計算されます。  

次の図に、ここで作成する円グラフを示します。 
 
![report-builder-pie-chart-final](../reporting-services/media/report-builder-pie-chart-final.png)
  
円グラフのデータ ポイントが多すぎると、データ ポイント ラベルが過密状態になって見づらくなる場合があります。 その場合は、複数の小さいスライスを組み合わせて 1 つの大きなスライスにすることを検討してください。 円グラフは、データを少数のデータ ポイントに集計すると見やすくなります。  
 
> [!NOTE]  
> このチュートリアルでは、ウィザードに関する手順を 2 つにまとめて示します。 レポート サーバーの参照、データ ソースの選択、データセットの作成に関する詳細な手順については、このシリーズの最初のチュートリアル (「[チュートリアル: 基本的な表レポートの作成 (レポート ビルダー)](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」) を参照してください。  
  
このチュートリアルの推定所要時間: 10 分  
  
## <a name="requirements"></a>必要条件  
要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/prerequisites-for-tutorials-report-builder.md) を参照してください。  
  
## <a name="Chart"></a>1.グラフ ウィザードから円グラフを作成する  
このセクションでは、グラフ ウィザードを使用して埋め込みデータセットを作成し、共有データ ソースを選択して、円グラフを作成します。  

  
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

    > [!NOTE]  
    > このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (省略可) [実行] ボタン ( **!** ) をクリックして、グラフの基になるデータを確認します。  
  
9. **[次へ]** をクリックします。  
  
## <a name="ChartType"></a>2.グラフの種類を選択する  
あらかじめ定義されているさまざまなグラフの種類から選択できます。  

  
1.  **[グラフの種類の選択]** ページで **[円]** をクリックし、 **[次へ]** をクリックします。 **[グラフのフィールドの配置]** ページが開きます。  
  
    **[グラフのフィールドの配置]** ページで、Product フィールドを **[カテゴリ]** ペインにドラッグします。 カテゴリは円グラフのスライスの数を定義します。 この例では、各製品に 1 つずつ、合計 8 個のスライスになります。  
  
2.  Sales フィールドを **[値]** ペインにドラッグします。 Sales は、サブカテゴリの売上高を表します。 各販売員の集計がグラフに表示されるため、 **[値]** ペインには " `[Sum(Sales)]` " と表示されます。  
  
3.  **次へ** をクリックしてプレビューを表示します。  
  
5.  **[完了]** をクリックします。  
  
    グラフがデザイン画面に追加されます。 円グラフの実際の値は表示されません。Product 1、Product 2 などが表示され、グラフがどのように表示されるかを確認できます。  
    
    ![report-builder-pie-chart-first-design](../reporting-services/media/report-builder-pie-chart-first-design.png)
  
6.  グラフをクリックして、グラフのハンドルを表示します。 グラフの右下隅をドラッグして、グラフを大きくします。 レポート デザイン画面も、グラフ サイズに合わせて大きくなります。  
  
7.  **[実行]** をクリックして、レポートをプレビューします。  
  
各製品に 1 つずつ、合計 8 個のスライスを含む円グラフがレポートに表示されます。 これで実際の製品が表示されます。各スライスのサイズはその製品の売上を表します。 これらのスライスのうち 3 つは、非常に小さくなります。  

![report-builder-pie-chart-first-preview](../reporting-services/media/report-builder-pie-chart-first-preview.png)
  
## <a name="Percentages"></a>3.各スライスにパーセンテージを表示する  
円グラフの各スライスには、そのスライスの全体に占めるパーセンテージを表示できます。  

  
1.  レポート デザイン ビューに切り替えます。  
  
2.  円グラフを右クリックし、 **[データ ラベルの表示]** をクリックします。 グラフにデータ ラベルが表示されます。  
  
3.  ラベルを右クリックし、 **[系列ラベルのプロパティ]** をクリックします。  
  
4.  **[ラベル データ]** ボックスで、 **[#PERCENT]** を選択します。  
    
5.  (省略可) ラベルに表示する小数点以下桁数を指定するには、 **[ラベル データ]** ボックスで、 **#PERCENT**の後に「 **{Pn}** 」と入力します。ここで、 *n* は、表示する小数点以下桁数を表します。 たとえば、小数点以下を表示しない場合は「 **#PERCENT{P0}** 」と入力します。  

6.  値をパーセンテージとして表示するには、UseValueAsLabel プロパティを false に設定する必要があります。 **[アクションの確認]** ダイアログでこの値の設定を求めるメッセージが表示されたら、 **[はい]** をクリックします。  
  
    > [!NOTE]  
    > **[系列ラベルのプロパティ]** ダイアログ ボックスの **[数値書式]** は、パーセンテージの表示形式には影響しません。 この場合、ラベルの表示形式がパーセンテージに設定されるだけで、円グラフに対する各スライスのパーセンテージが計算されるわけではありません。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  **[実行]** をクリックして、レポートをプレビューします。  
  
円グラフの各スライスがそれぞれ全体の何パーセントを占めているかが表示されます。  

![report-builder-pie-chart-preview-percents](../reporting-services/media/report-builder-pie-chart-preview-percents.png)
  
## <a name="CombineSlices"></a>4.小さな複数のスライスを 1 つのスライスにまとめる  
円グラフ内の 3 つのスライスは、非常に小さくなります。 この 3 つの小さなスライスをまとめて、"その他" という 1 つの大きなスライスで表すことができます。  

1.  レポート デザイン ビューに切り替えます。  
  
2.  [プロパティ] ペインが表示されない場合は、 **[表示]** タブの **[表示/非表示]** グループで、 **[プロパティ]** を選択します。  
  
3.  デザイン画面で、円グラフの任意のスライスをクリックします。 系列のプロパティが [プロパティ] ペインに表示されます。  
  
4.  **[全般]** セクションで、 **[CustomAttributes]** ノードを展開します。  
  
5.  **[CollectedStyle]** プロパティを **[SingleSlice]** に設定します。  

    ![report-builder-pie-chart-single-slice-property](../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
 
6.  **[CollectedThreshold]** プロパティが 5 に設定されていることを確認します。  
  
7.  **[CollectedThresholdUsePercent]** プロパティが **True**に設定されていることを確認します。  
  
8.  **[ホーム]** タブで **[実行]** をクリックして、レポートをプレビューします。  
  
凡例に "その他" というカテゴリが表示されます。 この新しいスライスでは、5% 未満のすべてのスライスが 1 つにまとめられて、円グラフ全体の 6% を占めるスライスが作成されています。  

![report-builder-pie-chart-start-at-90](../reporting-services/media/report-builder-pie-chart-start-at-90.png)
 
## <a name="DrawingEffect"></a>5.円グラフの値の開始位置を円の最上部にする 

円グラフでは、既定でデータセットの最初の値が円の最上部から 90 度の位置から開始されます。 前のセクションの円グラフでこれを確認できます。

このセクションでは、最初の値が円の最上部から始まるように変更します。

1.  レポート デザイン ビューに切り替えます。  

2. 円グラフを選択します。

3. プロパティ ペインの **[カスタム属性]** で、[PieStartAngle] を **0** から **270**に変更します。

4. **[実行]** をクリックして、レポートをプレビューします。

これで、円グラフのスライスはアルファベット順になり、円の最上部から始まり、最後は "その他" スライスになります。

![report-builder-pie-chart-start-at-top](../reporting-services/media/report-builder-pie-chart-start-at-top.png)
  
## <a name="Title"></a>6.レポート タイトルを追加する  
  
円グラフはレポート内のみの視覚エフェクトであるため、グラフには独自のタイトルは必要ありません。 レポート タイトルが使用されます。
  
1.  グラフで、[グラフのタイトル] ボックスを選択し、Del キーを押します。

2. デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Camera and Camcorder Sales**」と入力して Enter キーを押し、さらに「 **As a Percentage of Total Sales**」と入力します。次のように表示されます。  
  
    **Camera and Camcorder Sales**  
  
    **As a Percentage of Total Sales**  
  
3.  **Camera and Camcorder Sales** を選択し、 **[ホーム]** タブの **[フォント]** セクションで **[太字]** をクリックします。  
  
4.  **As a Percentage of Total Sales** を選択し、 **[ホーム]** タブの **[フォント]** セクションで、フォント サイズを **[10]** に設定します。  
  
5.  (省略可) 2 行のテキストに合わせて、[タイトル] テキスト ボックスの高さを高くする必要が生じる場合もあります。  
  
    このタイトルは、レポートの最上部に表示されます。 ページ ヘッダーが定義されていないとき、レポート本文の最上部にあるアイテムがレポート ヘッダーに相当します。  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Save"></a>7.レポートを保存する  
  
### <a name="to-save-the-report"></a>レポートを保存するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  **[ファイル]** メニューの **[保存]** をクリックします。  
  
3.  **[名前]** に「 **Sales Pie Chart**」と入力します。  
  
4.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。  
  
## <a name="next-steps"></a>Next Steps  
これで、「レポートへの円グラフの追加」チュートリアルを終了します。 グラフの詳細については、「[グラフ (レポート ビルダーおよび SSRS)](../reporting-services/report-design/charts-report-builder-and-ssrs.md)」と「[スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)  
[SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

