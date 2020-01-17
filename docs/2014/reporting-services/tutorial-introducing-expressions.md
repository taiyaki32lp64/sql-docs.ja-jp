---
title: チュートリアル:式の概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79563abac2c6a9ed64dff93667ff3d3966b70bc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098846"
---
# <a name="tutorial-introducing-expressions"></a>チュートリアル:式の概要
  式を使用すると、強力で柔軟なレポートを作成できます。 このチュートリアルでは、一般的な関数および演算子を使用した式を作成および実装する方法を説明します。 使用する、**式**名前値の連結、見て別のデータセット内の値式を作成する ダイアログ ボックスとフィールドの値に基づいた画像を表示します。  
  
 レポートは縞状で、各行には白と白でない色が交互に使用されます。 レポートには、白以外の行の色を選択するためのパラメーターが含まれています。  
  
 次の図に、ここで作成するレポートと同様のレポートを示します。  
  
 ![rs_ExpressionsTutorial](../../2014/tutorials/media/rs-expressionstutorial.gif "rs_ExpressionsTutorial")  
  
##  <a name="BackToTop"></a> 学習内容  
 このチュートリアルでは、次の方法を学習します。  
  
1.  [テーブルまたはマトリックス ウィザードから、テーブル レポートとデータセットを作成します。](#Setup)  
  
2.  [データの既定の名前を更新ソースとデータセット](#UpdateNames)  
  
3.  [表示名、初期、姓と名](#Concatenate)  
  
4.  [イメージを使用して性別を表示するには](#Gender)  
  
5.  [CountryRegion 名を検索します。](#Lookup)  
  
6.  [前回の購入からの日数のカウント](#Count)  
  
7.  [インジケーターを使用して売上比較を表示するには](#Indicator)  
  
8.  [「緑色のステータス バー」レポートのレポートを作成します。](#GreenBar)  
  
### <a name="other-optional-steps"></a>その他のオプションの手順  
  
-   [形式の日付列](#DateFormat)  
  
-   [レポート タイトルを追加します。](#Title)  
  
-   [レポートを保存します。](#Save)  
  
 このチュートリアルの推定所要時間:30 分。  
  
## <a name="requirements"></a>必要条件  
 要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/report-builder-tutorials.md) を参照してください。  
  
##  <a name="Setup"></a> 1.テーブルまたはマトリックス ウィザードを使用して表レポートとデータセットを作成する  
 表レポート、データ ソース、およびデータセットを作成します。 テーブルのレイアウト時には、少数のフィールドのみを含めておきます。 ウィザードの完了後に、列を手動で追加します。 ウィザードを使用すると、容易にテーブルをレイアウトし、スタイルを適用できます。  
  
> [!NOTE]  
>  このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
> [!NOTE]  
>  このチュートリアルでは、ウィザードに関する複数の手順を 1 つにまとめて示します。 レポート サーバーの参照、データ ソースの選択、およびデータセットの作成に関する詳細な手順については、このシリーズの最初のチュートリアルである「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。  
  
#### <a name="to-create-a-new-table-report"></a>新しい表レポートを作成するには  
  
1.  クリックして**開始**、 をポイント**プログラム**、 をクリックして[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**レポート ビルダー**、順にクリックします**レポート ビルダー**します。  
  
     **[作業の開始]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  場合、 **Getting Started** ] ダイアログ ボックスが表示されないから、**レポート ビルダー**ボタン、[**新規**します。  
  
    > [!NOTE]  
    >  レポート ビルダーの ClickOnce バージョンを使用する場合、レポート マネージャーを開き をクリックして**レポート ビルダー**、SharePoint サイト上のどの Reporting Services コンテンツの種類など、レポートが有効で、をクリックするか、または**レポート ビルダーのレポート**上、**新しいドキュメント**メニューで、**ドキュメント**の共有ドキュメント ライブラリ タブ。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで、 **[データセットを作成する]** をクリックします。  
  
5.  **[次へ]** をクリックします。  
  
6.  **[データ ソースへの接続の選択]** ページで、種類が **[SQL Server]** のデータ ソースを選択します。 一覧からデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。  
  
7.  **[次へ]** をクリックします。  
  
8.  **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
9. 次のクエリをクエリ ペインに貼り付けます。  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Unknown' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2010-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2010-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2010-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2010-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2010-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2010-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2010-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2010-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2010-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2010-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2010-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2010-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2010-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2010-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2010-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2010-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2010-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    ```  
  
     クエリには、生年月日、名前、姓、州または郡、国または地域の識別子、性別、年度累計購入額などを示す列の名前が指定されています。  
  
10. クエリ デザイナーのツール バーで、 **[実行]** ( **!** ) をクリックします。 結果セットは、20 行のデータを表示して、次の列が含まれています。FirstName、LastName、StateProvince、CountryRegionID、Gender、YTDPurchase、LastPurchase です。  
  
11. **[次へ]** をクリックします。  
  
12. **[フィールドの配置]** ページで、 **[使用できるフィールド]** ボックスから **[値]** ボックスに、次に示すフィールドを指定順にドラッグします。  
  
    -   StateProvince  
  
    -   CountryRegionID  
  
    -   LastPurchase  
  
    -   YTDPurchase  
  
     CountryRegionID および YTDPurchase には数値データが格納されているため、これらには既定で SUM 集計が適用されます。  
  
    > [!NOTE]  
    >  この時点で FirstName フィールドと LastName フィールドは含まれていません。 これらは後の手順で追加します。  
  
13. **値**一覧で、右クリックして`CountryRegionID` をクリックし、**合計**オプション。  
  
     これでもう CountryRegionID には合計が適用されていません。  
  
14. **[値]** ボックスの一覧の **[YTDPurchase]** を右クリックし、 **[合計]** をクリックします。  
  
     これでもう YTDPurchase には合計が適用されていません。  
  
15. **[次へ]** をクリックします。  
  
16. **[レイアウトの選択]** ページで、 **[次へ]** をクリックします。  
  
17. **スタイルの選択**] ページで [**スレート**、順にクリックします**完了**します。  
  
##  <a name="UpdateNames"></a> 2.データ ソースおよびデータセットの既定名を更新する  
  
#### <a name="to-update-the-default-name-of-the-data-source"></a>データ ソースの既定名を更新するには  
  
1.  レポート データ ペインで **[データ ソース]** を展開します。  
  
2.  **[DataSource1]** を右クリックし、 **[データ ソースのプロパティ]** をクリックします。  
  
3.  **[名前]** ボックスに「 **ExpressionsDataSource**」と入力します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-update-the-default-name-of-the-dataset"></a>データセットの既定名を更新するには  
  
1.  レポート データ ペインで **[データセット]** を展開します。  
  
2.  **[DataSet1]** を右クリックし、 **[データセットのプロパティ]** をクリックします。  
  
3.  **[名前]** ボックスに「 **Expressions**」と入力します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Concatenate"></a> 3.姓、名、およびイニシャルを表示する  
 姓およびイニシャルを含む名前に評価される式に、**Left** 関数および**連結** ( **&** ) 演算子を使用します。 式を手順どおりに作成することも、手順をスキップして先に進み、チュートリアルから式をコピーして **[式]** ダイアログ ボックスに貼り付けることもできます。  
  
#### <a name="to-add-the-name-column"></a>Name 列を追加するには  
  
1.  **[StateProvince]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[左]** をクリックします。  
  
     **[StateProvince]** 列の左側に、新しい列が追加されます。  
  
2.  新しい列のタイトルをクリックし、「**Name**」と入力します。  
  
3.  **[Name]** 列のデータ セルを右クリックし、 **[式]** をクリックします。  
  
4.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[テキスト]** をクリックします。  
  
5.  **[アイテム]** ボックスの一覧の **[Left]** をダブルクリックします。  
  
     **Left** 関数が式に追加されます。  
  
6.  **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
7.  **[値]** ボックスの一覧の **[FirstName]** をダブルクリックします。  
  
8.  「 **, 1)** 」と入力します。  
  
     この式により、**FirstName** 値の左から数えて 1 文字が抽出されます。  
  
9. 「 **&" "&** 」と入力します。  
  
10. **[値]** ボックスの一覧の **[LastName]** をダブルクリックします。  
  
     完成した式は、次のようになります。 `=Left(Fields!FirstName.Value, 1) &" "& Fields!LastName.Value`  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Gender"></a> 4.画像を使用して性別を表示する  
 画像を使用して個人の性別を示し、3 つ目の画像を使用して不明な性別値を識別します。 レポートに、非表示の画像を 3 つと、画像を表示するための新しい列を追加し、Gender フィールドの値に基づいて、この列に表示する画像を決定します。  
  
 レポートを縞状レポートにする際に、画像を格納するテーブル セルに色を適用するには、四角形を追加して、この四角形に画像を追加します。 四角形を使用するのは、背景色を画像には適用せず、四角形に適用できるようにするためです。  
  
 このチュートリアルでは、Windows と共にインストールされた画像を使用しますが、それ以外の任意の画像を使用することもできます。 埋め込み画像を使用する場合は、ローカル コンピューターにもレポート サーバーにもその画像をインストールする必要はありません。  
  
#### <a name="to-add-images-to-the-report-body"></a>画像をレポート本文に追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  リボンの **[挿入]** タブで **[画像]** をクリックして、レポート本文内のテーブルより下をクリックします。  
  
     **[画像のプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[インポート]** をクリックし、C:\Users\Public\Public Pictures\Sample Pictures に移動します。  
  
4.  Penguins.JPG をクリックし、 **[開く]** をクリックします。  
  
     **画像のプロパティ**ダイアログ ボックスで、をクリックして**可視性**順にクリックします、**を非表示に**オプション。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  手順 2. ～ 5. を繰り返します。ただし画像は Koala.JPG を選択します。  
  
7.  手順 2. ～ 5. を繰り返します。ただし画像は Tulips.JPG を選択します。  
  
#### <a name="to-add-the-gender-column"></a>Gender 列を追加するには  
  
1.  右クリックし、**名前**列、 をポイント**列の挿入**、 をクリックし、**右**。  
  
     右側に新しい列が追加された、**名前**列。  
  
2.  新しい列のタイトルをクリックし、「**Gender**」と入力します。  
  
#### <a name="to-add-a-rectangle"></a>四角形を追加するには  
  
-   **挿入** タブ、リボンのをクリックして**四角形**のデータ セル内をクリックし、**性別**列。  
  
     四角形がセルに追加されます。  
  
#### <a name="to-add-an-image-to-the-rectangle"></a>四角形に画像を追加するには  
  
1.  四角形内を右クリックし、[**挿入**、] をクリックし、**イメージ**します。  
  
2.  **画像のプロパティ** ダイアログ ボックスで、横にある下矢印をクリックして**このイメージを使用して、** 、Penguins.JPG など、追加した画像のいずれかを選択します。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-use-images-to-show-gender"></a>画像を使用して性別を示すには  
  
1.  内のデータ セル内のイメージを右クリックし、**性別**列をクリックします**画像のプロパティ**します。  
  
2.  **画像のプロパティ** ダイアログ ボックスで、式 をクリックして**fx**横に、**このイメージを使用して、** テキスト ボックス。  
  
3.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[プログラム フロー]** をクリックします。  
  
4.  **[アイテム]** ボックスの一覧の **[Switch]** をダブルクリックします。  
  
5.  **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
6.  **[値]** ボックスの一覧の **[Gender]** をダブルクリックします。  
  
7.  「 **="Male", "Koala",** 」と入力します。  
  
8.  **[値]** ボックスの一覧の **[Gender]** をダブルクリックします。  
  
9. 「 **="Female", "Penguins",** 」と入力します。  
  
10. **[値]** ボックスの一覧の **[Gender]** をダブルクリックします。  
  
11. 「 **="Unknown", "Tulips")** 」と入力します。  
  
     完成した式は、次のようになります。 `=Switch(Fields!Gender.Value ="Male", "Koala",Fields!Gender.Value ="Female","Penguins",Fields!Gender.Value ="Unknown","Tulips")`  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. をクリックして**OK**を閉じるためにもう一度、**画像のプロパティ** ダイアログ ボックス。  
  
14. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Lookup"></a> 5.CountryRegion 名を参照する  
 CountryRegion データセットを作成し、使用、**ルックアップ**国/地域の識別子の代わりに国/地域の名前を表示する関数。  
  
#### <a name="to-create-the-countryregion-dataset"></a>CountryRegion データセットを作成するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  レポート データ ペインで、 **[新規作成]** をクリックし、 **[データセット]** をクリックします。  
  
3.  **[レポートに埋め込まれたデータセットを使用します]** をクリックします。  
  
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
  
#### <a name="to-look-up-values-in-the-countryregion-dataset"></a>CountryRegion データセット内の値を参照するには  
  
1.  をクリックして、 **Country Region ID**列のタイトルとテキストを削除します。ID。  
  
2.  **[Country Region]** 列のデータ セルを右クリックし、 **[式]** をクリックします。  
  
3.  先頭の等号 (=) 部分を除いて、式を削除します。  
  
     式は次のようになります。 `=`  
  
4.  **式** ダイアログ ボックスで、展開**共通の関数**クリック**その他**。  
  
5.  **項目**リストで、ダブルクリック**ルックアップ**します。  
  
6.  **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
7.  **値**リストで、ダブルクリック`CountryRegionID`します。  
  
8.  カーソルが別の位置にある場合は、`CountryRegionID.Value` の直後に置きます。  
  
9. 右かっこを削除し、「 **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")** 」と入力します。  
  
     完成した式は、次のようになります。 `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
     構文、**ルックアップ**関数も、CountryRegion データセット内にある CountryRegion 値を返す CountryRegion データセット内の CountryRegionID と、ID の間に参照を指定します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="Count"></a> 6.前回の購入日からの日数をカウントする  
 列を追加し、使用、**今すぐ**関数または`ExecutionTime`個人の前回の今日からの日数を計算する組み込みのグローバル変数を購入します。  
  
#### <a name="to-add-the-days-ago-column"></a>Days Ago 列を追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **[Last Purchase]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[右]** をクリックします。  
  
     **[Last Purchase]** 列の右側に、新しい列が追加されます。  
  
3.  列ヘッダーに「 **Days Ago**」と入力します。  
  
4.  **[Days Ago]** 列のデータ セルを右クリックし、 **[式]** をクリックします。  
  
5.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[日付と時刻]** をクリックします。  
  
6.  **[アイテム]** ボックスの一覧の **[DateDiff]** をダブルクリックします。  
  
7.  カーソルが別の位置にある場合は、`DateDiff(` の直後に置きます。  
  
8.  「 **"d",** 」と入力します。  
  
9. **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
10. **値**リストで、ダブルクリック**LastPurchase**します。  
  
11. カーソルが別の位置にある場合は、`Fields!LastPurchase.Value` の直後に置きます。  
  
12. 「 **,** 」と入力します。  
  
13. **カテゴリ**一覧で、**日付と時刻の**もう一度です。  
  
14. **項目**リストで、ダブルクリック**今すぐ**します。  
  
    > [!WARNING]  
    >  運用環境のレポートでは、レポートのレンダリングごとに何度も評価される式に **Now** 関数を使用しないでください (レポートの詳細行内など)。 **Now** の値が行ごとに変わり、それが式の評価に影響して、微妙に一貫性に欠ける結果を招きます。 代わりに、使用する必要があります、`ExecutionTime`グローバル変数を[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]を提供します。  
  
15. カーソルが別の位置にある場合は、`Now(` の直後に置きます。  
  
16. 左かっこを削除し、「 **)** 」と入力します。  
  
     完成した式は、次のようになります。 `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Indicator"></a> 7.インジケーターを使用して売上比較を示す  
 新しい列を追加し、個人の年の日付 (YTD) 購入額が平均 YTD 購入額の上下でかどうかを表示するインジケーターを使用してください。 **Round** 関数では、値から小数が除去されます。  
  
 インジケーターとその状態を構成するには、多数の手順が必要です。 する場合、"、インジケーターを構成するには」の手順で前方にスキップしてこのチュートリアルから完成した式のコピー/貼り付け、**式** ダイアログ ボックス。  
  
#### <a name="to-add-the--or---avg-sales-column"></a>\+ or - AVG Sales 列を追加するには  
  
1.  **[YTD Purchase]** 列を右クリックし、 **[列の挿入]** をポイントして、 **[右]** をクリックします。  
  
     **[YTD Purchase]** 列の右側に、新しい列が追加されます。  
  
2.  新しい列のタイトルをクリックし、「 **+ or - AVG Sales**」と入力します。  
  
#### <a name="to-add-an-indicator"></a>インジケーターを追加するには  
  
1.  **挿入** タブ、リボンのをクリックして**インジケーター**、用のデータ セルをクリックして、 **+ OR-AVG sales**列。  
  
     **[インジケーターの種類の選択]** ダイアログ ボックスが表示されます。  
  
2.  アイコン セットの **[指向性]** グループ内で、3 つの灰色の矢印のセットをクリックします。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-configure-the-indicator"></a>インジケーターを構成するには  
  
1.  インジケーターを右クリックし、 **[インジケーターのプロパティ]** をクリックして、 **[値と状態]** をクリックします。  
  
2.  **[値]** ボックスの横にある式 ( **[Fx]** ) ボタンをクリックします。  
  
3.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[数学]** をクリックします。  
  
4.  **[アイテム]** ボックスの一覧の **[Round]** をダブルクリックします。  
  
5.  **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
6.  **値**リストで、ダブルクリック**YTDPurchase**します。  
  
7.  カーソルが別の位置にある場合は、`Fields!YTDPurchase.Value` の直後に置きます。  
  
8.  型  **-**  
  
9. 展開**共通の関数**もう一度クリック**集計**します。  
  
10. **項目**リストで、ダブルクリック**Avg**します。  
  
11. **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
12. **値**リストで、ダブルクリック**YTDPurchase**します。  
  
13. カーソルが別の位置にある場合は、`Fields!YTDPurchase.Value` の直後に置きます。  
  
14. 「 **, "Expressions"))** 」と入力します。  
  
     完成した式は、次のようになります。 `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. **[状態の単位]** ボックスの一覧の **[数値]** をクリックします。  
  
17. 下矢印のある行で、 **[開始]** 値のボックスの右にある **[fx]** ボタンをクリックします。  
  
18. **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[数学]** をクリックします。  
  
19. **[アイテム]** ボックスの一覧の **[Round]** をダブルクリックします。  
  
20. **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
21. **値**リストで、ダブルクリック**YTDPurchase**します。  
  
22. カーソルが別の位置にある場合は、`Fields!YTDPurchase.Value` の直後に置きます。  
  
23. 型  **-**  
  
24. 展開**共通の関数**もう一度クリック**集計**します。  
  
25. **項目**リストで、ダブルクリック**Avg**します。  
  
26. **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
27. **値**リストで、ダブルクリック**YTDPurchase**します。  
  
28. カーソルが別の位置にある場合は、`Fields!YTDPurchase.Value` の直後に置きます。  
  
29. 「 **, "Expressions")) < 0**」と入力します。  
  
     完成した式は、次のようになります。 `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. **[終了]** 値のボックスに「 **0**」と入力します。  
  
32. 水平矢印のある行をクリックし、 **[削除]** をクリックします。  
  
33. 上矢印のある行で、 **[開始]** ボックスに「 **0**」と入力します。  
  
34. **[終了]** 値のボックスの右にある **[Fx]** ボタンをクリックします。  
  
35. **式** ダイアログ ボックスで、式を作成します。 `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. **[OK]** を再度クリックして、 **[インジケーターのプロパティ]** ダイアログ ボックスを閉じます。  
  
38. **[実行]** をクリックして、レポートをプレビューします。  
  
##  <a name="GreenBar"></a> 8.「緑色のステータス バー」レポートのレポートを作成します。  
 パラメーターを使用して、レポート内で 1 行おきに適用する色を指定し、レポートを縞状にします。  
  
#### <a name="to-add-a-parameter"></a>パラメーターを追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  **レポート データ** ペインで、 **[パラメーター]** を右クリックし、 **[パラメーターの追加]** をクリックします。  
  
     **[レポート パラメーターのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[プロンプト]** に「 **Choose color**」と入力します。  
  
4.  **[名前]** に「 **RowColor**」と入力します。  
  
5.  左側のウィンドウで次のようにクリックします。**使用可能な値**します。  
  
6.  クリックして**値を指定**します。  
  
7.  **[追加]** をクリックします。  
  
8.  **ラベル**ボックスに、入力します。**黄色**  
  
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
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-apply-alternating-colors-to-detail-rows"></a>詳細行に色を交互に適用する  
  
1.  をクリックして、**ビュー**リボンのタブし、いることを確認**プロパティ**が選択されています。  
  
2.  データ セルをクリックして、**名前**列と Shift キーを押します。  
  
3.  行内のセルを 1 つおきにクリックします。  
  
4.  プロパティ ペインで、 **[BackgroundColor]** をクリックします。  
  
     カテゴリ別プロパティの一覧、プロパティ ペイン、検索すると、 **BackgroundColor**下、**入力**カテゴリ。  
  
5.  下矢印をクリックし、 **[式]** をクリックします。  
  
6.  **[式]** ダイアログ ボックスで、 **[共通の関数]** を展開し、 **[プログラム フロー]** をクリックします。  
  
7.  **[アイテム]** ボックスの一覧の **[IIf]** をダブルクリックします。  
  
8.  展開**共通の関数**クリック**集計**します。  
  
9. **項目**リストで、ダブルクリック**RunningValue**します。  
  
10. **[カテゴリ]** ボックスの一覧の **[フィールド (Expressions)]** をクリックします。  
  
11. **[値]** ボックスの一覧の **[FirstName]** をダブルクリックします。  
  
12. カーソルは既に直後にない場合`Fields!FirstName.Value`ありますに配置し、入力 **、**  
  
13. 展開**共通の関数**クリック**集計**します。  
  
14. **項目**リストで、ダブルクリック**カウント**します。  
  
15. カーソルが別の位置にある場合は、`Count(` の直後に置きます。  
  
16. 左かっこを削除し、入力 **、"Expressions")**  
  
    > [!NOTE]  
    >  Expressions は、データ行をカウントするデータセットの名前です。  
  
17. 展開**演算子**クリック**算術**。  
  
18. **項目**リストで、ダブルクリック**Mod**します。  
  
19. カーソルが別の位置にある場合は、`Mod` の直後に置きます。  
  
20. 「**2 =0,** 」と入力します。  
  
    > [!IMPORTANT]  
    >  2 という数値の前に、必ずスペースを入れてください。  
  
21. **[パラメーター]** をクリックし、 **[値]** ボックスの一覧の **[RowColor]** をダブルクリックします。  
  
22. カーソルが別の位置にある場合は、`Parameters!RowColor.Value` の直後に置きます。  
  
23. 入力 **,"White")**  
  
     完成した式は、次のようになります。 `=IIf(RunningValue(Fields!FirstName.Value,Count, "Expressions") Mod 2 =0, Parameters!RowColor.Value, "White")`  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="run-the-report"></a>レポートを実行する  
  
1.  されていない場合、**ホーム**] タブで [**ホーム**デザイン ビューに戻ります。  
  
2.  **[実行]** をクリックします。  
  
3.  **色を選択**ドロップダウン リストで、レポートの白以外のバーの色を選択します。  
  
4.  **[レポートの表示]** をクリックします。  
  
     選択した背景色が 1 行おきに適用された状態でレポートが表示されます。  
  
##  <a name="DateFormat"></a> (省略可能)形式の日付列  
 形式、 **Last Purchase**列は、日付が含まれています。  
  
#### <a name="to-format-date-column"></a>日付列の書式を設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  データ セルを右クリックし、 **Last Purchase**列をクリックします**テキスト ボックスのプロパティ**します。  
  
3.  **テキスト ボックスのプロパティ**ダイアログ ボックスで、をクリックして**数**、 をクリックして**日付**、種類をクリック **\*1/31/2000**します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Title"></a> (省略可能)レポート タイトルを追加します。  
 レポートにタイトルを追加します。  
  
#### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  
  
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  型**Sales Comparison Summary**、テキスト ボックスの外側をクリックします。  
  
3.  含むテキスト ボックスを右クリックして**Sales Comparison Summary**クリック**テキスト ボックスのプロパティ**します。  
  
4.  **[テキスト ボックスのプロパティ]** ダイアログ ボックスで、 **[フォント]** をクリックします。  
  
5.  **[サイズ]** ボックスの一覧の **[18pt]** を選択します。  
  
6.  **色**一覧で、**灰色**します。  
  
7.  選択**太字**と**斜体**します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> (省略可能)レポートを保存します。  
 レポートは、レポート サーバー、SharePoint ライブラリ、またはコンピューターに保存することができます。 詳細については、「[レポートの保存 &#40;レポート ビルダー&#41;](report-builder/saving-reports-report-builder.md)」を参照してください。  
  
 このチュートリアルでは、レポートをレポート サーバーに保存します。 レポート サーバーにアクセスできない場合は、レポートをコンピューターに保存してください。  
  
#### <a name="to-save-the-report-to-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
     "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **名前**、既定の名前を**Sales Comparison Summary**します。  
  
5.  **[保存]** をクリックします。  
  
 レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
#### <a name="to-save-the-report-to-your-computer"></a>自分のコンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **名前**、既定の名前を**Sales Comparison Summary**します。  
  
4.  **[保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [インジケーター&#40;レポート ビルダーおよび SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)   
 [画像、テキスト ボックス、四角形、および罫線 &#40;レポート ビルダーおよび SSRS&#41;](report-design/rectangles-and-lines-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
