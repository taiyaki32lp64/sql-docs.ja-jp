---
title: ユーザー定義階層の属性間の属性リレーションシップの指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 838185def1d562f51d810cebdf79684f341a5903
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69493849"
---
# <a name="specifying-attribute-relationships-between-attributes-in-a-user-defined-hierarchy"></a>ユーザー定義階層の属性間での属性リレーションシップの指定
  このチュートリアルで既に学習したように、ユーザー階層に属性階層を配置し、キューブ内を移動するためのパスを作ることができます。 ユーザー階層は、市区町村、州、国などの一般階層を表せるほか、従業員名、役職、部署名のように操作パスのみを表すこともできます。 階層内を移動するユーザーにとっては、どちらのユーザー階層も変わりません。  
  
 一般階層で、各層を構成する属性間に属性リレーションシップが定義されている場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、1 つの階層の集計結果を使用して、その階層に関連付けられている別の階層の結果を取得することができます。 属性間にリレーションシップを定義していない場合は、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] によってキー属性からすべての非キー属性が集計されます。 そのため、基になるデータで属性リレーションシップがサポートされる場合、属性間の属性リレーションシップを定義する必要があります。 属性リレーションシップを定義すると、ディメンション、パーティション、およびクエリの処理パフォーマンスが向上します。 詳細については、「[属性リレーションシップの定義](multidimensional-models/attribute-relationships-define.md)」および「[属性リレーションシップ](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」を参照してください。  
  
 属性リレーションシップを定義する際、リレーションシップを変更できるようにするのか、または固定するのかを指定できます。 固定のリレーションシップを定義した場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] によってディメンションの更新時の集計が保持されます。 固定のリレーションシップを変更すると、ディメンションが完全に処理されない限り、処理の途中で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] によってエラーが生成されます。 適切なリレーションシップとリレーションシップのプロパティを指定すると、クエリ パフォーマンスと処理パフォーマンスが向上します。 詳細については、「[属性リレーションシップの定義](multidimensional-models/attribute-relationships-define.md)」および「[ユーザー階層プロパティ](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)」を参照してください。  
  
 このトピックの実習では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial プロジェクトの一般ユーザー階層の属性に属性リレーションシップを定義します。 対象となるのは、 **Customer** ディメンションの **Customer Geography**階層、 **Sales Territory** ディメンションの **Sales Territory** 階層、 **Product** ディメンションの **Product Model Lines** 階層、 **Date** ディメンションの **Fiscal Date** 階層と **Calendar Date** 階層です。 これらのユーザー階層は、すべて一般階層です。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Customer Geography 階層の属性に対する属性リレーションシップの定義  
  
1.  Customer ディメンションのディメンション デザイナーに切り替え、 **[ディメンション構造]** タブをクリックします。  
  
     **[階層]** ペインを見ると、 **Customer Geography** ユーザー定義階層に複数のレベルがあることがわかります。 レベル間または属性間のリレーションシップが定義されていないため、この階層は、現時点ではまだユーザー用ドリルダウン パスにすぎません。  
  
2.  **[属性リレーションシップ]** タブをクリックします。  
  
     **Geography** テーブルの非キー属性を **Geography** テーブルのキー属性にリンクする 4 つの属性リレーションシップがあります。 **Geography** 属性が **Full Name** 属性に関連付けられています。 **Geography** 属性を介して、 **Postal Code** 属性が **Full Name** 属性に間接的にリンクしています。 **Postal Code** 属性は **Geography** 属性にリンクし、 **Geography** 属性は **Full Name** 属性にリンクしているためです。 次に、属性リレーションシップを変更して、 **Geography** 属性を使用できないようにします。  
  
3.  ダイアグラムで、 **[Full Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
4.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** を **[Full Name]** にします。 **[関連属性]** を **[Postal Code]** に設定します。 時間が経過するとメンバー間のリレーションシップが変化する可能性があるため、 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類の設定は **[可変]** のままにします。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     リレーションシップが重複しているため、ダイアグラムに警告アイコンが表示されます。 リレーションシップ **Full Name** -> **Geography**-> **Postal Code** が既に存在する状態で、リレーションシップ **Full Name** -> **Postal Code**を作成しました。 リレーションシップ **Geography**-> **Postal Code** が重複しているため、このリレーションシップを削除します。  
  
6.  **[属性リレーションシップ]** ペインで、 **[Geography**-> **Postal Code]** を右クリックし、 **[削除]** をクリックします。  
  
7.  **[オブジェクトの削除]** ダイアログ ボックスが表示されたら、 **[OK]** をクリックします。  
  
8.  ダイアグラムで、 **[Postal Code]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
9. **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Postal Code]** を指定します。 **[関連属性]** を **[City]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類の設定を **[可変]** のままにします。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     リレーションシップ **Geography**-> **City** が重複しているため、このリレーションシップを削除します。  
  
11. [属性リレーションシップ] ペインで、 **[Geography**-> **City]** を右クリックし、 **[削除]** をクリックします。  
  
12. **[オブジェクトの削除]** ダイアログ ボックスが表示されたら、 **[OK]** をクリックします。  
  
13. ダイアグラムで、 **[City]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
14. **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[City]** を指定します。 **[関連属性]** を **[State-Province]** に設定します。 市区町村と都道府県のリレーションシップは時間が経過しても変化しないので、 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. **[Geography]** と **[State-Province]** の間の矢印を右クリックし、 **[削除]** をクリックします。  
  
17. **[オブジェクトの削除]** ダイアログ ボックスが表示されたら、 **[OK]** をクリックします。  
  
18. ダイアグラムで、 **[State-Province]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
19. **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[State-Province]** を指定します。 **[関連属性]** を **[Country-Region]** に設定します。 都道府県と国/地域のリレーションシップは時間が経過しても変化しないので、 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. [属性リレーションシップ] ペインで、 **[Geography**-> **Country-Region]** を右クリックし、 **[削除]** をクリックします。  
  
22. **[オブジェクトの削除]** ダイアログ ボックスが表示されたら、 **[OK]** をクリックします。  
  
23. **[ディメンション構造]** タブをクリックします。  
  
     **Geography** と他の属性との最後の属性リレーションシップを削除すると、その **Geography** 自体が削除されます。 その後は属性が使用されなくなるためです。  
  
24. [ファイル] メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Sales Territory 階層の属性に対する属性リレーションシップの定義  
  
1.  **Sales Territory** ディメンションのディメンション デザイナーを開き、 **[属性リレーションシップ]** タブをクリックします。  
  
2.  ダイアグラムで、 **[Sales Territory Country]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Sales Territory Country]** を指定します。 **[関連属性]** を **[Sales Territory Group]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類の設定を **[可変]** のままにします。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     **Sales Territory Group** が **Sales Territory Country**にリンクされ、 **Sales Territory Country** が **Sales Territory Region**にリンクされました。 国内の販売グループや販売区域は時間と共に変わることがあり、各国の販売グループの編成も時間と共に変わる可能性があるので、これらのリレーションシップの **RelationshipType** プロパティは **Flexible** に設定します。  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Product Model Lines 階層の属性に対する属性リレーションシップの定義  
  
1.  **Product** ディメンションのディメンション デザイナーを開き、 **[属性リレーションシップ]** タブをクリックします。  
  
2.  ダイアグラムで、 **[Model Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Model Name]** を指定します。 **[関連属性]** を **[Product Line]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類の設定を **[可変]** のままにします。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Fiscal Date 階層の属性に対する属性リレーションシップの定義  
  
1.  **Date** ディメンションのディメンション デザイナーに切り替えて、 **[属性リレーションシップ]** タブをクリックします。  
  
2.  ダイアグラムで、 **[Month Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Month Name]** を指定します。 **[関連属性]** を **[Fiscal Quarter]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  ダイアグラムで、 **[Fiscal Quarter]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
6.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Fiscal Quarter]** を指定します。 **[関連属性]** を **[Fiscal Semester]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  ダイアグラムで、 **[Fiscal Semester]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
9. **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Fiscal Semester]** を指定します。 **[関連属性]** を **[Fiscal Year]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Calendar Date 階層の属性に対する属性リレーションシップの定義  
  
1.  ダイアグラムで、 **[Month Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
2.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Month Name]** を指定します。 **[関連属性]** を **[Calendar Quarter]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  ダイアグラムで、 **[Calendar Quarter]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
5.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Calendar Quarter]** を指定します。 **[関連属性]** を **[Calendar Semester]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  ダイアグラムで、 **[Calendar Semester]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
8.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Calendar Semester]** を指定します。 **[関連属性]** を **[Calendar Year]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Geography 階層の属性に対する属性リレーションシップの定義  
  
1.  Geography ディメンションのディメンション デザイナーを開き、 **[属性リレーションシップ]** タブをクリックします。  
  
2.  ダイアグラムで、 **[Postal Code]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Postal Code]** を指定します。 **[関連属性]** を **[City]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[可変]** に設定します。  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  ダイアグラムで、 **[City]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
6.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[City]** を指定します。 **[関連属性]** を **[State-Province]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  ダイアグラムで、 **[State-Province]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
9. **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[State-Province]** を指定します。 **[関連属性]** を **[Country-Region]** に設定します。 **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. ダイアグラムで、 **[Geography Key]** 属性を右クリックし、 **[プロパティ]** をクリックします。  
  
12. **AttributeHierarchyOptimizedState** プロパティを **NotOptimized**に設定し、 **AttributeHierarchyOrdered** プロパティを **False**に設定し、 **AttributeHierarchyVisible** プロパティを **False**に設定します。  
  
13. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
14. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、 **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [不明なメンバーと NULL 処理のプロパティの定義](lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>関連項目  
 [属性リレーションシップの定義](multidimensional-models/attribute-relationships-define.md)   
 [ユーザー階層プロパティ](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
