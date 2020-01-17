---
title: アプライアンスの監視
description: このアプライアンス監視ガイドでは、Analytics Platform System アプライアンスを監視するためのツールとタスクについて説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401422"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>分析プラットフォームシステムのアプライアンス監視
このアプライアンス監視ガイドでは、Analytics Platform System アプライアンスを監視するためのツールとタスクについて説明します。  
  
## <a name="Basics"></a>監視の基本とツール  
SQL Server PDW アプライアンスで監視できる値と情報は広範囲にわたっています。 たとえば、一般的な監視タスクを次に示します。  
  
-   SQL Server PDW によって発行されたアラートを確認します。  
  
-   障害が発生したハードウェアを監視します。  
  
-   ネットワーク接続の問題を監視します。  
  
-   クエリ処理中にユーザーに返されるエラーを確認します。  
  
-   現在アクティブなセッションとクエリの数を表示します。  
  
-   読み込み、バックアップ、復元の状態を確認します。  
  
### <a name="appliance-monitoring-tools"></a>アプライアンスの監視ツール  
アプライアンスの監視に使用できるツールは複数あります。  
  
管理コンソール  
SQL Server PDW には管理コンソールがあります。 これは、クエリ、読み込み、バックアップと復元、ロック、セッション、アラート、およびアプライアンスの状態に関する情報を表示する web ベースのツールです。 管理コンソールはアプライアンス上で実行されます。ユーザーは、Internet Explorer を使用して管理コンソールに接続します。 詳細については、次のドキュメントを参照してください。  
  
-   [管理コンソール &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理コンソールの警告](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
システム ビュー  
SQL Server PDW には、アプライアンスの正常性、状態、およびパフォーマンスに関する詳細情報を取得するための包括的なシステムビューが含まれています。 タスクを監視するためのシステムビューの一覧については、次を参照してください。  
  
-   [システムビュー &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW は、Systems Center Operations Manager と広範囲に統合されています。 SQL Server PDW 用の管理パックは、無料でダウンロードできます。 System Center を使用して SQL Server PDW を監視する方法の詳細については、次を参照してください。  
  
-   [System Center Operations Manager &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
カスタム ソリューション  
データセンターの監視ツールで System Center を使用できない場合は、サードパーティ製の監視ソリューションを使用してアプライアンスを監視できます。 現在、外部ソフトウェアエージェントのインストールは PDW ではサポートされていません\-が、ほとんどの監視ソリューションは transact sql の統合\-をサポートしているため、システム管理者は pdw アプライアンスに対して直接 transact sql クエリを実装できます。  
  
監視ソリューションで直接 Transact\-SQL クエリがサポートされていない場合、または監視ツールがない場合は、アラートが発生したときに電子メールを送信するなど、スクリプトを使用して監視タスクを実行できます。  TechNet wiki には、スクリプト化された監視ソリューションの例が含まれています。  
  
-   [SQL Server PDW のための電源シェルの監視の例](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>関連する監視タスク  
  
|監視タスク|説明|  
|-------------------|---------------|  
|管理コンソールを使用してアプライアンスを監視します。|[管理コンソール &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-the-admin-console.md)|  
|システムビューを使用してアプライアンスを監視します。|[システムビュー &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-system-views.md)|  
|System Center を使用してアプライアンスを監視する|[System Center Operations Manager &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|アプライアンスの状態を監視します。|[アプライアンスの正常性状態 &#40;Analytics Platform System&#41;を監視する](monitor-appliance-health-state.md)|  
|ハートビートの監視。|[テレメトリのフィードバックを Microsoft &#40;SQL Server PDW に送信する&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|アプライアンスのアラートを追跡します。|[アプライアンスアラートの追跡 &#40;Analytics Platform System&#41;](track-appliance-alerts.md)|  
|使用されている容量を確認します。|[容量使用率 &#40;Analytics Platform System&#41;を表示する](view-capacity-utilization.md)|  
|アプライアンスをポーリングする頻度を決定します。|[Analytics Platform System&#41;&#40;ポーリング頻度を決定する](determine-polling-frequency.md)|  
|クラスター障害が発生したときに、失敗したクラスターノードを特定します。|[分析プラットフォームシステム &#40;に失敗したクラスターノードを特定する&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[アプライアンス管理タスク &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
