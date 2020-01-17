---
title: 'チュートリアル: レポートへのパラメーターの追加 (レポート ビルダー) | Microsoft Docs'
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a50e32eb3d13e2b78705a3f2ba4fd63e9ccd442
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252139"
---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>チュートリアル: レポートへのパラメーターの追加 (レポート ビルダー)
このチュートリアルでは、 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] の改ページ調整されたレポートにパラメーターを追加し、レポート閲覧者が 1 つまたは複数の値でレポート データをフィルター処理できるようにします。 
  
![report-builder-parameter-tutorial](../reporting-services/media/report-builder-parameter-tutorial.png)

レポート パラメーターは、データセット クエリに追加したクエリ パラメーターごとに自動で作成されます。 パラメーターのデータ型により、パラメーターがレポート ビューアー ツール バーに表示される方法が決まります。 
   
> [!NOTE]  
> このチュートリアルでは、ウィザードに関する複数の手順を 1 つにまとめて示します。 レポート サーバーの参照、データ ソースの選択、データセットの作成に関する詳細な手順については、このシリーズの最初のチュートリアル (「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」) を参照してください。  
  
このチュートリアルの推定所要時間 : 25 分  
  
## <a name="requirements"></a>必要条件  
要件の詳細については、[「チュートリアルの前提条件 (レポート ビルダー)」](../reporting-services/prerequisites-for-tutorials-report-builder.md) を参照してください。  
  
## <a name="Setup"></a>1.テーブルまたはマトリックス ウィザードでマトリックス レポートとデータセットを作成する  
マトリックス レポート、データ ソース、およびデータセットを作成します。  
  
> [!NOTE]  
> このチュートリアルのクエリにはデータ値が含まれているため、外部のデータ ソースを必要としません。 このため、クエリが非常に長くなっています。 ビジネス環境でクエリにデータを含めることはありません。 これは、学習に使用することのみを目的としています。  
  
### <a name="to-create-a-new-matrix-report"></a>新しいマトリックス レポートを作成するには  
  
1.  コンピューター、[Web ポータル、SharePoint 統合モードのいずれかから](../reporting-services/report-builder/start-report-builder.md) レポート ビルダーを起動します [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが開きます。  
  
    **[新しいレポートまたはデータセット]** ダイアログ ボックスが表示されない場合、 **[ファイル]** メニューで **[新規作成]** を選択します。  
  
2.  左ペインで、 **[新しいレポート]** が選択されていることを確認します。  
  
3.  右ペインで、 **[テーブルまたはマトリックス ウィザード]** をクリックします。  
  
4.  **[データセットの選択]** ページで、 **[データセットを作成する]**  >  **[次へ]** をクリックします。  
  
7.  **[データ ソースへの接続の選択]** ページで、既存のデータ ソースを選択するか、レポート サーバーを参照してデータ ソースを選択します。 種類が **SQL Server**である任意のデータ ソースを選択します。  
      
8.  **[次へ]** をクリックします。  

    資格情報の入力が必要な場合があります。    
     
9. **[クエリのデザイン]** ページで、 **[テキストとして編集]** をクリックします。  
  
10. 上部にある空のペインに次のクエリを貼り付けます。  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
    Contoso サンプル データベースから抜粋した単純化されたカメラの販売データを使って値を指定する関係上、このクエリでは、複数の [!INCLUDE[tsql_md](../includes/tsql-md.md)] SELECT ステートメントの結果が共通テーブル式の中で結合されています。 サブカテゴリは、デジタル カメラ、デジタル一眼レフ (SLR) カメラ、ビデオ カメラ、およびアクセサリです。  
  
11. クエリ デザイナーのツール バーで、 **[実行]** ( **!** ) をクリックしてデータを表示します。   
  
    結果セットは StoreID 列、Subcategory 列、Quantity 列に、4 店舗のサブカテゴリごとの販売済み商品数量を示す 11 行のデータが表示されます。店舗名は結果セットには含まれません。 このチュートリアルで後ほど、店舗 ID に対応する店舗の名前を別のデータセットから参照します。  
  
    クエリ パラメーターは存在しません。 以降、このチュートリアルの中でクエリ パラメーターを追加していきます。   
  
12. **[次へ]** をクリックします。  
  
## <a name="CompleteWizard"></a>2.ウィザードでデータを整理し、レイアウトを選択する  
ウィザードは、データを表示するための最初のデザインを提供します。 ウィザードのプレビュー ペインでは、テーブルやマトリックスのデザインを完了する前にデータのグループ化の結果を表示できます。  
  
### <a name="to-organize-data-into-groups"></a>データをグループにまとめるには  
  
1.  **[フィールドの配置]** ページで、Subcategory を **[行グループ]** にドラッグします。  
  
2.  StoreID を **[列グループ]** にドラッグします。  
  
3.  Quantity を **[値]** にドラッグします。  
  
    販売数量の値を、店舗ごとに 1 つの列で、サブカテゴリごとにグループ化された行に整理しました。  
  
4.  **[次へ]** をクリックします。  
  
5.  **[レイアウトの選択]** ページの **[オプション]** で、 **[小計と総計を表示]** が選択されていることを確認します。  
  
    レポートを実行すると、最後の列にはすべての店舗のサブカテゴリごとの合計数量が表示され、最後の行には店舗ごとのすべてのサブカテゴリの合計数量が表示されます。  
  
6.  **[次へ]** をクリックします。  
  
8.  **[完了]** をクリックします。  
  
    マトリックスがデザイン画面に追加されます。 マトリックスは 3 行× 3 列で表示されます。 先頭行のセルの内容は、Subcategory、[StoreID]、および Total です。 2 番目の行のセルの内容は、サブカテゴリ、店舗ごとの販売品目の数量、および、すべての店舗のサブカテゴリごとの合計数量を表す式です。 最後の行のセルには、店舗ごとの総計が表示されます。  
      
    ![ssRB_ParamTut_Design](../reporting-services/media/ssrb-paramtut-design.png)  
  
9. マトリックス内をクリックし、最初の列の端にカーソルを合わせてハンドルをドラッグして、列の幅を拡張します。  
  
   ![ssRB_ParamTut_Drag](../reporting-services/media/ssrb-paramtut-drag.png)  
  
10. **[実行]** をクリックして、レポートをプレビューします。  
  
レポート サーバーでレポートが実行され、タイトルとレポートの処理時刻がレポートに表示されます。  

![ssRB_ParamTut__Preview1](../reporting-services/media/ssrb-paramtut-preview1.png)
  
ここでは、列見出しに店舗 ID は表示されますが店舗名は表示されません。 後ほど、店舗 ID と店舗名のペアが格納されているデータセットで店舗名を参照する式を追加します。  
  
## <a name="Query"></a>3.クエリ パラメーターを追加してレポート パラメーターを作成する  
クエリ パラメーターをクエリに対して追加すると、名前、プロンプト、およびデータ型に既定のプロパティを持つ単一値のレポート パラメーターがレポート ビルダーによって自動的に作成されます。  
  
### <a name="to-add-a-query-parameter"></a>クエリ パラメーターを追加するには  
  
1.  **[デザイン]** をクリックして再びデザイン ビューに切り替えます。  
  
2.  レポート データ ペインで、 **[データセット]** フォルダーを展開して **DataSet1**を右クリックし、 **[クエリ]** をクリックします。  
  
3.  クエリの最後の行に、次の [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** 句を追加します。  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
    この **WHERE** 句によって、取得されたデータが、クエリ パラメーター *\@StoreID* で指定した店舗 ID に限定されます。  
  
4.  クエリ デザイナーのツール バーで、 **[実行]** ( **!** ) をクリックします。 **[クエリ パラメーターの定義]** ダイアログ ボックスが開き、クエリ パラメーター *\@StoreID* の値を入力するように求められます。  
  
5.  **[パラメーター値]** に「 **200**」と入力します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    結果セットには、店舗 ID **200**について、Accessories、Camcorders、および Digital SLR Cameras の販売数量が表示されます。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  レポート データ ペインで **[パラメーター]** フォルダーを展開します。  
  
*\@StoreID* というレポート パラメーターと、レポート パラメーターをレイアウトできるパラメーター ペインが存在するようになったことがわかります。   
  
![ssRB_ParamPane](../reporting-services/media/ssrb-parampane.png)  
  
パラメーター ペインが表示されない場合は、 **[表示]** メニューの **[パラメーター]** をクリックします。  
  
## <a name="ChangeDefaultProperties"></a>4.レポート パラメーターの既定のデータ型とその他のプロパティを変更する  
プロパティの既定値は、レポート パラメーターの作成後に調整することができます。  
  
### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>レポート パラメーターの既定のデータ型を変更するには  
  
既定では、作成したパラメーターのデータ型は **[テキスト]** です。 店舗 ID は整数なので、データ型を [整数] に変更します。  
  
1.  **[パラメーター]** ノードのレポート データ ペインで、 *\@StoreID* を右クリックしてから、 **[パラメーターのプロパティ]** をクリックします。  
  
2.  **[プロンプト]** に「 **Store identifier?** 」と入力します。 レポートを実行すると、レポート ビューアーのツール バーにこのテキストが表示されます。  
  
3.  **[データ型]** のドロップダウン リストから **[整数]** を選択します。  
  
4.  このダイアログ ボックスのそれ以外の設定は、既定値のままにします。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **[実行]** をクリックして、レポートをプレビューします。 レポート ビューアーには、 *\@StoreID* の入力を求めるプロンプト **Store Identifier?** が表示されます。  
  
7.  レポート ビューアー ツール バーで、店舗 ID の横に「 **200**」と入力し、 **[レポートの表示]** をクリックします。  
  
![SSRB_ParamTutStoreID](../reporting-services/media/ssrb-paramtutstoreid.png)  
  
## <a name="AddDataset"></a>4a. 使用可能な値と表示名を提供するデータセットを追加する  
レポート閲覧者がパラメーターの有効な値しか入力できないようにするには、選択可能な値のドロップダウン リストを作成します。 値は、データセットまたは指定した一覧から取得できます。 使用可能な値は、パラメーターへの参照を含まないクエリが格納されているデータセットから指定する必要があります。  
  
### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>パラメーターの有効な値のデータセットを作成するには  
  
1.  **[デザイン]** をクリックしてデザイン ビューに切り替えます。  
  
2.  レポート データ ペインで、 **[データセット]** フォルダーを右クリックし、 **[データセットの追加]** をクリックします。  
  
3.  **[名前]** に、「 **Stores**」と入力します。  
  
4.  **[レポートに埋め込まれたデータセットを使用します]** を選択します。  
  
5.  **[データ ソース]** のドロップダウン リストから、最初の手順で使用したデータ ソースを選択します。  
  
6.  **[クエリの種類]** で **[テキスト]** が選択されていることを確認します。  
  
7.  **[クエリ]** に、次のテキストを貼り付けます。  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    レポート データ ペインの **Stores** データセット ノードに、StoreID フィールドと StoreName フィールドが表示されます。  
  
## <a name="AvailableValues"></a>4b. 一覧に表示される使用可能な値を指定する 
使用できる値のソースとなるデータセットを作成したら、レポートのプロパティで、レポート ビューアー ツール バーの有効な値のドロップダウン リストに値を設定するために使用するデータセットとフィールドを指定します。  
  
### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>パラメーターに使用できる値をデータセットから提供するには  
  
1.  レポート データ ペインでパラメーター *\@StoreID* を右クリックしてから、 **[パラメーターのプロパティ]** をクリックします。  
  
2.  **[使用できる値]** をクリックし、 **[クエリから値を取得]** をクリックします。  
  
3.  **[データセット]** ドロップダウン リストで **[Stores]** をクリックします。  
  
4.  **[値フィールド]** ドロップダウン リストで [StoreID] をクリックします。  
  
5.  **[ラベル フィールド]** ドロップダウン リストで [StoreName] をクリックします。 ラベル フィールドによって値の表示名が指定されます。  
  
6.  **[全般]** をクリックします。  
  
7.  **[プロンプト]** で、 **Sをre Identifer?** を **Sをre name?** に変更します。  
  
    これで、レポート閲覧者は、店舗 ID ではなく、店舗名の一覧から選択できるようになりました。 ただし、パラメーターは店舗名ではなく店舗 ID に基づいているので、パラメーターのデータ型は **[整数]** のままです。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. レポートをプレビューします。  
  
    レポート ビューアー ツール バーのパラメーター テキスト ボックスがドロップダウン リストに変わり、" **値を選択してください**" と表示されるようになりました。  
  
10. ドロップダウン リストから Contoso Catalog Store を選択し、 **[レポートの表示]** をクリックします。  
  
レポートには、店舗 ID **200**について、Accessories、Camcorders、および Digital SLR Cameras の販売数量が表示されます。  
  
## <a name="DefaultValues"></a>4c. 既定値を指定する 
各パラメーターの既定値を指定して、レポートが自動的に実行されるようにすることができます。  
  
### <a name="to-specify-a-default-value-from-a-dataset"></a>データセットから既定値を指定するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  レポート データ ペインで *\@StoreID* を右クリックし、 **[パラメーターのプロパティ]** をクリックします。  
  
3.  **[既定値]** をクリックし、 **[クエリから値を取得]** をクリックします。  
  
4.  **[データセット]** ドロップダウン リストで **[Stores]** をクリックします。  
  
5.  **[値フィールド]** ドロップダウン リストで [StoreID] をクリックします。  
  
6.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)]  
  
7.  レポートをプレビューします。  
  
*\@StoreID* に対して、レポート ビューアーによって値 "Contoso North America Online Store" が表示されます。これがデータセット **Stores** の結果セットの最初の値であるためです。 レポートには、店舗 ID **199**について、Digital Cameras の販売数量が表示されます。  
  
### <a name="to-specify-a-custom-default-value"></a>カスタムの既定値を指定するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  レポート データ ペインで *\@StoreID* を右クリックし、 **[パラメーターのプロパティ]** をクリックします。  
  
3.  **[既定値]**  >  **[値を指定]**  >  **[追加]** をクリックします。 新しい値の行が追加されます。  
  
4.  **[値]** に「 **200**」と入力します。  
  
5.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)] 
  
6.  レポートをプレビューします。  
  
*\@StoreID* に対して、レポート ビューアーによって "Contoso Catalog Store" が表示されます。これが店舗 ID **200** の表示名であるためです。 レポートには、店舗 ID **200**について、Accessories、Camcorders、および Digital SLR Cameras の販売数量が表示されます。  
  
## <a name="NameValue"></a>4d. 名前/値のペアを参照する  
データセットには、ID と対応する名前フィールドの両方が含まれている場合があります。 ID しかない場合は、名前と値のペアが格納されている作成済みのデータセットで対応する名前を参照できます。  
  
### <a name="to-look-up-a-value-from-a-dataset"></a>データセットから値を参照するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  デザイン画面のマトリックスの先頭行の列見出しで、 `[StoreID]` を右クリックし、 **[式]** をクリックします。  
  
3.  式ペインで、先頭の **等号** (=) を除くすべてのテキストを削除します。  
  
4.  **[カテゴリ]** で、 **[共通の関数]** を展開して **[その他]** をクリックします。 アイテム ペインに関数セットが表示されます。  
  
5.  [アイテム] で、 **[参照]** をダブルクリックします。 式ペインに " `=Lookup(`" と表示されます。 サンプル ペインに Lookup 構文の例が表示されます。  
  
6.  次の式を入力します。 

    ```  
    =Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")      
    ```  
  
    Lookup 関数は、StoreID の値を受け取って Stores データセットを検索して、StoreName の値を返します。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    店舗の列見出しに、複合式の表示テキスト " **Expr**" が示されます。  
  
8.  レポートをプレビューします。  
  
各列の上部にある列ヘッダーに、店舗 ID ではなく店舗名が表示されます。  
  
## <a name="Expression"></a>5.選択されたパラメーターの値をレポートに表示する  
レポート閲覧者がレポートの詳細を確認する場合に、選択したパラメーターの値がわかるようにすることができます。 レポートのパラメーターごとにユーザーが選択した値を保持できます。 そのための方法の 1 つとして、ページ フッターのテキスト ボックスにパラメーターを表示する方法があります。  
  
### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>選択されたパラメーターの値とラベルをページ フッターに表示するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  ページ フッターを右クリックし、 **[挿入]**  >  **[テキスト ボックス]** をクリックします。 タイムスタンプを示すテキスト ボックスの横にテキスト ボックスをドラッグします。 テキスト ボックスの側面にあるハンドルをクリックしてドラッグすることにより、幅を拡張します。  
  
3.  レポート データ ペインからテキスト ボックスにパラメーター *\@StoreID* をドラッグします。 テキスト ボックスに " `[@StoreID]`" と表示されます。  
  
4.  パラメーターのラベルを表示するには、既存の式の後ろに挿入カーソルが表示されるまでテキスト ボックスをクリックし、空白を入力した後、レポート データ ペインからテキスト ボックスにもう一度パラメーターをドラッグします。 テキスト ボックスに " `[@StoreID] [@StoreID]`" と表示されます。  
  
5.  1 つ目の `[@StoreID]` を右クリックし、 **[式]** をクリックします。 **[式]** ダイアログ ボックスが表示されます。 `Value` を `Label`に置き換えます。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    テキスト ボックスに " `[@StoreID.Label] [@StoreID]`" と表示されます。  
  
7.  レポートをプレビューします。  
  
## <a name="Filter"></a>6.フィルターにレポート パラメーターを使用する  
フィルターを使用すると、外部データ ソースから取得されたデータのうちどのデータをレポートで使用するかを制御できます。 表示するデータをレポート閲覧者が制御できるようにするには、マトリックスのフィルターにレポート パラメーターを含めます。  
  
### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>マトリックス フィルターにパラメーターを指定するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  マトリックス上の行ヘッダーまたは列ヘッダーのハンドルを右クリックし、 **[Tablix のプロパティ]** をクリックします。  
  
3.  **[フィルター]** をクリックして、 **[追加]** をクリックします。 新しいフィルター行が表示されます。  
  
4.  **[式]** ドロップダウン リストからデータセット フィールドの StoreID を選択します。 データ型に **[整数]** が表示されます。 式の値がデータセット フィールドの場合、データ型は自動的に設定されます。  
  
5.  **[演算子]** で **等号** (=) が選択されていることを確認します。  
  
6.  **[値]** に「 `[@StoreID]`」と入力します。 

    `[@StoreID]` は、 `=Parameters!StoreID.Value`を表す単純な式の構文です。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  レポートをプレビューします。  
  
    マトリックスに、"Contoso Catalog Store" のデータのみが表示されます。  
  
9. レポート ビューアー ツール バーで、" **Store name?** " に対して **Contoso Asia Online Store**を選択し、 **[レポートの表示]** をクリックします。  
  
マトリックスに、選択した店舗に対応するデータが表示されます。  
  
## <a name="Multivalued"></a>7.レポート パラメーターを複数値をとるように変更する  
パラメーターを単一値ではなく複数値を持つように変更するには、クエリと、フィルターなどのパラメーターへの参照を含むすべての式を変更する必要があります。 複数値パラメーターは値の配列です。 データセット クエリでは、クエリ構文で 1 つの値が一連の値に含まれているかどうかをテストする必要があります。 レポート式では、式の構文が個々の値ではなく値の配列にアクセスする必要があります。  
  
### <a name="to-change-a-parameter-from-single-to-multivalued"></a>パラメーターを単一値ではなく複数値をとるように変更するには  
  
1.  デザイン ビューに切り替えます。  
  
2.  レポート データ ペインで *\@StoreID* を右クリックし、 **[パラメーターのプロパティ]** をクリックします。  
  
3.  **[複数の値を許可]** を選択します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  レポート データ ペインで、 **[データセット]** フォルダーを展開して **DataSet1**を右クリックし、 **[クエリ]** をクリックします。  
  
6.  クエリの最後の行で、**等号** (=) を [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** 句の **IN** に変更します。  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
    **IN** 演算子によって、値が一連の値に含まれているかどうかがテストされます。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  マトリックス上の行ヘッダーまたは列ヘッダーのハンドルを右クリックし、 **[Tablix のプロパティ]** をクリックします。  
  
9. **[フィルター]** をクリックします。  
  
10. **[演算子]** で **[次に含まれる]** を選択します。  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. ページ フッターのパラメーターを表示するテキスト ボックスで、すべてのテキストを削除します。  
  
13. テキスト ボックスを右クリックして、 **[式]** をクリックします。 次の式を入力します。 `=Join(Parameters!StoreID.Label, ", ")`  
  
    この式は、ユーザーが選択したすべての店舗名を、コンマとスペースで区切って連結します。  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 作成した式の前にあるテキスト ボックス内をクリックして、 

    **「Parameter Values Selected:」と入力します。** 
  
16. レポートをプレビューします。  
  
17. "Store Name?" の横にあるドロップダウン リストをクリックします。  
  
    有効な各値がチェック ボックスの横に表示されます。  
  
18. **[すべて選択]** をクリックして、 **[レポートの表示]** をクリックします。  
  
    レポートに、全店舗のすべてのサブカテゴリの販売数量が表示されます。  
  
19. ドロップダウン リストで **[すべて選択]** をクリックして一覧を消去し、"Contoso Catalog Store" と "Contoso Asia Online Store" をクリックして **[レポートの表示]** をクリックします。  

    ![report-builder-parameter-multiselect](../reporting-services/media/report-builder-parameter-multiselect.png)
  
 
## <a name="Boolean"></a>8.条件付き表示のためにブール型パラメーターを追加する  
  
### <a name="to-add-a-boolean-parameter"></a>ブール型パラメーターを追加するには  
  
1.  デザイン画面のレポート データ ペインで **[パラメーター]** を右クリックし、 **[パラメーターの追加]** をクリックします。  
  
2.  **[名前]** に「ShowSelections」と入力します。  
  
3.  **[プロンプト]** に「Show selections?」と入力します。  
  
4.  **[データ型]** で、 **[ブール]** をクリックします。  
  
5.  **[既定値]** をクリックします。  
  
6.  **[値の指定]** をクリックして、 **[追加]** をクリックします。  
  
7.  **[値]** に「 **False**」と入力します。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>ブール型パラメーターに基づいて表示を設定するには  
  
1.  デザイン画面で、ページ フッターのパラメーター値を表示するテキスト ボックスを右クリックし、 **[テキスト ボックスのプロパティ]** をクリックします。  
  
2.  **[表示]** をクリックします。  
  
3.  **[式を基に表示/非表示を切り替える]** オプションを選択し、式ボタン ( **[Fx]** ) をクリックします。  
  
4.  次の式を入力します。 `=Not Parameters!ShowSelections.Value`  
  
    テキスト ボックスの [表示] オプションは、[非表示] プロパティによって制御されます。 **Not** 演算子を適用すると、パラメーターが選択されたときに、[非表示] プロパティが false になり、テキスト ボックスが表示されます。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  レポートをプレビューします。  
  
    パラメーターの選択肢を表示するテキスト ボックスがフッターに表示されません。  
  
8.  レポート ビューアー ツール バーで、" **Show selections**" の横の **[True]**  >  **[レポートの表示]** をクリックします。  
  
    ページ フッターにテキスト ボックスが表示され、選択したすべての店舗名が示されます。  
  
## <a name="Title"></a>9.レポート タイトルを追加する  
  
### <a name="to-add-a-report-title"></a>レポート タイトルを追加するには  

1.  デザイン ビューに切り替えます。  
   
1.  デザイン画面で、 **[クリックしてタイトルを追加]** をクリックします。  
  
2.  「Parameterized Product Sales」と入力し、テキスト ボックスの外側をクリックします。  
  
## <a name="Save"></a>10.レポートを保存する  
  
### <a name="to-save-the-report-on-a-report-server"></a>レポート サーバーにレポートを保存するには  
  
1.  **レポート ビルダー** のボタンの **[名前を付けて保存]** をクリックします。  
  
2.  **[最近使ったサイトとサーバー]** をクリックします。  
  
3.  レポートを保存する権限があるレポート サーバーの名前を入力するか選択します。  
  
    " **レポート サーバーに接続しています**" というメッセージが表示されます。 接続が完了すると、レポート サーバー管理者がレポートの既定の場所として指定したレポート フォルダーのコンテンツが表示されます。  
  
4.  **[名前]** に表示されている既定の名前を Parameterized Sales Report に変更します。  
  
5.  **[保存]** をクリックします。  
  
レポートがレポート サーバーに保存されます。 接続しているレポート サーバーがウィンドウ下部のステータス バーに表示されます。  
  
## <a name="next-steps"></a>Next Steps  
これで、レポートにパラメーターを追加する方法のチュートリアルは終了です。 パラメーターの詳細については、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
* [レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md)
* [SQL Server のレポート ビルダー](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
*  [Lookup 関数](../reporting-services/report-design/report-builder-functions-lookup-function.md)   
