---
title: 'チュートリアル: レポートへの横棒グラフの追加 (レポート ビルダー) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8e6855a7a6a47021a635e12b2c53515ed20aa6f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041185"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>チュートリアル: レポートへの横棒グラフの追加 (レポート ビルダー)
このチュートリアルでは、ウィザードを使用して、 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] で [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポートに横棒グラフを作成します。 次にフィルターを追加してグラフを強化します。 

横棒グラフでは、カテゴリ データが水平方向に表示されます。 これは、次のようなことに役立ちます。  
  
-   長いカテゴリ名を読みやすくする。  
-   値としてプロットされた時間をわかりやすく示す。   
-   複数の系列の相対値を比較する。  
  
次の図は、ここで作成する横棒グラフを示しています。このグラフでは、2014 年と 2015 年の上位 5 人の販売員の売上を 2015 年の売上が高い順に示します。  
  
![report-builder-bar-chart](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> このチュートリアルでは、ウィザードに関する複数の手順を 1 つにまとめて示します。 レポート サーバーの参照、データセットの作成、データ ソースの選択に関する詳細な手順については、このシリーズの最初のチュートリアル (「[チュートリアル: 基本的な表レポートの作成 (レポート ビルダー)](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」) を参照してください。  
  
このチュートリアルの推定所要時間: 15 分  
  
## <a name="requirements"></a>必要条件  
要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。  
  
## <a name="Chart"></a>1.グラフ ウィザードからグラフ レポートを作成する  
埋め込みデータセットを作成し、共有データ ソースを選択します。グラフ ウィザードを使用して横棒グラフを作成します。  
  
> [!NOTE]  
> このチュートリアルでは、外部のデータ ソースが必要ないようにクエリにデータ値が含まれています。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
1.  [Web ポータル、SharePoint 統合モードのレポート サーバー、またはコンピューターから、](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。  
  
     **[作業の開始]** ダイアログ ボックスが表示されます。  
  
     ![レポート ビルダーの作業の開始](../reporting-services/media/rb-getstarted.png "レポート ビルダーの作業の開始")  
  
     **[作業の開始]** ダイアログ ボックスが表示されない場合は、 **[ファイル]**  > **[新規作成]** をクリックします。 **[新しいレポートまたはデータセット]** ダイアログ ボックスは、 **[作業の開始]** ダイアログ ボックスとほぼ同じ内容です。 
      
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[グラフ ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで **[データセットを作成する]** をクリックし、 **[次へ]** をクリックします。  
  
5.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択し、 **[次へ]** をクリックします。 ユーザー名とパスワードの入力が必要な場合があります。  
  
    > [!NOTE]  
    > 適切な権限を持っている限り、選択するデータ ソースは重要ではありません。 データ ソースからはデータを取得しません。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
6.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
7.  次のクエリをクエリ ペインに貼り付けます。  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (省略可) [実行] ボタン ( **!** ) をクリックして、グラフの基になるデータを確認します。  
  
9. **[次へ]** をクリックします。  
  
## <a name="ChartType"></a>2.横棒グラフを作成する  
 
1.  **[グラフの種類の選択]** ページでは、縦棒グラフが既定のグラフの種類です。  
  
2.  **[横棒]** をクリックし、 **[次へ]** をクリックします。  
  
    **[グラフのフィールドの配置]** ページでは、 **使用できるフィールド** ペインに、FirstName、LastName、SalesYear2015、および SalesYear2014 の 4 つのフィールドがあります。  
  
3.  LastName をカテゴリ ペインにドラッグします。  
  
4.  SalesYear2015 を値ペインにドラッグします。 SalesYear2015 は、2015 年の各販売員の売上高を表します。 各製品の集計がグラフに表示されるため、値ペインには " `[Sum(SalesYear2015)]` " と表示されます。  
  
5.  SalesYear2014 を SalesYear2015 の値ペインにドラッグします。 SalesYear2014 は、2014 年の各販売員の売上高を表します。  
  
6.  **[次へ]** をクリックします。  
  
7.  **[完了]** をクリックします。  
  
    グラフがデザイン画面に追加されます。 新しい横棒グラフは主要なデータのみを示すことに注意してください。 凡例には、レポートの概要を把握できるように、人名ではなく Last Name A、Last Name B などと表示しています。 
  
9. グラフをクリックして、グラフのハンドルを表示します。 グラフの右下隅をドラッグして、グラフのサイズを大きくします。 デザイン画面はドラッグすると拡大することに注意してください。 
  
10. **[実行]** をクリックして、レポートをプレビューします。  
  
2014 年と 2015 年の各販売員の売上を示す横棒グラフが表示されます。 横棒の長さは、売上総額に対応します。  
  
## <a name="AllValues"></a>3.縦軸にすべての名前を表示する  
既定では、縦軸の値の一部のみが表示されます。 すべてのカテゴリを表示するようにグラフを変更できます。  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  縦軸を右クリックし、 **[縦軸のプロパティ]** をクリックします。  
  
3.  **[軸の範囲と間隔]** の **[間隔]** ボックスに「 **1**」と入力します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  **[実行]** をクリックして、レポートをプレビューします。  
  
> [!NOTE]  
> 縦軸に表示される販売員の名前が読みにくい場合は、グラフを縦方向に大きくするか、軸ラベルの形式オプションを変更します。  
  
### <a name="CategoryExpression"></a>縦軸に姓と名を表示する  
各販売員の姓と名を含むように、カテゴリ式を変更できます。  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフをダブルクリックして、 **グラフ データ** ペインを表示します。  
  
3.  **[カテゴリ グループ]** 領域で、[LastName] を右クリックして、 **[カテゴリ グループのプロパティ]** をクリックします。  
  
4.  [ラベル] で、式 ([Fx]) ボタンをクリックします。  
  
5.  次の式を入力します。 `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    この式は、姓、コンマ、および名を連結します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  **[実行]** をクリックして、レポートをプレビューします。  
  
レポートを実行したときに名が表示されない場合は、データを手動で更新します。 プレビュー モードのまま、 **[実行]** タブの **[ナビゲーション]** グループで、 **[更新]** をクリックします。  
  
> [!NOTE]  
> 縦軸に表示される販売員の名前が読みにくい場合は、グラフを縦方向に大きくするか、軸ラベルの形式オプションを変更します。  
  
## <a name="Sort"></a>4.縦軸に表示される並べ替え順序を変更する  
グラフのデータを並べ替えると、カテゴリ軸の値の順序が変更されます。  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフをダブルクリックして、 **グラフ データ** ペインを表示します。  
  
3.  **[カテゴリ グループ]** 領域で、[LastName] を右クリックして、 **[カテゴリ グループのプロパティ]** をクリックします。  
  
4.  **[並べ替え]** をクリックします。 **[並べ替えのオプションを変更します]** ページに、並べ替え式の一覧が表示されます。 既定では、この一覧には、元のカテゴリ グループの式と同じである 1 つの並べ替え式が含まれています。  
  
5.  **[並べ替え]** の **[SalesYear2015]** をクリックします。  
  
6.  **[順序]** リストで **[昇順]** を選択して、2015 年の売上が高い順に名前が表示されるようにします。
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **[実行]** をクリックして、レポートをプレビューします。  
  
横軸の名前は 2015 年の売上が高い順に並べ替えられ、 **Zeng** が先頭になります。  
  
## <a name="Legend"></a>5.凡例を移動する  
グラフの凡例を移動することで、グラフの値を読みやすくすることができます。 たとえば、バーが横方向に表示される横棒グラフでは、グラフ領域の上または下に来るように凡例の位置を変更します。 こうすることで、バーの水平方向のスペースを広げることができます。  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>凡例を横棒グラフのグラフ領域の下に表示するには  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフの凡例を右クリックします。  
  
3.  **[凡例のプロパティ]** を選択します。  
  
4.  **[凡例の位置]** で、異なる位置を選択します。 たとえば、下部中央の位置を選択します。  
  
    凡例をグラフの上または下に配置すると、凡例のレイアウトが縦方向から横方向に変更されます。 **[レイアウト]** ドロップダウン リストから、異なるレイアウトを選択できます。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="ChartTitle"></a>6.グラフのタイトルを設定する  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフ上部の **[グラフのタイトル]** というテキストを選択し、「 **Sales for 2014 and 2015**」と入力します。  
  
3.  [プロパティ] ペインで、タイトルを選択した状態で **[色]** を **[黒]** に、 **[フォント サイズ]** を **[12 ポイント]** に変更します。 
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Horizontal"></a>7.横軸の形式とラベルを設定する  
既定では、横軸の値が一般的な形式で表示されます。この場合、グラフのサイズに合わせて自動的にスケーリングされます。 この形式を通貨形式に変更できます。  
   
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフの底辺に沿った横軸をクリックして選択します。  
  
3.  **[ホーム]** タブの **[数値]** グループで、 **[通貨]** をクリックします。 横軸ラベルが通貨に変更されます。  
  
3.  (省略可) 小数点以下の桁を削除します。 **[通貨]** ボタンの近くにある **[小数点表示桁下げ]** ボタンを 2 回クリックします。  
  
4.  横軸を右クリックし、 **[横軸のプロパティ]** をクリックします。  
  
5.  **[数値]** タブで、 **[値を千単位で表示]** を選択します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  横軸を右クリックし、 **[軸のタイトルの表示]** をクリックします。
  
7.  **[軸のタイトル]** ボックスに「 **Sales in thousands** 」と入力し、Enter キーを押します。  

    >**注:** 入力時には、[軸のタイトル] ボックスが縦軸に表示されます。 Enter キーを押すと、横軸に表示されます。
  
9. **[実行]** をクリックして、レポートをプレビューします。  
  
レポートの横軸に売上高が千単位の通貨で表示され、小数点以下の桁が省略されます。  
  
## <a name="Filter"></a>8.フィルターを追加して上位 5 件の値を表示する  
グラフにフィルターを追加して、データセットのどのデータをグラフに含め、どのデータをグラフに含めないかを指定できます。   
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  グラフをダブルクリックして、 **グラフ データ** ペインを表示します。  
  
3.  **[カテゴリ グループ]** 領域で、[LastName] フィールドを右クリックして、 **[カテゴリ グループのプロパティ]** をクリックします。  
  
4.  **[フィルター]** をクリックします。 **[フィルターを変更します]** ページに、フィルター式の一覧を表示することもできます。 既定では、この一覧には何も表示されません。  
  
5.  **[追加]** をクリックします。 新しい空のフィルターが表示されます。  
  
6.  **[式]** に「 **[Sum(SalesYear2015)]** 」と入力します。 基になる式 `=Sum(Fields!SalesYear2015.Value)`が作成され、この式は **[fx]** ボタンをクリックすると表示できます。  
  
7.  データ型が **Text**であることを確認します。  
  
8.  **[演算子]** で、ドロップダウン リストから **[上位 N]** を選択します。  
  
9. **[値]** に式「 **=5**」を入力します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **[実行]** をクリックして、レポートをプレビューします。  
  
レポートを実行したときに結果がフィルター選択されない場合は、データを手動で更新します。 **[実行]** タブの **[ナビゲーション]** グループで、 **[更新]** をクリックします。  
  
グラフに、2015 年の売上データから取得された上位 5 人の販売員の名前が表示されます。  
  
## <a name="Title"></a>9.レポート タイトルを追加する  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Sales Bar Chart**」と入力して Enter キーを押し、さらに「 **Top Five Sellers for 2015**」と入力します。次のように表示されます。  
  
    **Sales Bar Chart**  
  
    **Top Five Sellers for 2015**  
  
3.  **[Sales Bar Chart]** を選択し、 **[太字]** ボタンをクリックします。  
  
4.  **[Top Five Sellers for 2015]** を選択し、 **[ホーム]** タブの **[フォント]** セクションで、フォント サイズを **[10]** に設定します。  
  
5.  (省略可) 必要に応じて、2 行のテキストに合わせて [タイトル] テキスト ボックスの高さを高くし、棒グラフの上部を下げます。  
  
    このタイトルは、レポートの最上部に表示されます。 ページ ヘッダーが定義されていないとき、レポート本文の最上部にあるアイテムがレポート ヘッダーに相当します。  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Save"></a>10.レポートを保存する  
  
1.  レポート デザイン ビューに切り替えます。  
  
2.  **[ファイル]**  >  **[名前を付けて保存]** をクリックします。  
  
3.  **[名前]** に「 **Sales Bar Chart**」と入力します。  

    コンピューターまたはレポート サーバーに保存できます。
  
4.  **[保存]** をクリックします。   
  
## <a name="next-steps"></a>Next Steps  
これで、「レポートへの横棒グラフの追加」チュートリアルを終了します。 グラフの詳細については、「 [グラフ](../reporting-services/report-design/charts-report-builder-and-ssrs.md) 」と「 [横棒グラフ](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)  
[SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

