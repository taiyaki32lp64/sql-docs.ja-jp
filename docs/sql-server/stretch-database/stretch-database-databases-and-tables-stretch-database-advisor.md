---
title: データベースとテーブルの識別
ms.date: 10/30/2017
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: ec8df33c7af98889529232bbcd56437745339fba
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843751"
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>Data Migration Assistant で Stretch Database 向きのデータベースとテーブルを識別する
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database の候補になるデータベースとテーブル、および潜在的なブロッキングの問題を識別するには、Microsoft Data Migration Assistant をダウンロードして実行します。
  
## <a name="get-data-migration-assistant"></a>Data Migration Assistant を入手する
 Data Migration Assistant を [ここ](https://www.microsoft.com/download/details.aspx?id=53595)からダウンロードしてインストールします。 このツールは、SQL Server のインストール メディアには含まれていません。  
  
## <a name="run-data-migration-assistant"></a>Data Migration Assistant を実行する  
  
1.  Microsoft Data Migration Assistant を実行します。  

2.  **[評価]** タイプの新しいプロジェクトを作成し、名前を指定します。

3.  **[ソース サーバーの種類]** と **[ターゲット サーバーの種類]** の両方で、 **[SQL Server]** を選びます。

4.  **[作成]** を選択します。 

5. **[オプション]** ページ (ステップ 1) で、 **[New features recommendation]\(新しい機能の推奨事項\)** を選びます。 必要に応じて、 **[Compatibility issues]\(互換性の問題\)** をオフにします。

6.  **[Select sources]\(ソースの選択\)** ページ (ステップ 2) で、サーバーに接続し、データベースを選んで、 **[追加]** を選びます。

7.  **[Start Assessment]\(評価の開始\)** を選びます。

## <a name="review-the-results"></a>結果の確認  
  
1.  分析が終了したら、 **[Review results]\(結果のレビュー\)** ページ (ステップ 3) で **[機能に関する推奨事項]** オプションを選び、 **[ストレージ]** タブを選びます。

2.  Stretch Database に関する推奨事項を確認します。 各推奨事項には、Stretch Database が適している可能性のあるテーブルの一覧と、潜在的なブロッキングの問題が表示されます。

## <a name="historical-note"></a>これまでの経緯
Stretch Database Advisor は、以前は SQL Server 2016 アップグレード アドバイザーのコンポーネントでした。 その時点では、別のアクションとして Stretch Database Advisor を選んで実行する必要がありました。

アップグレード アドバイザーの代わりとなる拡張版の Data Migration Assistant のリリースを機に、Stretch Database Advisor の機能はこの新しいツールに組み込まれます。 Stretch Database に関する推奨事項を取得するために、オプションを選ぶ必要はありません。 Data Migration Assistant で Assessment を実行すると、Stretch Database に関する結果が、 **[機能に関する推奨事項]** の **[ストレージ]** タブに表示されます。
  
## <a name="next-step"></a>次の手順  
 Stretch Database を有効にします。  
  
-   **データベース**の Stretch Database を有効にするには、「 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)」を参照してください。  
  
-   Stretch が データベースで既に有効な場合に、別の **テーブル**の Stretch Database を有効にするには、「 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)」を参照してください。 
  
## <a name="see-also"></a>参照  
 [Stretch Database の制限事項](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
