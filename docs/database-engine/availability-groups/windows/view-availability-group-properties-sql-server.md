---
title: 可用性グループのプロパティを表示する
description: 'SQL Server Management Studio (SSMS)、Transact-SQL (T-SQL)、または SQL PowerShell のいずれかを使用して Always On 可用性グループのプロパティを表示します。 '
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server]
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 44328d275c962c1f6315e56e763c3a8550318ffb
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74821814"
---
# <a name="view-availability-group-properties-sql-server"></a>可用性グループのプロパティの表示 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[tsql](../../../includes/tsql-md.md)] または [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]を使用して、Always On 可用性グループの可用性グループのプロパティを表示する方法について説明します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性グループのプロパティを表示および変更するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  表示するプロパティを持つ可用性グループを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[可用性グループのプロパティ]** ダイアログ ボックスで、 **[全般]** および **[バックアップの設定]** ページを使用して、選択された可用性グループのプロパティを表示し、必要に応じて変更します。 詳細については、「[可用性グループのプロパティ: 新しい可用性グループ &#40;[全般] ページ&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-general-page.md)」と「[可用性グループのプロパティ: 新しい可用性グループ &#40;[バックアップの設定] ページ&#41;](../../../database-engine/availability-groups/windows/availability-group-properties-new-availability-group-backup-preferences-page.md)」を参照してください。  
  
     **[権限]** ページを使用して、可用性グループに関連付けられている現在のログイン、ロール、および明示的な権限を表示できます。 詳細については、「 [[権限] ページまたは [セキュリティ保護可能なリソース] ページ](../../../relational-databases/security/permissions-or-securables-page.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性グループのプロパティおよび状態を表示するには**  
  
 サーバー インスタンスが可用性レプリカをホストしている可用性グループのプロパティおよび状態を確認するには、次のビューを使用します。  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスが可用性レプリカをホストしている各可用性グループの行を返します。 各行には、可用性グループ メタデータのキャッシュされたコピーが含まれます。  
  
 **列名:** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 WSFC クラスター内の可用性グループごとに 1 行のデータを返します。 各行には、Windows Server フェールオーバー クラスタリング (WSFC) クラスターからの可用性グループ メタデータが含まれます。  
  
 **列名:** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のローカル インスタンスで可用性レプリカを保持する可用性グループごとに 1 行のデータを返します。 各行には、特定の可用性グループの正常性を定義する状態が表示されます。  
  
 **列名:** group_id、primary_replica、primary_recovery_health、primary_recovery_health_desc、secondary_recovery_health、secondary_recovery_health_desc、synchronization_health、synchronization_health_desc  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **可用性グループに関する情報を表示するには**  
  
-   [可用性レプリカのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [可用性グループ リスナーのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
 **既存の可用性グループを構成するには**  
  
-   [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [可用性グループへのデータベースの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/availability-group-add-a-database.md)  
  
-   [可用性グループからのセカンダリ データベースの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループ リスナーの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループからのプライマリ データベースの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [可用性グループの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
 **可用性グループで手動フェールオーバーを行うには**  
  
-   [可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
  
