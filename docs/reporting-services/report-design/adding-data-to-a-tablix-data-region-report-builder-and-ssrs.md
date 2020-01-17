---
title: Tablix データ領域へのデータの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 847e3f6e7e76041749b0588bff510caebed11817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581884"
---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>Tablix データ領域へのデータの追加 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートで、レポート データセットのデータをテーブルまたはマトリックス形式で表示するには、各データ セルで表示するデータセット フィールドの名前を指定します。 詳細データまたはグループ化されたデータを表示できます。 グループをテーブルまたはマトリックスに追加すると、グループの値およびデータの行と列が自動的に追加されます。 データの小計および合計を追加できます。  
  
 データ領域内のすべてのデータは、少なくとも 1 つのグループに属しています。 詳細データは、詳細グループのメンバーです。 詳細データとグループ化されたデータの詳細については、「[グループについて &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>詳細データの追加  
 詳細データは、データセット、データ領域、および詳細グループにフィルターが適用された後のレポート データセットのすべてのデータです。 1 つの Tablix データ領域に表示されるすべての詳細データは、同じレポート データセットから取得されます。  
  
 レポート データセットの詳細データを Tablix データ領域に追加するには、レポート データ ペインから詳細行の各セルにデータセット フィールドをドラッグします。 Tablix データ領域内の既存のセルについては、各セルのフィールド セレクターを使用するか、レポート データ ペインからセルにフィールドをドラッグすることによって、データセット フィールド式を追加または編集できます。 追加の列を作成するには、レポート データ ペインからフィールドをドラッグし、既存の Tablix データ領域に挿入します。  
  
 既定では、実行時に詳細行内のセルに詳細データが表示され、グループ行内のセルに集計値が表示されます。 Tablix の行と列に関する詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。  
  
 テーブル テンプレートと一覧のテンプレートには詳細行があります。 マトリックス テンプレートには詳細行がありません。 Tablix データ領域に詳細行がない場合は、詳細グループを定義すると追加できます。 詳細については、「[詳細グループの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="adding-grouped-data"></a>グループ化されたデータの追加  
 グループ化されたデータは、データセット、データ領域、およびグループにフィルターが適用された後の、グループ式によって指定されたすべての詳細データです。 グループ内の詳細データを整理するには、レポート データ ペインからグループ化ペインにフィールドをドラッグします。 グループを追加すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、グループ化されたデータが表示される Tablix データ領域に、関連する行や列が自動的に追加されます。 これらの行や列内のセルは、グループ化されたデータに関連付けられます。 詳細については、「 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
 既定では、数値データを表すデータセット フィールドを、グループ行またはグループ列内のセルに追加すると、セルの値は、スコープがセルの最も内側の行グループおよび列グループのメンバーシップに設定された、グループ化されたデータの合計になります。 既定の集計関数 Sum を、Avg や Count などの他の集計関数に変更できます。 集計計算の既定のスコープを変更することもできます。たとえば、行グループに対して値が占める割合を計算するように変更できます。 詳細については、「 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)を表しています。  
  
 既定では、グループ化されたデータはすべて同じレポート データセットのデータです。 Tablix データ領域で、データセット名をスコープとして指定して、他のデータセットの集計値を含めることができます。 1 つの Tablix データ領域内で複数のデータセットの集計値を複数指定できます。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
## <a name="adding-subtotals-and-totals"></a>小計と合計の追加  
 グループの小計とデータ領域の総計を追加するには、セルまたはグループ化ペインのショートカット メニューの [合計の追加] 機能を使用します。 合計を表示するための行および列が自動的に追加されます。 小計および合計の式の既定では、 [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) 集計関数を使用します。 式を追加した後、既定の関数を変更できます。 詳細については、「[グループまたは Tablix データ領域への合計の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)」と「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="adding-labels"></a>ラベルの追加  
 グループまたはデータ領域のラベルを追加するには、ラベルを作成するグループの外側に行または列を追加します。 ラベルの行および列は、合計を表示するために追加した行および列に似ています。 詳細については、「[行の挿入または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md)」または「[列の挿入または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>別のレポートにある既存の Tablix データ領域の追加  
 別のレポートからデータ領域をコピーし、新しいレポートまたは既存のレポートに貼り付けることができます。 データ領域を貼り付けた後で、データ領域が使用するデータセットが定義されており、データセット フィールドの名前およびデータ型が元のレポートと同じであることを確認する必要があります。 データセットは、異なるレポート間でコピーできません。ただし、レポートが共有データ ソースを使用している場合は、別のレポートにデータセットをすばやく複製できます。 また、データセット用にデータを取得するクエリのクエリ テキストもインポートできます。この操作によって、複数のレポート内でクエリを簡単に複製できます。 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [対話的な並べ替え、ドキュメント マップ、およびリンク &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [式の追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
