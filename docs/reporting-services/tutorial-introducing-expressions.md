---
title: 'チュートリアル: 式の概要 | Microsoft Docs'
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a26065cc1d65e5c187123ead990888aa4de0e60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63295623"
---
# <a name="tutorial-introducing-expressions"></a>チュートリアル: 式の概要
[!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] のこのチュートリアルでは、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 強力かつ柔軟性のあるページネーション付きのレポートを作成するために、式と共に一般的な関数や演算子を使用します。 

名前値の連結、独立したデータセット内の値の参照、フィールド値に基づいた色の表示などを行うための式を作成します。  
  
レポートは縞模様で、各行には白と白でない色が交互に使用されます。 レポートには、白以外の行の色を選択するためのパラメーターが含まれています。  
  
この図に、ここで作成するレポートと同様のレポートを示します。  
  
![report-builder-expression-tutorial-in-browser](../reporting-services/media/report-builder-expression-tutorial-in-browser.png) 
  
このチュートリアルの推定所要時間: 30 分。  
  
## <a name="requirements"></a>必要条件  
要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/prerequisites-for-tutorials-report-builder.md) を参照してください。  
  
## <a name="Setup"></a>1.テーブルまたはマトリックス ウィザードを使用して表レポートとデータセットを作成する  
このセクションでは、表レポート、データ ソース、データセットを作成します。 テーブルのレイアウト時には、少数のフィールドのみを含めておきます。 ウィザードの完了後に、列を手動で追加します。 ウィザードを使用すると、容易にテーブルをレイアウトできます。  
  
> [!NOTE]  
> このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-table-report"></a>表形式レポートを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで、 **[データセットを作成する]**  >  **[次へ]** をクリックします。  
  
6.  **[データ ソースへの接続の選択]** ページで、種類が **[SQL Server]** のデータ ソースを選択します。 一覧からデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。  

    > [!NOTE]  
    > 適切な権限を持っている限り、選択するデータ ソースは重要ではありません。 データ ソースからはデータを取得しません。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
7.  **[次へ]** をクリックします。  
  
8.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
9. 次のクエリをクエリ ペインに貼り付けます。  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Female' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2015-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2015-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2015-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2015-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2015-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2015-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2015-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2015-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2015-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2015-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2015-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2015-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2015-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2015-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2015-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2015-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2015-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    ```  

  
10. クエリ デザイナーのツール バーで、 **[実行]** ( **!** ) をクリックします。 結果セットでは、FirstName、LastName、StateProvince、CountryRegionID、Gender、YTDPurchase、LastPurchase の各列に 23 行のデータが表示されます。  

    ![report-builder-expression-tutorial-query-as-text](../reporting-services/media/report-builder-expression-tutorial-query-as-text.png)
  
11. **[次へ]** をクリックします。  
  
12. **[フィールドの配置]** ページで、 **[使用できるフィールド]** ボックスから **[値]** ボックスに、次に示すフィールドを指定順にドラッグします。  
  
    -   StateProvince   
    -   CountryRegionID  
    -   LastPurchase  
    -   YTDPurchase  
  
    CountryRegionID と YTDPurchase には数値データが格納されているため、これらには既定で SUM 集計が適用されますが、あなたは SUM 集計を望みません。  
   
13. **[値]** ボックスの一覧の **[CountryRegionID]** を右クリックし、 **[合計]** チェック ボックスをオフにします。  
  
    これでもう CountryRegionID には合計が適用されていません。  
  
14. **[値]** ボックスの一覧の **[YTDPurchase]** を右クリックし、 **[合計]** をクリックします。  
  
    これでもう YTDPurchase には合計が適用されていません。  
    
    ![report-builder-expression-not-sum](../reporting-services/media/report-builder-expression-not-sum.png)
  
15. **[次へ]** をクリックします。  
  
16. **[レイアウトの選択]** ページで、既定の設定をすべてそのまま選択し、 **[次へ]** をクリックします。  

    ![report-builder-expression-tutorial-choose-layout](../reporting-services/media/report-builder-expression-tutorial-choose-layout.png)
  
17. **[完了]** をクリックします。  
  
## <a name="UpdateNames"></a>2.データ ソースおよびデータセットの既定名を更新する  
  
### <a name="to-update-the-default-name-of-the-data-source"></a>データ ソースの既定名を更新するには  
  
1.  レポート データ ペインで **[データ ソース]** フォルダーを展開します。  
  
2.  **[DataSource1]** を右クリックし、 **[データ ソースのプロパティ]** をクリックします。  
  
3.  **[名前]** ボックスに「 **ExpressionsDataSource**」と入力します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-update-the-default-name-of-the-dataset"></a>データセットの既定名を更新するには  
  
1.  レポート データ ペインで **[データセット]** フォルダーを展開します。  
  
2.  **[DataSet1]** を右クリックし、 **[データセットのプロパティ]** をクリックします。  

    ![report-builder-expression-tutorial-rename-dataset](../reporting-services/media/report-builder-expression-tutorial-rename-dataset.png)
  
3.  **[名前]** ボックスに「 **Expressions**」と入力します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Concatenate"></a>3.名のイニシャルと姓を表示する  
このセクションでは、イニシャルと姓を含む名前に評価される式に、 **Left** 関数および **連結** ( **&** ) 演算子を使用します。 式を手順どおりに作成することも、手順をスキップして先に進み、チュートリアルから式をコピーして **[式]** ダイアログ ボックスに貼り付けることもできます。   
  
1.  **[StateProvince]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[左]** をクリックします。  
  
    **[StateProvince]** 列の左側に、新しい列が追加されます。 
    
    ![report-builder-expression-tutorial-insert-column](../reporting-services/media/report-builder-expression-tutorial-insert-column.png) 
  
2.  新しい列のヘッダーをクリックし、「 **Name**」と入力します。  
  
3.  **[Name]** 列のデータ セルを右クリックし、 **[式]** をクリックします。  

    ![report-builder-expression-tutorial-insert-expression](../reporting-services/media/report-builder-expression-tutorial-insert-expression.png)
  
4.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[テキスト]** をクリックします。  
  
5.  **[アイテム]** ボックスの一覧の **[Left]** をダブルクリックします。  
  
    **Left** 関数が式に追加されます。  
    
    ![report-builder-expression-tutorial-left-function](../reporting-services/media/report-builder-expression-tutorial-left-function.png)
  
6.  **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
7.  **[値]** ボックスの一覧の **[FirstName]** をダブルクリックします。  
  
8.  「 **, 1)** 」と入力します。  
  
    この式により、 **FirstName** 値の左から数えて 1 文字が抽出されます。  
  
9. 「 **&". "&** 」と入力します。  

    式の後にピリオドとスペースが追加されます。
  
10. **[値]** ボックスの一覧の **[LastName]** をダブルクリックします。  
  
    完成した式は `=Left(Fields!FirstName.Value, 1) &". "& Fields!LastName.Value`です。  
    
    ![report-builder-expression-tutorial-complete-name-expression](../reporting-services/media/report-builder-expression-tutorial-complete-name-expression.png)
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. **[実行]** をクリックして、レポートをプレビューします。  

## <a name="DateFormat"></a>(省略可能) 日付列、通貨列、ヘッダー行の書式を設定する  
このセクションでは、日付を含む **[Last Purchase]** 列と通貨を含む [YTDPurchase] 列の書式を設定します。 ヘッダー行の書式も設定します。  
  
### <a name="to-format-the-date-column"></a>日付列の書式を設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **[Last Purchase]** 列のデータ セルを選択し、 **[ホーム]** タブの **[数値]** セクションで **[日付]** を選択します。  

    ![report-builder-expression-tutorial-date-format](../reporting-services/media/report-builder-expression-tutorial-date-format.png)
  
3.  **[数値]** セクションでもう一度、 **[プレースホルダーのスタイル]** の隣にある矢印をクリックし、 **[サンプルの値]** を選択します。 

    ![report-builder-expression-tutorial-sample-values](../reporting-services/media/report-builder-expression-tutorial-sample-values.png)

    これで選択した書式設定のサンプルを表示できます。 
  
### <a name="to-format-the-currency-column"></a>通貨の書式を設定するには

- **[YTDPurchase]** 列のデータ セルを選択し、 **[数値]** セクションで **[通貨記号]** を選択します。
 
### <a name="to-format-the-column-headers"></a>列ヘッダーの書式を設定するには

1. 列ヘッダーの行を選択します。

2. **[ホーム]** タブの **[段落]** セクションで、 **[左]** を選択します。 

    ![report-builder-expression-tutorial-format-headings](../reporting-services/media/report-builder-expression-tutorial-format-headings.png)

3. **[実行]** をクリックして、レポートをプレビューします。 

レポートのここまでの完成状態はこのようになります。日付、通貨、列のヘッダーが書式設定されています。

![report-builder-expression-tutorial-preview-formatted](../reporting-services/media/report-builder-expression-tutorial-preview-formatted.png)

  
## <a name="Gender"></a>4.色を使用して性別を表示する  
このセクションでは、個人の性別を示す色を追加します。 色を表示するための新しい列を追加し、Gender フィールドの値に基づいてその列に表示する色を決定します。  
  
レポートを縞模様にするとき、その表のセルに適用した色を維持するには、四角形を追加し、四角形に背景色を追加します。  
    
 
### <a name="to-add-an-mf-column"></a>M/F 列を追加するには  
  
1.  **[Name]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[左]** をクリックします。  
  
    **[Name]** 列の左側に、新しい列が追加されます。  
  
2.  新しい列のヘッダーをクリックし、「 **M/F**」と入力します。  
  
### <a name="to-add-a-rectangle"></a>四角形を追加するには  
  
1.   **[挿入]** タブで **[四角形]** をクリックし、 **[M/F]** 列のデータ セル内をクリックします。  
  
     四角形がセルに追加されます。  
     
     ![report-builder-expression-tutorial-insert-rectangle](../reporting-services/media/report-builder-expression-tutorial-insert-rectangle.png)
  
2. **M/F** と **Name** の間の分割線をドラッグし、 **M/F** 列を狭くします。

    ![report-builder-expression-tutorial-narrow-column](../reporting-services/media/report-builder-expression-tutorial-narrow-column.png)
  
### <a name="to-use-color-to-show-gender"></a>色を使用して性別を示すには  
  
1.  **[M/F]** 列のデータ セル内の四角形を右クリックし、 **[四角形のプロパティ]** をクリックします。  
  
2.  **[四角形のプロパティ]** ダイアログ ボックスの **[塗りつぶし]** タブで、 **[塗りつぶしの色]** ボックスの横にある式 ( **[fx]** ) ボタンをクリックします。  
  
3.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[プログラム フロー]** をクリックします。  
  
4.  **[アイテム]** ボックスの一覧の **[Switch]** をダブルクリックします。  
  
5.  **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
6.  **[値]** ボックスの一覧の **[Gender]** をダブルクリックします。  
  
7.  「 **="Male",** 」と入力します (コンマを含む)。

8. **[カテゴリ]** ボックスの一覧で **[定数]** をクリックし、 **[値]** ボックスの一覧で **[コーンフラワー ブルー]** をクリックします。

    ![report-builder-expression-tutorial-color-expression-cornflower-blue](../reporting-services/media/report-builder-expression-tutorial-color-expression-cornflower-blue.png)

9. その後にコンマを入力します。 
  
5.  **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[Gender]** をもう一度ダブルクリックします。  
  
7.  「 **="Female",** 」と入力します (コンマを含む)。 

8. **[カテゴリ]** ボックスの一覧で **[定数]** をクリックし、 **[値]** ボックスの一覧で **[トマト]** をクリックします。

13. その後に終わりかっこ **)** を入力します。 
  
    完成した式は `=Switch(Fields!Gender.Value ="Male", "CornflowerBlue",Fields!Gender.Value ="Female","Tomato")`です。  
    
    ![report-builder-expression-tutorial-color-expression-complete](../reporting-services/media/report-builder-expression-tutorial-color-expression-complete.png)
  
12. **[OK]** をクリックします。さらに **[OK]** をクリックし、 **[四角形のプロパティ]** ダイアログ ボックスを閉じます。  
  
14. **[実行]** をクリックして、レポートをプレビューします。  

    ![report-builder-expression-tutorial-preview-m-f-column](../reporting-services/media/report-builder-expression-tutorial-preview-m-f-column.png)

### <a name="to-format-the-color-rectangles"></a>色の四角形の書式を設定するには

1. **[デザイン]** をクリックしてデザイン ビューに戻ります。  

16. **[M/F]** 列の四角形を選択します。 プロパティ ペインの [罫線] セクションでこれらのプロパティを設定します。

    - BorderColor = 白
    - BorderStyle = 実線
    - BorderWidth = 5pt
    
    ![report-builder-expression-tutorial-format-m-f-column](../reporting-services/media/report-builder-expression-tutorial-format-m-f-column.png)

18. **[実行]** をクリックし、レポートを再びプレビューします。 今度は色のブロックの周りに空白が表示されます。

    ![report-builder-expression-tutorial-preview-formatted-m-f-column](../reporting-services/media/report-builder-expression-tutorial-preview-formatted-m-f-column.png)  
  
## <a name="Lookup"></a>5.CountryRegion 名を参照する  
このセクションでは、CountryRegion データセットを作成し、 **Lookup** 関数を使用して、国/地域の識別子の代わりに国/地域の名前を表示します。  
  
### <a name="to-create-the-countryregion-dataset"></a>CountryRegion データセットを作成するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  レポート データ ペインで、 **[新規作成]** をクリックし、 **[データセット]** をクリックします。  
  
3.  [**データセットのプロパティ] で **[レポートに埋め込まれたデータセットを使用します]** をクリックします。  
  
4.  **[データ ソース]** ボックスの一覧の [ExpressionsDataSource] をクリックします。  
  
5.  **[名前]** ボックスに「 **CountryRegion**」と入力します。  
  
6.  クエリの種類に **[テキスト]** が選択されていることを確認し、 **[クエリ デザイナー]** をクリックします。  
  
7.  **[テキストとして編集]** をクリックします。  
  
8.  次のクエリをコピーし、クエリ ペインに貼り付けます。  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. **[実行]** ( **!** ) をクリックしてクエリを実行します。  
  
    クエリ結果は国/地域の識別子と名前です。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **[OK]** を再度クリックして、 **[データセットのプロパティ]** ダイアログ ボックスを閉じます。  

     **[レポート データ]** 列に 2 つ目のデータセットが表示されます。
  
### <a name="to-look-up-values-in-the-countryregion-dataset"></a>CountryRegion データセット内の値を参照するには  
  
1.  **[Country Region ID]** 列ヘッダーをクリックし、テキストの **ID**という部分を削除し、「 **Country Region**」にします。  
  
2.  **[Country Region]** 列のデータ セルを右クリックし、 **[式]** をクリックします。  
  
3.  先頭の等号 (=) 部分を除いて、式を削除します。  
  
    式は次のようになります。 `=`  
  
4.  **[式]** ダイアログ ボックスで **[共通の関数]** を展開し、 **[その他]** をクリックします。 **[アイテム]** ボックスの一覧で **[参照]** をダブルクリックします。  
  
6.  **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[CountryRegionID]** をもう一度ダブルクリックします。  
  
8.  `CountryRegionID.Value`のすぐ後にカーソルを置き、「 **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")** 」と入力します。  
  
    完成した式は、次のようになります。 `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
    この **Lookup** 関数の構文は、Expressions データセットの CountryRegionID と、CountryRegion データセットから CountryRegion 値を返す CountryRegion データセットの ID の間の参照を指定します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Count"></a>6.前回の購入日からの日数をカウントする  
このセクションでは、列を追加し、 **Now** 関数または `ExecutionTime` 組み込みグローバル変数を使用して、顧客の前回購入日から今日までの日数を計算します。  
  
### <a name="to-add-the-days-ago-column"></a>Days Ago 列を追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **[Last Purchase]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[右]** をクリックします。  
  
    **[Last Purchase]** 列の右側に、新しい列が追加されます。  
  
3.  列ヘッダーに「 **Days Ago**」と入力します。  
  
4.  **[Days Ago]** 列のデータ セルを右クリックし、 **[式]** をクリックします。  
  
5.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[日付と時刻]** をクリックします。  
  
6.  **[アイテム]** ボックスの一覧の **[DateDiff]** をダブルクリックします。  
  
7.  `DateDiff(`のすぐ後に「 **"d",** 」と入力します (引用符の "" とコンマを含めます)。 
  
9. **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[LastPurchase]** をもう一度ダブルクリックします。  
  
11. `Fields!LastPurchase.Value`のすぐ後に「 **,** 」を入力します (コンマを入力します)。 
  
13. **[カテゴリ]** ボックスの一覧で **[日付と時刻]** をもう一度クリックし、 **[アイテム]** ボックスの一覧で **[Now]** をダブルクリックします。  
  
    > [!WARNING]  
    > 運用環境のレポートでは、レポートのレンダリングごとに何度も評価される式に **Now** 関数を使用しないでください (レポートの詳細行内など)。 **Now** の値が行ごとに変わり、それが式の評価に影響して、微妙に一貫性に欠ける結果を招きます。 これを回避するには、 `ExecutionTime` で提供されている [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] グローバル変数を使用してください。  
  
15. `Now(`の後の始めかっこを削除し、終わりかっこ **)** を入力します。  
  
    完成した式は `=DateDiff("d", Fields!LastPurchase.Value, Now)`です。  
    
    ![report-builder-expression-tutorial-date-since-last-purchase](../reporting-services/media/report-builder-expression-tutorial-date-since-last-purchase.png)
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

11. **[実行]** をクリックして、レポートをプレビューします。  
  
## <a name="Indicator"></a>7.インジケーターを使用して売上比較を示す  
このセクションでは、新しい列を追加し、インジケーターを使用して、個人の年度累計 (YTD) 購入額が平均 YTD 購入額を上回るか下回るかを示します。 **Round** 関数では、値から小数が除去されます。  
  
インジケーターとその状態を構成するには、多くの手順を踏む必要があります。 必要であれば、「インジケーターを構成するには」の手順をスキップして先に進み、このチュートリアルから完成した式をコピーして、 **[式]** ダイアログ ボックスに貼り付けることができます。  
  
### <a name="to-add-the--or---avg-sales-column"></a>\+ or - AVG Sales 列を追加するには  
  
1.  **[YTD Purchase]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[右]** をクリックします。  
  
    **[YTD Purchase]** 列の右側に、新しい列が追加されます。  
  
2.  列ヘッダーをクリックし、「 **+ or - AVG Sales**」と入力します。  
  
### <a name="to-add-an-indicator"></a>インジケーターを追加するには  
  
1.  **[挿入]** タブで **[インジケーター]** をクリックし、 **[+ or - AVG Sales]** 列のデータ セルをクリックします。  
  
    **[インジケーターの種類の選択]** ダイアログ ボックスが表示されます。  
  
2.  アイコン セットの **[指向性]** グループ内で、3 つの灰色の矢印のセットをクリックします。  

    ![report-builder-expression-tutorial-select-indicator](../reporting-services/media/report-builder-expression-tutorial-select-indicator.png)
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-configure-the-indicator"></a>インジケーターを構成するには  
  
1.  インジケーターを右クリックし、 **[インジケーターのプロパティ]** をクリックして、 **[値と状態]** をクリックします。  
  
2.  **[値]** ボックスの横にある式 ( **[Fx]** ) ボタンをクリックします。  
  
3.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[数学]** をクリックします。  
  
4.  **[アイテム]** ボックスの一覧の **[Round]** をダブルクリックします。  
  
5.  **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[YTDPurchase]** をもう一度ダブルクリックします。  
  
7.  `Fields!YTDPurchase.Value`のすぐ後に「  **-** 」を入力します (マイナス記号を入力します)。 
  
9. **[共通の関数]** をもう一度展開して **[集計]** をクリックし、 **[アイテム]** ボックスの一覧で **[Avg]** をダブルクリックします。  
  
11. **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[YTDPurchase]** をもう一度ダブルクリックします。  
  
13. `Fields!YTDPurchase.Value`のすぐ後に「 **, "Expressions"))** 」と入力します。  
  
    完成した式は `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`です。  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. **[状態の単位]** ボックスの一覧の **[数値]** をクリックします。  
  
17. 下矢印のある行で、 **[開始]** 値のボックスの右にある **[fx]** ボタンをクリックします。  

    ![report-builder-expression-tutorial-indicator-start](../reporting-services/media/report-builder-expression-tutorial-indicator-start.png)
  
18. **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[数学]** をクリックします。  
  
19. **[アイテム]** ボックスの一覧の **[Round]** をダブルクリックします。  
  
20. **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[YTDPurchase]** をもう一度ダブルクリックします。  
  
22. `Fields!YTDPurchase.Value`のすぐ後に「  **-** 」を入力します (マイナス記号を入力します)。 
  
24. **[共通の関数]** をもう一度展開して **[集計]** をクリックし、 **[アイテム]** ボックスの一覧で **[Avg]** をダブルクリックします。  
  
26. **[カテゴリ]** ボックスの一覧で **[フィールド (Expressions)]** をクリックし、 **[値]** ボックスの一覧で **[YTDPurchase]** をもう一度ダブルクリックします。  
  
28. `Fields!YTDPurchase.Value` のすぐ後に「 **, "Expressions")) < 0**」と入力します。  
  
    完成した式は、次のようになります。 `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. **[終了]** 値のボックスに「 **0**」と入力します。  
  
32. 水平矢印のある行をクリックし、 **[削除]** をクリックします。  

    ![report-builder-expression-tutorial-delete-indicator-state](../reporting-services/media/report-builder-expression-tutorial-delete-indicator-state.png)
    
    これで矢印は 2 つだけになりました。上矢印または下矢印です。
  
33. 上矢印のある行で、 **[開始]** ボックスに「 **0**」と入力します。  
  
34. **[終了]** 値のボックスの右にある **[Fx]** ボタンをクリックします。  
  
35. **[式]** ダイアログ ボックスで、 **100** を削除し、次の式を作成します。 `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. **[OK]** を再度クリックして、 **[インジケーターのプロパティ]** ダイアログ ボックスを閉じます。  
  
38. **[実行]** をクリックして、レポートをプレビューします。  

    ![report-builder-expression-tutorial-preview-indicator](../reporting-services/media/report-builder-expression-tutorial-preview-indicator.png)
  
## <a name="GreenBar"></a>8.縞模様のレポートを作成する  
レポートを読む人がレポート内で 1 行おきに適用する色を指定し、レポートを縞模様にできるようにパラメーターを作成します。  
  
### <a name="to-add-a-parameter"></a>パラメーターを追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **レポート データ** ペインで、 **[パラメーター]** を右クリックし、 **[パラメーターの追加]** をクリックします。  

    ![report-builder-expression-tutorial-add-parameter](../reporting-services/media/report-builder-expression-tutorial-add-parameter.png)
  
    **[レポート パラメーターのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[プロンプト]** に「 **Choose color**」と入力します。  
  
4.  **[名前]** に「 **RowColor**」と入力します。  
  
5.  **[使用できる値]** タブで **[値の指定]** をクリックします。  
  
7.  **[追加]** をクリックします。  
  
8.  **[ラベル]** ボックスに「 **Yellow**」と入力します。  
  
9. **[値]** ボックスに「 **Yellow**」と入力します。  
  
10. **[追加]** をクリックします。  
  
11. **[ラベル]** ボックスに「 **Green**」と入力します。  
  
12. **[値]** ボックスに「 **PaleGreen**」と入力します。  
  
13. **[追加]** をクリックします。  
  
14. **[ラベル]** ボックスに「 **Blue**」と入力します。  
  
15. **[値]** ボックスに「 **LightBlue**」と入力します。  
  
16. **[追加]** をクリックします。  
  
17. **[ラベル]** ボックスに「 **Pink**」と入力します。  
  
18. **[値]** ボックスに「 **Pink**」と入力します。  

    ![report-builder-expression-tutorial-parameter-available](../reporting-services/media/report-builder-expression-tutorial-parameter-available.png)
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-apply-alternating-colors-to-detail-rows"></a>詳細行に色を交互に適用する  
  
1.   独自の背景色を持つ **[M/F]** 列のセルを除き、データ行のすべてのセルを選択します。  

     ![report-builder-expression-tutorial-select-banded](../reporting-services/media/report-builder-expression-tutorial-select-banded.png)
  
4.  プロパティ ペインで、 **[BackgroundColor]** をクリックします。 

     プロパティ ペインが表示されない場合、 **[表示]** タブの **[プロパティ]** ボックスをオンにします。  
  
    プロパティ ペインでプロパティがカテゴリ別に一覧表示されている場合、 **[その他]** カテゴリに **BackgroundColor** があります。  
  
5.  下矢印をクリックし、 **[式]** をクリックします。  

    ![report-builder-expression-tutorial-banded-color-property](../reporting-services/media/report-builder-expression-tutorial-banded-color-property.png)
  
6.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[プログラム フロー]** をクリックします。  
  
7.  **[アイテム]** ボックスの一覧の **[IIf]** をダブルクリックします。  
  
8.  **[共通の関数]** で **[その他]** をクリックし、 **[アイテム]** ボックスの一覧で **[RowNumber]** をダブルクリックします。  

9. **RowNumber(** のすぐ後に「 **Nothing) MOD 2,** 」と入力します。
  
8. **[パラメーター]** をクリックし、 **[値]** ボックスの一覧の **[RowColor]** をダブルクリックします。  
  
22. `Parameters!RowColor.Value` のすぐ後に「 **, "White")** 」を入力します。  
  
    完成した式は `=IIF(RowNumber(Nothing) MOD 2, Parameters!RowColor.Value, "White")`です。  
    
    ![report-builder-expression-tutorial-banded-color-expressn](../reporting-services/media/report-builder-expression-tutorial-banded-color-expressn.png)
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="run-the-report"></a>レポートを実行する  
  
1.  **[ホーム]** タブで **[実行]** をクリックします。  

    レポートを実行しても、白以外の縞の色を選択するまでレポートが表示されません。
  
3.  **[色の選択]** ボックスの一覧で、レポートの白以外の縞の色を選択します。  
    
    ![report-builder-expression-tutorial-select-color](../reporting-services/media/report-builder-expression-tutorial-select-color.png)
  
4.  **[レポートの表示]** をクリックします。  
  
    選択した背景色が 1 行おきに適用された状態でレポートが表示されます。 
    
    ![report-builder-expression-tutorial-preview-banded](../reporting-services/media/report-builder-expression-tutorial-preview-banded.png) 
  
## <a name="Title"></a>(省略可能) レポート タイトルを追加する  
レポートにタイトルを追加します。  
  
### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「 **Sales Comparison Summary**」と入力し、テキストを選択します。  
  
3.  **[ホーム]** タブの **[フォント]** で次のように設定します。

    -  サイズ = 18
    -  色 = 灰色
    -  太字
  
4.  **[ホーム]** タブで **[実行]** をクリックします。  
  
3.  レポートの白以外の縞の色を選択し、 **[レポートの表示]** をクリックします。  
  
## <a name="Save"></a>(省略可能) レポートを保存する  
レポートは、レポート サーバー、SharePoint ライブラリ、またはコンピューターに保存することができます。 詳細については、「[レポートの保存 &#40;レポート ビルダー&#41;](../reporting-services/report-builder/saving-reports-report-builder.md)」を参照してください。  
  
このチュートリアルでは、レポートをレポート サーバーに保存します。 レポート サーバーにアクセスできない場合は、レポートをコンピューターに保存してください。  
  
### <a name="to-save-the-report-to-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **[ファイル]** メニューの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  レポートに名前を付けて **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。

これで [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web ポータルでレポートが表示されます。

![report-builder-expression-tutorial-final-in-browser](../reporting-services/media/report-builder-expression-tutorial-final-in-browser.png)

   
## <a name="see-also"></a>参照  
[式 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
[式の例 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
[インジケーター &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
[画像、テキスト ボックス、四角形、および罫線 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)  
[テーブル &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[レポート データセット &#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
  

