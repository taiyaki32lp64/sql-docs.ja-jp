---
title: レポートの計画 (レポート ビルダー) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- getting started
- report design
ms.assetid: 79113505-1ce8-4f8c-9260-d861838f7813
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9c65d1db987f5d317b0719ff101012b4db0a5873
ms.sourcegitcommit: c40f663d4486e574fd749f2c8e84c98d41970352
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2019
ms.locfileid: "67038024"
---
# <a name="planning-a-report-report-builder"></a>レポートの計画 (レポート ビルダー)
  レポート ビルダーでは、さまざまな種類のページ分割されたレポートを作成できます。 たとえば、売上データの概要または詳細、マーケティングと売上の傾向、経営報告、またはダッシュボードを示すレポートを作成できます。 また、販売注文、製品カタログ、定型書簡などの高度な書式付きテキストを利用したレポートも作成できます。 これらのレポートはすべて、レポート ビルダーの同じ基本的な構成要素をさまざまに組み合わせて作成されます。 便利でわかりやすいレポートを作成するには、まず計画を立てることが役立ちます。 開始する前に検討すると役立ついくつかの事項を次に示します。  
  
-   **どの形式でレポートを表示するか**  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルなどのブラウザーでレポートをオンラインで表示したり、Excel、Word、PDF などの他の形式にレポートをエクスポートしたりすることができます。 エクスポート形式によっては一部の機能を使用できないので、レポートの最終的な形式を検討することは重要です。 詳しくは、「 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)におけるページ割り付けの制御規則を理解しておく必要があります。  
  
-   **どのような構造を使用してレポートのデータを表すか**  
  
     テーブル、マトリックス (クロス集計レポートや PivotTable レポートに似ています)、グラフ、自由形式の構造を選択するか、これらの構造を組み合わせてデータを表します。 詳細については、「[テーブル、マトリックス、および一覧 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)」と「[グラフ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)」を参照してください。  
  
-   **レポートをどのように表示するか**  
  
     レポート ビルダーには、レポートを読みやすくしたり、重要な情報を強調したり、対象ユーザーがレポート内を移動しやすくしたりするためにレポートに追加できる多数のレポート アイテムが用意されています。 レポートの希望の表示方法がわかっていれば、テキスト ボックス、四角形、画像、線などのレポート アイテムが必要かどうかを判断できます。 また、アイテムの表示と非表示を切り替えたり、ドキュメント マップを追加したり、詳細レポートまたはサブレポートを含めたり、他のレポートにリンクしたりすることもできます。 詳細については、「[画像、テキスト ボックス、四角形、および罫線 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)」と「[対話的な並べ替え、ドキュメント マップ、およびリンク (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)」を参照してください。  
  
-   **どのデータを表示するか、データまたは形式をさまざまな対象ユーザーに合わせてフィルター選択する必要があるかどうか**  
  
     レポートの範囲を特定のユーザーまたは場所、あるいは特定の期間などに絞り込むことができます。 レポート データをフィルター処理するには、パラメーターを使用して、必要なデータのみを取得して表示します。 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)にあります。  
  
-   **独自の計算を作成する必要があるかどうか**  
  
     レポートに必要な特定のフィールドがデータ ソースやデータセットに含まれていない場合があります。 そのような状況では、独自の計算フィールドの作成が必要になることがあります。 たとえば、行アイテムの販売額を取得するために数量と単価を乗算するような場合があります。 条件付き書式やその他の拡張機能にも式が使用されます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
-   **最初にレポート アイテムを非表示にするかどうか**  
  
     レポートを最初に実行するときにデータ領域、グループ、列などのレポート アイテムを非表示にするかどうかを検討します。 たとえば、最初に概要テーブルを表示しておき、詳細データにドリル ダウンできるようにします。 詳細については、「[ドリルダウン アクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)」を参照してください。  
  
-   **どのようにしてレポートを配信するか**  
  
     レポートをローカル コンピューターに保存して、引き続き操作したり、独自の情報に関してローカルで実行したりすることができます。 ただし、レポートを他のユーザーと共有するには、ネイティブ モードで構成されたレポート サーバーまたは SharePoint 統合モードのレポート サーバーにレポートを保存する必要があります。 サーバーに保存すると、他のユーザーが必要なときにいつでも実行できます。 または、レポート サーバー管理者がレポートのサブスクリプションを設定したり、他のユーザーへのレポートの電子メール配信を設定したりすることができます。 必要に応じて、レポートを特定のエクスポート形式で配信できます。 詳細については、「 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server のレポート ビルダー](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Reporting Services の概念 (SSRS)](../reporting-services-concepts-ssrs.md) [レポート ビルダー チュートリアル](../../reporting-services/report-builder-tutorials.md)  
  
  
