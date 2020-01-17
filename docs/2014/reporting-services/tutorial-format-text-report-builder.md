---
title: チュートリアル:書式文字列 (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dc58232ed3025063fb329392b58895ed667465f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098898"
---
# <a name="tutorial-format-text-report-builder"></a>チュートリアル:テキストを書式設定する (レポート ビルダー)
  このチュートリアルでは、さまざまな方法でテキストの書式設定を実習します。 空のレポートと、データ ソースおよびデータセットを設定した後、必要な手順を選んで進めることができます。  
  
 次の図に、ここで作成するレポートと同様のレポートを示します。  
  
 ![rs_FormatTextFinal](../../2014/tutorials/media/rs-formattextfinal.gif "rs_FormatTextFinal")  
  
 途中の手順で一度わざと正しくない方法を試し、それがなぜ問題なのかを確認します。 その後、必要な効果が得られるように問題を修正します。  
  
 このチュートリアルで作成するレポートについては、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] レポート ビルダーのサンプル レポートに発展版が含まれています。 このサンプル レポートおよびその他のダウンロードの詳細については、次を参照してください。[レポート ビルダーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=184851)します。  
  
##  <a name="BackToTop"></a> 学習内容  
  
### <a name="set-up-the-report"></a>レポートを設定する  
 1. [空のレポートを作成、データ ソースおよびデータセット](#CreateReport)  
  
 2. [(間違ってし正しく) は、レポート デザイン画面にフィールドを追加します。](#AddField)  
  
 3. [レポート デザイン画面にテーブルを追加します。](#AddTable)  
  
### <a name="pick-and-choose"></a>選択する  
 [レポートにハイパーリンクを追加します。](#AddHyperlink)  
  
 [レポート内のテキストを回転させる](#RotateText)  
  
 [HTML 形式でテキストを表示する方法](#FormatHTML)  
  
 [通貨の書式設定](#FormatCurrency)  
  
 [レポートを保存します。](#Save)  
  
 このチュートリアルの推定所要時間:20 分  
  
## <a name="requirements"></a>必要条件  
 要件に関する詳細については、「[チュートリアルの前提条件 (レポート ビルダー)](../reporting-services/report-builder-tutorials.md)」を参照してください。  
  
##  <a name="CreateReport"></a> 空のレポートを作成、データ ソースおよびデータセット  
  
#### <a name="to-create-a-blank-report"></a>空のレポートを作成するには  
  
1.  クリックして**開始**、 をポイント**プログラム**、 をポイント[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]**レポート ビルダー**、順にクリックします**レポート ビルダー**します。  
  
    > [!NOTE]  
    >  **[作業の開始]** ダイアログ ボックスが表示されます。 表示されない場合は、レポート ビルダーのボタンの **[新規作成]** をクリックします。  
  
2.  **[作業の開始]** ダイアログ ボックスの左ペインで **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[空のレポート]** をクリックします。  
  
#### <a name="to-create-a-data-source"></a>データ ソースを作成するには  
  
1.  レポート データ ペインで、 **[新規作成]** をクリックし、 **[データ ソース]** をクリックします。  
  
2.  **[名前]** ボックスに、「**TextDataSource**」と入力します。  
  
3.  **[レポートに埋め込まれた接続を使用する]** をクリックします。  
  
4.  接続の種類が Microsoft SQL Server であることを確認したら **[接続文字列]** ボックスに次のように入力します。**Data Source = \<servername>**  
  
    > [!NOTE]  
    >  式\<servername >、たとえば report001 など、SQL Server データベース エンジンのインスタンスがインストールされているコンピューターを指定します。 このチュートリアルでは、特定のデータは必要ありません。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] データベースへの接続だけが必要です。 **[データ ソース接続]** の一覧に既にデータ ソース接続が表示されている場合は、データ ソース接続を選択してから次の手順「データセットを作成するには」に進みます。 詳細については、[「別の方法でデータ接続を取得する &#40;レポート ビルダー&#41;」](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)を参照してください。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-create-a-dataset"></a>データセットを作成するには  
  
1.  レポート データ ペインで、 **[新規作成]** をクリックし、 **[データセット]** をクリックします。  
  
2.  データ ソースが **TextDataSource**であることを確認します。  
  
3.  **[名前]** ボックスに、「**TextDataset**」と入力します。  
  
4.  クエリの種類に **[テキスト]** が選択されていることを確認してから、 **[クエリ デザイナー]** をクリックします。  
  
5.  **[テキストとして編集]** をクリックします。  
  
6.  次のクエリをクエリ ペインに貼り付けます。  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  [実行]\( **!** ) をクリックしてクエリを実行します。  
  
     クエリの結果が、レポートに表示できるデータになります。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="AddField"></a> レポート デザイン画面にフィールドを追加します。  
 レポート内にデータセットのフィールドを表示する場合、まず、デザイン画面に直接フィールドをドラッグしたくなるかもしれません。 ここでは、その方法がうまくいかない理由と、正しい方法について学びます。  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>レポートにフィールドを追加する (うまくいかない方法を試す) には  
  
1.  [レポート データ] ペインからデザイン画面に **FullName** フィールドをドラッグします。  
  
     レポート ビルダーとして表される内に式テキスト ボックスを作成する\<Expr >。  
  
2.  **[実行]** をクリックします。  
  
     1 つのレコードがあることに注意してください。 **Fernando Ross**、アルファベット順には、クエリの最初のレコード。 フィールドの表示が繰り返されず、フィールド内の他のレコードが表示されません。  
  
3.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
4.  式を選択して\<Expr >、テキスト ボックスにします。  
  
5.  プロパティ ペインの **[値]** プロパティが次のように表示されています (プロパティ ペインが表示されていない場合は、 **[表示]** タブの **[プロパティ]** チェック ボックスをオンにします)。  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
     `First` 関数は、フィールド内の最初の値のみを取得するように設計されているので、最初の値のみが取得されました。  
  
     デザイン画面にフィールドを直接ドラッグすることによって、テキスト ボックスが作成されました。 テキスト ボックス自体はデータ領域ではないので、レポート データセットのデータを表示しません。 テーブル、マトリックス、一覧などのデータ領域のテキスト ボックスが、データを表示します。  
  
6.  テキスト ボックスを選択して (式を選択している場合は、&lt;localizedText&gt;Esc&lt;/localizedText&gt; キーを押してからテキスト ボックスを選択します)、&lt;localizedText&gt;Del&lt;/localizedText&gt; キーを押します。  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>レポートにフィールドを追加する (正しい結果を得る) には  
  
1.  リボンの **[挿入]** タブの **[データ領域]** で、 **[一覧]** をクリックします。 デザイン画面でマウスをドラッグして、幅約 5 センチ メートル、高さ約 3 センチ メートルのボックスを作成します。  
  
2.  作成したリスト ボックスに [レポート データ] ペインから **FullName** フィールドをドラッグします。  
  
     今度は、レポート ビルダーによって、 `[FullName]` という式が表示されたテキスト ボックスが作成されます。  
  
3.  **[実行]** をクリックします。  
  
     今回は、ボックスの表示が繰り返され、クエリ内のすべてのレコードが表示されています。  
  
4.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
5.  テキスト ボックス内の式を選択します。  
  
6.  [プロパティ] ペインの **[値]** プロパティが次のように表示されます。  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
     テキスト ボックスを一覧データ領域にドラッグすることによって、データセット内のデータが表示されます。  
  
7.  リスト ボックスを選択し、<localizedText>Del</localizedText> キーを押します。  
  
##  <a name="AddTable"></a> レポート デザイン画面にテーブルを追加します。  
 ハイパーリンクと回転したテキストを配置する必要があるありますには、このテーブルを作成します。  
  
#### <a name="to-add-a-table-to-the-report"></a>テーブルをレポートに追加するには  
  
1.  **挿入** メニューのをクリックして**テーブル**、 をクリックし、**テーブル ウィザード**します。  
  
2.  **データセットの選択**ページ、新しいテーブル/マトリックス ウィザードの次のようにクリックします**このレポートまたは共有データセットの既存のデータセットを選択**、 をクリック**TextDataset (このレポートで)** 。、 をクリックし、**次**します。  
  
3.  **フィールドの配置** ページで、ドラッグ、 **Territory**、 **LinkText**、および**製品**フィールドを**行グループ**、ドラッグ、 **Sales**フィールドを**値**、順にクリックします**次**します。  
  
4.  **レイアウトの選択** ページで、クリア、**グループの展開/折りたたみ**チェック ボックスをクリックして、テーブル全体を表示できるように**次**。  
  
5.  **スタイルの選択**] ページで [**スレート**、順にクリックします**完了**します。  
  
6.  テーブルをドラッグして、タイトルのブロックの下へ移動します。  
  
7.  **[実行]** をクリックします。  
  
     テーブルは問題ないように見えますが、合計行が 2 か所に含まれています。 **LinkText**フィールドは合計行は必要ありません。  
  
8.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
9. 含むテキスト ボックスを右クリックして`[LinkText]`、 をクリック**セルの分割**します。  
  
10. 下の空のセルを選択して、`[LinkText]`セル、SHIFT キーを押しながらし、し、その右側に 2 つのセルを選択します。**合計**セル、**製品**列と`[Sum(Sales)]`内のセル**Sales**列。  
  
11. これら 3 つのセルで選択されている、それらのセルの 1 つを右クリックし、をクリックして**行の削除**します。  
  
12. **[実行]** をクリックします。  
  
##  <a name="AddHyperlink"></a> レポートにハイパーリンクを追加します。  
 ここでは、前のセクションで作成したテーブルのテキストに、ハイパーリンクを追加します。  
  
#### <a name="to-add-a-hyperlink-to-the-report"></a>レポートにハイパーリンクを追加するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  `[LinkText]`を含むセルを右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
3.  **テキスト ボックスのプロパティ**ボックスで、**アクション**します。  
  
4.  クリックして**URL に移動する**します。  
  
5.  **URL の選択**ボックスで、 **[URL]** 、順にクリックします**OK**します。  
  
6.  テキストが、他と同じに見えることに注目してください。 リンク テキストのように表示する必要があります。  
  
7.  [ `[LinkText]`] を選択します。  
  
8.  **フォント**のセクション、**ホーム** タブで、をクリックして、**に下線を引く**ボタンをクリックし、ドロップダウン矢印をクリックし、**色** ボタンをクリックして**青い**します。  
  
9. **[実行]** をクリックします。  
  
     テキストがリンクらしく見えるようになりました。  
  
10. リンクをクリックします。 コンピューターがインターネットに接続している場合は、レポート ビルダー ヘルプのトピックが表示されたブラウザーが開きます。  
  
##  <a name="RotateText"></a> レポート内のテキストを回転させる  
 ここでは、前のセクションで使用したテーブル内のテキストの一部を回転します。  
  
#### <a name="to-rotate-text"></a>テキストを回転するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに戻ります。  
  
2.  次を含むセルをクリックします。 `[Territory].`  
  
3.  **[ホーム]** タブの **[フォント]** セクションで、 **[太字]** ボタンをクリックします。  
  
4.  プロパティ ペインが表示されていない場合は、 **[表示]** タブの **[プロパティ]** チェック ボックスをオンにします。  
  
5.  プロパティ ペインで、WritingMode プロパティを見つけます。  
  
    > [!NOTE]  
    >  プロパティ ペインのプロパティがカテゴリごとに整理されている場合、WritingMode は、 **[ローカライズ]** カテゴリ内にあります。 テキストではなくセルを選択してあることを確認します。 WritingMode は、テキストではなくテキスト ボックスのプロパティです。  
  
6.  リスト ボックスで、次のようにクリックします。 **Rotate270**します。  
  
7.  **ホーム**] タブで、**段落**セクションで、[、**中間**と**Center**セルの中央にテキストを検索するボタン垂直方向および水平方向にします。  
  
8.  [実行]\( **!** ) をクリックします。  
  
 `[Territory]` セル内のテキストがセルの下から上に向かって縦に表示されます。  
  
##  <a name="FormatHTML"></a> HTML 形式でテキストを表示する方法  
  
#### <a name="to-display-text-formatted-as-html"></a>HTML 形式のテキストを表示するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  **[挿入]** タブで **[テキスト ボックス]** をクリックしてから、デザイン画面のテーブルの下でマウスをドラッグして、幅約 10 センチ メートル、高さ約 8 センチ メートルのボックスを作成します。  
  
3.  次のテキストをコピーして、テキスト ボックスに貼り付けます。  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  テキスト ボックス内のすべてのテキストを選択します。  
  
     これは、テキスト ボックスではなくテキストのプロパティなので、1 つのテキスト ボックス内にプレーンテキストと HTML タグを使用したテキストの両方のスタイルを混在させることもできます。  
  
5.  選択したテキスト全体を右クリックして、 **[テキスト プロパティ]** をクリックします。  
  
6.  **全般** ページ **マークアップの種類**、 をクリックして**HTML - HTML タグのスタイルとして解釈**します。  
  
7.  **[OK]** をクリックします。  
  
8.  [実行] ( **!** ) をクリックして、レポートをプレビューします。  
  
 テキスト ボックス内のテキストが、見出し、段落、箇条書きとして表示されます。  
  
##  <a name="FormatCurrency"></a> 通貨の書式設定  
  
#### <a name="to-format-numbers-as-currency"></a>数値を通貨として書式設定するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  テーブルの一番上の `[Sum(Sales)]`が含まれているセルをクリックし、&lt;localizedText&gt;Shift&lt;/localizedText&gt; キーを押しながらテーブルの一番下の `[Sum(Sales)]`が含まれているセルをクリックします。  
  
3.  **[ホーム]** タブの **[数値]** グループで、 **[通貨]** ボタンをクリックします。  
  
4.  (省略可能)**ホーム**] タブで、**数**グループで、[、**プレース ホルダーのスタイル**ボタンをクリックし、をクリックして**サンプル値**番号がどのように表示するには書式設定します。  
  
5.  (省略可) **[ホーム]** タブの **[数値]** グループで、 **[小数点表示桁下げ]** ボタンを 2 回クリックして、表示されるドルの値にセントの部分が含まれないようにします。  
  
6.  [実行]\( **!** ) をクリックして、レポートをプレビューします。  
  
 レポートには書式が設定されたデータが表示され、読みやすくなりました。  
  
##  <a name="Save"></a> レポートを保存します。  
 レポートは、レポート サーバー、SharePoint ライブラリ、またはコンピューターに保存することができます。  
  
 このチュートリアルでは、レポートをレポート サーバーに保存します。 レポート サーバーにアクセスできない場合は、レポートをコンピューターに保存してください。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
     "レポート サーバーに接続しています" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に表示されている既定の名前を任意の名前に変更します。  
  
5.  **[保存]** をクリックします。  
  
 レポートがレポート サーバーに保存されます。 接続しているレポート サーバーの名前がウィンドウ下部のステータス バーに表示されます。  
  
#### <a name="to-save-the-report-on-your-computer"></a>コンピューターにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[デスクトップ]** 、 **[マイ ドキュメント]** 、または **[マイ コンピューター]** をクリックして、レポートを保存するフォルダーを参照します。  
  
3.  **[名前]** に表示されている既定の名前を任意の名前に変更します。  
  
4.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 レポート ビルダーでのテキストの書式設定する方法はたくさんあります[チュートリアル。自由形式レポートを作成する&#40;レポート ビルダー&#41; ](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)他の例が含まれています。  
  
## <a name="see-also"></a>参照  
 [チュートリアル&#40;レポート ビルダー&#41;](report-builder-tutorials.md)   
 [レポート アイテムの書式設定 (レポート ビルダーおよび SSRS)](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [SQL Server 2014 のレポート ビルダー](report-builder/report-builder-in-sql-server-2016.md)  
  
  
