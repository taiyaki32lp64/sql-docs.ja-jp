---
title: 計算されるメンバーを定義する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 07f13e1c-0b20-4f9e-ad62-c438983f2785
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ede0a23a6e37c47a1af242748233ca49b0cdfab7
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69493882"
---
# <a name="defining-calculated-members"></a>計算されるメンバーの定義
  計算されるメンバーとは、キューブ データ、算術演算子、数値、関数を組み合わせて定義した、ディメンション グループまたはメジャー グループのメンバーです。 たとえば、キューブ内の 2 つの物理的なメジャーの合計を計算する、計算されるメンバーを作成できます。 計算されるメンバーの定義はキューブ内に保存されますが、その値はクエリ時に計算されます。  
  
 計算されるメンバーを作成するには、キューブ デザイナーの **[計算]** タブで **[新しい計算されるメンバー]** コマンドを使用します。 計算されるメンバーは、メジャー ディメンションなどの任意のディメンション内に作成できます。 **[計算プロパティ]** ダイアログ ボックスを使用して、計算されるメンバーを表示フォルダー内に配置することもできます。 詳しくは、「 [計算](multidimensional-models-olap-logical-cube-objects/calculations.md)」、「 [多次元モデルの計算](multidimensional-models/calculations-in-multidimensional-models.md)」、および「 [計算されるメンバーの作成](multidimensional-models/create-calculated-members.md)」を参照してください。  
  
 このトピックの作業では、計算されるメジャーを定義し、インターネット販売、再販業者による販売、およびすべての販売について、売上総利益率と売上比率を表示できるようにします。  
  
## <a name="defining-calculations-to-aggregate-physical-measures"></a>物理メジャーを集計する計算の定義  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーを開き、 **[計算]** タブをクリックします。  
  
     **計算式** ペインと **[スクリプト オーガナイザー]** ペインには、既定で CALCULATE コマンドが表示されています。 このコマンドは、AggregateFunction プロパティで指定されている値に基づいて、キューブ内のメジャーを集計するように指定します。 通常、メジャー値は合計されますが、他の方法でカウントまたは集計することも可能です。  
  
     次の図は、キューブ デザイナーの **[計算]** タブを示しています。  
  
     ![キューブデザイナーの [計算] タブ](../../2014/tutorials/media/l6-calculatedmembers-1.gif "キューブデザイナーの [計算] タブ")  
  
2.  **[計算]** タブのツール バーで、 **[新しい計算されるメンバー]** をクリックします。  
  
     **計算式** ペインに新しいフォームが表示されます。このフォームで、この新しい計算されるメンバーのプロパティを定義します。 新しいメンバーは **[スクリプト オーガナイザー]** ペインにも表示されます。  
  
     次の図は、 **[新しい計算されるメンバー]** をクリックしたとき、 **計算式**ペインに表示されるフォームを示しています。  
  
     ![計算式ペインフォーム](../../2014/tutorials/media/l6-calculatedmembers-02.gif "計算式ペインフォーム")  
  
3.  **[名前]** ボックスで、計算されるメジャーの名前を`[Total Sales Amount]`に変更します。  
  
     計算されるメンバーの名前に空白文字が含まれる場合は、その名前全体を角かっこで囲む必要があります。  
  
     **[親階層]** ボックスを見るとわかるように、既定では、新しい計算されるメンバーは **Measures** ディメンションに作成されます。 Measures ディメンションの計算されるメンバーは、多くの場合、計算されるメジャーと呼ばれます。  
  
4.  **[計算]** タブの **[計算ツール]** ペインで **[メタデータ]** タブをクリックし、 **[Measures]** 、 **[Internet Sales]** の順に展開します。 **Internet Sales** メジャー グループのメタデータが表示されます。  
  
     メタデータ要素を **[計算ツール]** ペインから **[式]** ボックスにドラッグし、さらに演算子と他の要素を追加して、多次元式 (MDX) を作成します。 **[式]** ボックスには、MDX 式を直接入力することもできます。  
  
    > [!NOTE]  
    >  **[計算ツール]** ペインにメタデータが表示されない場合、ツール バーの **[再接続]** をクリックします。 それでも表示されない場合は、キューブを処理するか、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスを開始する必要があります。  
  
5.  **[計算ツール]** ペインの **[メタデータ]** タブで **[Internet Sales-Sales Amount]** をクリックし、 **計算式** ペインの **[式]** ボックスまでドラッグします。  
  
6.  **[式]** ボックスに、`+` **[Measures]. の後にプラス記号 () を入力します。 [Internet Sales-Sales Amount]** 。  
  
7.  **[計算ツール]** ペインの **[メタデータ]** タブで **[Reseller Sales]** を展開します。次に、 **[Reseller Sales-Sales Amount]** を、 **計算式** ペインの **[式]** ボックスにあるプラス符号 (+) の後ろにドラッグします。  
  
8.  **[書式設定文字列]** ボックスの一覧の **["Currency"]** を選択します。  
  
9. **[空以外の動作]** ボックスの一覧で、 **Internet Sales-Sales Amount** と **Reseller Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
     **[空以外の動作]** ボックスで指定したメジャーは、MDX の NON EMPTY クエリを解決するために使用されます。 **[空以外の動作]** ボックスで 1 つ以上のメジャーを指定すると、指定したメジャーがすべて空である場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は計算されるメンバーを空として処理します。 **[空以外の動作]** プロパティを空白にした場合は、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は計算されるメンバー自体を評価し、空メンバーであるかどうかを判断する必要があります。  
  
     次の図は、上記の手順で指定した設定が入力された **計算式** ペインを示しています。  
  
     ![計算式ペイン](../../2014/tutorials/media/l6-calculatedmembers-03.gif "計算式ペイン")  
  
10. **[計算]** タブのツール バーにある **[スクリプト ビュー]** をクリックし、 **計算式** ペインで計算スクリプトを確認します。  
  
     新しい計算が最初の CALCULATE 式に追加されているはずです。個々の計算はセミコロンで区切られています。 計算スクリプトの冒頭には、コメントが挿入されています。 計算スクリプト内で計算のグループごとにコメントを追加すると、開発者が複雑な計算スクリプトを理解するのに役立ちます。  
  
11. 計算スクリプトで、 **Calculate;** コマンドの後、新しく追加された計算スクリプトの前に新しい行を追加し、その行に以下のテキストを独自の行として追加します。  
  
    ```  
    /* Calculations to aggregate Internet Sales and Reseller Sales measures */  
    ```  
  
     次の図は、チュートリアルのこの時点で **計算式** ペインに表示される計算スクリプトを示しています。  
  
     ![計算式ペインのスクリプト](../../2014/tutorials/media/l6-calculatedmembers-04.gif "計算式ペインのスクリプト")  
  
12. **[計算]** タブのツールバーで、 **[フォームビュー]** を`[Total Sales Amount]`クリックし、 **[スクリプトオーガナイザー]** ペインでが選択されていることを確認して、 **[新しい計算]** されるメンバー をクリックします。  
  
13. この新しい計算されるメンバーの名前を`[Total Product Cost]`に変更し、 **[式]** ボックスに次の式を作成します。  
  
    ```  
    [Measures].[Internet Sales-Total Product Cost] + [Measures].[Reseller Sales-Total Product Cost]  
    ```  
  
14. **[書式設定文字列]** ボックスの一覧の **["Currency"]** を選択します。  
  
15. **[空以外の動作]** ボックスの一覧で、 **Internet Sales-Total Product Cost** と **Reseller Sales-Total Product Cost**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
     これで 2 つの計算されるメンバーが定義され、どちらも **[スクリプト オーガナイザー]** ペインに表示されます。 これらの計算されるメンバーは、計算スクリプト内で後に定義する他の計算で使用することができます。 **[スクリプト オーガナイザー]** ペインでいずれかの計算されるメンバーを選択すると、その計算されるメンバーの定義を表示できます。計算されるメンバーの定義は、フォーム ビューの **計算式** ペインに表示されます。 新しく定義した計算されるメンバーは、配置されるまでは **[計算ツール]** ペインに表示されません。 計算は処理を必要としません。  
  
## <a name="defining-gross-profit-margin-calculations"></a>売上総利益率の計算の定義  
  
1.  `[Total Product Cost]` **[スクリプトオーガナイザー]** ペインでが選択されていることを確認し、 **[計算]** タブのツールバーの **[新しい計算]** されるメンバー をクリックします。  
  
2.  **[名前]** ボックスで、この新しい計算されるメジャーの名前`[Internet GPM]`をに変更します。  
  
3.  **[式]** ボックスで、以下の MDX 式を作成します。  
  
    ```  
    ([Measures].[Internet Sales-Sales Amount] -   
    [Measures].[Internet Sales-Total Product Cost]) /  
    [Measures].[Internet Sales-Sales Amount]  
    ```  
  
4.  **[書式設定文字列]** ボックスの一覧で **["Percent"]** を選択します。  
  
5.  **[空以外の動作]** ボックスの一覧で、 **Internet Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
6.  **[計算]** タブのツール バーで、 **[新しい計算されるメンバー]** をクリックします。  
  
7.  **[名前]** ボックスで、この新しい計算されるメジャーの名前`[Reseller GPM]`をに変更します。  
  
8.  **[式]** ボックスで、以下の MDX 式を作成します。  
  
    ```  
    ([Measures].[Reseller Sales-Sales Amount] -   
    [Measures].[Reseller Sales-Total Product Cost]) /  
    [Measures].[Reseller Sales-Sales Amount]  
    ```  
  
9. **[書式設定文字列]** ボックスの一覧で **["Percent"]** を選択します。  
  
10. **[空以外の動作]** ボックスの一覧で、 **Reseller Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
11. **[計算]** タブのツール バーで、 **[新しい計算されるメンバー]** をクリックします。  
  
12. **[名前]** ボックスで、この計算されるメジャーの名前`[Total GPM]`をに変更します。  
  
13. **[式]** ボックスで、以下の MDX 式を作成します。  
  
    ```  
    ([Measures].[Total Sales Amount] -   
    [Measures].[Total Product Cost]) /  
    [Measures].[Total Sales Amount]  
    ```  
  
     この計算されるメンバーは、他の計算されるメンバーを参照しています。 この計算されるメンバーは、参照している計算されるメンバーの後に計算されるため、有効な計算されるメンバーになります。  
  
14. **[書式設定文字列]** ボックスの一覧で **["Percent"]** を選択します。  
  
15. **[空以外の動作]** ボックスの一覧で、 **Internet Sales-Sales Amount** と **Reseller Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
16. **[計算]** タブのツール バーで **[スクリプト ビュー]** をクリックし、計算スクリプトに追加した 3 つの計算を確認します。  
  
17. 計算スクリプト内の計算の`[Internet GPM]`直前に新しい行を追加し、次のテキストを独自の行にスクリプトに追加します。  
  
    ```  
    /* Calculations to calculate gross profit margin */  
    ```  
  
     次の図は、新しい 3 つの計算が表示されている **計算式** ペインを示しています。  
  
     ![計算式ペインの新しい計算](../../2014/tutorials/media/l6-calculatedmembers-05.gif "計算式ペインの新しい計算")  
  
## <a name="defining-the-percent-of-total-calculations"></a>全体に対する比率の計算の定義  
  
1.  **[計算]** タブのツール バーで、 **[フォーム ビュー]** をクリックします。  
  
2.  **[スクリプトオーガナイザー]** ペインで、 `[Total GPM]` を選択し、 **[計算]** タブのツールバーの **[新しい計算されるメンバー]** をクリックします。  
  
     **[スクリプト オーガナイザー]** ペインで最後の計算されるメンバーをクリックしてから **[新しい計算されるメンバー]** をクリックすると、新しい計算されるメンバーがスクリプトの末尾に挿入されます。 スクリプトは、 **[スクリプト オーガナイザー]** ペインに表示される順序で実行されます。  
  
3.  この新しい計算されるメンバーの名前を`[Internet Sales Ratio to All Products]`に変更します。  
  
4.  **[式]** ボックスに以下の式を入力します。  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Internet Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Internet Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Internet Sales-Sales Amount] )  
        End  
    ```  
  
     この MDX 式は、インターネット販売の合計売上に占める各製品の割合を計算します。 Case ステートメントを ISEMPTY 関数と共に使用すると、製品の売上がない場合でも、ゼロによる除算のエラーが発生しません。  
  
5.  **[書式設定文字列]** ボックスの一覧で **["Percent"]** を選択します。  
  
6.  **[空以外の動作]** ボックスの一覧で、 **Internet Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
7.  **[計算]** タブのツール バーで、 **[新しい計算されるメンバー]** をクリックします。  
  
8.  この計算されるメンバーの名前を`[Reseller Sales Ratio to All Products]`に変更します。  
  
9. **[式]** ボックスに以下の式を入力します。  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Reseller Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Reseller Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Reseller Sales-Sales Amount] )  
        End  
    ```  
  
10. **[書式設定文字列]** ボックスの一覧で **["Percent"]** を選択します。  
  
11. **[空以外の動作]** ボックスの一覧で、 **Reseller Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
12. **[計算]** タブのツール バーで、 **[新しい計算されるメンバー]** をクリックします。  
  
13. この計算されるメンバーの名前を`[Total Sales Ratio to All Products]`に変更します。  
  
14. **[式]** ボックスに以下の式を入力します。  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Total Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Total Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Total Sales Amount] )  
        End  
    ```  
  
15. **[書式設定文字列]** ボックスの一覧で **["Percent"]** を選択します。  
  
16. **[空以外の動作]** ボックスの一覧で、 **Internet Sales-Sales Amount** と **Reseller Sales-Sales Amount**のチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
17. **[計算]** タブのツール バーで **[スクリプト ビュー]** をクリックし、計算スクリプトに追加した 3 つの計算を確認します。  
  
18. 計算スクリプト内の計算の`[Internet Sales Ratio to All Products]`直前に新しい行を追加し、次のテキストを独自の行にスクリプトに追加します。  
  
    ```  
    /* Calculations to calculate percentage of product to total product sales */  
    ```  
  
     これで、合計 8 つの計算されるメンバーを定義しました。これらはフォーム ビューの **[スクリプト オーガナイザー]** ペインに表示されます。  
  
## <a name="browsing-the-new-calculated-members"></a>新しい計算されるメンバーの表示  
  
1.  **で、** [ビルド] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 **[ブラウザー]** タブに切り替えて、 **[再接続]** をクリックします。  
  
3.  Excel アイコンをクリックし、 **[有効化]** をクリックします。  
  
4.  **[ピボットテーブルのフィールドの一覧]** ペインで **[Values]** を展開して、メジャー ディメンションの新しい計算されるメンバーを表示します。  
  
5.  **Total Sales Amount** を値領域にドラッグして、結果を確認します。  
  
     **Internet Sales** および **Reseller Sales** メジャー グループから **Internet Sales-Sales Amount** および **Reseller Sales-Sales Amount** メジャーを値領域にドラッグします。  
  
     **Total Sales Amount** メジャーは、 **Internet Sales-Sales Amount** メジャーと **Reseller Sales-Sales Amount** メジャーの合計になっています。  
  
6.  **Product Categories** ユーザー定義階層を **[レポート フィルター]** 領域のフィルター領域に追加し、 **Mountain Bikes**でデータをフィルターします。  
  
     製品売上の計算対象が **Mountain Bikes** カテゴリになります。つまり、 **Mountain Bikes** の **Internet Sales-Sales Amount** メジャーと **Reseller Sales-Sales Amount** メジャーに基づいて **Total Sales Amount**が計算されます。  
  
7.  **Date.Calendar Date** ユーザー定義階層を行ラベル領域に追加して、結果を確認します。  
  
     今度は、 **Mountain Bikes** の **Internet Sales-Sales Amount** メジャーと **Reseller Sales-Sales Amount** メジャーに基づき、 **Mountain Bikes** カテゴリを対象とした製品売上が年度ごとに計算され、 **Total Sales Amount**として表示されます。  
  
8.  **Total GPM**、 **Internet GPM**、および **Reseller GPM** メジャーを値領域に追加して、結果を確認します。  
  
     次の図のように、再販業者による売上の売上総利益率は、インターネットでの販売と比べて著しく低くなっています。  
  
     ![再販業者の売上を示すデータペイン](../../2014/tutorials/media/l6-calculatedmembers-7b.gif "再販業者の売上を示すデータペイン")  
  
9. **Total Sales Ratio to All Products**、 **Internet Sales Ratio to All Products**、および **Reseller Sales Ratio to All Products** メジャーを値領域に追加します。  
  
     全製品の合計売上に占めるマウンテン バイクの売上の比率は、インターネット販売では毎年増加しているのに対し、再販業者販売では減少しています。 全製品の合計売上に占めるマウンテン バイクの売上の比率は、インターネット販売の場合よりも、再販業者販売の場合の方が低いことにも注目してください。  
  
10. フィルターを **Mountain Bikes** から **Bikes**に変更して、結果を確認します。  
  
     再販業者によるすべての自転車の販売に関する売上総利益率は負の値になっています。これはツーリング バイクおよびロード バイクの販売が赤字であるためです。  
  
11. フィルターを **Accessories**に変更して、結果を確認します。  
  
     アクセサリの売上は毎年増加しているものの、合計売上に占める割合が非常に小さいことがわかります。 また、アクセサリの売上における総利益率は、自転車よりも高くなっています。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [名前付きセットの定義](lesson-6-2-defining-named-sets.md)  
  
## <a name="see-also"></a>関連項目  
 [Custom](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [多次元モデルの計算](multidimensional-models/calculations-in-multidimensional-models.md)   
 [計算されるメンバーの作成](multidimensional-models/create-calculated-members.md)  
  
  
