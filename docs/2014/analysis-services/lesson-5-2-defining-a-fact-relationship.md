---
title: ファクトリレーションシップの定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4b49a078-6848-4286-bc71-cf4862d29064
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4408e9b884e2cb5a0b47d9e6f95a16dec2bd20f6
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493863"
---
# <a name="defining-a-fact-relationship"></a>ファクト リレーションシップの定義
  ディメンション メジャーをファクト テーブルのデータ アイテムに関連付けなければならない場合があります。また、特定の販売ファクター (請求番号や受注番号) など、関連している特定の補足情報について、ファクト テーブルから情報を抽出しなければならない場合があります。 このように、ファクト テーブル アイテムに基づいて定義されたディメンションを、 *ファクト ディメンション*と呼びます。 ファクト ディメンションは、逆ディメンションとも呼ばれます。 特定の請求番号に関連するすべての行をグループ化する場合などのように、関連するテーブルの行をまとめてグループ化するには、ファクト ディメンションを使用すると便利です。 この情報は、リレーショナル データベースの個々のディメンション テーブルに格納することができます。しかし、情報ごとに異なるディメンション テーブルを作成してもメリットはありません。ファクト テーブルのサイズに比例してディメンション テーブルが大きくなり、データを複製することによって不要な複雑さを招くことになるからです。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]では、MOLAP ディメンションにファクト ディメンション データを複製してクエリ パフォーマンスを向上させる方法か、ファクト ディメンションを ROLAP ディメンションとして定義し、クエリ パフォーマンスという点を譲歩して記憶領域を節約する方法を選択できます。 MOLAP ストレージ モードでディメンションを格納する場合、すべてのディメンション メンバーは、メジャー グループのパーティションの他に、圧縮率の高い MOLAP 構造内の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスに格納されます。 ROLAP ストレージモードでディメンションを格納する場合、MOLAP 構造にはディメンション定義のみが格納されます。ディメンションメンバー自体は、クエリ時に基になるリレーショナルファクトテーブルからクエリが実行されます。 ファクト ディメンションにクエリを送信する頻度、通常のクエリにより返される行数、クエリのパフォーマンス、および処理コストなどを考慮し、適切なストレージ モードを決定します。 ディメンションを ROLAP モードとして定義する場合は、そのディメンションを使用するすべてのキューブを ROLAP ストレージ モードで格納しなければならないということではありません。 各ディメンションのストレージ モードは、個別に構成できます。  
  
 ファクト ディメンションを定義している場合は、ファクト ディメンションとメジャー グループの間のリレーションシップを、ファクト リレーションシップとして定義できます。 ファクト リレーションシップには、次の制限が適用されます。  
  
-   粒度属性は、ディメンションとファクト テーブル内のファクトとの間に一対一のリレーションシップを作成するディメンションのキー列でなければなりません。  
  
-   ディメンションに定義できるファクト リレーションシップは、1 メジャー グループとのファクト リレーションシップに限定されます。  
  
> [!NOTE]  
>  ファクト リレーションシップが参照するメジャー グループを更新するたびに、ファクト ディメンションを増分更新しなければなりません。  
  
 詳細については、「 [ディメンション リレーションシップ](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)」および「 [ファクト リレーションシップとファクト リレーションシップのプロパティの定義](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)」を参照してください。  
  
 このトピックの実習では、 **FactInternetSales** ファクト テーブルの **CustomerPONumber** 列に基づく新しいキューブ ディメンションを追加します。 次に、新しいキューブ ディメンションと **Internet Sales** メジャー グループの間のリレーションシップを、ファクト リレーションシップとして定義します。  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>Internet Sales Orders ファクト ディメンションの定義  
  
1.  ソリューション エクスプローラーで **[ディメンション]** を右クリックし、 **[新しいディメンション]** をクリックします。  
  
2.  **[ディメンション ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[作成方法の選択]** ページで **[既存のテーブルの使用]** オプションが選択されていることを確認し、 **[次へ]** をクリックします。  
  
4.  **[基になる情報の指定]** ページで、 **Adventure Works DW 2012** データ ソース ビューが選択されていることを確認します。  
  
5.  **[メイン テーブル]** ボックスの一覧で、 **[InternetSales]** を選択します。  
  
6.  **[キー列]** ボックスの一覧に **[SalesOrderNumber]** と **[SalesOrderLineNumber]** が表示されていることを確認します。  
  
7.  **[名前列]** ボックスの一覧から **[SalesOrderLineNumber]** を選択します。  
  
8.  **[次へ]** をクリックします。  
  
9. **[関連テーブルの選択]** ページで、すべてのテーブルの横のチェック ボックスをオフにし、 **[次へ]** をクリックします。  
  
10. **[ディメンション属性の選択]** ページで、ヘッダーのチェック ボックスを 2 回クリックしてすべてのチェック ボックスをオフにします。 **Sales Order Number** 属性はキー属性なので、選択されたままになります。  
  
11. **Customer PO Number** 属性を選択し、 **[次へ]** をクリックします。  
  
12. **[ウィザードの完了]** ページで、名前を **Internet Sales Order Details** に変更します。 **[完了]** をクリックしてウィザードを終了します。  
  
13. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
14. **Internet Sales Order Details**ディメンションのディメンションデザイナーの **[属性]** ペインで、 **[Sales order Number]** を選択し、プロパティウィンドウの**Name**プロパティをに変更し `Item Description.`  
  
15. **NameColumn**プロパティセルで、参照ボタン ([. **..])** をクリックします。 **[名前列]** ダイアログボックスで、基に **[なるテーブル]** ボックスの一覧から **[Product]** を選択し、基になる **[列]** で **[EnglishProductName]** を選択して、 **[OK]** をクリックします。  
  
16. **[データ ソース ビュー]** ペインで、 **InternetSales** テーブルの **SalesOrderNumber** 列をクリックし、 **[属性]** ペインにドラッグします。これにより、 **Sales Order Number** 属性がディメンションに追加されます。  
  
17. 新しい**Sales Order Number**属性の**Name**プロパティを `Order Number`に変更し、 **OrderBy**プロパティを**Key**に変更します。  
  
18. **[階層]** ペインで、`Order Number` と**項目の説明**のレベルを含む**Internet Sales Orders**ユーザー階層をこの順序で作成します。  
  
19. **[属性]** ペインで **Internet Sales Order Details**をクリックします。次に、[プロパティ] ウィンドウで、 **StorageMode** プロパティの値を確認します。  
  
     既定では、このディメンションは MOLAP ディメンションに格納されます。 このストレージ モードを ROLAP に変更すると、処理時間を短縮し、記憶領域を節約できますが、クエリのパフォーマンスが低下します。 このチュートリアルでは、MOLAP ストレージ モードを使用します。  
  
20. 新しく作成したディメンションをキューブ ディメンションとして [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブに追加するには、 **キューブ デザイナー**に切り替えます。 **[キューブ構造]** タブの **[ディメンション]** ペイン内で右クリックし、 **[キューブ ディメンションの追加]** をクリックします。  
  
21. **[キューブ ディメンションの追加]** ダイアログ ボックスで、 **[Internet Sales Order Details]** を選択し、 **[OK]** をクリックします。  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>ファクト ディメンションへのファクト リレーションシップの定義  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーを開いて、 **[ディメンションの使用法]** タブをクリックします。  
  
     以下のアイコンが示すように、 **Internet Sales Order Details** キューブ ディメンションがファクト リレーションシップを保持するよう、自動的に構成されます。  
  
2.  **Internet sales**メジャーグループと**Internet sales Order Details**ディメンションが交差する位置にある**Item Description**セルで参照ボタン ([. **..** ]) をクリックし、ファクトリレーションシップのプロパティを確認します。  
  
     **[リレーションシップの定義]** ダイアログ ボックスが開きます。 構成できるプロパティはありません。  
  
     次の図は **[リレーションシップの定義]** ダイアログ ボックスのファクト リレーションシップのプロパティです。  
  
     ![[リレーションシップの定義] ダイアログボックス](../../2014/tutorials/media/l5-factrelationship-2.gif "[リレーションシップの定義] ダイアログ ボックス")  
  
3.  **[キャンセル]** をクリックします。  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>ファクト ディメンションを使用したキューブの表示  
  
1.  **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックし、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスへの変更を配置して、データベースを処理します。  
  
2.  配置が正常に完了したら、 **Tutorial キューブのキューブ デザイナーで** [ブラウザー] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] タブをクリックし、 **[再接続]** ボタンをクリックします。  
  
3.  データ ペインからすべてのメジャーと階層を消去します。次に、データ ペインのデータ領域に **Internet Sales-Sales Amount** メジャーを追加します。  
  
4.  メタデータ ペインで、 **[Customer]** 、 **[Location]** 、 **[Customer Geography]** 、 **[Members]** 、 **[All Customers]** 、 **[Australia]** 、 **[Queensland]** 、 **[Brisbane]** 、 **[4000]** の順にクリックし、 **[Adam Powell]** を右クリックして **[フィルターに追加]** をクリックします。  
  
     フィルタリングを使用し、1 顧客から返される販売注文数を制限すると、クエリ パフォーマンスを大幅に犠牲にすることなく、基となる詳細情報を大規模なファクト テーブルから検索できます。  
  
5.  **Internet Sales Order Details** ディメンションの **Internet Sales Orders** ユーザー定義階層を、データ ペインの行領域に追加します。  
  
     Adam Powell 氏の注文数と、それに対応するインターネット販売量がデータ ペインに表示されます。  
  
     次の図は、前の手順の結果を示します。  
  
     ![Internet Sales-Sales Amount の寸法](../../2014/tutorials/media/l5-factrelationship-3.gif "Internet Sales-Sales Amount の寸法")  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [多対多関係の定義](lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>参照  
 [ディメンション リレーションシップ](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [ファクト リレーションシップとファクト リレーションシップのプロパティの定義](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
