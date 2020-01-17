---
title: レポートのスクロール時にヘッダーを表示したままにする (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 6d9192a4-fd5c-41ad-b9ef-f88f9496afed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 61263520f5d519c2b908c753b72c1d5ec7f67e13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580138"
---
# <a name="keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs"></a>レポートのスクロール時にヘッダーを表示したままにする (レポート ビルダーおよび SSRS)
  レポートを表示した後に、スクロールによって行ラベルや列ラベルが隠れないようにするために、行見出しまたは列見出しを固定できます。  
  
 行と列を制御する方法は、テーブルとマトリックスのどちらを使用しているかによって異なります。 テーブルを使用している場合は、静的メンバー (行見出しと列見出し) を表示したままにするよう構成します。 マトリックスを使用している場合は、行と列のグループ ヘッダーを表示したままにするよう構成します。  
  
 レポートを Excel にエクスポートしても、ヘッダーは自動的には固定表示されません。 Excel でウィンドウ枠を固定できます。 詳細については、「[Microsoft Excel へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)」の「**ページ ヘッダーとページ フッター**」を参照してください。  
  
> [!NOTE]  
>  テーブルに行グループおよび列グループがある場合でも、スクロール中にこれらのグループ ヘッダーを表示したままにすることはできません。  
  
 次の図はテーブルを示しています。  
  
 ![テーブル](../../reporting-services/report-design/media/table.png "テーブル")  
  
 次の図はマトリックスを示しています。  
  
 ![マトリックス](../../reporting-services/report-design/media/matrix.png "マトリックス")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-matrix-group-headers-visible-while-scrolling"></a>スクロール中もマトリックス グループ ヘッダーを表示したままにするには  
  
1.  Tablix データ領域の行、列、またはコーナー ハンドルを右クリックし、 **[Tablix のプロパティ]** をクリックします。  
  
2.  **[全般]** タブの **[行のヘッダー]** または **[列のヘッダー]** で、 **[スクロール中もヘッダーを表示したままにする]** チェック ボックスをオンにします。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-keep-a-static-tablix-member-row-or-column-visible-while-scrolling"></a>スクロール中も静的 Tablix メンバー (行または列) を表示したままにするには  
  
1.  デザイン画面でテーブル内の任意の場所をクリックし、グループ化ペインにグループと静的メンバーを表示します。  
  
     ![グループ化ペイン](../../reporting-services/report-design/media/grouppane-updated.png "グループ化ペイン")  
  
     行グループ ペインに、行グループ階層の静的メンバーおよび動的メンバーが階層的に表示され、列グループ ペインに、列グループ階層のメンバーが同様に表示されます。  
  
2.  グループ化ペインの右側にある下矢印をクリックし、 **[詳細設定モード]** をクリックします。  
  
3.  スクロール中も表示したままにする静的メンバー (行または列) をクリックします。 プロパティ ペインに **[Tablix メンバー]** プロパティが表示されます。  
  
     ![Tablix メンバー プロパティ](../../reporting-services/report-design/media/grouppane-tablixmember-updated.png "Tablix メンバー プロパティ")  
  
4.  プロパティ ペインで、 **[FixedData]** を **True**に設定します。  
  
5.  スクロール中も表示したままにするすべての隣接するメンバーに対して、この手順を繰り返します。  
  
6.  レポートをプレビューします。  
  
 レポートを下方向または横方向にスクロールしたときに、静的な Tablix メンバーが表示されたままになります。  
  
## <a name="see-also"></a>参照  
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [グループ単位でのヘッダーとフッターの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [複数のページへの行および列ヘッダーの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)   
 [グループ化ペイン &#40;レポート ビルダー&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)  
  
  
