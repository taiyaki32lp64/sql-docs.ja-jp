---
title: 行の挿入または削除 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b20b95586e387484d536ad8005c6f57c1de4698
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580170"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>行の挿入または削除 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートの Tablix データ領域では、行を追加したり削除したりできます。 Tablix データ領域は、テーブル、マトリックス、一覧のいずれかです。 次の手順は、グラフおよびゲージのデータ領域には適用されません。  
  
 Tablix データ領域では、グループに関連付けられている行 (グループ内の行)、または、グループに関連付けられていない行 (グループ外の行) を追加できます。 グループ内の行は、一意のグループ値ごとに 1 つ存在します。 たとえば、グループ内の行が、色名を格納するデータ列の値に基づいている場合、色名ごとに 1 つの行が存在することになります。 入れ子にされているグループの場合は、行を子グループの外側、かつ親グループの内側に置くことができます。 この場合は、親グループ内の一意の値ごとに 1 つの行が表示されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>行ハンドルと列ハンドルが表示されるようにデータ領域を選択するには  
  
-   [デザイン] ビューで、Tablix データ領域の左上隅をクリックすると、その上部および横に列ハンドルと行ハンドルが表示されます。  
  
     詳細については、「 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)」をご覧ください。  
  
## <a name="to-insert-a-row-in-a-selected-data-region"></a>選択したデータ領域に行を挿入するには  
  
-   行の挿入位置にある行ハンドルを右クリックし、 **[行を挿入]** をクリックして、 **[上]** または **[下]** をクリックします。  
  
     \- - または -  
  
-   行の挿入位置にあるデータ領域のセルを右クリックし、 **[行を挿入]** をクリックし、 **[上]** または **[下]** をクリックします。  
  
## <a name="to-delete-a-row-from-a-selected-data-region"></a>選択したデータ領域から行を削除するには  
  
-   削除する行を選択し、選択した行のうち 1 つのハンドルを右クリックして、 **[行の削除]** をクリックします。  
  
     \- - または -  
  
-   行の削除位置にあるデータ領域のセルを右クリックし、 **[行の削除]** をクリックします。  
  
## <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>選択したデータ領域のグループに行を挿入するには  
  
-   Tablix データ領域の行グループ領域で、行の挿入位置の行グループのセルを右クリックし、 **[行を挿入]** をクリックした後、 **[上 - 外側のグループ]** 、 **[上 - 内側のグループ]** 、 **[下 - 内側のグループ]** 、または **[下 - 外側のグループ]** をクリックします。  
  
     クリックした行グループのセルに対応するグループの内側または外側に行が追加されます。  
  
## <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>選択したデータ領域のグループから行を削除するには  
  
-   Tablix データ領域の行グループ領域で、行の削除位置にある行グループ セルを右クリックし、 **[行の削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [グループについて &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)     
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
