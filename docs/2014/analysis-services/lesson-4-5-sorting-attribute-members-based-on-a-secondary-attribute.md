---
title: 2次属性に基づく属性メンバーの並べ替え |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 67dacf68-9ab7-4524-8698-844d0f6e6c6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 067348432bc7a460b4dbf39444852e14c7ef2ce5
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69493907"
---
# <a name="sorting-attribute-members-based-on-a-secondary-attribute"></a>2 次属性に基づく属性メンバーの並べ替え
  レッスン 3 では、名前とキー値に基づいて属性メンバーを並べ替える方法を学習しました。 また、属性メンバーと並べ替え順序に影響する複合メンバー キーの使用方法も学習しました。 詳細については、「 [Date ディメンションの変更](lesson-3-4-modifying-the-date-dimension.md)」を参照してください。 ただし、属性の名前とキーのどちらを使用しても目的の順序での並べ替えを実現できない場合は、2 次属性を使用して目的の順序で並べ替えるようにすることもできます。 属性間にリレーションシップを定義すると、2 次属性を使用して、1 次属性のメンバーを並べ替えることができます。  
  
 属性リレーションシップは、属性間のリレーションシップまたは依存関係を定義します。 1 つのリレーショナル テーブルから派生しているディメンションでは、通常、キー属性を介してすべての属性が互いに関連付けられています。 これは、ディメンションのすべての属性によって、関連する各メジャー グループのファクト テーブル内のファクトにディメンションのキー属性によってリンクされているメンバーの情報が提供されるためです。 複数のテーブルから派生しているディメンションでは、通常、テーブル間の属性が結合キーに基づいて関連付けられています。 基になるデータでサポートされている場合は、関連属性を使用して並べ替え順序を指定できます。 たとえば、関連属性に並べ替えのロジックを提供する新しい属性を作成できます。  
  
 ディメンション デザイナーでは、属性間に新しいリレーションシップを定義できるほか、既定のリレーションシップを変更してパフォーマンスを向上させることができます。 属性リレーションシップを作成するときの主な制限は、参照元の属性のメンバーに対応する値が参照先の属性に複数あってはならない点です。 2 つの属性の間にリレーションシップを定義する際には、リレーションシップを変更できるようにするのか、または固定するのかを定義できます。どちらに指定するかは、メンバー間のリレーションシップが時間と共に変化するかどうかによります。 たとえば、従業員が別の販売地域に移動することはありますが、都市が別の州に移動することはありません。 リレーションシップを固定すると、ディメンションの処理が進むたびに属性の集計が再計算されるようなことはありません。 しかし、メンバー間のリレーションシップが変わる場合は、常にディメンションを処理する必要があります。 詳細については、「 [属性リレーションシップ](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」、「 [属性リレーションシップの定義](multidimensional-models/attribute-relationships-define.md)」、「 [属性リレーションシップのプロパティの構成](multidimensional-models/attribute-relationships-configure-attribute-properties.md)」、および「 [ユーザー定義階層の属性間での属性リレーションシップの指定](4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)」を参照してください。  
  
 このトピックの実習では、基になるディメンション テーブルの既存の列に基づき、 **Date** ディメンションに新しい属性を定義します。 この新しい属性を使用して、アルファベット順に並んでいるカレンダーの月メンバーを日付順に並べ替えます。 また、 **Commute Distance** 属性メンバーを並べ替える名前付き計算に基づいて、 **Customer** ディメンションに新しい属性を定義します。 次のトピックでは、属性リレーションシップを使用してクエリのパフォーマンスを向上させる方法について学習します。  
  
## <a name="defining-an-attribute-relationship-and-sort-order-in-the-date-dimension"></a>Date ディメンションの属性リレーションシップおよび並べ替え順序の定義  
  
1.  **Date** ディメンションのディメンション デザイナーを開きます。次に、[プロパティ] ウィンドウで、 **OrderBy** プロパティの **Month Name** 属性を確認します。  
  
     **Month Name** 属性のメンバーは、各メンバーのキー値の順に並んでいます。  
  
2.  **[ブラウザー]** タブに切り替え、 **[階層]** ボックスの一覧で **[Calendar Date]** が選択されていることを確認します。次に、ユーザー定義階層の各レベルを展開し、カレンダー月の並べ替え順序を確認します。  
  
     属性階層のメンバーは、ASCII 値である各メンバー キー (月と年) を基準にして並べ替えられています。 この場合、属性名やキーで並べ替えても、カレンダー月は日付順に並びません。 これを解決するには、新しい属性である **MonthNumberOfYear** 属性に基づいて属性階層のメンバーを並べ替えます。 この属性の基になる列がちょうど **Date** ディメンション テーブルにあるので、この列を使用して MonthNumberOfYear 属性を作成します。  
  
3.  Date ディメンションの **[ディメンションの構造]** タブに切り替え、 **[データ ソース ビュー]** ペインで **[MonthNumberOfYear]** を右クリックします。次に、 **[列から新しい属性を作成]** をクリックします。  
  
4.  **[属性]** ペインで、 **[Month Number Of Year]** をクリックします。次に、[プロパティ] ウィンドウで、 **AttributeHierarchyEnabled** プロパティを **False** に設定します。さらに、 **AttributeHierarchyOptimizedState** を **NotOptimized**に設定し、 **AttributeHierarchyOrdered** プロパティを **False**に設定します。  
  
     これらの設定により、ユーザーからはこの属性が見えなくなり、処理時間が短縮されます。 この属性は参照用には使用されません。 別の属性のメンバーを並べ替えるためにのみ使用されます。  
  
    > [!NOTE]  
    >  プロパティを [プロパティ] ウィンドウ内でアルファベット順に並べると、この 3 つのプロパティどうしが隣に並ぶので、このタスクが単純化されます。  
  
5.  **[属性リレーションシップ]** タブをクリックします。  
  
     **Date** ディメンションのすべての属性が **Date** 属性に直接関連付けられています。この Date 属性は、ディメンションのメンバーを関連するメジャー グループのファクトに関連付けているメンバー キーです。 **Month Name** 属性と **Month Number Of Year** 属性の間には、リレーションシップが何も定義されていません。  
  
6.  ダイアグラムで、 **[Month Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
7.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Month Name]** を指定します。 **[関連属性]** を **[Month Number Of Year]** に設定します。  
  
8.  **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
     **Month Name** 属性のメンバーおよび **Month Number Of Year** 属性のメンバー間のリレーションシップは、時間が経過しても変わりません。 その結果、増分処理中に、このリレーションシップの集計が削除されません。 このリレーションシップが変化すると、増分処理時に処理エラーが発生し、ディメンションの完全な処理を実行する必要が生じます。 以上の操作で、 **Month Name**のメンバーの並べ替え順序を設定する準備が整いました。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **[ディメンション構造]** タブをクリックします。  
  
11. **[属性]** ペインで、 **[Month Name]** をクリックします。次に、[プロパティ] ウィンドウの **[OrderBy]** プロパティの値を **AttributeKey** に変更し、 **[OrderByAttribute]** プロパティの値を **Month Number Of Year**に変更します。  
  
12. **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
13. 配置が正常に完了したら、Date ディメンションの **[ブラウザー]** タブに切り替え、 **[再接続]** をクリックします。次に、 **Calendar Date** および **Fiscal Date** ユーザー階層を表示し、月が日付順に並んでいることを確認します。  
  
     次の図のように、月が日付順に並べ替えられました。  
  
     変更された![ユーザー階層 (時間順])変更された(../../2014/tutorials/media/l4-memberproperties-3.gif "ユーザー階層 (時間順"))  
  
## <a name="defining-attribute-relationships-and-sort-order-in-the-customer-dimension"></a>Customer ディメンションの属性リレーションシップおよび並べ替え順序の定義  
  
1.  Customer ディメンションのディメンション デザイナーで **[ブラウザー]** タブに切り替え、 **Commute Distance** 属性階層のメンバーを表示します。  
  
     この属性階層のメンバーは、ASCII 値であるメンバー キーを基準に並べ替えられています。 この場合、属性名やキーで並べ替えても、通勤距離が短い順には並びません。 この実習では、列内の個々の値に対して数値を適切に並べ替える **CommuteDistanceSort** 名前付き計算に基づいて、メンバーを並べ替えます。 時間を節約するため、 **DW データ ソース ビューの** Customer [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] テーブルに、この名前付き計算が既に用意されています。 このデータ ソース ビューに切り替えれば、CommuteDistanceSort 名前付き計算で使用する SQL スクリプトを表示できます。 詳細については、「[データ ソース ビューでの名前付き計算の定義 &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)」をご覧ください。  
  
     次の図は、 **Commute Distance** 属性階層のメンバーを、ASCII 値のメンバー キーの順で表示しているようすを示します。  
  
     ![Commute Distance 属性階層](../../2014/tutorials/media/l4-memberproperties-4.gif "Commute Distance 属性階層")  
  
2.  Customer ディメンションのディメンション デザイナーで **[ディメンションの構造]** タブに切り替えます。次に、 **[データ ソース ビュー]** ペインで、 **[Customer]** テーブルの **[CommuteDistanceSort]** を右クリックして、 **[列から新しい属性を作成]** をクリックします。  
  
3.  **[属性]** ペインで、 **[Commute Distance Sort]** をクリックします。次に、[プロパティ] ウィンドウで、 **AttributeHierarchyEnabled** プロパティを **False** に設定します。さらに、 **AttributeHierarchyOptimizedState** を **NotOptimized**に設定し、 **AttributeHierarchyOrdered** プロパティを **False**に設定します。  
  
     これらの設定により、ユーザーからはこの属性が見えなくなり、処理時間が短縮されます。 この属性は参照用には使用されません。 別の属性のメンバーを並べ替えるためにのみ使用されます。  
  
4.  **[Geography]** をクリックします。次に、[プロパティ] ウィンドウで、 **AttributeHierarchyVisible** プロパティを **False** に設定します。さらに、 **AttributeHierarchyOptimizedState** プロパティを **NotOptimized**に設定し、 **AttributeHierarchyOrdered** プロパティを **False**に設定します。  
  
     これらの設定により、ユーザーからはこの属性が見えなくなり、処理時間が短縮されます。 この属性は参照用には使用されません。 別の属性のメンバーを並べ替えるためにのみ使用されます。 **Geography** にはメンバー プロパティが存在するので、その **AttributeHierarchyEnabled** プロパティを **True**に設定する必要があります。 したがって、この属性を非表示にするには、 **AttributeHierarchyVisible** プロパティを **False**に設定します。  
  
5.  **[属性リレーションシップ]** タブをクリックします。  
  
6.  属性の一覧で **[Commute Distance]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
7.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Commute Distance]** を指定します。 **[関連属性]** を **[Commute Distance Sort]** に設定します。  
  
8.  **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
     **Commute Distance** 属性のメンバーおよび **Commute Distance Sort** 属性のメンバー間のリレーションシップは、時間が経過しても変わりません。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     以上の操作で、 **Commute Distance** のメンバーの並べ替え順序を設定する準備が整いました。  
  
10. **[ディメンション構造]** タブをクリックします。  
  
11. **[属性]** ペインで、 **[Commute Distance]** をクリックします。次に、[プロパティ] ウィンドウの **[OrderBy]** プロパティの値を **AttributeKey**に変更し、 **OrderByAttribute** プロパティの値を **Commute Distance Sort**に変更します。  
  
12. **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
13. 配置が正常に完了したら、Customer ディメンションのディメンション デザイナーで **[ブラウザー]** タブをクリックし、 **[再接続]** をクリックします。次に、 **Commute Distance** 属性階層を表示します。  
  
     次の図のように、属性階層のメンバーは、通勤距離の長い順に論理的な順序で並べ替えられました。  
  
     ![Commute Distance 属性階層の再並べ替え](../../2014/tutorials/media/l4-memberproperties-5.gif "Commute Distance 属性階層の再並べ替え")  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [ユーザー定義階層の属性間での属性リレーションシップの指定](4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)  
  
  
