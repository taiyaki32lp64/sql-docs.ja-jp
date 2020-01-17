---
title: グループ化ペイン (レポート ビルダー) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10033"
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 983ee5a4-944c-491e-8720-7cd9f3881961
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: aad20a916864bb8ed0d281af768989a0a7d9e85a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572198"
---
# <a name="grouping-pane-report-builder"></a>グループ化ペイン (レポート ビルダー)
  グループ化ペインには、現在選択されている Tablix データ領域の行グループと列グループが表示されます。 グラフおよびゲージのデータ領域では、グループ化ペインは使用できません。 グループ化ペインには、行グループ ペインと列グループ ペインが含まれています。 グループ化ペインには、既定モードと詳細設定モードの 2 つのモードがあります。 既定モードでは、行グループおよび列グループの動的メンバーの階層ビューが表示されます。 詳細設定モードでは、行グループと列グループの動的メンバーと静的メンバーの両方が表示されます。 グループは、データ領域に表示されるレポート データセットの名前付きセットです。 グループは、静的および動的なメンバーを含む階層で構成されます。 詳細については、「[グループについて &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  グループ化ペインが表示されない場合は、 **[表示]** タブの **[表示/非表示]** グループで、 **[グループ化]** をクリックします。  
  
 行グループ領域と列グループ領域のセルは、Tablix の行グループまたは列グループの静的メンバーまたは動的メンバーです。 静的メンバーはグループごとに 1 回繰り返され、通常、ラベルまたは合計が格納されています。 動的メンバーはグループ インスタンスごとに 1 回繰り返され、通常、グループ式の固有の値が格納されています。 行グループ領域または列グループ領域で Tablix セルを選択すると、対応するグループ メンバーが行グループ ペインまたは列グループ ペインで選択されます。 反対に、グループ化ペインでグループを選択すると、そのグループ メンバーに関連した対応するセルがデザイン画面で選択されます。 Tablix の行グループ領域と列グループ領域の詳細については、「[Tablix データ領域部分 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md)」を参照してください。  
  
 グループ化ペインでは、次のモードがサポートされています。  
  
-   **既定値です。** グループの追加、編集、削除を行うには、既定モードを使用します。 レポート データ ペインからフィールドをドラッグし、グループ階層に挿入することによって、親グループ、子グループ、および詳細グループを追加できます。 隣接するグループを追加するには、 **[グループの追加]** ショートカットを使用する必要があります。 詳細については、「 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
-   **詳細設定**。 行グループと列グループのすべてのメンバーを表示し、静的メンバーのプロパティを設定するには、 **詳細設定モード** を使用します。 グループを作成したり合計を追加したりすると、Tablix データ領域で各レポート ページの行と列の表示方法を制御するプロパティが自動的に設定されます。 これらのプロパティを手動で調整するには、Tablix メンバーのプロパティを設定する必要があります。 詳細については、「 [レポート ページでの Tablix データ領域の表示の制御 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)」を参照してください。  
  
## <a name="default-mode"></a>既定モード  
 既定モードでは、行グループ ペインと列グループ ペインにすべての親グループ、子グループ、および隣接グループの階層ビューが表示されます。 子グループは親グループの下にインデント表示されます。 隣接グループは、その兄弟グループと同じインデント レベルに表示されます。 次の図に、行グループと隣接列グループが入れ子になった Tablix データ領域を示します。  
  
 ![Tablix、入れ子になった隣接する行と列のグループ](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix、入れ子になった隣接する行と列のグループ")  
  
 グループ化ペインには、対応する行グループと列グループが表示されます。 次の図では、サブカテゴリに基づくグループが行グループ ペインで選択され、[Subcat] グループ化セルが Tablix データ領域で選択されています。  
  
 ![入れ子になった行と列のグループのグループ化ペイン](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "入れ子になった行と列のグループのグループ化ペイン")  
  
 行グループ ペインでは、サブカテゴリに基づくグループは、カテゴリに基づくグループの子になります。 列グループ ペインでは、国/地域グループは地理グループの子になります。 年度グループと国/地域グループは、隣接するグループです。  
  
 詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="advanced-mode"></a>詳細設定モード  
 詳細設定モードでは、行グループ ペインと列グループ ペインに、静的メンバーと動的メンバーを含む、すべてのグループの階層ビューが表示されます。 メンバーを選択すると、現在選択されている Tablix メンバーのプロパティが [プロパティ] ペインに表示されます。  
  
> [!NOTE]  
>  **詳細設定モード**に切り替えるには、列グループ ペインの横の下向き矢印を右クリックして **[詳細設定モード]** をクリックします。  
  
 ほとんどの場合、静的および動的グループ行とグループ列の表示を制御するプロパティは、グループの作成時または合計の追加時に自動設定されます。 既定値を編集するには、行グループ ペインまたは列グループ ペインでグループ メンバーを選択し、[プロパティ] ウィンドウでプロパティ値を変更する必要があります。 使用できるプロパティは次のとおりです。  
  
-   **FixedData**。 Boolean です。 外部行ヘッダーおよび外部列ヘッダーに使用します。 HTML などのレンダラーで、縦にスクロールする場合は行グループ領域を固定し、横にスクロールする場合は列グループ領域を固定します。  
  
-   **HideIfNoRows**。 Boolean です。 静的メンバーにのみ使用します。 設定した場合、Hidden と ToggleItem は無視されます。 Tablix データ領域に行データが含まれていない場合は、このメンバーを非表示にしてください。  
  
-   **KeepTogether**。 Boolean です。 可能な場合、Tablix メンバー全体および入れ子になっているすべてのメンバーを 1 ページにまとめるように指定します。  
  
-   **KeepWithGroup**。 Boolean です。 静的行メンバーにのみ使用します。 可能な場合、非表示でなければ、この行が前の動的な兄弟メンバーまたは次の動的な兄弟メンバーに付随するようにします。 行ヘッダーをその関連グループと一緒に表示するには KeepWithGroup を **After**に設定します。  
  
-   **RepeatOnNewPage**。 Boolean です。 静的行メンバー専用であり、KeepWithGroup の値が [なし] 以外の場合に使用します。 可能な場合、KeepWithGroup で指定された動的メンバーのインスタンスが少なくとも 1 つ含まれるページごとに、この静的行を繰り返します。 行ヘッダーをその関連グループと一緒に表示するには RepeatOnNewPage を **True**に設定します。  
  
-   **Hidden**。 Boolean です。 行または列を初期設定で非表示にしておくかどうかを示します。  
  
-   **ToggleItem。** 文字列です。 切り替えイメージを追加するテキスト ボックスの名前。 テキスト ボックスは、同じグループのスコープまたはコンテナー スコープに存在する必要があります。  
  
 詳細については、「[レポート ページでの Tablix データ領域の表示の制御 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)」、「[グループ単位でのヘッダーとフッターの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)」、「[複数のページへの行および列ヘッダーの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)」を参照してください。  
  
 すべての静的メンバーにデザイン画面のセルに対応するヘッダーがあるわけではありません。 グループ化ペインでは、次の規則を使用して静的メンバーにヘッダーがあるかどうかを示します。  
  
-   **Static** 静的メンバーにヘッダー セルがあります。  
  
-   **(Static)** 静的メンバーにはヘッダー セルがなく、非表示静的と呼ばれます。  
  
## <a name="see-also"></a>参照  
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
