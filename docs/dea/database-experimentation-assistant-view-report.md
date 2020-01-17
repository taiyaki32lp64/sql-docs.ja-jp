---
title: SQL Server アップグレードの分析レポートの表示
description: Database Experimentation Assistant で分析レポートを表示する
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: b72d49e691311104481637ff49d6c1e09ae0c230
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317740"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Database Experimentation Assistant で分析レポートを表示する

Database Experimentation Assistant (DEA) を使用して[分析レポートを作成](database-experimentation-assistant-create-report.md)した後、次の手順を使用して、A/B テストに基づいてパフォーマンスの洞察に関するレポートを確認します。

## <a name="select-a-server"></a>サーバーを選択します。

DEA で、メニューアイコンを選択します。 展開されたメニューで、チェックリストアイコンの横にある [**分析レポート**] を選択し、[分析レポート] ウィンドウを開きます。

[**分析レポート**] で、分析データベースを持つ SQL Server を実行しているコンピューターの名前を入力し、[**接続**] を選択します。

![既存のレポートへの接続](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

依存関係が不足している場合は、[**必須コンポーネント**] ページに、インストールするためのリンクが表示されます。 必要に応じて、前提条件をインストールし**て**から、[再試行] を選択します。

![[前提条件] ページ](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>表示する分析レポートの選択

分析レポートの一覧で、レポートをダブルクリックして開きます。

![既存のレポートの表示](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

次のグラフの例に示すように、ワークロードがどの程度適切に表されているかを調べることができます。

![ワークロードの担当グラフ](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>分析レポートを表示して理解する

このセクションでは、分析レポートについて説明します。

### <a name="query-categories"></a>クエリカテゴリ

左側の円グラフの別のスライスを選択すると、そのカテゴリに該当するクエリのみが表示されます。

![円スライスのレポート](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **低下**したクエリ: B よりもでは、より適切に実行されたクエリ。  
- **エラー**: インスタンス B にエラーを表示するが、インスタンス a には存在しないクエリ。  
- **改善**されたクエリ: インスタンス a よりもインスタンス B でパフォーマンスが向上したクエリ。  
- **不確定クエリ**: パフォーマンスが不確定な状態のクエリ。  
- **同じ**: パフォーマンスがインスタンス A とインスタンス B で同じままであるクエリ。

### <a name="individual-query-drill-down"></a>個々のクエリのドリルダウン

クエリテンプレートのリンクを選択すると、特定のクエリに関する詳細情報を表示できます。

![クエリのドリルダウン](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

特定のクエリを選択すると、クエリの比較の概要が表示されます。

![比較の概要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

クエリが実行された A と B のインスタンスを確認できます。 クエリがどのように表示されるかのテンプレートを表示することもできます。 テーブルには、インスタンス A とインスタンス B に固有のクエリ情報が表示されます。

### <a name="error-queries"></a>エラークエリ

比較概要レポートには、展開可能な**エラー情報**と**クエリプラン情報**のセクションが含まれています。 これらのセクションでは、両方のインスタンスのエラーと計画に関する情報を示します。

エラー (赤) の円グラフを選択して、次の種類のエラーを表示します。

- **既存のエラー**: 内にあったエラー。
- **新しいエラー**: B で発生したエラー。
- **解決済みのエラー**: 内にあって B にはないエラー。

![エラーグラフ](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="see-also"></a>参照

- コマンドプロンプトで分析レポートを生成する方法については、「[コマンドプロンプトでの実行](database-experimentation-assistant-run-command-prompt.md)」を参照してください。
