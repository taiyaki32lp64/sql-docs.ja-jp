---
title: 列の挿入または削除 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2796447d65a7fcabe029c67f460a76284daf242f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580204"
---
# <a name="insert-or-delete-a-column-report-builder-and-ssrs"></a>列の挿入または削除 (レポート ビルダーおよび SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートの Tablix データ領域では、列を追加したり削除したりできます。 Tablix データ領域は、テーブル、マトリックス、一覧のいずれかです。 次の手順は、グラフおよびゲージのデータ領域には適用されません。  
  
 Tablix データ領域では、グループに関連付けられている列 (グループ内の列)、またはグループに関連付けられていない列 (グループ外の列) を追加できます。 グループ内の列は、一意のグループ値ごとに 1 つ存在します。 たとえば、グループ内の列の値が、色名を格納するデータ列に基づいている場合、色名ごとに 1 つの列が存在することになります。 入れ子にされているグループの場合は、子グループの外側、かつ、親グループの内側に列を配置できます。 この場合は、親グループ内の一意の値ごとに 1 つの行が表示されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-that-the-row-and-column-handles-appear"></a>行ハンドルと列ハンドルが表示されるようにデータ領域を選択するには  
  
-   [デザイン] ビューで、Tablix データ領域の左上隅をクリックすると、その上部および横に列ハンドルと行ハンドルが表示されます。  
  
     詳細については、「 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)」をご覧ください。  
  
## <a name="to-insert-a-column-in-a-selected-data-region"></a>選択したデータ領域に列を挿入するには  
  
-   列の挿入位置にある列ハンドルを右クリックし、 **[列の挿入]** をクリックして、 **[左]** または **[右]** をクリックします。  
  
     -- または --  
  
-   データ領域で、行の挿入位置にあるセルを右クリックし、 **[列の挿入]** をクリックして、 **[左]** または **[右]** をクリックします。  
  
## <a name="to-delete-a-column-from-a-selected-data-region"></a>選択したデータ領域から列を削除するには  
  
-   削除する 1 つ以上の列を選択し、選択したいずれかの列のハンドルを右クリックして、 **[列の削除]** をクリックします。  
  
     -- または --  
  
-   データ領域で、列の削除位置にあるセルを右クリックして、 **[列の削除]** をクリックします。  
  
## <a name="to-insert-a-column-in-a-group-in-a-selected-data-region"></a>選択したデータ領域のグループに列を挿入するには  
  
-   Tablix データ領域の列グループ領域で、列の挿入位置にある列グループ セルを右クリックし、 **[列の挿入]** をクリックした後、 **[左 - 外側のグループ]** 、 **[左 - 内側のグループ]** 、 **[右 - 内側のグループ]** 、または **[右 - 外側のグループ]** をクリックします。  
  
     クリックした列グループのセルに対応するグループの内側または外側に列が追加されます。  
  
## <a name="to-delete-a-column-from-a-group-in-a-selected-data-region"></a>選択したデータ領域のグループから列を削除するには  
  
-   Tablix データ領域の列グループ領域で、列の削除位置にある列グループ セルを右クリックし、 **[列の削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [グループについて &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
