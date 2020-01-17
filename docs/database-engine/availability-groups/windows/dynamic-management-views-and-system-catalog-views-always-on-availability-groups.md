---
title: 可用性グループの DMV とシステム カタログ ビュー
description: Always On 可用性グループの正常性を監視し、診断するために役立つ一連の動的管理ビューとカタログ ビュー。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 4320a4a4-6183-462b-8bda-e7424e7cb706
author: rothja
ms.author: jroth
ms.openlocfilehash: 0389f613d9b7a26aa14c5a8388ee8cd34036ddf8
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822332"
---
# <a name="dynamic-management-views-and-system-catalog-views-always-on-availability-groups"></a>動的管理ビューおよびシステム カタログ ビュー (Always On 可用性グループ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、可用性グループの監視とトラブルシューティングに使用できる Always On 動的管理ビュー (DMV) に対する一般的なクエリをいくつか紹介します。  
  
> [!TIP]  
>  Always On ダッシュボードでは、各テーブル ヘッダーを右クリックし、表示または非表示にする DMV を選択することで、可用性レプリカおよび可用性データベース用の多数の DMV を表示する GUI を簡単に構成できます。  
  
 可用性グループの DMV の詳細については、「[Always On Availability Groups dynamic management views and functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)」(AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;) を参照してください。 可用性グループ カタログ ビューの詳細については、「[Always On Availability Groups catalog views &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)」(AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;) を参照してください。  
  
## <a name="check-the-wsfc-cluster-node-configuration"></a>WSFC クラスター ノード構成を確認する  
 次の Transact-SQL (T-SQL) クエリでは、現在の Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のすべてのノードの状態が取得されます。  
  
```sql  
use master  
go  
select * from sys.dm_hadr_cluster_members  
go  
```  
  
 この結果セットでは、現在の WSFC クラスターの各メンバー ノードの状態が報告されます。 クォーラムが**ノードとファイル共有マジョリティ**として定義されている場合は、ファイル共有も報告されます。 各ノードの投票の重み ([number_of_quorum_votes](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md) 値) を含め、各ノードの状態を確認できます。  
  
## <a name="explore-the-cluster-network"></a>クラスター ネットワークを探索する  
 次のクエリでは、現在の WSFC クラスターのネットワーク構成が取得されます。  
  
```sql  
select * from sys.dm_hadr_cluster_networks  
```  
  
 結果セットには、WSFC クラスター内のネットワーク アダプターごとに 1 行が含まれています。 たとえば、各ノードに 2 つのネットワーク アダプターを含む 2 ノード クラスターの場合、このクエリで 4 行が返されます。  
  
## <a name="explore-the-availability-groups"></a>可用性グループを探索する  
 次のクエリでは、可用性グループに関する情報が取得されます。  
  
```sql  
select primary_replica, primary_recovery_health_desc, synchronization_health_desc from sys.dm_hadr_availability_group_states  
go  
select * from sys.availability_groups  
go  
select * from sys.availability_groups_cluster  
go  
```  
  
 DMV [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md)、[sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)、および [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md) では、いずれも現在の WSFC クラスター内の可用性グループに関する情報が返されます。 実際のところ、[sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) と [sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md) では同じ情報が返されるようです。  
  
 ただし、[sys.availability_groups_cluster](~/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql.md) では WSFC クラスターに格納されている可用性グループのメタデータが報告されますが、[sys.availability_groups &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) では SQL Server プロセス空間にキャッシュされている可用性グループ メタデータが報告されます。 さらに、これら 2 つの DMV で構成情報が報告されますが、[sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql.md) では可用性グループの現在の正常性状態が報告されます。  
  
> [!IMPORTANT]  
>  この命名規則は、可用性レプリカと可用性データベースを文書化した DMV に引き継がれます。  
  
## <a name="explore-the-availability-replicas"></a>可用性レプリカを探索する  
 次のクエリでは、可用性グループに定義されている可用性レプリカに関する情報が取得されます。  
  
```sql  
select replica_id, role_desc, connected_state_desc, synchronization_health_desc from sys.dm_hadr_availability_replica_states  
go  
select replica_server_name, replica_id, availability_mode_desc, endpoint_url from sys.availability_replicas  
go  
select replica_server_name, join_state_desc from sys.dm_hadr_availability_replica_cluster_states  
go  
```  
  
 可用性グループ DMV と同様に、可用性レプリカについて報告する 3 つの DMV があります。 [sys.dm_hadr_availability_replica_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) では、SQL Server のローカルにキャッシュされている可用性レプリカに関する状態情報が報告され、[sys.dm_hadr_availability_replica_cluster_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md) では、WSFC クラスターから可用性レプリカに関する状態情報が報告されます。 最後に、[sys.availability_replicas](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql.md) では、SQL Server のローカルにキャッシュされている可用性レプリカの構成データが報告されます。  
  
## <a name="explore-availability-replica-health"></a>可用性レプリカ ヘルスの正常性を探索する  
 次のクエリでは、可用性レプリカに関する現在の正常性情報が取得されます。  
  
```sql  
select replica_id, role_desc, recovery_health_desc, synchronization_health_desc from sys.dm_hadr_availability_replica_states  
go  
```  
  
 プライマリ レプリカとセカンダリ レプリカのクエリ結果を比較すると、セカンダリ レプリカでは、そのレプリカについての状態情報のみが報告され、可用性グループ内の他のレプリカについては報告されないことがわかります。  
  
## <a name="explore-the-availability-databases"></a>可用性データベースを探索する  
 次のクエリでは、可用性グループに定義されている可用性レプリカに関する情報が取得されます。 可用性データベース上のデータ移動を停止する前後で、クエリ結果の変化を確認することができます。  
  
```sql
select * from sys.availability_databases_cluster  
go  
select group_database_id, database_name, is_failover_ready  from sys.dm_hadr_database_replica_cluster_states  
go  
select database_id, synchronization_state_desc, synchronization_health_desc, last_hardened_lsn, redo_queue_size, log_send_queue_size from sys.dm_hadr_database_replica_states  
go  
```  
  
 この場合も、3 台の Always On DMV から可用性データベースについて報告されます。 [sys.availability_databases_cluster](~/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql.md) では、WSFC クラスターから可用性データベースに関する構成情報が報告されます。 [sys.dm_hadr_database_replica_cluster_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md) では、SQL Server のローカルにキャッシュされているデータベース レプリカに関する状態情報が報告されます。 この報告には、可用性レプリカのフェールオーバーの準備などのいくつかの重要な状態情報が含まれています。 最後に、[sys.dm_hadr_database_replica_states](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) は、プライマリおよびセカンダリ データベース レプリカのログの LSN 進行情報など、各可用性データベースの ID と状態情報を報告する非常に詳細な結果セットです。  
  
## <a name="explore-availability-database-health"></a>可用性データベースの正常性を探索する  
 次のクエリでは、レプリカ上の各可用性データベースの正常性に関する情報が取得されます。 可用性データベース上のデータ移動を停止する前後で、クエリ結果の変化を確認することができます。  
  
```sql  
select dc.database_name, dr.database_id, dr.synchronization_state_desc,   
dr.suspend_reason_desc, dr.synchronization_health_desc  
from sys.dm_hadr_database_replica_states dr  join sys.availability_databases_cluster dc  
on dr.group_database_id=dc.group_database_id   
where is_local=1  
go  
```  
  
  
