---
title: 可用性グループ システム オブジェクト リファレンス
description: Always On 可用性グループを使用する場合に使用できる各種システム オブジェクトのリファレンス。
ms.custom: seo-lt-2019
ms.date: 04/03/2010
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2014||=sqlallproducts-allversions'
ms.openlocfilehash: 140953484006d33e7814c19b9eb5bd6abcd29009
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822468"
---
# <a name="always-on-availability-group-system-object-reference"></a>AlwaysOn 可用性グループ システム オブジェクト リファレンス

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
    
このトピックは、AlwaysOn 可用性グループを使用する場合に使用できる各種システム オブジェクトのすべてに対するリファレンス ページとして機能します。 

## <a name="system-catalog-views"></a>システム カタログ ビュー

| システム カタログ ビュー | [説明]|
| :------ | :----------------------------- |
| [可用性データベースの監視](../../../relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md)   | Windows Server フェールオーバー クラスタリング (WSFC) クラスター内にある任意の AlwaysOn 可用性グループの可用性レプリカをホストしている SQL Server インスタンス上の可用性データベースごとに 1 行のデータを格納します。ローカル コピー データベースが可用性グループに参加しているかどうかは問いません。 |
| [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  | Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の任意の AlwaysOn 可用性グループ リスナーに関連付けられている IP アドレスごとに 1 行のデータを返します。 |
| [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)    | 各 AlwaysOn 可用性グループについて、可用性グループにネットワーク名が関連付けられていないことを示すゼロ行を返すか、Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の可用性グループ リスナーの構成ごとに 1 行のデータを返します。  |
| [sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   | SQL Server のローカル インスタンスが可用性レプリカをホストしている各可用性グループの行を返します。 各行には、可用性グループ メタデータのキャッシュされたコピーが含まれます。 |
| [sys.availability_groups_cluster](../../../relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md)    | Windows Server フェールオーバー クラスタリング (WSFC) の各 AlwaysOn 可用性グループに対する行を返します。 各行には、WSFC クラスターからの可用性グループ メタデータが含まれます。 |
| [sys.availability_read_only_routing_lists](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)    | WSFC フェールオーバー クラスター内の AlwaysOn 可用性グループにある各可用性レプリカの読み取り専用ルーティング リストに対する行を返します。 |
| [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)    | WSFC フェールオーバー クラスター内の AlwaysOn 可用性グループに属している各可用性レプリカに対する行を返します。 |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>システム動的管理ビュー


| システム動的管理ビュー | [説明]|
| :------ | :----------------------------- |
| [sys.dm_hadr_auto_page_repair](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)   | サーバー インスタンスで任意の可用性グループに対してホストされている可用性レプリカの可用性データベースに対するページの自動修復の試行ごとに 1 行のデータを返します。  |
| [sys.dm_hadr_availability_group_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)    | SQL Server のローカル インスタンスで可用性レプリカを保持する AlwaysOn 可用性グループごとに 1 行のデータを返します。 各行には、特定の可用性グループの正常性を定義する状態が表示されます。 |
| [sys.dm_hadr_availability_replica_cluster_nodes](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql.md)     | Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の AlwaysOn 可用性グループの可用性レプリカ (結合状態に関係なく) ごとに 1 行のデータを返します。 |
| [sys.dm_hadr_availability_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md)     | Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のすべての AlwaysOn 可用性グループ (レプリカの場所を問いません) の AlwaysOn 可用性レプリカ (結合状態を問いません) ごとに 1 行のデータを返します。 |
| [sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)    | ローカル レプリカごとに 1 行のデータと、ローカル レプリカと同じ AlwaysOn 可用性グループに含まれるリモート レプリカごとに 1 行のデータを返します。 各行には、特定のレプリカの状態に関する情報が含まれています。 |
| [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md)    | クラスターの名前とクォーラムに関する情報を公開する行を返します。 |
| [sys.dm_hadr_cluster_members](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)    | クォーラムを構成するメンバーとそれぞれの状態を示す行を返します。 |
| [sys.dm_hadr_cluster_networks](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql.md)    | 可用性グループのサブネット構成に参加している WSFC クラスター メンバーごとに 1 行のデータを返します。  |
| [sys.availability_databases_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)     | Windows Server フェールオーバー クラスタリング (WSFC) クラスター上の各 AlwaysOn 可用性グループについて、AlwaysOn 可用性グループ内の可用性データベースの正常性を把握するための情報を含む行を返します。  |
| [sys.dm_hadr_database_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)    | SQL Server のローカル インスタンスが可用性レプリカをホストしている AlwaysOn 可用性グループに参加しているデータベースごとに 1 行のデータを返します。 |
| [sys.dm_hadr_instance_node_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql.md)    | Always On 可用性グループに参加させる可用性レプリカをホストする SQL Server のすべてのインスタンスに対して、サーバー インスタンスをホストする Windows Server フェールオーバー クラスター (WSFC) ノードの名前を返します。 |
| [sys.dm_hadr_name_id_map](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql.md)    | SQL Server の現在のインスタンスが参加する Always On 可用性グループの、可用性グループ ID、WSFC リソース ID、および WSFC グループ ID という 3 つの一意の ID に対するマッピングを示します。 |
| [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)    | 各 TCP リスナーの動的状態情報を含む行を返します。 |
| &nbsp; | &nbsp; |

## <a name="system-functions"></a>システム関数


| システム関数 | [説明]|
| :------ | :----------------------------- |
| [sys.fn_hadr_is_primary_replica](../../../relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql.md)  | 現在のレプリカがプライマリ レプリカであるかどうかを決定するために使用されます。 |
| [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)    | 現在のレプリカが推奨されるバックアップ レプリカであるかどうかを決定するために使用されます。 |
| [sys.fn_hadr_distributed_ag_replica](../../../relational-databases/system-functions/sys-fn-hadr-distributed-ag-replica-transact-sql.md)    | 分散型可用性グループ内のレプリカをローカル可用性グループにマップするために使用されます。 |
| &nbsp; | &nbsp; |


  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   

  
