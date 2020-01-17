---
title: Customer ディメンションの変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2530d42c70b506fe927d35fd4e6f862e22e1ea1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078927"
---
# <a name="modifying-the-customer-dimension"></a>Customer ディメンションの変更
  キューブのディメンションの使いやすさと機能性を向上させる方法は数多くあります。 このトピックの実習では、Customer ディメンションを変更します。  
  
## <a name="renaming-attributes"></a>属性名の変更  
 属性名は、ディメンション デザイナーの **[ディメンション構造]** タブで変更できます。  
  
#### <a name="to-rename-an-attribute"></a>属性名を変更するには  
  
1.  **で Customer ディメンションの** ディメンション デザイナー [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]に切り替えます。 これを行うには、ソリューション エクスプローラーの **[ディメンション]** ノードで **[Customer]** ディメンションをダブルクリックします。  
  
2.  **[属性]** ペインで **[English Country Region Name]** を右クリックし、 **[名前の変更]** をクリックします。 属性の名前を変更`Country-Region`します。  
  
3.  同様に、次の属性の名前も変更します。  
  
    -   **English Education**属性 - 変更 `Education`  
  
    -   **English Occupation**属性 - 変更 `Occupation`  
  
    -   **State Province Name**属性 - 変更 `State-Province`  
  
4.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="creating-a-hierarchy"></a>階層の作成  
 新しい階層は、属性を **[属性]** ペインから **[階層]** ペインにドラッグすることで作成できます。  
  
#### <a name="to-create-a-hierarchy"></a>階層を作成するには  
  
1.  ドラッグ、`Country-Region`属性を**属性**ペイン、**階層**ウィンドウ。  
  
2.  ドラッグ、`State-Province`属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層**下のウィンドウ`Country-Region`レベル。  
  
3.  ドラッグ、**市区町村**属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層**ウィンドウで、下にある、`State-Province`レベル。  
  
4.  **階層**のウィンドウ、**ディメンション構造** タブのタイトル バーを右クリックし、**階層**階層で、 **の名前を変更**、し、入力`Customer Geography`します。  
  
     階層の名前が`Customer Geography`します。  
  
5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="adding-a-named-calculation"></a>名前付き計算の追加  
 名前付き計算 (計算列として表される SQL 式) をデータ ソース ビューに追加できます。 この式は、テーブルの列として表示され、動作します。 名前付き計算により、基になるデータ ソースのテーブルを変更せずに、データ ソース ビューの既存のテーブルのリレーショナル スキーマを拡張できます。 詳細については、「[データ ソース ビューでの名前付き計算の定義 (Analysis Services)](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
#### <a name="to-add-a-named-calculation"></a>名前付き計算を追加するには  
  
1.  **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** データ ソース ビューを開きます。これには、ソリューション エクスプローラーの **[データ ソース ビュー]** フォルダーでこのデータ ソース ビューをダブルクリックします。  
  
2.  左側の **[テーブル]** ペインで **Customer**を右クリックし、 **[新しい名前付き計算]** をクリックします。  
  
3.  **名前付き計算の作成**ダイアログ ボックスに「`FullName`で、**列名**ボックスに、入力またはコピーして貼り付け、次`CASE`内のステートメント、**式**ボックス。  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
     `CASE`ステートメントの連結、 **FirstName**、 **MiddleName**、および**LastName**ディメンションとしてのお客様に使用する 1 つの列に列表示名、**顧客**属性。  
  
4.  **[OK]** をクリックします。次に、 **[テーブル]** ペインで **Customer** を展開します。  
  
     `FullName`名前付き計算が Customer テーブル内の列の一覧に表示されることを示すアイコンが表示されたが名前付き計算します。  
  
5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
6.  **[テーブル]** ペインで **[Customer]** を右クリックし、 **[データの探索]** をクリックします。  
  
7.  **[Customer テーブルの探索]** ビューで、最後の列を確認します。  
  
     なお、`FullName`元のデータ ソースを変更せずに、複数の列を基になるデータ ソースからデータを正しく連結列、データ ソース ビューに表示されます。  
  
8.  **[Customer テーブルの探索]** タブを閉じます。  
  
## <a name="using-the-named-calculation-for-member-names"></a>メンバー名に対応する名前付き計算の使用  
 データ ソース ビューで名前付き計算を作成したら、その名前付き計算を属性のプロパティとして使用できます。  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>メンバー名に対応する名前付き計算を使用するには  
  
1.  Customer ディメンションのディメンション デザイナーに切り替えます。  
  
2.  **[ディメンション構造]** タブの **[属性]** ペインで、 **[Customer Key]** 属性をクリックします。  
  
3.  [プロパティ] ウィンドウを開いて、タイトル バーにある **[自動的に隠す]** ボタンをクリックします。これにより、[プロパティ] ウィンドウが開いたままになります。  
  
4.  **名前**プロパティ フィールドに「`Full Name`します。  
  
5.  をクリックして、 **NameColumn**プロパティは、下部にあるフィールドし、クリックし、参照 ( **.** ) ボタンをクリックする、**名前列** ダイアログ ボックス。  
  
6.  選択`FullName`の下部にある、**基になる列**ボックスの一覧をクリックして**OK**。  
  
7.  ディメンション構造 タブで、ドラッグ、`Full Name`属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層**ウィンドウで、下、**市区町村**レベル。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-display-folders"></a>表示フォルダーの定義  
 表示フォルダーを使用してユーザー階層と属性階層をフォルダー構造内にグループ化することで、使いやすさを向上させることができます。  
  
#### <a name="to-define-display-folders"></a>表示フォルダーを定義するには  
  
1.  Customer ディメンションの **[ディメンション構造]** タブを開きます。  
  
2.  **[属性]** ペインで、Ctrl キーを押しながら次の各属性をクリックして選択します。  
  
    -   **City**  
  
    -   `Country-Region`  
  
    -   **Postal Code**  
  
    -   `State-Province`  
  
3.  [プロパティ] ウィンドウ、 **AttributeHierarchyDisplayFolder**プロパティ フィールド ([完全な名前を表示する] をポイントする必要がありますが)、上部にあるし、入力`Location`します。  
  
4.  **階層**ウィンドウで、をクリックして`Customer Geography`、し、右側の プロパティ ウィンドウで、`Location`の値として、 **DisplayFolder**プロパティ。  
  
5.  **[属性]** ペインで、Ctrl キーを押しながら次の各属性をクリックして選択します。  
  
    -   **Commute Distance**  
  
    -   `Education`  
  
    -   **Gender**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   `Occupation`  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  [プロパティ] ウィンドウ、 **AttributeHierarchyDisplayFolder**プロパティは、上部にあるフィールドし、入力`Demographic`します。  
  
7.  **[属性]** ペインで、Ctrl キーを押しながら次の各属性をクリックして選択します。  
  
    -   **Email Address**  
  
    -   **Phone**  
  
8.  [プロパティ] ウィンドウ、 **AttributeHierarchyDisplayFolder**プロパティ フィールドと種類`Contacts`します。  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-composite-keycolumns"></a>複合 KeyColumns の定義  
 **KeyColumns** プロパティは、属性のキーを表す 1 つ以上の列を示します。 このレッスンでは、複合キーを作成、**市区町村**と`State-Province`属性。 複合キーは、属性を一意に識別する必要がある場合に役立ちます。 など、このチュートリアルで後ほど属性リレーションシップを定義するときに、**市区町村**属性を一意に識別する必要があります、`State-Province`属性。 ただし、異なる州に同じ名前の都市が存在する可能性もあります。 そのため、 **City** 属性に対しては **StateProvinceName** 列と **City** 列で構成される複合キーを作成します。 詳細については、「[属性の KeyColumn プロパティの変更](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)」を参照してください。  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>City 属性の複合 KeyColumns を定義するには  
  
1.  Customer ディメンションの **[ディメンション構造]** タブを開きます。  
  
2.  **[属性]** ペインで、 **[City]** 属性をクリックします。  
  
3.  **[プロパティ]** ウィンドウで、下部付近の **[KeyColumns]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
4.  **[キー列]** ダイアログ ボックスの **[使用できる列]** ボックスの一覧で **[StateProvinceName]** 列を選択し、 **[>]** をクリックします。  
  
     **[City]** 列と **[StateProvinceName]** 列が **[キー列]** ボックスの一覧に表示されるようになりました。  
  
5.  **[OK]** をクリックします。  
  
6.  **City** 属性の **NameColumn** プロパティを設定するには、[プロパティ] ウィンドウで **[NameColumn]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
7.  **[名前列]** ダイアログ ボックスの **[基になる列]** ボックスの一覧で **[City]** を選択し、 **[OK]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>State-Province 属性の複合 KeyColumns を定義するには  
  
1.  Customer ディメンションの **[ディメンション構造]** タブが開いていることを確認します。  
  
2.  **属性**ウィンドウで、をクリックして、`State-Province`属性。  
  
3.  **[プロパティ]** ウィンドウで **[KeyColumns]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
4.  **[キー列]** ダイアログ ボックスの **[使用できる列]** ボックスの一覧で **[EnglishCountryRegionName]** 列を選択し、 **[>]** をクリックします。  
  
     **[EnglishCountryRegionName]** 列と **[StateProvinceName]** 列が **[キー列]** ボックスの一覧に表示されるようになりました。  
  
5.  **[OK]** をクリックします。  
  
6.  設定する、 **NameColumn**のプロパティ、`State-Province`属性をクリックして、 **NameColumn**プロパティ ウィンドウでフィールドし、クリックし、参照 ( **.** ) ボタンをクリックします。  
  
7.  **[名前列]** ダイアログ ボックスの **[基になる列]** ボックスの一覧で **[StateProvinceName]** を選択し、 **[OK]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-attribute-relationships"></a>属性リレーションシップの定義  
 基になるデータで属性リレーションシップがサポートされる場合、属性間の属性リレーションシップを定義する必要があります。 属性リレーションシップを定義すると、ディメンション、パーティション、およびクエリの処理速度が上がります。 詳細については、「 [属性リレーションシップの定義](multidimensional-models/attribute-relationships-define.md) 」および「 [属性リレーションシップ](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」を参照してください。  
  
#### <a name="to-define-attribute-relationships"></a>属性リレーションシップを定義するには  
  
1.  Customer ディメンションの **ディメンション デザイナー** で、 **[属性リレーションシップ]** タブをクリックします。場合によっては、しばらく待つ必要があります。  
  
2.  ダイアグラムで、 **[City]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[City]** を指定します。 設定、**関連属性**に`State-Province`します。  
  
4.  **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
     リレーションシップの種類を **[固定]** に設定するのは、時間が経過してもメンバー間のリレーションシップが変化しないためです。 たとえば、ある都市が別の都道府県の一部となることは通常ありません。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  図を右クリックし、`State-Province`属性選び**新しい属性リレーションシップ**します。  
  
7.  **属性リレーションシップの作成** ダイアログ ボックスで、**基になる属性**は`State-Province`します。 設定、**関連属性**に`Country-Region`します。  
  
8.  **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
9. **[OK]** をクリックします。  
  
10. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>オブジェクトの配置、変更、処理、および変更内容の表示  
 属性と階層を変更したら、変更を表示する前に変更を配置し、関連するオブジェクトを再処理する必要があります。  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>変更の配置、オブジェクトの処理、および変更の表示を行うには  
  
1.  **で、** [ビルド] [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  " **配置が正常に完了しました** " というメッセージが表示されたら、Customer ディメンションのディメンション デザイナーの **[ブラウザー]** タブをクリックし、ディメンション デザイナーのツール バーの左側にある [再接続] ボタンをクリックします。  
  
3.  いることを確認`Customer Geography`でが選択されている、**階層**一覧し、ブラウザーのウィンドウで次のように展開します**すべて**、展開**オーストラリア**、展開**新しい南部。ウェールズ州**、順に展開**Coffs Harbour**します。  
  
     この都市の顧客がブラウザーに表示されます。  
  
4.  **Tutorial キューブの** キューブ デザイナー [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] に切り替えます。 これを行うには、 **ソリューション エクスプローラー** の **[キューブ]** ノードで **[Analysis Services Tutorial]** キューブをダブルクリックします。  
  
5.  **[ブラウザー]** タブをクリックし、キューブ デザイナーのツール バーにある [再接続] ボタンをクリックします。  
  
6.  **[メジャー グループ]** ペインで **[Customer]** を展開します。  
  
     [Customer] の下には、属性が展開されて表示される代わりに、表示フォルダーが表示されています。表示フォルダー値が割り当てられていない属性はそのまま表示されます。  
  
7.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Product ディメンションの変更](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>参照  
 [ディメンションの属性のプロパティの参照](multidimensional-models/dimension-attribute-properties-reference.md)   
 [ディメンションから属性を削除します。](multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)   
 [属性名の変更します。](multidimensional-models/attribute-properties-rename-an-attribute.md)   
 [データ ソース ビューでの名前付き計算の定義 (Analysis Services)](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
