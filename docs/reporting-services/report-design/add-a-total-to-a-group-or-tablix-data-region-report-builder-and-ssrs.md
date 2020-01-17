---
title: グループまたは Tablix データ領域への合計の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: cf1b96c3-7f0f-4c94-ad08-5239c77ccfe4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f751557bf0124466960182ebf50029bd1e34282f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582133"
---
# <a name="add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs"></a>グループまたは Tablix データ領域への合計の追加 (レポート ビルダーおよび SSRS)
 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートでは、グループまたはデータ領域全体の Tablix データ領域に合計を追加できます。 既定では、合計は、フィルターを適用した後のグループまたはデータ領域内の NULL 以外の数値データの合計です。 グループに合計を追加するには、グループ化ペインでグループのショートカット メニューの **[合計の追加]** をクリックします。 Tablix 本体領域の個々のセルの合計を追加するには、セルのショートカット メニューの **[合計の追加]** をクリックします。 **[合計の追加]** は状況依存のコマンドで、数値フィールドでのみ有効です。 選択した Tablix セルに応じて、Tablix 本体領域のセルを選択して 1 つのセルの合計を追加することも、Tablix 行グループ領域または Tablix 列グループ領域のセルを選択してグループ全体の合計を追加することもできます。 Tablix 領域の詳細については、「 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
 合計を追加した後、既定の関数 Sum を組み込みのレポート関数の一覧に含まれる別の集計関数に変更できます。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。 [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-total-for-an-individual-value-in-the-tablix-body-area"></a>Tablix 本体領域の個々の値の合計を追加するには  
  
-   Tablix データ領域の本体領域で、合計を追加するセルを右クリックします。 そのセルには数値フィールドが含まれている必要があります。 **[合計の追加]** をポイントして **[行]** または **[列]** をクリックします。  
  
     現在のグループの外側の新しい行または列がデータ領域に追加され、クリックしたセルのフィールドの既定の合計が表示されます。  
  
     Tablix データ領域がテーブルの場合は、行が自動的に追加されます。  
  
## <a name="to-add-totals-for-a-row-group"></a>行グループの合計を追加するには  
  
-   Tablix データ領域の行グループ領域で、合計する行グループ領域内のセルを右クリックし、 **[合計の追加]** をポイントして **[前]** または **[後]** をクリックします。  
  
     現在のグループの外側の新しい行がデータ領域に追加され、行の各数値フィールドの既定の合計が追加されます。  
  
## <a name="to-add-totals-for-a-column-group"></a>列グループの合計を追加するには  
  
-   Tablix データ領域の行グループ領域で、合計する列グループ領域内のセルを右クリックし、 **[合計の追加]** をポイントして **[前]** または **[後]** をクリックします。  
  
     現在のグループの外側の新しい列がデータ領域に追加され、列の各数値フィールドの既定の合計が追加されます。  
  
## <a name="see-also"></a>参照  
 [合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
