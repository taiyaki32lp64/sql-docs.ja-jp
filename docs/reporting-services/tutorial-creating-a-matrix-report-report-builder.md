---
title: 'チュートリアル: マトリックス レポートの作成 (レポート ビルダー) | Microsoft Docs'
ms.date: 06/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ed53800a1b45dd79548c59aaab57f71bd700d94d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294670"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>チュートリアル: マトリックス レポートの作成 (レポート ビルダー)
このチュートリアルでは、入れ子になった行および列グループ内のサンプル売上データのマトリックスを使用して、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポートを作成する方法について説明します。 

また、隣接する列グループの作成、列の書式設定、およびテキストの回転も行います。 次の図に、ここで作成するレポートと同様のレポートを示します。  
  
![report-builder-matrix-tutorial](../reporting-services/media/report-builder-matrix-tutorial.png)
   
このチュートリアルの推定所要時間 : 20 分  
  
## <a name="requirements"></a>必要条件  
要件については、「 [チュートリアルの前提条件](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。 
  
## <a name="CreateMatrix"></a>1.テーブルまたはマトリックスの新規作成ウィザードを使用してマトリックス レポートとデータセットを作成する  
このセクションでは、共有データ ソースを選択し、埋め込みデータセットを作成して、データをマトリックスに表示します。  
  
> [!NOTE]  
> このチュートリアルのクエリには既にデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-matrix"></a>マトリックスを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで、 **[データセットを作成する]** をクリックします。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。 使用できるデータ ソースがなく、レポート サーバーにもアクセスできない場合は、代わりに埋め込みデータ ソースを使用できます。 埋め込みデータ ソースの作成については、「[チュートリアル: 基本的な表レポートの作成 (レポート ビルダー)](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。  
  
7.  **[次へ]** をクリックします。  
  
8.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
9. 次のクエリをコピーし、クエリ ペインに貼り付けます。  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. (省略可能) [実行] アイコン (!) をクリックしてクエリを実行し、データを表示します。

11. **[次へ]** をクリックします。  
  
## <a name="Groups"></a>2.テーブルまたはマトリックスの新規作成ウィザードを使用してデータを整理し、レイアウトを選択する  
ウィザードを使用して、データを表示する最初のデザインを作成します。 ウィザードのプレビュー ペインでは、マトリックスのデザインを完了する前にデータのグループ化の結果を表示できます。  
  
1.  **[フィールドの配置]** ページで、 **[使用できるフィールド]** から Territory を **[行グループ]** にドラッグします。  
  
2.  SalesDate を **[行グループ]** にドラッグして Territory の下に配置します。  
  
    **[行グループ]** 内でフィールドが表示される順序によって、グループの階層が決まります。 手順 1. および 2. で、フィールドの値がまず販売区域でまとめられ、次に販売日でまとめられます。  
  
3.  Subcategory を **[列グループ]** にドラッグします。  
  
4.  Product を **[列グループ]** にドラッグして Subcategory の下に配置します。  
  
    ここでも、 **[列グループ]** 内でフィールドが表示される順序によって、グループの階層が決まります。 手順 3. および 4. で、フィールドの値がまずサブカテゴリでまとめられ、次に製品でまとめられます。  
  
5.  Sales を **[値]** にドラッグします。  
  
    Sales は Sum 関数 (数値フィールドを集計するための既定の関数) を使用して集計されます。  
  
6.  Quantity を **[値]** にドラッグします。  
  
    Quantity は Sum 関数を使用して集計されます。  
  
    手順 5. および 6. で、マトリックスのデータ セルに表示するデータが指定されます。
    
    ![report-builder-arrange-fields-report-wizard](../reporting-services/media/report-builder-arrange-fields-report-wizard.png)  
  
7.  **[次へ]** をクリックします。  
  
8.  [レイアウトの選択] ページの **[オプション]** で、 **[小計と総計を表示]** が選択されていることを確認します。  
  
9. **[ブロック、小計は下]** が選択されていることを確認します。  
  
10. **[グループの展開/折りたたみ]** チェック ボックスがオンであることを確認します。  
  
11. **[次へ]** をクリックします。  
  
13. **[完了]** をクリックします。  
  
    マトリックスがデザイン画面に追加されます。 行グループ ペインには、Territory と SalesDate の 2 つの行グループが表示されます。 列グループ ペインには、Subcategory と Product の 2 つの行グループが表示されます。 詳細データは、データセット クエリによって取得されるすべてのデータです。  
    
    ![report-builder-row-and-column-groups](../reporting-services/media/report-builder-row-and-column-groups.png)
  
14. **[実行]** をクリックして、レポートをプレビューします。  
  
    マトリックスには、特定の日付に販売された製品ごとに、製品のサブカテゴリと販売区域が表示されます。  

14. サブカテゴリを展開します。 すばやくレポートの幅が広くなります。

![report-builder-expand-matrix](../reporting-services/media/report-builder-expand-matrix.png)
  
## <a name="FormatData"></a>3.データの書式を設定する  
既定では Sales フィールドの概要データでは通常の数値が、SalesDate フィールドには日付と時刻の両方の情報が表示されます。 このセクションでは、書式を設定して Sales フィールドでは数値が通貨として表示されるようにし、SalesDate フィールドでは日付のみが表示されるようにします。 書式設定したテキスト ボックスおよびプレースホルダー テキストのサンプル値を表示するには、 **[プレースホルダーのスタイル]** の設定を切り替えます。  
  
### <a name="to-format-fields"></a>フィールドの書式を設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  Ctrl&lt;/localizedText&gt; キーを押しながら、 `[Sum(Sales)]`が格納されている 9 つのセルを選択します。  
  
3.  **[ホーム]** タブで、 **[数値]**  >  **[通貨]** の順に選択します。 書式設定された通貨を表示するようにセルが変化します。  
  
    地域設定が英語 (米国) の場合、既定のサンプル テキストは **[$12,345.00]** です。 通貨値の例が表示されない場合は、 **[数値]** グループで、 **[プレースホルダーのスタイル]**  >  **[サンプルの値]** の順にクリックします。  
    
    ![report-builder-placeholder-value](../reporting-services/media/report-builder-placeholder-value.png)
  
4.  `[SalesDate]`が格納されたセルをクリックします。  
  
5.  **[数値]** グループの **[日付]** を選択します。  
  
    セルに、日付の例として **[2000/1/31]** と表示されます。 日付の例が表示されない場合は、 **[数値]** グループの **[プレースホルダーのスタイル]** をクリックし、 **[サンプルの値]** をクリックします。  
  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
日付値には日付のみが表示され、売上の値は通貨として表示されます。  
  
## <a name="AdjacentGroup"></a>4.隣接する列グループを追加する  
行グループと列グループは親子リレーションシップを使用して入れ子にしたり、兄弟リレーションシップを使用して隣接させたりすることができます。  
  
このセクションでは、Subcategory 列グループに隣接する列グループを追加し、セルをコピーして新しい列グループに値を設定し、式を使用して列グループ ヘッダーの値を作成します。  
  
### <a name="to-add-an-adjacent-column-group"></a>隣接する列グループを追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  `[Subcategory]`を格納しているセルを右クリックし、 **[グループの追加]** をポイントして **[右に隣接]** をクリックします。  
  
    **[Tablix のグループ]** ダイアログ ボックスが表示されます。  
  
3.  **[グループ化]** ボックスの一覧で [SalesDate] を選択し、 **[OK]** をクリックします。  
  
    Subcategory 列グループの右側に新しい列グループが追加されます。  
  
4.  新しい列グループで `[SalesDate],` を格納しているセルを右クリックして、 **[式]** をクリックします。  
  
5.  式ボックスに次の式をコピーします。  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
    この式により、販売日から曜日が抽出されます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
6.  Subcategory 列グループで Total を格納しているセルを右クリックして、 **[コピー]** をクリックします。  
  
7.  手順 5. で作成した式が格納されているセルの直下のセルを右クリックして、 **[貼り付け]** をクリックします。  
  
8.  Ctrl&lt;/localizedText&gt; キーを押します。  
  
9. Subcategory グループで Sales 列ヘッダーとその下の 3 つのセルをクリックして右クリックし、 **[コピー]** をクリックします。  
  
10. この 4 つのセルを新しい列グループの 4 つの空のセルに貼り付けます。  
  
11. **[実行]** をクリックして、レポートをプレビューします。  
  
レポートには、月曜日と火曜日という名前の列が表示されます。 データセットには、この 2 つの曜日のデータのみが含まれています。  

![report-builder-matrix-weekdays](../reporting-services/media/report-builder-matrix-weekdays.png)
  
> [!NOTE]  
> 他の曜日のデータが含まれている場合は、レポートにそれらの曜日の列も表示されます。 各列には **Sales**という列ヘッダーと、販売区域ごとの売上合計が表示されます。  
  
## <a name="Width"></a>5.列幅を変更する  
通常、マトリックスを含むレポートは、実行すると、水平方向と垂直方向に拡張されます。 水平方向の拡張の制御は、印刷レポートに使用される Microsoft Word や Adobe PDF などの形式にレポートをエクスポートする場合、特に重要です。 レポートが複数のページにまたがって水平方向に拡張される場合、印刷レポートは理解しにくくなります。 水平方向の拡張を最小限に抑えるには、列のサイズを変更して、折り返しをしないでデータを表示できるだけの幅にします。 また、列の名前を変更して、タイトルがデータの表示に必要な幅に収まるようにすることもできます。  
  
### <a name="to-rename-and-resize-the-columns"></a>列の名前とサイズを変更するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  一番左にある Quantity 列のテキストを選択して、「 **QTY**」と入力します。  
  
    列のタイトルが、QTY になります。  
  
3.  他の 2 つの Quantity 列についても、手順 2 を実行します。
  
4.  マトリックスをクリックし、列ハンドルおよび行ハンドルをマトリックスの上部および横に表示します。  
  
    テーブルの上と横のグレーのバーは、列および行ハンドルです。  
    
    ![report-builder-column-handles](../reporting-services/media/report-builder-column-handles.png)
  
5.  一番左にある QTY 列のサイズを変更するには、列ハンドルの間の罫線をポイントします。カーソルが 2 方向の矢印の形状に変化します。 列を左にドラッグして、幅を 1/2 インチにします。  
  
    幅が 1/2 インチの列であれば、数量を表示できます。  
  
6.  その他の QTY 列についても、手順 5. を実行します。  
  
7.  **[実行]** をクリックして、レポートをプレビューします。  
  
数量を含む列は幅が狭くなり、名前が QTY になりました。  
  
## <a name="MergeCells"></a>6.マトリックス セルを結合する  
コーナー領域は、マトリックスの左上隅にあります。 マトリックス内の行グループと列グループの数に応じて、コーナー領域にセル数は変わります。 このチュートリアルで作成するマトリックスには、コーナー領域に 4 つのセルがあります。 これらのセルは、行グループと列グループの階層の深さに対応して、2 行 2 列で表示されています。 これらの 4 つのセルはこのレポートでは使用されないので、結合して 1 つのセルにします。  
  
### <a name="to-merge-matrix-cells"></a>マトリックス セルを結合するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  マトリックスをクリックし、列ハンドルおよび行ハンドルをマトリックスの上部および横に表示します。  
  
3.  Ctrl キーを押しながら、4 つのコーナー セルを選択します。  
  
4.  選択したセルを右クリックし、 **[セルの結合]** をクリックします。  
  
5.  新たに結合されたセルを右クリックして、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
6.  **[罫線]** タブで、 **[プリセット]**  >  **[なし]** の順に選択します。
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **[実行]** をクリックして、レポートをプレビューします。  
  
マトリックスの上隅のセルは表示されなくなりました。 
  
## <a name="HeaderTitle"></a>7.レポート ヘッダーおよびレポート タイトルを追加する  
レポート タイトルは、レポートの最上部に表示されます。 レポート ヘッダーがあれば、そこにレポート タイトルを配置します。レポート ヘッダーを使用しない場合は、レポート本文の一番上のテキスト ボックスに配置します。 このチュートリアルでは、レポートの一番上に配置されているテキスト ボックスを削除し、ヘッダーにタイトルを追加します。  
  
### <a name="to-add-a-report-header-and-report-title"></a>レポート ヘッダーおよびレポート タイトルを追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  レポート本文の一番上にある **"クリックしてタイトルを追加"** という文字列が含まれているテキスト ボックスを選択し、Delete キーを押します。  
  
3.  **[挿入]** タブで、 **[ヘッダー]**  >  **[ヘッダーの追加]** の順に選択します。  
  
    ヘッダーがレポート本文の先頭に追加されます。  
  
4.  **[挿入]** タブの **[テキスト ボックス]** をクリックし、テキスト ボックスをレポート ヘッダーの内側にドラッグします。 テキスト ボックスのサイズをおおよそ横 6 インチ、縦 3/4 インチにして、レポート ヘッダーの左側に配置します。  
  
5.  テキスト ボックスに「 **Territory、Subcategory、および Day ごとの売上**」と入力します。  
  
6.  入力したテキストを選択し、 **[ホーム]** タブで次のように **[フォント]** を選択します。
    * **サイズ: 24 pt**
    * **色: 茶色**
 
10. **[実行]** をクリックして、レポートをプレビューします。  
  
レポートのレポート ヘッダーにレポート タイトルが表示されます。  
  
## <a name="Save"></a>8.レポートを保存する  
レポートは、レポート サーバー、SharePoint ライブラリ、またはコンピューターに保存することができます。  
  
このチュートリアルでは、レポートをレポート サーバーに保存します。 レポート サーバーにアクセスできない場合は、レポートをコンピューターに保存してください。  
  
### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に表示されている既定の名前を「 **SalesByTerritorySubcategory**」に変更します。  
  
5.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
#### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **[名前]** に表示されている既定の名前を「 **SalesByTerritorySubcategory**」に変更します。  
  
4.  **[保存]** をクリックします。  
  
## <a name="RotateTextBox"></a>9.(省略可) テキスト ボックスを 270 度回転させる  
マトリックスを含むレポートは、実行すると、水平方向と垂直方向に拡張されます。 テキストボックスを垂直方向に、つまり 270 度回転させると、水平方向のスペースを節約できます。 表示レポートの幅は狭くなり、Microsoft Word などの形式にエクスポートした場合は、印刷ページ内に収まる可能性が高くなります。  
  
テキスト ボックスでも、テキストを水平方向または垂直方向 (上から下) に表示できます。 詳細については、「[テキスト ボックス (レポート ビルダーおよび SSRS)](../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="to-rotate-text-box-270-degrees"></a>テキスト ボックスを 270 度回転させるには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  次が格納されたセルを選択します。 `[Territory].` 

    >**注**: テキストではなくセルを選択します。 WritingMode プロパティは、セルにのみ使用できます。
    
     ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
  
3.  [プロパティ] ペインで [WritingMode] プロパティを探し、 **[既定値]** から **[Rotate270]** に変更します。  
  
    [プロパティ] ペインが表示されていない場合は、リボンの **[表示]** タブの **[プロパティ]** チェック ボックスをオンにします。  
  
4.  CanGrow プロパティが **True**に設定されていることを確認します。  
  
5.  **[ホーム]** タブの **[段落]** セクションで、垂直方向と水平方向で **[中央揃え]** をクリックして、テキストをセルの**中央**に配置します。  
 
6. Territory 列の幅を 1/2 インチに変更して、列タイトルを削除します。  
6.  **[実行]** をクリックして、レポートをプレビューします。  
  
販売区域名が垂直方向 (上から下) に表示されます。 Territory 行グループの高さは、販売区域名の長さによって変わります。  
  
## <a name="next-steps"></a>Next Steps  
これで、マトリックス レポートを作成する方法のチュートリアルは終了です。 マトリックスの詳細については、以下を参照してください。 
-    [テーブル、マトリックス、および一覧](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)
-    [マトリックスを作成する](../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)
-    [Tablix データ領域部分](../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md) 
-    [Tablix データ領域のセル、行、および列](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)  
[SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

