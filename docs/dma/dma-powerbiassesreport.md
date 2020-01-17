---
title: Power BI を使用した統合される評価レポートの分析
titleSuffix: Data Migration Assistant
description: Power BI を使用して、でインポートおよび統合したデータ移行の評価レポートを分析する方法について説明し SQL Server
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056503"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Power BI を使用して Data Migration Assistant によって作成された統合評価レポートを分析する

この記事では、Power BI レポートを作成して、統合された移行評価を分析する方法について説明します。

Data Migration Assistant によって作成された移行評価の統合の詳細については、「[評価レポートの統合](../dma/dma-consolidatereports.md)」を参照してください。

## <a name="sample-power-bi-reports"></a>サンプル Power BI レポート

この[GitHub リポジトリ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)から統合移行評価用の Power BI レポートの例をダウンロードできます。

次のレポートが含まれています。 

- [デジタル](#dashboard-report)

  スナップショット統計とドリルダウンレポートが含まれます。

- [オンプレミスのアップグレードの準備](#on-premises-upgrade-readiness-report)

  データソースは、DMAReporting データベースのアップグレード時の順位付けビューです。  このレポートには、評価されたデータベースのアップグレードが成功した割合が表示されます。

- [オンプレミス機能のパリティ](#on-premises-feature-parity-report)

  ターゲット SQL Server バージョンの機能に関する推奨事項を示します。

- [Azure SQL DB upgrade readiness](#azure-sql-db-upgrade-readiness-report)

  データソースは、DMAReporting データベースのアップグレード時の順位付けビューです。  このレポートには、Azure SQL DB の移行について評価されたデータベースのアップグレードの成功率が表示されます。

- [Azure SQL DB のサポートされていない機能](#azure-sql-db-unsupported-features-report)

  Azure SQL DB (V12) でサポートされていない既存のデータベースの機能を示します。

Power BI のデータソースを変更することで、環境で動作するようにこれらのレポートを変更できます。 

1. **[クエリの編集]** の横にある下矢印を選択し、 **[データソースの設定]** を選択します。

   ![クエリ メニューの データ ソースの設定を編集します。](../dma/media/DataSourceSettings.png)

1. **[ソースの変更]** を選択し、サーバーとデータベースの値を入力します。

   ![ソース、サーバー、データベースの変更](../dma/media/ChangeSource.png)

1. **[OK]** を選択し、 **[閉じる]** を選択します。

1. レポートを最新の状態に更新します。

   ![Power BI レポートの更新](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>ダッシュボードレポート

![ダッシュボードレポート](../dma/media/DashboardReport.png)

ダッシュボードには、すべての評価の詳細が表示されます。 左側のスライサーを使用して、インスタンスまたはデータベースでフィルター処理できます。 横棒グラフを使用して、特定のカテゴリにドリルダウンし、問題の発生場所を確認できます。

ドリルダウンするには、横棒グラフの右上隅にある下向き矢印の付いた円を選択します。

![カテゴリのドリルダウン](../dma/media/CategoryDrillDown.png)

ドリルダウンシーケンスは、次の図のように設定されます ( **[軸]** の下)。 順序を変更するには、目的の順序に列をドラッグします。

![視覚化、横棒グラフの軸](../dma/media/VisualizationsAxis.png)

このビューは、特定のデータベースで最初にフィルターを適用し、特定のカテゴリの問題にドリルダウンすると、さらに強力なものになります。 次の例では、インスタンス**という**に対して、移行を妨げるすべてのオブジェクト (重大な変更) を表示するために、HR データベースが選択されています。

![HR データベースの重大な変更](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>オンプレミスのアップグレード準備レポート

![オンプレミスのアップグレード準備レポート](../dma/media/OnPremisesUpgradeReadinessReport.png)

このレポートには、データベースを新しいバージョンの SQL Server に移行する準備ができたことを示すスナップショットが表示されます。 このレポートのデータは、dbo から取得されます。DMAReporting データベースのオンプレミスビューに\_アップグレードします。

インスタンス名とデータベース名でフィルター処理し、上部にあるスコアカードを使用すると、データベースがどのバージョンに移行されたかを確認できます。 たとえば、AdventureWorks 2012 データベースでフィルター処理を実行すると、レポートに表示されているすべての SQL Server バージョンにデータベースを移動する準備ができていることがわかります。 これは、そのデータベースと互換性レベルに重大な変更がないことを確認することによって決定されます。

![AdventureWorks データベースのアップグレード成功率](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>オンプレミス機能のパリティレポート

![オンプレミス機能のパリティレポート](../dma/media/OnPremisesFeatureParityReport.png)

このレポートを使用して、ターゲット SQL Server バージョンのデータベースで使用できる新機能を強調表示します。

じょうごグラフで特徴を選択すると、その機能によって影響を受けるオブジェクトが下部のデータで強調表示されます。 次の例では、 **[ストレージを節約するための Stretch database]** 機能が選択されており、この機能のメリットを得られるテーブルが一覧表示されています。

![Stretch Database の機能に関する推奨事項](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB のアップグレード準備レポート

![Azure SQL DB のアップグレード準備レポート](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

このレポートには、Azure SQL Database V12 に移行するためのデータベースの準備状態が表示されます。 このレポートのデータは、dbo から取得されます。DMAReporting データベースのアップグレードを行います。

### <a name="azure-features-parity-report"></a>Azure の機能のパリティレポート

![Azure の機能のパリティレポート](../dma/media/AzureFeaturesParityReport.png)

このレポートを使用して、Azure SQL Database V12 でサポートされていない*インスタンスレベルの機能*を強調表示します。

じょうごグラフで特徴を選択すると、下部にあるデータに、サポートされていないインスタンスとデータベースの機能が一覧表示されます。 次の例では、この機能が選択されています。 **Always On 可用性グループの構成は、Azure SQL Database ではサポートされていません**。  

![Always on 可用性グループ機能](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB のサポートされていない機能のレポート

![Azure SQL DB のサポートされていない機能のレポート](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

このレポートでは、ターゲットが Azure SQL Database (V12) の場合に、特定の**データベース**でサポートされていない機能が強調表示されます。

じょうごグラフのデータベース名と機能値でフィルター処理することにより、サポートされていない機能の詳細を確認できます。 詳細には、影響を受けるオブジェクトと問題に対処するための推奨事項が含まれます。

たとえば、DTC データベースおよび読み取り専用データベースによるフィルター処理を**アップグレードすることはできません**。影響を受けるオブジェクトの一覧が表示されます。

![読み取り専用データベースをアップグレードできない問題](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>参照

[Data Migration Assistant の概要](../dma/dma-overview.md)

[Data Migration Assistant のダウンロード](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI のダウンロード](https://powerbi.microsoft.com/)
