---
title: Product ディメンションの変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff912ed43048e00f0ed77989a46b3b7d0b111cff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078841"
---
# <a name="modifying-the-product-dimension"></a>Product ディメンションの変更
  このトピックの実習では、名前付き計算を使用して製品ラインにわかりやすい名前を指定し、Product ディメンションに階層を定義して、その階層の (All) メンバー名を指定します。 また、属性をグループ化して別々の表示フォルダーに格納します。  
  
## <a name="adding-a-named-calculation"></a>名前付き計算の追加  
 データ ソース ビューで名前付き計算をテーブルに追加できます。 次の実習では、製品ラインの完全な名前を表示する名前付き計算を作成します。  
  
#### <a name="to-add-a-named-calculation"></a>名前付き計算を追加するには  
  
1.  **Adventure Works DW 2012** データ ソース ビューを開くには、ソリューション エクスプローラーの **[データ ソース ビュー]** フォルダーで **[Adventure Works DW 2012]** をダブルクリックします。  
  
2.  ダイアグラム ペインの下部で **[Product]** テーブル ヘッダーを右クリックし、 **[新しい名前付き計算]** をクリックします。  
  
3.  **名前付き計算の作成**ダイアログ ボックスに「`ProductLineName`で、**列名**ボックス。  
  
4.  **[式]** ボックスに、次の **CASE** ステートメントを入力するか、またはコピーして貼り付けます。  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
     この **CASE** ステートメントは、キューブ内の各製品ラインにわかりやすい名前を付けるためのものです。  
  
5.  クリックして**OK**を作成する、`ProductLineName`名前付き計算します。 場合によっては、しばらく待つ必要があります。  
  
6.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>属性の NameColumn プロパティの変更  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>属性の NameColumn プロパティ値を変更するには  
  
1.  Product ディメンションのディメンション デザイナーに切り替えます。 これを行うには、ソリューション エクスプローラーの **[ディメンション]** ノードで **[Product]** ディメンションをダブルクリックします。  
  
2.  **[ディメンション構造]** タブの **[属性]** ペインで、 **[Product Line]** をクリックします。  
  
3.  画面の右側にある プロパティ ウィンドウで、 **NameColumn**プロパティ ウィンドウの下部にあるフィールドし、クリックし、参照 ( **.** ) ボタンをクリックする、**名前列** ダイアログ ボックス。 (場合によっては、画面右側の **[プロパティ]** タブをクリックして、[プロパティ] ウィンドウを開く必要があります)。  
  
4.  選択`ProductLineName`の下部にある、**基になる列**ボックスの一覧をクリックして**OK**。  
  
     NameColumn フィールドに、テキスト " **Product.ProductLineName (WChar)** " が表示されるようになりました。 これで、 **Product Line** 属性階層のメンバーが、簡略名ではなく製品ラインの完全な名前で表示されるようになりました。  
  
5.  **[ディメンション構造]** タブの **[属性]** ペインで、 **[Product Key]** をクリックします。  
  
6.  プロパティ ウィンドウ、 **NameColumn**プロパティ フィールドし、参照ボタンをクリックし ( **.** ) ボタンをクリックする、**名前列** ダイアログ ボックス。  
  
7.  **[基になる列]** ボックスの一覧で **[EnglishProductName]** を選択し、 **[OK]** をクリックします。  
  
     NameColumn フィールドに、テキスト " **Product.EnglishProductName (WChar)** " が表示されるようになりました。  
  
8.  プロパティ ウィンドウで上にスクロール をクリックして、**名前**プロパティ フィールドと入力し、`Product Name`します。  
  
## <a name="creating-a-hierarchy"></a>階層の作成  
  
#### <a name="to-create-a-hierarchy"></a>階層を作成するには  
  
1.  **[属性]** ペインの **[Product Line]** 属性を **[階層]** ペインにドラッグします。  
  
2.  ドラッグ、**モデル名**属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層**ウィンドウで、下、**製品ライン**レベル。  
  
3.  ドラッグ、`Product Name`属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層**下のウィンドウ**モデル名**レベル。 (前のセクションで、Product Key を Product Name に名前変更しました)。  
  
4.  **階層**のウィンドウ、**ディメンション構造** タブのタイトル バーを右クリックし、**階層**階層、 をクリックして**の名前を変更**、し、入力`Product Model Lines`します。  
  
     階層の名前が`Product Model Lines`します。  
  
5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="specifying-folder-names-and-all-member-names"></a>フォルダー名およびすべてのメンバー名の指定  
  
#### <a name="to-specify-the-folder-and-member-names"></a>フォルダー名とメンバー名を指定するには  
  
1.  **[属性]** ペインで、Ctrl キーを押しながら次の各属性をクリックして選択します。  
  
    -   **クラス**  
  
    -   **色**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **Size**  
  
    -   **Size Range**  
  
    -   **スタイル**  
  
    -   **Weight**  
  
2.  **AttributeHierarchyDisplayFolder**プロパティ フィールドの種類プロパティ ウィンドウで`Stocking`します。  
  
     上記の属性をグループ化し、1 つの表示フォルダーに表示されるようにしました。  
  
3.  **[属性]** ペインで、次の属性を選択します。  
  
    -   **Dealer Price**  
  
    -   **List Price**  
  
    -   **Standard Cost**  
  
4.  **AttributeHierarchyDisplayFolder**プロパティのセルの種類プロパティ ウィンドウに`Financial`します。  
  
     上記の属性をグループ化し、別の表示フォルダーに表示されるようにしました。  
  
5.  **[属性]** ペインで、次の属性を選択します。  
  
    -   **End Date**  
  
    -   **[開始日]**  
  
    -   **ステータス**  
  
6.  **AttributeHierarchyDisplayFolder**プロパティのセルの種類プロパティ ウィンドウに`History`します。  
  
     上記の属性をグループ化し、3 番目の表示フォルダーに表示されるようにしました。  
  
7.  選択、`Product Model Lines`内の階層、**階層**ウィンドウで、変更し、 **AllMemberName**をプロパティ ウィンドウでプロパティ`All Products`します。  
  
8.  空いている領域をクリックして、**階層**ウィンドウで、変更し、 **AttributeAllMemberName**プロパティを [プロパティ] ウィンドウの上部にある`All Products`します。  
  
     空いている領域をクリックすると、Product ディメンション自体のプロパティを変更できます。 **[属性]** ペインの属性リストの上部にある **[Product]** をクリックすることもできます。  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-attribute-relationships"></a>属性リレーションシップの定義  
 基になるデータで属性リレーションシップがサポートされる場合、属性間の属性リレーションシップを定義する必要があります。 属性リレーションシップを定義すると、ディメンション、パーティション、およびクエリの処理速度が上がります。 詳細については、「 [属性リレーションシップの定義](multidimensional-models/attribute-relationships-define.md) 」および「 [属性リレーションシップ](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」を参照してください。  
  
#### <a name="to-define-attribute-relationships"></a>属性リレーションシップを定義するには  
  
1.  Product ディメンションの **ディメンション デザイナー** で、 **[属性リレーションシップ]** タブをクリックします。  
  
2.  ダイアグラムで、 **[Model Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Model Name]** を指定します。 **[関連属性]** を **[Product Line]** に設定します。  
  
     時間が経過するとメンバー間のリレーションシップが変化する可能性があるため、 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類の設定は **[可変]** のままにします。 たとえば、製品モデルが最終的に別の製品ラインに移動される場合があります。  
  
4.  **[OK]** をクリックします。  
  
5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="reviewing-product-dimension-changes"></a>Product ディメンションの変更の確認  
  
#### <a name="to-review-the-product-dimension-changes"></a>Product ディメンションの変更を確認するには  
  
1.  **で、** [ビルド] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  " **配置が正常に完了しました** " というメッセージが表示されたら、 **Product** ディメンションの **ディメンション デザイナー** の **[ブラウザー]** タブをクリックし、ディメンション デザイナーのツール バーにある再接続ボタンをクリックします。  
  
3.  いることを確認`Product Model Lines`でが選択されている、**階層**一覧を展開し、展開`All Products`します。  
  
     注意の名前、**すべて**としてメンバーが表示されます`All Products`します。 これは、変更したため、 **AllMemberName**プロパティの階層を`All Products`以前のレッスンでは。 また、 **Product Line** レベルのメンバー名が、1 文字の簡略名から、わかりやすい名前に変わりました。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Date ディメンションの変更](lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>関連項目  
 [データ ソース ビューでの名前付き計算の定義 (Analysis Services)](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [ユーザー定義階層の作成](multidimensional-models/user-defined-hierarchies-create.md)   
 [属性階層の &#40;All&#41; レベルの構成](multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
