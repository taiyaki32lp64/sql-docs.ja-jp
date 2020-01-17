---
title: ドリルスルーアクションの定義と使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 3765f865-2b93-44be-b290-28e3815d5ecb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbc9ad315792fc4198988a53713f978ff119d2ee
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69493822"
---
# <a name="defining-and-using-a-drillthrough-action"></a>ドリルスルー アクションの定義と使用
  ファクト ディメンションによってファクト データを多次元化する場合、必要なデータのみが返されるようにフィルターを設定しないとクエリのパフォーマンスが低下する可能性があります。 これを回避するために、返される合計行数を制限するドリルスルー アクションを定義できます。 これにより、クエリのパフォーマンスが大幅に向上します。  
  
 このトピックの作業では、インターネット経由での顧客への販売について注文の詳細情報を返すドリルスルー アクションを定義します。  
  
## <a name="defining-the-drillthrough-action-properties"></a>ドリルスルー アクション プロパティの定義  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーを開いて、 **[アクション]** タブをクリックします。  
  
     **[アクション]** タブにはいくつかのペインがあります。 このタブの左側には **[アクション オーガナイザー]** ペインと **[計算ツール]** ペインがあります。 これら 2 つのペインの右側には **[表示]** ペインがあり、 **[アクション オーガナイザー]** ペインで選択したアクションの詳細が表示されます。  
  
     次の図はキューブ デザイナーの **[アクション]** タブを示しています。  
  
     ![キューブデザイナーの [アクション] タブ](../../2014/tutorials/media/l8-action1.gif "キューブデザイナーの [アクション] タブ")  
  
2.  **[アクション]** タブのツール バーで **[新しいドリルスルー アクション]** ボタンをクリックします。  
  
     表示ペインに、空のアクション テンプレートが表示されます。  
  
     ![表示ウィンドウの空のアクションテンプレート](../../2014/tutorials/media/l8-action2.gif "表示ウィンドウの空のアクションテンプレート")  
  
3.  **[名前]** ボックスで、このアクションの名前をに`Internet Sales Details Drillthrough Action`変更します。  
  
4.  **[メジャー グループのメンバー]** リストで **[Internet Sales]** をクリックします。  
  
5.  **[ドリルスルー列]** で、 **[ディメンション]** リストから **[Internet Sales Order Details]** を選択します。  
  
6.  **[返される列]** リストで、 **[Item Description]** と **[Order Number]** チェック ボックスをオンにして、 **[OK]** をクリックします。 次の図は、ここまでの手順を実行した場合に表示されるアクション テンプレートを示しています。  
  
     ![[ドリルスルー列] ボックス](../../2014/tutorials/media/l8-action3.gif "[ドリルスルー列] ボックス")  
  
7.  次の図のように、 **[追加のプロパティ]** ボックスを展開します。  
  
     ![[追加のプロパティ] ボックス](../../2014/tutorials/media/l8-action4.gif "[追加のプロパティ] ボックス")  
  
8.  **[最大行数]** ボックスに「 `10`」と入力します。  
  
9. **[キャプション]** ボックスに「 `Drillthrough to Order Details...`」と入力します。  
  
     これらの設定は、返される行数を制限し、クライアント アプリケーションのメニューに表示されるキャプションを指定します。 次の図は、 **[追加のプロパティ]** ボックスでの設定を示しています。  
  
     ![[追加のプロパティ] ボックス](../../2014/tutorials/media/l8-action5.gif "[追加のプロパティ] ボックス")  
  
## <a name="using-the-drillthrough-action"></a>ドリルスルー アクションの使用  
  
1.  **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 **Tutorial キューブのキューブ デザイナーで** [ブラウザー] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] タブをクリックし、 **[再接続]** ボタンをクリックします。  
  
3.  Excel を起動します。  
  
4.  **Internet Sales-Sales Amount** メジャーを値領域に追加します。  
  
5.  **Customer** ディメンションの **Location** フォルダーの **Customer Geography** ユーザー定義階層を **[レポート フィルター]** 領域に追加します。  
  
6.  ピボットテーブルの **Customer Geography**で、1 人の顧客を選択するフィルターを追加します。 **[All Customers]** 、 **[Australia]** 、 **[Queensland]** 、 **[Brisbane]** 、 **[4000]** の順に展開し、 **Adam Powell**のチェック ボックスをオンにして **[OK]** をクリックします。  
  
     Adam Powell に対する [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 社製品の売上合計がデータ領域に表示されます。  
  
7.  売上高を右クリックし、 **[追加アクション]** をポイントして、 **[Drillthrough to Order Details]** をクリックします。  
  
     次の図のように、Adam Powell に発送された注文の詳細が **[データ サンプル ビューアー]** に表示されます。 しかし、注文日、期限、発送日などの追加の情報があればさらに便利です。 次の手順では、これらの情報を追加します。  
  
     ![Adam Powell に発送](../../2014/tutorials/media/l8-action6.gif "された注文Adam Powell に発送")された注文  
  
8.  Excel を閉じます。  
  
## <a name="modifying-the-drillthrough-action"></a>ドリルスルー アクションの変更  
  
1.  **Internet Sales Order Details** ディメンションのディメンション デザイナーを開きます。  
  
     このディメンションには 3 つの属性しか定義されていません。  
  
2.  **[データ ソース ビュー]** ペインで、何もない領域を右クリックし、 **[すべてのテーブルを表示]** をクリックします。  
  
3.  **[書式]** メニューの **[自動レイアウト]** をポイントし、 **[ダイアグラム]** をクリックします。  
  
4.  **InternetSales (dbo.FactInternetSales)** テーブルを検索します。検索するには、 **[データ ソース ビュー]** ペインの空いている領域を右クリックし、 **[テーブルの検索]** 、 **[InternetSales]** 、 **[OK]** の順にクリックします。  
  
5.  以下の列を基にして、新しい属性を作成します。  
  
    -   OrderDateKey  
  
    -   DueDateKey  
  
    -   ShipDateKey  
  
6.  **Order Date Key**属性の`Order Date` **name**プロパティをに変更し、 **name column**プロパティの参照ボタンをクリックします。次に、**名前列** ダイアログボックスで、ソーステーブルとして **日付** を選択し、 を選択します。ソース列としての SimpleDate。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  **[期限切れ]** 日 属性の **[名前]** プロパティ`Due Date`をに変更し、 **Order Date key**属性と同じ方法を使用して、この属性の**name Column**プロパティを**date. simpledate (WChar) に変更します。** .  
  
8.  **Ship date Key**属性の`Ship Date` **name**プロパティをに変更し、この属性の**name Column**プロパティを**date. simpledate (WChar)** に変更します。  
  
9. **Tutorial キューブのキューブ デザイナーを開き、** [アクション] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] タブに切り替えます。  
  
10. **[ドリルスルー列]** ボックスで、チェック ボックスをオンにして以下の列を **[返される列]** リストに追加し、 **[OK]** をクリックします。  
  
    -   Order Date  
  
    -   Due Date  
  
    -   Ship Date  
  
     次の図はこれらの列が選択された状態を示しています。  
  
     ![[ドリルスルー列] ボックス](../../2014/tutorials/media/l8-action7.gif "[ドリルスルー列] ボックス")  
  
## <a name="reviewing-the-modified-drillthrough-action"></a>変更されたドリルスルー アクションの確認  
  
1.  **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 **Tutorial キューブのキューブ デザイナーで** [ブラウザー] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] タブに切り替え、 **[再接続]** ボタンをクリックします。  
  
3.  Excel を起動します。  
  
4.  値領域の **Internet Sales-Sales Amount** とレポート フィルターの **Customer Geography** を使用してピボットテーブルを再作成します。  
  
     **All Customers**、 **Australia**、 **Queensland**、 **Brisbane**、 **4000**、 **Adam Powell**から選択するフィルターを追加します。  
  
5.  **Internet Sales-Sales Amount** データ セルをクリックし、 **[追加アクション]** をポイントして、 **[Drillthrough to Order Details]** をクリックします。  
  
     Adam Powell に発送された注文の詳細が一時ワークシートに表示されます。 表示される情報には、次の図に示すように、アイテムの説明、注文番号、受注日、期日、出荷日が含まれます。  
  
     ![Adam Powell に発送](../../2014/tutorials/media/l8-action8.gif "された注文Adam Powell に発送")された注文  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 9:パースペクティブと翻訳の定義](lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>関連項目  
 [アクション&#40;Analysis Services-多次元データ&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)   
 [多次元モデルでのアクション](multidimensional-models/actions-in-multidimensional-models.md)   
 [ディメンション リレーションシップ](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [ファクトリレーションシップの定義](lesson-5-2-defining-a-fact-relationship.md)   
 [ファクト リレーションシップとファクト リレーションシップのプロパティの定義](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
