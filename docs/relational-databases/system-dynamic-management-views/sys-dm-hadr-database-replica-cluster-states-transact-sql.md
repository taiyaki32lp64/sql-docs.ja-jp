---
title: sys.dm_hadr_database_replica_cluster_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_replica_cluster_states
- dm_hadr_database_replica_cluster_states_TSQL
- sys.dm_hadr_database_replica_cluster_states_TSQL
- dm_hadr_database_replica_cluster_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_database_replica_cluster_states dynamic management view
ms.assetid: 6f719071-ebce-470d-aebd-1f55ee8cd70a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2fbd066113f5ad4394b83e0151643ab9ea3b7b82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900664"
---
# <a name="sysdmhadrdatabasereplicaclusterstates-transact-sql"></a>sys.dm_hadr_database_replica_cluster_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Windows Server フェールオーバー クラスタリング (WSFC) クラスター上の各 AlwaysOn 可用性グループについて、AlwaysOn 可用性グループ内の可用性データベースの正常性を把握するための情報を含む行を返します。 クエリ**sys.dm_hadr_database_replica_states**次の質問に回答します。  
  
-   可用性グループのすべてのデータベースでフェールオーバーの準備ができているか。  
  
-   強制フェールオーバー後に、セカンダリ データベース自体がローカルで中断されており、その中断状態が新しいプライマリ レプリカに対して通知されたか。  
  
-   プライマリ レプリカが現在使用できない場合、プライマリ レプリカになったときにデータ損失を最小限に抑えることができるセカンダリ レプリカはどれか。  
  
-   ときの値、 [sys.databases](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)**log_reuse_wait_desc**列は"availability_replica"の場合、可用性グループのセカンダリ レプリカを維持している特定のプライマリ データベースでログの切り捨て?  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|可用性グループ内の可用性レプリカの識別子。|  
|**group_database_id**|**uniqueidentifier**|可用性グループ内のデータベースの識別子。 この識別子は、このデータベースが参加しているすべてのレプリカで同じです。|  
|**database_name**|**sysname**|可用性グループに属しているデータベースの名前。|  
|**is_failover_ready**|**bit**|セカンダリ データベースが対応するプライマリ データベースと同期されているかどうかを示します。 いずれか:<br /><br /> 0 = データベースはクラスター内で同期済みとしてマークされていません。 データベースはフェールオーバーの準備ができていません。<br /><br /> 1 = データベースは、クラスター内で同期済みに設定します。 データベースは、フェールオーバーの準備ができました。|  
|**is_pending_secondary_suspend**|**bit**|強制フェールオーバー後に、データベースの中断が保留されているかどうかを示します。次のいずれかになります。<br /><br /> 0 = HADR_SYNCHRONIZED_ SUSPENDED 以外の状態。<br /><br /> 1 = HADR_SYNCHRONIZED_ SUSPENDED。 強制フェールオーバーが完了すると、各セカンダリ データベースは HADR_SYNCHONIZED_SUSPENDED に設定され、新しいプライマリ レプリカがそのセカンダリ データベースから SUSPEND メッセージに対する受信確認を受け取るまでその状態のままになります。<br /><br /> NULL = 不明 (クォーラムなし)|  
|**is_database_joined**|**bit**|この可用性レプリカ上のデータベースが 1 つの可用性グループに参加しているかどうかを示します。<br /><br /> 0 = データベースがこの可用性レプリカの可用性グループに参加していません。<br /><br /> 1 = この可用性レプリカ上のデータベースは可用性グループに参加しています。<br /><br /> NULL = 不明 (可用性レプリカのクォーラムが不足します)|  
|**recovery_lsn**|**numeric(25,0)**|プライマリ レプリカの場合は、レプリカ前に、のトランザクション ログの末尾は、復旧またはフェールオーバー後に新しいログ レコードを書き込みます。 プライマリ レプリカでは、特定のセカンダリ データベースの行の値が、プライマリ レプリカによって要求されるセカンダリ レプリカの同期先 (つまり、復元先および再初期化先) の値になります。<br /><br /> セカンダリ レプリカではこの値は NULL です。 各セカンダリ レプリカが最大値またはプライマリ レプリカには、セカンダリ レプリカに戻りますが指示の下限値のいずれかを持つことに注意してください。|  
|**truncation_lsn**|**numeric(25,0)**|ローカル ログの切り捨てが (バックアップ操作などにより) ブロックされている場合にローカル切り捨て LSN を超える可能性のある [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ログ切り捨て値。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
  
