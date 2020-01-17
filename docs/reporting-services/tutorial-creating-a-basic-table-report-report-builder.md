---
title: 'チュートリアル: 基本的な表レポートの作成 (レポート ビルダー) | Microsoft Docs'
ms.date: 06/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a97a0cfc446a32e02172d22391dec8e5ca13af6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041205"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>チュートリアル: 基本的な表レポートの作成 (レポート ビルダー)
このチュートリアルでは、サンプルの売上データに基づいて基本的な表レポートを作成する方法を説明します。 次の図に、ここで作成するレポートを示します。  
  
![SSRS_Tutorial_Basic_Table_Report](../reporting-services/media/ssrs-tutorial-basic-table-report.png)  
  

このチュートリアルの推定所要時間 : 20 分  
  
## <a name="requirements"></a>必要条件  
要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。  
  
## <a name="CreateTable"></a>1.ウィザードを使用してレポートを作成する  
テーブルまたはマトリックス ウィザードを使用してテーブルを追加します。 レポート デザイン モードと共有データセット デザイン モードの 2 つのモードがあります。 レポート デザイン モードでは、レポート データ ペインでデータを指定し、デザイン画面でレポート レイアウトを指定します。 共有データセット デザイン モードでは、他のユーザーと共有するデータセット クエリを作成します。 このチュートリアルでは、レポート デザイン モードを使用します。  
  
### <a name="to-create-a-report"></a>レポートを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
## <a name="DataConnection"></a>1a. テーブル ウィザードでデータ接続を指定する  
データ接続には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースなどの外部データ ソースに接続するときに必要な情報が含まれます。 通常、使用する接続情報と資格情報の種類はデータ ソースの所有者から提供されます。 データ接続を指定するには、レポート サーバーの共有データ ソースを使用するか、このレポートでのみ使用する埋め込みデータ ソースを作成します。  
  
このチュートリアルでは、埋め込みデータ ソースを使用します。 共有データ ソースの使用方法の詳細については、「[別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)」を参照してください。  
  
### <a name="to-create-an-embedded-data-source"></a>埋め込みデータ ソースを作成するには  
  
1.  **[データセットの選択]** ページで **[データセットを作成する]** を選択し、 **[次へ]** をクリックします。 **[データ ソースへの接続の選択]** ページが開きます。  
  
2.  **[新規作成]** をクリックします。 **[データ ソースのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[名前]** に、データ ソースの名前として「 **Product_Sales** 」と入力します。  
  
4.  **[接続の種類の選択]** で、 **[Microsoft SQL Server]** が選択されていることを確認します。  
  
5.  **[接続文字列]** に次のテキストを入力します。\<servername> には、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスの名前を入力します。  
  
    ```  
    Data Source=<servername>  
    ```  
  
    データベースからデータを取得する代わりに、データを指定するクエリを使用するため、接続文字列にデータベース名は含まれません。 詳細については、「[チュートリアルの前提条件 &#40;レポート ビルダー&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)」を参照してください。  
  
6.  **[資格情報]** タブをクリックします。外部データ ソースへのアクセスに必要な資格情報を入力します。  
  
7. 再度 [全般] タブをクリックします。 データ ソースに接続できることを確認するために、 **[接続テスト]** をクリックします。  
  
    "接続が正常に作成されました" というメッセージが表示されます。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    新しいデータ ソースが選択された状態で **[データ ソースへの接続の選択]** ページに戻ります。  
  
9. **[次へ]** をクリックします。  
  
## <a name="Query"></a>1b. テーブル ウィザードでクエリを作成する  
レポートでは、クエリが事前に定義された共有データセットを使用するか、そのレポートでのみ使用する埋め込みデータセットを作成できます。 このチュートリアルでは、埋め込みデータセットを作成します。  
  
> [!NOTE]  
> このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-query"></a>クエリを作成するには  
  
1.  **[クエリのデザイン]** ページでは、リレーショナル クエリ デザイナーが開きます。 このチュートリアルでは、テキスト ベースのクエリ デザイナーを使用します。  
  
    **[テキストとして編集]** をクリックします。 テキスト ベースのクエリ デザイナーは、クエリ ペインと結果ペインで構成されています。  
  
2.  上部の空白ボックスに、次の [!INCLUDE[tsql](../includes/tsql-md.md)] クエリを貼り付けます。  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
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
  
3.  クエリ デザイナーのツール バーで、 **[実行]** ( **!** ) をクリックします。  
  
    SalesDate、Subcategory、Product、Sales、および Quantity の各フィールドを取得するクエリが実行され、結果セットが表示されます。  
  
    結果セットの列見出しはクエリの名前に基づきます。 データセットの列見出しはフィールド名になり、レポートに保存されます。 ウィザードを完了した後、レポート データ ペインを使用してデータセット フィールドのコレクションを表示できます。  
  
4.  **[次へ]** をクリックします。  
  
## <a name="Groups"></a>1c. テーブル ウィザードでデータをグループにまとめる  
グループ化するフィールドを選択し、詳細データおよび集計データを表示する行と列を含むテーブルをデザインします。  
  
### <a name="to-organize-data-into-groups"></a>データをグループにまとめるには  
  
1.  **[フィールドの配置]** ページで、Product を **[値]** にドラッグします。  
  
2.  Quantity を **[値]** にドラッグして Product の下に配置します。  
  
    Quantity は Sum 関数 (数値フィールドの既定の集計関数) を使用して自動的に集計されます。 値は [Sum(Quantity)] です。  
  
    [Sum (quantity)] の横の矢印を選択し、使用可能なその他の集計関数を表示します。 集計関数は変更しないでください。  
  
3.  Sales を **[値]** にドラッグして [Sum(Quantity)] の下に配置します。  
  
    Sales は Sum 関数を使用して集計されます。 値は [Sum(Sales)] です。  
  
    手順 1. ～ 3. で、テーブルに表示するデータが指定されます。  
  
4.  SalesDate を **[行グループ]** にドラッグします。  
  
5.  Subcategory を **[行グループ]** にドラッグして SalesDate の下に配置します。  
  
    手順 4. および 5. で、フィールドの値がまず日付でまとめられ、次にその日付の製品サブカテゴリでまとめられます。  
  
6.  **[次へ]** をクリックします。  
  
## <a name="Subtotals"></a>1d. テーブル ウィザードで小計行と合計行を追加する  
グループを作成したら、フィールドの集計値を表示する行を追加して書式を設定できます。 すべてのデータを表示するか、グループ化されたデータの展開と折りたたみをユーザーが対話的に行えるようにするかを選択できます。  
  
### <a name="to-add-subtotals-and-totals"></a>小計と合計を追加するには  
  
1.  **[レイアウトの選択]** ページの **[オプション]** で、 **[小計と総計を表示]** が選択されていることを確認します。  
  
2.  **[ブロック、小計は下]** が選択されていることを確認します。  
  
    ウィザードのプレビュー ペインに、5 行を含むテーブルが表示されます。 レポートを実行すると、各行は次のように表示されます。  
  
    1.  1 行目はテーブルで 1 回表示され、列見出しを示します。  
  
    2.  2 行目は販売注文の行アイテムごとに 1 回表示され、製品名、注文数量、および行の合計を示します。  
  
    3.  3 行目は販売注文ごとに 1 回表示され、注文あたりの小計を示します。  
  
    4.  4 行目は注文日ごとに 1 回表示され、1 日あたりの小計を示します。  
  
    5.  5 行目はテーブルで 1 回表示され、総計を示します。  
  
3.  **[グループの展開/折りたたみ]** オプションをオフにします。 このチュートリアルで作成するレポートでは、ユーザーが親グループ階層を展開して子グループ行および詳細行を表示できるようにするドリル ダウン機能は使用されません。  
  
4.  **[次へ]** をクリックしてテーブルを確認し、 **[完了]** をクリックします。  
  
テーブルがデザイン画面に追加されます。 テーブルには 5 列および 5 行が含まれています。 行グループ ペインに、SalesDate、Subcategory、および Details の 3 つの行グループが表示されます。 詳細データは、データセット クエリによって取得されるすべてのデータです。  
  
## <a name="FormatCurrency"></a>2.データに通貨の書式を設定する  
既定では、Sales フィールドの集計データは通常の数値として表示されます。 このフィールドを書式設定して、数値を通貨として表示します。   
  
### <a name="to-format-a-currency-field"></a>通貨フィールドを書式設定するには  
  
1.  [デザイン] ビューで、書式設定されたテキスト ボックスとプレース ホルダー テキストのサンプル値を表示するには、 **[ホーム]** タブの **[数値]** グループで、 **[プレース ホルダーのスタイル]** アイコンの横の矢印をクリックし **[サンプル値]** をクリックします。  
  
2.   [Sales] 列の 2 行目 (列見出しの次の行) のセルをクリックして下にドラッグし、 `[Sum(Sales)]`が格納されたすべてのセルを選択します。  
  
3.  **[ホーム]** タブの **[数値]** グループで、 **[通貨]** ボタンをクリックします。 書式設定された通貨を表示するようにセルが変化します。  
  
    地域設定が英語 (米国) の場合、既定のサンプル テキストは **[$12,345.00]** です。 通貨値の例が表示されない場合は、 **[ホーム]** タブの **[数値]** グループで、 **[プレース ホルダーのスタイル]** アイコンの横の矢印をクリックし、 **[サンプル値]** をクリックします。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
Sales の集計値が通貨として表示されます。  
  
## <a name="FormatDate"></a>3.データに日付の書式を設定する  
既定では、SalesDate フィールドに日付と時刻の両方が表示されます。 このフィールドを書式設定して、日付のみを表示できます。  
  
### <a name="to-format-a-date-field-as-the-default-format"></a>日付フィールドの書式を既定の書式に設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  `[SalesDate]`が格納されたセルをクリックします。  
  
3.  リボンの **[ホーム]** タブの **[数値]** グループで、 **[日付]** を選択します。  
  
    セルに、日付の例として **[2000/1/31]** と表示されます。 日付の例が表示されない場合は、 **[ホーム]** タブの **[数値]** グループで、 **[プレース ホルダーのスタイル]** アイコンの横の矢印をクリックし、 **[サンプル値]** をクリックします。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
SalesDate の値が、既定の日付の書式で表示されます。  
  
### <a name="to-change-the-date-format-to-a-custom-format"></a>日付の書式をカスタム書式に変更するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  `[SalesDate]`が格納されたセルを選択します。  
  
3.  **[ホーム]** タブの **[数値]** グループで、右下隅の矢印をクリックしてダイアログ ボックスを開きます。  
  
    **[テキスト ボックスのプロパティ]** ダイアログ ボックスが表示されます。  
  
4.  [カテゴリ] ペインで、 **[日付]** が選択されていることを確認します。  
  
5.  **[型]** ペインで **[2000 年 1 月 31 日]** を選択します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    セルに、日付の例として **[2000 年 1 月 31 日]** と表示されます。  
  
7.  **[実行]** をクリックして、レポートをプレビューします。  
  
SalesDate の値が、月の数字ではなく月の名前で表示されます。  
  
## <a name="Width"></a>4.列幅を変更する  
テーブルの各セルには、既定でテキスト ボックスが含まれます。 テキスト ボックスは、ページを表示するときにテキストに合わせて垂直方向に拡張されます。 表示されるレポートでは、各行がその行で最も高いテキスト ボックスの高さに拡張されます。 デザイン画面の行の高さは、表示されるレポートの行の高さには影響しません。  
  
各行の垂直方向の領域を小さくするには、列の幅を広げ、列で想定されるテキスト ボックスの内容が 1 行に収まるようにします。  
  
### <a name="to-change-the-width-of-table-columns"></a>テーブル列の幅を変更するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  テーブルをクリックし、列ハンドルおよび行ハンドルをテーブルの上部および横に表示します。  
  
    テーブルの上と横のグレーのバーは、列および行ハンドルです。  
  
3.  列ハンドルの間の罫線をポイントします。カーソルが 2 方向の矢印の形状に変化します。 希望のサイズに列をドラッグします。 たとえば、製品名が 1 行に表示されるように Product 列を広げます。  
  
4.  **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Title"></a>5.レポート タイトルを追加する  
レポート タイトルは、レポートの最上部に表示されます。 レポート ヘッダーがあれば、そこにレポート タイトルを配置します。レポート ヘッダーを使用しない場合は、レポート本文の一番上のテキスト ボックスに配置します。 このチュートリアルでは、自動的にレポート本文の一番上に配置されるテキスト ボックスを使用します。  
  
テキストの語句や文字のフォントのスタイル、サイズ、および色を変更して、テキストをさらに強調することもできます。 詳細については、「[テキスト ボックス内のテキストの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Product Sales**」と入力し、テキスト ボックスの外側をクリックします。  
  
3.  **Product Sales** が含まれているテキスト ボックスを右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
4.  **[テキスト ボックスのプロパティ]** ダイアログ ボックスで、 **[フォント]** をクリックします。  
  
5.  **[サイズ]** ボックスの一覧の **[18pt]** を選択します。  
  
6.  **[色]** ボックスの一覧の **[コーンフラワー ブルー]** を選択します。  
  
7.  **[太字]** を選択します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>6.レポートを保存する  
レポートをレポート サーバーまたは自分のコンピューターに保存します。 レポート サーバーに保存しない場合は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のいくつかの機能 (レポート パーツ、サブレポートなど) が使用できなくなります。  
  
### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **[ファイル]**  >  **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** の **[無題]** を **Product_Sales**に置き換えます。  
  
5.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **[ファイル]**  >  **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **[名前]** の **[無題]** を **Product Sales**に置き換えます。  
  
4.  **[保存]** をクリックします。  
  
## <a name="Export"></a>7.レポートをエクスポートする  
レポートは、Microsoft Excel や CSV (コンマ区切り) ファイル形式など、別の形式にエクスポートすることができます。 詳しくは、「 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)におけるページ割り付けの制御規則を理解しておく必要があります。  
  
このチュートリアルでは、レポートを Excel にエクスポートします。また、レポートのプロパティを設定して、ブック見出しに独自の名前を指定します。  
  
### <a name="to-specify-the-workbook-tab-name"></a>ブック見出しの名前を指定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  デザイン画面で、レポート外の任意の場所をクリックします。  
  
3.  [プロパティ] ペインの [InitialPageName] を探し、「 **Product Sales Excel**」と入力します。  
  
    > [!NOTE]  
    > プロパティ ペインが表示されていない場合は、 **[表示]** タブの **[プロパティ]** を選択します。  
    > [プロパティ] ペインにプロパティが表示されない場合、ペイン上部の **アルファベット** ボタンを選択し、すべてのプロパティをアルファベット順に並べ替えます。   
  
### <a name="to-export-a-report-to-excel"></a>レポートを Excel にエクスポートするには  
  
1.  **[実行]** をクリックして、レポートをプレビューします。  
  
2.  リボンの **[エクスポート]**  >  **[Excel]** をクリックします。  
  
    が開きます。  
  
3.  **[名前を付けて保存]** ダイアログ ボックスで、ファイルの保存先に進みます。  
  
4.  **[ファイル名]** ボックスに「 **Product_Sales_Excel**」と入力します。  
  
5.  ファイルの種類が **Excel (\*.xlsx)** であることを確認します。  
  
6.  **[保存]** をクリックします。  
  
### <a name="to-view-the-report-in-excel"></a>Excel でレポートを表示するには  
  
1.  ブックを保存するフォルダーを開き、 **Product_Sales_Excel.xlsx**をダブルクリックします。  
  
2.  ブック見出しの名前が「 **Product Sales Excel**」であることを確認します。  
  
## <a name="next-steps"></a>Next Steps  
これで、基本的なテーブル レポートを作成する方法のチュートリアルは終了です。 テーブルの詳細については、「[テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)  
[SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

