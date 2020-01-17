---
title: 属性メンバーの自動的なグループ化 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9fb2cda3-a122-4a4c-82e0-3454865eef04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6dc768188f25640a3685c8526bfceb3874154f40
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "69890833"
---
# <a name="automatically-grouping-attribute-members"></a>属性メンバーの自動的なグループ化
  キューブを表示するとき、通常は、ある属性階層のメンバーと別の属性階層のメンバーとを多次元化します。 たとえば、都市別、製品別、または性別ごとに顧客の売上をグループ化して表示します。 このとき、属性の種類によっては、属性階層内のメンバー分布に基づいて、属性が自動的にグループ化されるように [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] を設定しておくと便利です。 たとえば、顧客の年収に基づいてグループが作成されるように [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] を設定できます。 このようにグループ化した場合、属性階層を表示したときには、メンバーそのものではなく、グループの名前と値が表示されます。 ユーザーに提示されるレベル数が限定されるので、分析が容易になります。  
  
 **DiscretizationMethod** プロパティは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] にグループを作成させるかどうか、どのような種類のグループ化を実行するかを指定します。 既定では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] はグループ化を実行しません。 自動グループ化を有効にすると、属性の構造に基づいて、最適なグループ化の方法が [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] によって自動的に判断されます。また、次の一覧からいずれかのグループ化アルゴリズムを選択してグループ化の方法を指定することもできます。  
  
 **EqualAreas**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ディメンション メンバーの母集団全体がすべてのグループに均等に分散するように、グループ範囲が作成されます。  
  
 **Clusters**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] K-Means クラスタリング法とガウス分布を使用し、入力値に対して 1 次元クラスタリングが実行されます。 このオプションは、数値列でのみ使用できます。  
  
 グループ化方法を指定したら、 **DiscretizationBucketCount** プロパティでグループの数を指定します。 詳細については、「 [属性メンバーのグループ化 (分離)](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
 このトピックの実習では、 **Customer** ディメンションの年収値、 **Employees** ディメンションの病気休暇時間、および **Employees** ディメンションの休暇時間でグループ化を行います。 その後、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブを処理して表示し、メンバー グループの効果を確認します。 最後に、メンバー グループのプロパティを変更し、グループの種類を変更した場合の影響を確認します。  
  
## <a name="grouping-attribute-hierarchy-members-in-the-customer-dimension"></a>Customer ディメンションにおける属性階層メンバーのグループ化  
  
1.  ソリューション エクスプローラーで、 **[ディメンション]** フォルダーの **Customer** をダブルクリックし、Customer ディメンションのディメンション デザイナーを開きます。  
  
2.  **[データ ソース ビュー]** ペインで **Customer** テーブルを右クリックし、 **[データの探索]** をクリックします。  
  
     **YearlyIncome** 列の値の範囲に注目してください。 メンバーをグループ化しない限り、これらの値は **Yearly Income** 属性階層のメンバーになります。  
  
3.  **[Customer テーブルの探索]** タブを閉じます。  
  
4.  **[属性]** ペインで、 **[Yearly Income]** を選択します。  
  
5.  プロパティウィンドウで、 **DiscretizationMethod**プロパティの値を**Automatic**に変更し、 **DiscretizationBucketCount**プロパティの値を `5` に変更します。  
  
     次の図は、変更後の **Yearly Income**プロパティを示しています。  
  
     ![年収の変更されたプロパティ](../../2014/tutorials/media/l4-discretizationmethod-1.gif "年収の変更されたプロパティ")  
  
## <a name="grouping-attribute-hierarchy-members-in-the-employee-dimension"></a>Employee ディメンションにおける属性階層メンバーのグループ化  
  
1.  Employee ディメンションのディメンション デザイナーに切り替えます。  
  
2.  **[データ ソース ビュー]** ペインで **Employee** テーブルを右クリックし、 **[データの探索]** をクリックします。  
  
     **SickLeaveHours** 列および **VacationHours** 列の値に注目してください。  
  
3.  **[Employee テーブルの探索]** タブを閉じます。  
  
4.  **[属性]** ペインで、 **[Sick Leave Hours]** を選択します。  
  
5.  プロパティウィンドウで、 **DiscretizationMethod**プロパティの値を**クラスター**に変更し、 **DiscretizationBucketCount**プロパティの値を `5` に変更します。  
  
6.  **[属性]** ペインで、 **[Vacation Hours]** を選択します。  
  
7.  プロパティウィンドウで、 **DiscretizationMethod**プロパティの値を**Equal Areas**に変更し、 **DiscretizationBucketCount**プロパティの値を `5` に変更します。  
  
## <a name="browsing-the-modified-attribute-hierarchies"></a>変更した属性階層の表示  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、 **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーに切り替え、 **[ブラウザー]** タブのツール バーで **[再接続]** をクリックします。  
  
3.  Excel アイコンをクリックし、 **[有効化]** をクリックします。  
  
4.  **Internet Sales-Sales Amount** メジャーをピボットテーブル フィールド リストの値領域にドラッグします。  
  
5.  フィールド リストで **Product** ディメンションを展開します。次に、 **[Product Model Lines]** ユーザー階層をフィールド リストの **[行ラベル]** 領域にドラッグします。  
  
6.  フィールド リストで **Customer** ディメンションを展開し、 **Demographic** 表示フォルダーを展開します。次に、 **Yearly Income** 属性階層を **[列ラベル]** 領域にドラッグします。  
  
     **Yearly Income** 属性階層のメンバーが 6 つのバケットにグループ化されました。この中には、年収が不明である顧客への売上のバケットも含まれています。 すべてのバケットが表示されるわけではありません。  
  
7.  列領域から **Yearly Income** 属性階層を削除し、 **[値]** 領域から **Internet Sales-Sales Amount** メジャーを削除します。  
  
8.  **Reseller Sales-Sales Amount** メジャーをデータ領域に追加します。  
  
9. フィールド リストで **Employee** ディメンションを展開し、 **Organization**を展開します。次に、 **[Sick Leave Hours]** を **[列ラベル]** にドラッグします。  
  
     2 つのグループのうちの 1 つは、すべて従業員によって売り上げられた売上データです 病欠時間が 32 ～ 42 時間の従業員は、病欠時間が 20 ～ 31 時間の従業員よりも大幅に売り上げていることもわかります。  
  
     次の図は、従業員の病欠時間別の売上ディメンションを示します。  
  
     ![従業員の病欠時間別の売上](../../2014/tutorials/media/l4-discretizationmethod-2.gif "従業員の病欠時間別の売上")  
  
10. **データ** ペインの列領域から **Sick Leave Hours** 属性階層を削除します。  
  
11. **Vacation Hours** を **データ** ペインの列領域に追加します。  
  
     EqualAreas グループ化方法に基づいて、2 つのグループが表示されます。 他の 3 つのグループはデータ値がないため、表示されません。  
  
## <a name="modifying-grouping-properties-and-reviewing-the-effect-of-the-changes"></a>グループ化のプロパティの変更と、その影響の確認  
  
1.  **Employee** ディメンションのディメンション デザイナーに切り替え、 **[属性]** ペインで **[Vacation Hours]** を選択します。  
  
2.  [プロパティ] ウィンドウで、 **DiscretizationBucketCount** プロパティの値を **10**に変更します。  
  
3.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で、 **[ビルド]** メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
4.  配置が正常に完了したら、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーに戻ります。  
  
5.  **[ブラウザー]** タブで **[再接続]** をクリックし、Excel アイコンをクリックします。グループ化の方法を変更した場合の影響を確認できるように、次のようにピボットテーブルを再構築します。  
  
    1.  Reseller Sales-Sales Amount を [値] にドラッグする  
  
    2.  Vacation Hours (Employees Organization フォルダー内) を [列] にドラッグする  
  
    3.  Product Model Lines を [行] にドラッグする  
  
     **Vacation Hours** 属性メンバーのグループが 3 つあります。各メンバーに製品の売上の値が含まれています (他の 7 つのグループには、売上データのあるメンバーが存在しません)。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [属性階層の非表示化と無効化](lesson-4-4-hiding-and-disabling-attribute-hierarchies.md)  
  
## <a name="see-also"></a>「  
 [属性メンバーのグループ化 (分離)](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
  
