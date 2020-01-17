---
title: Tablix データ領域の柔軟性について (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fef19359-a618-4d21-a7e4-e391cdefd4eb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e2ed258caa8019b13ddd8600a5ada2956913977
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105947"
---
# <a name="exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs"></a>Tablix データ領域の柔軟性について (レポート ビルダーおよび SSRS)
  リボンの [挿入] タブからテーブル、マトリックス、または一覧のデータ領域を追加するとき、Tablix データ領域用の初期テンプレートを使用しますが、このテンプレートによって制限されることはありません。 グループ、行、列などの Tablix データ領域機能を追加または削除することによって、引き続きデータの表示方法を設定できます。  
  
 行グループや列グループを削除するとき、グループの値を表示するのに使用されている行や列を削除することもできます。 行や列を手動で追加または削除することもできます。 行や列を使用して詳細やグループ データを表示する方法については、「 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)」をご覧ください。  
  
 Tablix データ領域の構造を変更した後、プロパティを設定して、レポートでのデータ領域の表示方法を制御できます。たとえば、すべてのページの上部に列ヘッダーを繰り返し表示したり、グループでグループ ヘッダーを保持したりすることができます。 詳細については、「 [レポート ページでの Tablix データ領域の表示の制御 &#40;レポート ビルダーおよび SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="changing-a-table-to-a-matrix"></a>テーブルからマトリックスへの変更  
 既定のテーブルには、レポート データセットの値が表示される詳細行が含まれています。 テーブルには通常、詳細データをグループ別に整理する行グループが含まれており、各グループに基づいて集計された値が含められます。 テーブルをマトリックスに変更するには、列グループを追加します。 データ領域に行グループと列グループが両方ともある場合は、通常詳細グループを削除します。そうすることによって、グループの集計値のみを表示できます。 詳細については、「 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
 定義上、マトリックスを作成するときに Tablix コーナー セルを追加します。 この領域のセルを結合し、ラベルを追加できます。 詳細については、「[データ領域内のセルの結合 &#40;レポート ビルダーおよび SSRS&#41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="changing-a-matrix-to-a-table"></a>マトリックスからテーブルへの変更  
 既定のマトリックスには行グループと列グループが含まれていますが、詳細グループはありません。 マトリックスをテーブルに変更するには、列グループを削除し、詳細行上に表示する詳細グループを追加します。 詳細については、「[データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」および「[詳細グループの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-details-group-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="changing-a-default-list-to-a-grouped-list"></a>既定の一覧からグループ化された一覧への変更  
 既定の一覧には詳細行が含まれていますが、グループはありません。 グループ行を使用するように一覧を変更するには、詳細グループの名前を変更し、グループ式を指定します。 詳細については、「[データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="creating-stepped-displays"></a>階段状表示の作成  
 既定では、グループを Tablix データ領域に追加すると、行グループ ヘッダー領域内のセルの列にグループ値が表示されます。 入れ子構造のグループがあるときは、各グループが個別の列に表示されます。 階段状の表示を作成するには、1 つのグループ列を除いたすべてのグループ列を削除し、グループ階層をインデントされたテキスト表示として表示するように残りの列を書式設定します。 詳細については、「[階段状レポートの作成 &#40;レポート ビルダーおよび SSRS&#41;](create-a-stepped-report-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="adding-an-adjacent-details-group"></a>隣接する詳細グループの追加  
 既定では、詳細グループはグループ階層の最も内側にある子グループです。 詳細グループの下にグループを入れ子にすることはできません。 たとえば、売上で上位 5 つの製品と下位 5 つの製品を表示するように、隣接する詳細グループを追加で作成できます。 各グループでフィルターと並べ替え式を追加できるので、1 つの Tablix データ領域に同じデータセットの詳細データのビューを 2 つ表示できます。 詳細については、「[グループについて &#40;レポート ビルダーおよび SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)」、「[データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」、および「[データセットへのフィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
