---
title: 多対多リレーションシップの定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b7b091c6e963af043533bfe362a801d7d4c91f2
ms.sourcegitcommit: d0e5543e8ebf8627eebdfd1e281adb47d6cc2084
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "69493877"
---
# <a name="defining-a-many-to-many-relationship"></a>多対多関係の定義
  通常、ディメンションを定義する場合、1 つのディメンション メンバーは多数のファクトに結合できますが、各ファクトを結合できるのは 1 つのディメンションのみです。 たとえば、各顧客は多数の商品を注文できますが、それぞれの注文は 1 人の顧客に所属します。 リレーショナル データベース用語では、これを *一対多のリレーションシップ*と呼びます。 しかし、1 つのファクトが複数のディメンション メンバーに結合する場合があります。 リレーショナル データベース用語では、これを *多対多のリレーションシップ*と呼びます。 たとえば、1 回の購入には複数の購入動機があることが考えられ、また、1 つの購入動機が複数の購入に結び付く (関連付けられる) ことがあります。 結合テーブルは、各購入に関連する購入動機の定義に使用されます。 このようなリレーションシップから作成された Sales Reason ディメンションには、1 回の販売取り引きに関連付けられるメンバーが複数存在します。 多対多のディメンションは、従来のスター スキーマ以上にディメンショナル モデルを展開し、ディメンションが直接ファクト テーブルに関連付けられていなくても複雑な分析を可能にします。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]では、ディメンションとメジャー グループの間に多対多のリレーションシップを定義します。この定義は、ディメンション テーブルに関連付けられる中間ファクト テーブルを指定することにより行われます。 その後、中間ファクト テーブルは、ファクト テーブルを関連付ける中間ディメンション テーブルに関連付けられます。 中間ファクト テーブルとリレーションシップ内のディメンション テーブル、および中間ファクトと中間ディメンション間の多対多のリレーションシップにより、そのリレーションシップに指定されている主ディメンションのメンバーおよびメジャー グループ内のグループとの間に多対多のリレーションシップが作成されます。 中間メジャー グループを通じてディメンションとメジャー グループ間の多対多のリレーションシップを定義するには、中間メジャー グループは 1 つ以上のディメンションを元のメジャー グループと共有する必要があります。  
  
 多対多のディメンションでは値は個別に集計され、すべてのメンバーに対して 2 回以上集計されることはありません。  
  
> [!NOTE]  
>  多対多のディメンションリレーションシップをサポートするには、関連するすべてのテーブル間のデータソースビューで主キーと外部キーのリレーションシップを定義する必要があります。 このようにしないと、キューブ デザイナーの **[ディメンションの使用法]** タブでリレーションシップを確立するときに正しいメジャー グループを選択できません。  
  
 詳細については、「 [ディメンション リレーションシップ](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)」および「 [多対多のリレーションシップと多対多のリレーションシップのプロパティの定義](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)」を参照してください。  
  
 このトピックの実習では、まず、Sales Reasons ディメンションと Sales Reasons メジャー グループを作成します。次に、Sales Reasons メジャー グループを介して、Sales Reasons ディメンションと Internet Sales メジャー グループの間に多対多のリレーションシップを定義します。  
  
## <a name="adding-required-tables-to-the-data-source-view"></a>データ ソース ビューへの必要なテーブルの追加  
  
1.  データ ソース ビュー デザイナーを開き、 **Adventure Works DW 2012** データ ソース ビューを表示します。  
  
2.  **[ダイアグラムオーガナイザー]** ペイン内の任意の場所を右クリックし、 **[新しいダイアグラム]** をクリックして、この新しいダイアグラムの名前として `Internet Sales Order Reasons` を指定します。  
  
3.  **[テーブル]** ペインの **[InternetSales]** テーブルを、 **[ダイアグラム]** ペインにドラッグします。  
  
4.  **[ダイアグラム]** ペイン内を右クリックし、 **[テーブルの追加と削除]** をクリックします。  
  
5.  **[テーブルの追加と削除]** ダイアログ ボックスで、 **[含まれているオブジェクト]** ボックスの一覧に **DimSalesReason** テーブルと **FactInternetSalesReason** テーブルを追加し、 **[OK]** をクリックします。  
  
     関連するテーブル間の主キーと外部キーのリレーションシップは、基になるリレーショナルデータベースで定義されているため、自動的に確立されることに注意してください。 これらのリレーションシップが基のリレーショナル データベースに定義されていない場合は、データ ソース ビューで定義する必要があります。  
  
6.  **[書式]** メニューで **[自動レイアウト]** をポイントし、 **[ダイアグラム]** をクリックします。  
  
7.  プロパティウィンドウで、 **DimSalesReason**テーブルの**friendlyname**プロパティを `SalesReason`に変更し、 **FactInternetSalesReason**テーブルの**friendlyname**プロパティを `InternetSalesReason`に変更します。  
  
8.  **[テーブル]** ペインで **[InternetSalesReason (dbo.FactInternetSalesReason)]** を展開し、 **[SalesOrderNumber]** をクリックします。次に、[プロパティ] ウィンドウで、このデータ列の **DataType** プロパティを確認します。  
  
     **[SalesOrderNumber]** 列のデータ型は文字列になっています。  
  
9. `InternetSalesReason` テーブル内の他の列のデータ型を確認します。  
  
     このテーブルでは、他の 2 つの列のデータ型が数値型になっています。  
  
10. **[テーブル]** ペインで **[InternetSalesReason (dbo.FactInternetSalesReason)]** を右クリックし、 **[データの探索]** をクリックします。  
  
     次の図のように、各並び順の行番号では、その行の商品の購入動機がキー値により識別されます。  
  
     ![購入の理由を識別するキー値](../../2014/tutorials/media/l5-many-to-many-1.gif "購入の理由を識別するキー値")  
  
## <a name="defining-the-intermediate-measure-group"></a>中間メジャー グループの定義  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーに切り替え、 **[キューブ構造]** タブをクリックします。  
  
2.  **[メジャー]** ペイン内を右クリックし、 **[新しいメジャー グループ]** をクリックします。 詳細については、「 [多次元モデル内のメジャーおよびメジャー グループの作成](multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)」を参照してください。  
  
3.  **[新しいメジャーグループ]** ダイアログボックスの **[データソースビューからテーブルを選択]** ボックスの一覧の [`InternetSalesReason`] をクリックし、[ **OK]** をクリックします。  
  
     **Internet Sales Reason** メジャー グループが **[メジャー]** ペインに表示されます。  
  
4.  **Internet Sales Reason** メジャー グループを展開します。  
  
     この新しいメジャー グループには、メジャー ( **Internet Sales Reason Count** メジャー) が 1 つだけ定義されています。  
  
5.  **[Internet Sales Reason Count]** を選択し、[プロパティ] ウィンドウでこのメジャーのプロパティを確認します。  
  
     このメジャーの **AggregateFunction** プロパティは、 **Sum** ではなく、 **Count**として定義されていることがわかります。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] でこのプロパティが **Count** になっているのは、基のデータ型が文字列データ型であるためです。 基のファクト テーブルの他の 2 つの列は、メジャーとしては選択されていません。これらは実際のメジャーではなく、数値キーであることを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] が検出したためです。 準加法の動作の詳細については、「 [準加法の動作の定義](multidimensional-models/define-semiadditive-behavior.md)」を参照してください。  
  
6.  [プロパティ] ウィンドウで、 **Internet Sales Reason Count** メジャーの **Visible** プロパティを **False**に変更します。  
  
     このメジャーは、Internet Sales ディメンションの隣に定義する Sales Reason ディメンションを結合するためにのみ使用されます。 ユーザーがこのメジャーを直接表示することはありません。  
  
     次の図は、 **Internet Sales Reason Count** メジャーのプロパティを示しています。  
  
     ![Internet Sales Reason Count メジャーのプロパティ](../../2014/tutorials/media/l5-many-to-many-2.gif "Internet Sales Reason Count メジャーのプロパティ")  
  
## <a name="defining-the-many-to-many-dimension"></a>多対多ディメンションの定義  
  
1.  ソリューション エクスプローラーで **[ディメンション]** を右クリックし、 **[新しいディメンション]** をクリックします。  
  
2.  **[ディメンション ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[作成方法の選択]** ページで **[既存のテーブルの使用]** オプションが選択されていることを確認し、 **[次へ]** をクリックします。  
  
4.  **[基になる情報の指定]** ページで、 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 データ ソース ビューが選択されていることを確認します。  
  
5.  **[メインテーブル]** ボックスの一覧で、[`SalesReason`] を選択します。  
  
6.  **[キー列]** ボックスの一覧に **[SalesReasonKey]** が表示されていることを確認します。  
  
7.  **[名前列]** ボックスの一覧から **[SalesReasonName]** を選択します。  
  
8.  **[次へ]** をクリックします。  
  
9. **[ディメンション属性の選択]** ページで、 **Sales Reason Key** 属性が自動的に選択されます。これは、この属性がキー属性であるためです。 **Sales Reason Reason Type**属性の横にあるチェックボックスをオンにし、名前を `Sales Reason Type`に変更して、 **[次へ]** をクリックします。  
  
10. **[ウィザードの完了]** ページで **[完了]** をクリックすると、Sales Reason ディメンションが作成されます。  
  
11. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
12. **Sales reason**ディメンションのディメンションデザイナーの **[属性]** ペインで、 **[sales reason Key]** を選択し、プロパティウィンドウの**Name**プロパティをに変更し `Sales Reason.`  
  
13. ディメンションデザイナーの **[階層]** ペインで、`Sales Reason Type` レベルと**sales Reason**レベルを含む**sales** Reason ユーザー階層をこの順序で作成します。  
  
14. プロパティウィンドウで、Sales 理由階層の**Allmembername**プロパティの値として `All Sales Reasons` を定義します。  
  
15. Sales Reason ディメンションの**Attributeallmembername**プロパティの値として、`All Sales Reasons` を定義します。  
  
16. 新しく作成したディメンションをキューブ ディメンションとして [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブに追加するには、 **キューブ デザイナー**に切り替えます。 **[キューブ構造]** タブの **[ディメンション]** ペイン内で右クリックし、 **[キューブ ディメンションの追加]** をクリックします。  
  
17. **[キューブ ディメンションの追加]** ダイアログ ボックスで、 **[Sales Reason]** を選択し、 **[OK]** をクリックします。  
  
18. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-the-many-to-many-relationship"></a>多対多リレーションシップの定義  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーに切り替え、 **[ディメンションの使用法]** タブをクリックします。  
  
     **Sales Reason** ディメンションには、 **Internet Sales Reason** メジャー グループで定義されている標準のリレーションシップがあります。ただし、 **Internet Sales** メジャー グループおよび **Reseller Sales** メジャー グループで定義されたリレーションシップはありません。 また、 **Internet Sales Order Details** ディメンションには **Internet Sales Reason** ディメンションで定義されている標準のリレーションシップがあり、 **Internet Sales** メジャー グループとの **ファクト リレーションシップ** があります。 このディメンションが存在しなかった場合 (または **Internet Sales Reason** メジャー グループおよび **Internet Sales** メジャー グループとのリレーションシップを持つ別のディメンションが存在しなかった場合)、多対多のリレーションシップを定義することはできません。  
  
2.  **Internet Sales** メジャー グループと **Sales Reason** ディメンションが交差する位置にあるセルをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
3.  **[リレーションシップの定義]** ダイアログ ボックスで、 **[リレーションシップの種類の選択]** ボックスの一覧から **[多対多]** を選択します。  
  
     Sales Reason ディメンションを Internet Sales メジャー グループに接続する中間メジャー グループを定義する必要があります。  
  
4.  **[中間メジャー グループ]** ボックスの一覧で **[Internet Sales Reason]** を選択します。  
  
     次の図は、 **[リレーションシップの定義]** ダイアログ ボックスでの操作を示しています。  
  
     ![[リレーションシップの定義] ダイアログボックス](../../2014/tutorials/media/l5-many-to-many-3.gif "[リレーションシップの定義] ダイアログ ボックス")  
  
5.  クリックして **OK**です。  
  
     多対多アイコンにより、Sales Reason ディメンションと Internet Sales メジャー グループの間のリレーションシップが表されます。  
  
## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>キューブおよび多対多ディメンションの表示  
  
1.  **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 **Tutorial キューブのキューブ デザイナーで** [ブラウザー] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] タブに切り替え、 **[再接続]** をクリックします。  
  
3.  データ ペインのデータ領域に **Internet Sales-Sales Amount** メジャーを追加します。  
  
4.  **Sales Reason** ディメンションの **Sales Reasons** ユーザー定義階層を、データ ペインの行領域に追加します。  
  
5.  メタデータ ペインで、 **[Customer]** 、 **[Location]** 、 **[Customer Geography]** 、 **[Members]** 、 **[All Customers]** 、 **[Australia]** の順にクリックし、 **[Queensland]** を右クリックして **[フィルターに追加]** をクリックします。  
  
6.  `Sales Reason Type` レベルの各メンバーを展開し、Queensland の顧客がインターネット経由で [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 製品を購入するために使用した各理由に関連付けられているドル値を確認します。  
  
     購入理由に関連付けられている売上金額をすべて加算すると、総売上額を上回ります。 これは、製品の購入理由を複数選択した顧客がいたためです。  
  
     次の図は、キューブ デザイナーの **[フィルター]** ペインと **[データ]** ペインです。  
  
     ![キューブデザイナーのフィルターおよびデータペイン](../../2014/tutorials/media/l5-many-to-many-5.gif "キューブデザイナーのフィルターおよびデータペイン")  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [メジャー グループでのディメンション粒度の定義](lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)  
  
## <a name="see-also"></a>参照  
 [データ ソース ビュー デザイナーでのダイアグラムの操作 (Analysis Services)](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [ディメンション リレーションシップ](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [多対多のリレーションシップと多対多のリレーションシップのプロパティの定義](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)  
  
  
