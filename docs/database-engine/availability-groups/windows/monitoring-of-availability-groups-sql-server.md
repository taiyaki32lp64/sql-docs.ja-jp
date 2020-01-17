---
title: 可用性グループを監視するツール
description: 'Always On 可用性グループのパフォーマンスと正常性を監視するために使用できる、さまざまなツールに関する資料です。 '
ms.custom: seodec18
ms.date: 06/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 1d5e3291-0d0a-45a1-88e5-1fc242d17210
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 31cf3fcc59ad9dbe694b7a11f6b90981f37fc78b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014672"
---
# <a name="tools-to-monitor-always-on-availability-groups"></a>Always On 可用性グループを監視するツール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  AlwaysOn 可用性グループのプロパティと状態を監視するには、次のツールを使用します。  
  
|ツール|簡単な説明|リンク|  
|----------|-----------------------|-----------|  
|System Center Monitoring pack for SQL Server|Monitoring pack for SQL Server (SQLMP) は、可用性グループ、可用性レプリカ、および可用性データベースを IT 管理者が監視するための推奨ソリューションです。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に特に関連する監視機能は次のとおりです。<br /><br /> 可用性グループ、可用性レプリカ、および可用性データベースを多数のコンピューターから自動検出する機能。 これにより、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の在庫を簡単に追跡できます。<br /><br /> System Center Operations Manager (SCOM) の完全な警告機能とチケット機能。 これらの機能は、問題の早期解決を可能にする詳細な情報を提供します。<br /><br /> ポリシー ベースの管理 (PBM) を使用した AlwaysOn 正常性状態の監視のカスタム拡張機能。<br /><br /> 正常性状態は、可用性データベースから可用性レプリカにロールアップされます。<br /><br /> System Center Operations Manager コンソールから [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を管理するカスタム タスク。|監視パック (SQLServerMP.msi) および *SQL Server Management Pack Guide for System Center Operations Manager* (SQLServerMPGuide.doc) をダウンロードするには、以下を参照してください。<br /><br /> [System Center Monitoring pack for SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のカタログ ビューと動的管理ビューは、可用性グループとそのレプリカ、データベース、リスナー、および WSFC クラスター環境に関する豊富な情報を提供します。|[可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**[オブジェクト エクスプローラーの詳細]** ペインには、接続先の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスでホストされている可用性グループの基本情報が表示されます。<br /><br /> **\*\* ヒント \*\*** このペインを使用して、複数の可用性グループ、レプリカ、またはデータベースを選択し、選択したオブジェクトで一般的な管理タスク (可用性グループからの複数の可用性レプリカまたはデータベースの削除など) を実行します。|[[オブジェクト エクスプローラーの詳細] を使用した可用性グループの監視 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|**[プロパティ]** ダイアログ ボックスを使用して、可用性グループ、レプリカ、またはリスナーのプロパティを表示し、必要に応じてその値を変更できます。|-   [可用性グループのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)<br />-   [可用性レプリカのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)<br />-   [可用性グループ リスナーのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)|  
|システム モニター|**SQLServer:Availability Replica** パフォーマンス オブジェクトには、可用性レプリカに関する情報を報告するパフォーマンス カウンターが含まれています。|[SQL Server、Availability Replica](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|システム モニター|**SQLServer:Database Replica** パフォーマンス オブジェクトには、特定のセカンダリ レプリカのセカンダリ データベースに関する情報を報告するパフォーマンス カウンターが含まれています。<br /><br /> SQL Server の **SQLServer:Databases** オブジェクトには、トランザクション ログの利用状況などを監視するパフォーマンス カウンターが含まれています。 可用性データベースでのトランザクション ログの利用状況の監視に関連性が高いカウンターは、**Log Flush Write Time (ms)** 、**Log Flushes/sec**、**Log Pool Cache Misses/sec**、**Log Pool Disk Reads/sec**、**Log Pool Requests/sec** です。|[SQL Server、Database ReplicaQL Server](../../../relational-databases/performance-monitor/sql-server-database-replica.md) および [SQL Server、Databases オブジェクト](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [AlwaysOn の正常性モデル: パート 1: 正常性モデルのアーキテクチャ](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/08/the-alwayson-health-model-part-1-health-model-architecture/)  
  
     [AlwaysOn の正常性モデル: パート 2: 正常性モデルの拡張](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/the-alwayson-health-model-part-2-extending-the-health-model/)  
  
     [PowerShell を使用した Always On 正常性状態の監視: パート 1:基本的なコマンドレットの概要](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
     [PowerShell を使用した Always On 正常性状態の監視: パート 2:高度なコマンドレットの使用方法](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
     [PowerShell を使用した Always On 正常性状態の監視: パート 3:シンプルな監視アプリケーション](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
     [PowerShell を使用した Always On 正常性状態の監視: パート 4:SQL Server エージェントとの統合](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
     [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.microsoft.com/psssql/)  
  
-   **ホワイト ペーパー:**  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [可用性グループの自動フェールオーバーのための柔軟なフェールオーバー ポリシー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [ページの自動修復 &#40;可用性グループ:データベース ミラーリング&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
