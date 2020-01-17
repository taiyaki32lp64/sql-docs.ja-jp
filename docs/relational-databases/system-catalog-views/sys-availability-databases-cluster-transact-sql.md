---
title: sys.availability_databases_cluster (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 206c9b1c250cb95a6ad49ccf20f8badf11f870ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046537"
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  インスタンスで可用性データベースごとに 1 つの行を含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ローカルでデータベースをコピーするかどうかに関係なく、Windows Server フェールオーバー クラスタ リング (WSFC) クラスターで Always On 可用性グループの可用性レプリカをホストしています。可用性グループにまだ参加しています。  
  
> [!NOTE]  
>  データベースを可用性グループに追加すると、プライマリ データベースは自動的にそのグループに参加します。 セカンダリ データベースを可用性グループに参加させるには、各セカンダリ レプリカでそのデータベースを準備する必要があります。   
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|これで、可用性グループ、存在するデータベースが参加している場合、可用性グループの一意の識別子。<br /><br /> NULL = データベースが可用性グループの可用性レプリカの一部ではありません。|  
|**group_database_id**|**uniqueidentifier**|存在するデータベースが参加している場合、可用性グループ内のデータベースの一意の識別子。 **group_database_id**をデータベースが参加している可用性グループにすべてのセカンダリ レプリカとプライマリ レプリカでは、このデータベースに同じです。<br /><br /> NULL = データベースは、任意の可用性グループの可用性レプリカの一部ではありません。|  
|**database_name**|**sysname**|可用性グループに追加されたデータベースの名前。|  
  
## <a name="permissions"></a>アクセス許可  
 場合、呼び出し元の**sys.availability_databases_cluster**データベース、ALTER ANY DATABASE、対応する行を確認するために必要最低限のアクセス許可または VIEW ANY DATABASE のサーバー レベルの権限、または作成の所有者ではないです。DATABASE 権限、**マスター**データベース。  
  
## <a name="see-also"></a>関連項目  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys.dm_hadr_database_replica_cluster_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
