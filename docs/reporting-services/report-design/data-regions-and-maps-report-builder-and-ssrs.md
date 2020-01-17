---
title: データ領域とマップ (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3ddd2d78cc983e1855007d144193d70035931177
ms.sourcegitcommit: c40f663d4486e574fd749f2c8e84c98d41970352
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2019
ms.locfileid: "67037830"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>データ領域とマップ (レポート ビルダーおよび SSRS)
  データ領域は、レポート データセットのデータを表示するレポート内のオブジェクトです。 レポート データは、数字やテキストとしてテーブル、マトリックス、または一覧に表示することも、グラフまたはゲージでグラフィカルに表示することも、マップの地理的背景上に表示することもできます。 テーブル、マトリックス、および一覧は、 *Tablix* データ領域に基づいており、データセットのデータをすべて表示するために必要に応じて拡張されます。 Tablix データ領域では、複数の行グループおよび列グループと、静的および動的な行と列がサポートされます。 グラフでは、複数の系列グループとカテゴリ グループをさまざまなグラフ形式で表示します。 ゲージでは、データセットの単一の値または集計値を表示します。 マップでは、データセットの集計データに基づいて表示を変更できるマップ要素として空間データを表示します。  
  
 データ領域やマップは、 *レポート パーツ*として保存できます。 [レポート パーツ](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)の詳細を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>テーブル  
 テーブルは、データを行ごとに表示するデータ領域です。 テーブルの列は静的です。列数はレポートのデザイン時に指定します。 テーブルの行は動的であり、データに応じて下方向に拡張されます。 テーブルにグループを追加すると、選択したフィールドまたは式ごとにデータを整理できます。 レポートにテーブルを追加する方法の詳細については、「[テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="matrix"></a>マトリックス  
 マトリックスは、クロス集計ともいいます。 マトリックス データ領域では、動的な列と行の両方がデータに応じて拡張されます。 マトリックスには、動的な列と行、および静的な列と行を含めることができます。 列または行には、他の列または行を含めることができ、データのグループ化にも使用できます。 レポートにマトリックスを追加する方法の詳細については、 [「レポートへのマトリックスの追加」](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)を参照してください。  
  
## <a name="list"></a>一覧  
 一覧は、任意の形式で配置されたデータを表すデータ領域です。 レポート アイテムを配置して、テキスト ボックス、画像、およびその他のデータ領域が一覧内の任意の場所に配置されたフォームを作成できます。 レポートに一覧を追加する方法の詳細については、 [「レポートへのリストの追加」](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)を参照してください。  
  
## <a name="chart"></a>グラフ  
 グラフを使用すると、データをグラフィカルに表示できます。 グラフの例としては、棒グラフ、円グラフ、折れ線グラフなどがありますが、その他にも多くの形式がサポートされています。 詳細については、 [「レポートへのグラフの追加」](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)を参照してください。  
  
## <a name="gauge"></a>ゲージ  
 ゲージは、特定の値を指すインジケーターを内部に含む領域としてデータを表示します。 ゲージは、主要業績評価指標 (KPI) やその他の基準を表示するために使用されます。 ゲージの例として、線形ゲージや円形ゲージなどがあります。 詳細については、 [「レポートへのゲージの追加」](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)を参照してください。  
  
## <a name="map"></a>マップ  
 マップでは、地理的な背景にデータを表現することができます。 マップ データには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ、ESRI シェープファイル、または [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing マップのタイルの空間データを指定できます。 空間データは、形状または領域を表す多角形、ルートまたはパスを表す線、およびマーカーで表されるポイントを定義する座標のセットで構成されます。 集計データをマップ要素に関連付けて、マップ要素の色とサイズを自動的に変化させることができます。 たとえば、売上高に基づいて店舗のマーカーの種類を変えたり、制限速度に基づいて道路の色を変えたりできます。 詳細については、「[マップ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="data-regions-in-the-report-layout"></a>レポート レイアウトのデータ領域  
 レポートには複数のデータ領域を追加できます。 データ領域は、リンクされているデータセットのデータに合わせて拡大されます。 たとえば、年ごとに各製品の売上を表示するマトリックスには、製品名に基づく行グループと年に基づく列グループがあります。 レポートを実行すると、マトリックスのページは、各製品に合わせて下方向に拡張され、各年に合わせて横方向に拡張されます。 レポート デザイン画面でマトリックスの横に配置したグラフは、表示レポートでは、拡張されたマトリックスの横に表示されます。 ページ上のデータ領域の表示方法には、レポートの出力形式に基づく一連の規則が適用されます。 たとえば、ページ上のグラフとマトリックスの表示方法を制御するには、コンテナーとして四角形を使用するか、両方のデータ領域を一覧内に入れ子にします。 詳細については、「 [ページ レイアウトとレンダリング (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)として保存できます。  
  
## <a name="nested-data-regions"></a>入れ子になったデータ領域  
 データ領域を他のデータ領域内に入れ子にすることができます。 たとえば、データベース内の各販売員ごとの売上記録を作成する場合、テキスト ボックスおよび画像を使用して一覧を作成し、従業員に関する情報を表示します。次に、この一覧にテーブルおよびグラフ データ領域を追加して従業員の売上記録を表示します。 詳細については、「 [入れ子になったデータ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>同じデータセットにリンクされた複数のデータ領域  
 複数のデータ領域を同じデータセットにリンクすることで、同じデータをさまざまな形式で表示することができます。 たとえば、同じデータをテーブルやグラフで表示できます。 レポートのテーブルに対話的な並べ替えボタンを組み込むことで、テーブルを並べ替えたときにグラフも自動的に並べ替えられるようにすることができます。 詳細については、「 [同じデータセットへの複数のデータ領域のリンク (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="data-for-a-data-region"></a>データ領域のデータ  
 Tablix、グラフ、およびゲージはそれぞれ、単一のデータセットのデータを表示するために設計されています。 マップには、同じデータセットまたは異なるデータセットの空間データと分析データが表示されます。 また、以下のように、データ領域にリンクされていないデータセットの値を含めることもできます。  
  
-   並べ替え順序およびグループ化に依存せず、スコープが別のデータセットに設定されている集計値。  
  
-   別のデータセットの名前と値のペアの参照値。  
  
 詳細については、「[式 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の概念 (SSRS)](../reporting-services-concepts-ssrs.md) [レポート、レポート パーツ、およびレポート定義&#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [ページ レイアウトとレンダリング &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)   
 [レポート ビルダー チュートリアル](../../reporting-services/report-builder-tutorials.md)   
 [Reporting Services チュートリアル (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
