---
title: Transact-SQL (T-SQL) を使用した可用性グループの監視
description: Transact-SQL (T-SQL) を使用した Always On 可用性グループの監視方法の説明。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- dynamic management views [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], databases
- catalog views [SQL Server], AlwaysOn Availability Groups
ms.assetid: 881a34de-8461-4811-8c62-322bf7226bed
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a95082cd732b644105c14c4ba598f859f48456e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014699"
---
# <a name="monitor-availability-groups-transact-sql"></a>可用性グループの監視 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して可用性グループ、可用性レプリカ、および関連付けられているデータベースを監視できるように、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] には、一連のカタログ ビュー、動的管理ビュー、およびサーバー プロパティが用意されています。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT ステートメントを使用すると、これらのビューで、可用性グループや、そのレプリカおよびデータベースを監視できます。 特定の可用性グループに対して返される情報は、接続している [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスにプライマリ レプリカとセカンダリ レプリカのどちらがホストされているかによって変わります。  
  
> [!TIP]  
>  これらのビューの多くは ID 列を使用して結合可能であり、1 つのクエリで複数のビューの情報を取得できます。  
  
  
##  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] カタログ ビューでは、サーバー インスタンスに対する VIEW ANY DEFINITION 権限が必要です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 動的管理ビューでは、サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
##  <a name="AoAgFeatureOnSI"></a> サーバー インスタンス上の Always On 可用性グループ機能の監視  
 サーバー インスタンス上の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 機能を監視するには、次の組み込み関数を使用します。  
  
 [SERVERPROPERTY](../../../t-sql/functions/serverproperty-transact-sql.md) 関数  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] が有効かどうかと、それが有効な場合はサーバー インスタンスで開始されているかどうかに関するサーバー プロパティ情報を返します。  
  
 **列名:** IsHadrEnabled、HadrManagerStatus  
  
##  <a name="WSFC"></a> WSFC クラスターの可用性グループの監視  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に対応したローカル サーバー インスタンスをホストする Windows Server フェールオーバー クラスタリング (WSFC) クラスターを監視するには、次のビューを使用します。  
  
 [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に対応した SQL Server のインスタンスをホストする Windows Server フェールオーバー クラスタリング (WSFC) ノードに WSFC のクォーラムが存在する場合、 **sys.dm_hadr_cluster** は、クラスター名とクォーラムに関する情報を公開する行を返します。 WSFC ノードにクォーラムが存在しない場合、行は返されません。  
  
 **列名:** cluster_name、quorum_type、quorum_type_desc、quorum_state、quorum_state_desc  
  
 [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
 Always On が有効な SQL Server のローカル インスタンスをホストする WSFC ノードに WSFC クォーラムが存在する場合は、クォーラムを構成するメンバーごとに 1 行のデータと、各メンバーの状態を返します。  
  
 **列名:** member_name、member_type、member_type_desc、member_state、member_state_desc、number_of_quorum_votes  
  
 [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)  
 可用性グループのサブネット構成に参加しているメンバーごとに 1 行のデータを返します。 この動的管理ビューを使用して、可用性レプリカごとに構成されているネットワーク仮想 IP を検証できます。  
  
 **列名:** member_name、network_subnet_ip、network_subnet_ipv4_mask、network_subnet_prefix_length、is_public、is_ipv4  
  
 **主キー:** member_name + network_subnet_IP + network_subnet_prefix_length  
  
 [sys.dm_hadr_instance_node_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)  
 Always On 可用性グループに参加させる可用性レプリカをホストする SQL Server のすべてのインスタンスに対して、サーバー インスタンスをホストする Windows Server フェールオーバー クラスタリング (WSFC) ノードの名前を返します。 この動的管理ビューには、次の用途があります。  
  
-   この動的管理ビューは、同一の WSFC ノードでホストされている複数の可用性レプリカを持つ可用性グループを検出するために役に立ちます。これはサポート外の構成であり、可用性グループが間違って構成されているときに FCI フェールオーバーが発生した場合にこの状態になることがあります。  
  
-   複数の SQL Server インスタンスが同一の WSFC ノードでホストされている場合、Resource DLL はこの動的管理ビューを使用して接続先の SQL Server インスタンスを決定します。  
  
 **列名:** ag_resource_id、instance_name、node_name  
  
 [sys.dm_hadr_name_id_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)  
 SQL Server の現在のインスタンスが参加する Always On 可用性グループの、可用性グループ ID、WSFC リソース ID、および WSFC グループ ID という 3 つの一意の ID に対するマッピングを示します。 このマッピングの目的は、WSFC リソースまたは WSFC グループの名前が変更されるシナリオを処理することです。  
  
 **列名:** ag_name、ag_id、ag_resource_id、ag_group_id  
  
> [!NOTE]  
>  このトピックの「[可用性レプリカの監視](#AvReplicas)」セクションの **sys.dm_hadr_availability_replica_cluster_nodes** と **sys.dm_hadr_availability_replica_cluster_states** 、および「[可用性データベースの監視](#AvDbs)」セクションの **sys.availability_databases_cluster** と **sys.dm_hadr_database_replica_cluster_states** も参照してください。  
  
 WSFC クラスターと [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] についての詳細は、「[Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)」および「[フェールオーバー クラスタリングと Always On 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)」を参照してください。  
  
##  <a name="AvGroups"></a> 可用性グループの監視  
 サーバー インスタンスが可用性レプリカをホストしている可用性グループを監視するには、次のビューを使用します。  
  
 [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスが可用性レプリカをホストしている各可用性グループの行を返します。 各行には、可用性グループ メタデータのキャッシュされたコピーが含まれます。  
  
 **列名:** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)  
 WSFC クラスター内の可用性グループごとに 1 行のデータを返します。 各行には、Windows Server フェールオーバー クラスタリング (WSFC) クラスターからの可用性グループ メタデータが含まれます。  
  
 **列名:** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のローカル インスタンスで可用性レプリカを保持する可用性グループごとに 1 行のデータを返します。 各行には、特定の可用性グループの正常性を定義する状態が表示されます。  
  
 **列名:** group_id、primary_replica、primary_recovery_health、primary_recovery_health_desc、secondary_recovery_health、secondary_recovery_health_desc、synchronization_health、synchronization_health_desc  
  
##  <a name="AvReplicas"></a> sys.dm_hadr_availability_replica_cluster_states  
 可用性レプリカを監視するには、次のビューとシステム関数を使用します。  
  
 [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスが可用性レプリカをホストしている各可用性グループ内の可用性レプリカごとに 1 行のデータを返します。  
  
 **列名:** replica_id、group_id、replica_metadata_id、replica_server_name、owner_sid、endpoint_url、availability_mode、availability_mode_desc、failover_mode、failover_mode_desc、session_timeout、primary_role_allow_connections、primary_role_allow_connections_desc、secondary_role_allow_connections、secondary_role_allow_connections_desc、create_date、modify_date、backup_priority、read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
 WSFC フェールオーバー クラスター内の AlwaysOn 可用性グループにある各可用性レプリカの読み取り専用ルーティング リストに対する行を返します。  
  
 **列名:** replica_id、routing_priority、read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)  
 Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の AlwaysOn 可用性グループの可用性レプリカ (結合状態に関係なく) ごとに 1 行のデータを返します。  
  
 **列名:** group_name、replica_server_name、node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
 Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のすべての AlwaysOn 可用性グループ (レプリカの場所に関係なく) のレプリカ (結合状態に関係なく) ごとに 1 行のデータを返します。  
  
 **列名:** replica_id、replica_server_name、group_id、join_state、join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
 各ローカル可用性レプリカの状態を示す 1 行のデータと、同じ可用性グループに含まれるリモート可用性グループごとの 1 行のデータを返します。  
  
 **列名:** replica_id、group_id、is_local、role、role_desc、operational_state、operational_state_desc、connected_state、connected_state_desc、recovery_health、recovery_health_desc、synchronization_health、synchronization_health_desc、last_connect_error_number、last_connect_error_description、last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
 現在のレプリカが推奨されるバックアップ レプリカであるかどうかを判別します。  
  
> [!NOTE]  
>  可用性レプリカのパフォーマンス カウンター ( **SQLServer:可用性レプリカ**  パフォーマンス オブジェクト) の詳細については、「 [SQL Server、可用性レプリカ](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)」を参照してください。  
  
##  <a name="AvDbs"></a> sys.dm_hadr_database_replica_cluster_states  
 可用性データベースを監視するには、次のビューを使用します。  
  
 [可用性データベースの監視](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)  
 クラスターのすべての Always On 可用性グループに含まれる SQL Server インスタンス上のデータベースごとに、1 行のデータを格納します。ローカル コピー データベースが可用性グループに参加しているかどうかは問いません。  
  
> [!NOTE]  
>  データベースを可用性グループに追加すると、プライマリ データベースは自動的にそのグループに参加します。 セカンダリ データベースを可用性グループに参加させるには、各セカンダリ レプリカでそのデータベースを準備する必要があります。  
  
 **列名:** group_id、group_database_id、database_name  
  
 [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに、データベースごとに 1 行のデータを保持します。 データベースが可用性レプリカに属している場合は、そのデータベースの行に、レプリカの GUID と、その可用性グループ内のデータベースの一意識別子が表示されます。  
  
 **[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 列名:** replica_id、group_database_id  
  
 [sys.dm_hadr_auto_page_repair](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
 サーバー インスタンスで任意の可用性グループに対してホストされている可用性レプリカの可用性データベースに対するページの自動修復の試行ごとに 1 行のデータを返します。 このビューには、特定のプライマリまたはセカンダリ データベースに対して最近試行されたページの自動修復に対応する行が含まれます (データベースあたり最大 100 行)。 データベースあたりの最大行数に達すると、その後に試行されたページの自動修復の行によって、既存のエントリが置き換えられます。  
  
 **列名:** database_id、file_id、page_id、error_type、page_status、modification_time  
  
 [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスが可用性レプリカをホストしている任意の可用性グループに参加しているデータベースごとに 1 行のデータを返します。  
  
 **列名:** database_id、group_id、replica_id、group_database_id、is_local、synchronization_state、synchronization_state_desc、is_commit_participant、synchronization_health、synchronization_health_desc、database_state、database_state_desc、is_suspended、suspend_reason、suspend_reason_desc、recovery_lsn、truncation_lsn、last_sent_lsn、last_sent_time、last_received_lsn、last_received_time、last_hardened_lsn、last_hardened_time、last_redone_lsn、last_redone_time、log_send_queue_size、log_send_rate、redo_queue_size、redo_rate、filestream_send_rate、end_of_log_lsn、last_commit_lsn、last_commit_time、low_water_mark_for_ghosts  
  
 [sys.availability_databases_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
 Windows Server フェールオーバー クラスタリング (WSFC) クラスター上の各可用性グループに含まれる可用性データベースの正常性を把握するための情報を含む行を返します。 この動的管理ビューは、フェールオーバーを計画する際やフェールオーバーに応答する際のほか、特定のプライマリ データベースでログの切り捨てを維持している可用性グループ内のセカンダリ レプリカを検出する際に役立ちます。  
  
 **列名:** replica_id、group_database_id、database_name、is_failover_ready、is_pending_secondary_suspend、is_database_joined、recovery_lsn、truncation_lsn  
  
> [!NOTE]  
>  プライマリ レプリカの場所は、可用性グループに対して権限を持つソースです。  
  
> [!NOTE]  
>  可用性データベースの [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] パフォーマンス カウンター ( **SQLServer:Database Replica** パフォーマンス オブジェクト) の詳細については、「 [SQL Server、データベース レプリカ](../../../relational-databases/performance-monitor/sql-server-database-replica.md)」を参照してください。 また、可用性データベースのトランザクション ログ アクティビティを監視するには、**SQLServer:Databases** パフォーマンス オブジェクトのカウンター、**Log Flush Write Time (ms)** 、**Log Flushes/sec**、**Log Pool Cache Misses/sec**、**Log Pool Disk Reads/sec**、**Log Pool Requests/sec** です。詳しくは、「 [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md)」をご覧ください。  
  
##  <a name="AGlisteners"></a> 可用性グループ リスナーの監視  
 WSFC クラスターのサブネット上の可用性グループ リスナーを監視するには、次のビューを使用します。  
  
 [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
 可用性グループ リスナーに対してオンラインになっている準拠仮想 IP アドレスごとに 1 行のデータを返します。  
  
 **列名:** listener_id、ip_address、ip_subnet_mask、is_dhcp、network_subnet_ip、network_subnet_prefix_length、network_subnet_ipv4_mask、state, state_desc  
  
 [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
 特定の可用性グループについて、可用性グループにネットワーク名が関連付けられていないことを示すゼロ行を返すか、WSFC クラスター内の可用性グループ リスナーの構成ごとに 1 行のデータを返します。  
  
 **列名** : group_id、listener_id、dns_name、port、is_conformant、ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
 各 TCP リスナーの動的状態情報を含む行を返します。  
  
 **列名** : listener_id、ip_address、is_ipv4、port、type、type_desc、state、state_desc、start_time  
  
 **主キー:** listener_id  
  
 可用性グループ リスナーの詳細については、「[可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **Always On 可用性グループと監視タスク:**  
  
-   [[オブジェクト エクスプローラーの詳細] を使用した可用性グループの監視 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)  
  
-   [可用性グループのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [可用性レプリカのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [可用性グループ リスナーのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
 **Always On 可用性グループの監視に関するリファレンス (Transact-SQL):**  
  
-   [SERVERPROPERTY &#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)  
  
-   [sys.availability_group_listener_ip_addresses &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
  
-   [sys.availability_group_listeners &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
  
-   [sys.availability_databases_cluster &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)  
  
-   [sys.availability_groups &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_nodes &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
-   [sys.dm_hadr_auto_page_repair &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
  
-   [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_cluster &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)  
  
-   [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
-   [sys.dm_hadr_cluster_networks &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   [sys.dm_hadr_instance_node_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)  
  
-   [sys.dm_hadr_name_id_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)  
  
-   [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
-   [sys.dm_tcp_listener_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
  
-   [sys.fn_hadr_backup_is_preferred_replica  &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **Always On パフォーマンス カウンター:**  
  
-   [SQL Server、可用性レプリカ](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)  
  
-   [SQL Server、データベース レプリカ](../../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
-   [SQL Server, Databases Object](../../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 **Always On 可用性グループのポリシー ベースの管理**  
  
-   [Always On ポリシーを使用した可用性グループの正常性の確認 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Always On ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
