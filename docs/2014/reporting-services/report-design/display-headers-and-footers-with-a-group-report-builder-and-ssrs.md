---
title: グループ単位でのヘッダーとフッターの表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b330b5aedaeff4cf73ad6dca3e88860dde0f90b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106060"
---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>グループ単位でのヘッダーとフッターの表示 (レポート ビルダーおよび SSRS)
  Tablix データ領域では、グループに関連付けられている動的行と一緒に、静的行 (グループ ヘッダー、グループ フッターなど) を表示するかどうかを制御できます。  
  
 複数のページですべての列見出しまたは行見出しを繰り返し表示するには、Tablix データ領域のプロパティを設定します。 詳細については、「[複数のページへの行および列ヘッダーの表示 &#40;レポート ビルダーおよび SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)」を参照してください。  
  
 入れ子になったグループに関連付けられている動的行と動的列の表示動作、または、ラベルや小計に関連付けられている静的行と静的列の表示動作を制御するには、Tablix メンバーのプロパティを設定する必要があります。 Tablix メンバーは、静的な行または列、あるいは動的な行または列を表します。 静的メンバーが表示されるのは 1 回だけです。 たとえば、代表的な静的行に、総計行があります。 動的メンバーは、1 グループにつき 1 回表示されます。 たとえば、特定のグループに対し [Territory] というグループ式が割り当てられているとき、そのグループに関連付けられている行は、一意の区域 (territory) 値ごとに 1 回表示されることになります。 Tablix のメンバーに関する詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。  
  
 Tablix メンバーのプロパティを設定するには、グループ化ペインで Tablix メンバーを選択し、プロパティ ペインで **KeepWithGroup**、 **KeepTogether**、および **RepeatOnNewPage** の各プロパティを設定します。 グループ ヘッダーとグループ フッターをグループと同じページに表示するには、 **KeepWithGroup** を使用します。 グループの行または列と一緒に静的メンバーを表示するには、 **KeepTogether** を使用します。 **KeepWithGroup** 値によって指定された行グループ メンバーの少なくとも 1 つの完全なインスタンスが表示されるページごとにグループ ヘッダーまたはグループ フッターを繰り返すには、 **RepeatOnNewPage** を使用します。 列グループ メンバーに対して、**RepeatOnNewPage** はサポートされません。  
  
> [!NOTE]  
>  **KeepWithGroup**、**KeepTogether**、および **RepeatOnNewPage** は、グループ化ペインの **[詳細設定モード]** を使用して設定できるグループ メンバーのプロパティです。 詳細については、「[グループ化ペイン &#40;レポート ビルダー&#41;](grouping-pane-report-builder.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>静的行を行グループに関連付けられている一連の動的行と一緒に表示するには  
  
1.  デザイン画面で、Tablix データ領域の任意の場所をクリックして選択します。 グループ化ペインに、データ領域の行グループと列グループが表示されます。  
  
2.  グループ化ペインの右側にある下矢印をクリックし、 **[詳細設定モード]** をクリックします。 行グループ ペインには、行グループ階層の静的メンバーおよび動的メンバーが階層的に表示されます。  
  
3.  グループ行と共に維持する行ヘッダーまたは行フッターに対応する静的メンバーをクリックします。 プロパティ ペインに **[Tablix メンバー]** プロパティが表示されます。  
  
4.  プロパティ ペインで、 **KeepWithGroup**をクリックし、ドロップダウン リストから次のいずれかの値を選択します。  
  
    -   **[なし]** 選択した行グループのメンバーと共にこのメンバーを維持しない場合は、このオプションを選択します。  
  
    -   **[前]** 前のグループのメンバーと共にこのメンバーを維持する場合は、このオプションを選択します。 このオプションはグループ フッター行に使用できます。  
  
    -   **[後]** 次のグループのメンバーと共にこのメンバーを維持する場合は、このオプションを選択します。 このオプションはグループ ヘッダー行に使用できます。  
  
5.  (省略可) レポートをプレビューします。 レポート レンダラーは、可能な限り、指定された行グループ メンバーと共にこのメンバーを維持します。  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>静的列を列グループに関連付けられている一連の動的列と一緒に表示するには  
  
1.  デザイン画面で、Tablix データ領域の任意の場所をクリックして選択します。 グループ化ペインに、データ領域の行グループと列グループが表示されます。  
  
2.  グループ化ペインの右側にある下矢印をクリックし、 **[詳細設定モード]** をクリックします。 列グループ ペインには、列グループ階層の静的メンバーおよび動的メンバーが階層的に表示されます。  
  
3.  グループ列と共に維持する静的列に対応する静的メンバーをクリックします。 プロパティ ペインに **[Tablix メンバー]** プロパティが表示されます。  
  
4.  プロパティ ペインで、 **KeepWithGroup**をクリックし、ドロップダウン リストから次のいずれかの値を選択します。  
  
    -   **[なし]** 選択した列グループのメンバーと共にこのメンバーを維持しない場合は、このオプションを選択します。  
  
    -   **[前]** 前のグループのメンバーと共にこのメンバーを維持する場合は、このオプションを選択します。 このオプションは、指定した列グループ メンバーの前に表示する列ラベルに使用できます。  
  
    -   **[後]** 次のグループのメンバーと共にこのメンバーを維持する場合は、このオプションを選択します。 このオプションは、指定した列グループ メンバーの後に表示する列の合計に使用できます。  
  
5.  (省略可) レポートをプレビューします。 可能な限り、レポート レンダラーは指定された列グループ メンバーと共にこのメンバーを維持します。  
  
## <a name="see-also"></a>関連項目  
 [Tablix データ領域のセル、行、および列&#40;レポート ビルダー&#41;と SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)   
 [Tablix データ領域部分&#40;レポート ビルダーおよび SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)   
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
