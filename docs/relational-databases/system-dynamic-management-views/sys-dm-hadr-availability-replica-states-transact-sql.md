---
title: sys.dm_hadr_availability_replica_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 05964e0557cb08e874424af542b8fc8a57ce0835
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900621"
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  ローカル レプリカごとに 1 行のデータと、ローカル レプリカと同じ AlwaysOn 可用性グループに含まれるリモート レプリカごとに 1 行のデータを返します。 各行には、特定のレプリカの状態に関する情報が含まれています。  
  
> [!IMPORTANT]  
>  特定の可用性グループのすべてのレプリカに関する情報を取得するクエリ**sys.dm_hadr_availability_replica_states**プライマリ レプリカをホストするサーバー インスタンスでします。 可用性グループのセカンダリ レプリカをホストしているサーバー インスタンスに対してクエリを実行した場合、この動的管理ビューはその可用性グループのローカル情報のみを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|レプリカの一意の識別子。|  
|**group_id**|**uniqueidentifier**|可用性グループの一意識別子。|  
|**is_local**|**bit**|レプリカが、ローカルかどうかのいずれか。<br /><br /> 0 = プライマリ レプリカがローカル サーバー インスタンスでホストされている可用性グループ内のリモート セカンダリ レプリカを示します。 この値が表示されるのは、プライマリ レプリカの場所だけです。<br /><br /> 1 = ローカル レプリカを示します。 セカンダリ レプリカの場合、これはそのレプリカが属する可用性グループに対して使用できる唯一の値です。|  
|**role**|**tinyint**|現在[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]ローカル レプリカまたは接続されているリモート レプリカのいずれかのロール。<br /><br /> 0 = 解決中<br /><br /> 1 = プライマリ<br /><br /> 2 = セカンダリ<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] のロールについては、「[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。|  
|**role_desc**|**nvarchar(60)**|説明**ロール**、1 つの。<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|1 つのレプリカの現在の操作状態:<br /><br /> 0 = フェールオーバー保留<br /><br /> 1 = 保留中<br /><br /> 2 = オンライン<br /><br /> 3 = オフライン<br /><br /> 4 = 失敗<br /><br /> 5 = 失敗、クォーラムなし<br /><br /> NULL = レプリカがローカルでない<br /><br /> 詳細については、次を参照してください。[ロールと操作状態](#RolesAndOperationalStates)、このトピックで後述します。|  
|**operational\_state\_desc**|**nvarchar(60)**|説明**運用\_状態**、1 つの。<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**recovery\_health**|**tinyint**|プログラムのロールアップ、**データベース\_状態**の列、 [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)動的管理ビュー。 使用可能な値とその説明を次に示します。<br /><br /> 0:進行中です。  少なくとも 1 つの参加データベースがオンライン以外のデータベースの状態 (**データベース\_状態**が 0 ではありません)。<br /><br /> 1:オンライン。 すべての参加データベースがオンラインのデータベース状態になります (**database_state**は 0 です)。<br /><br /> NULL : **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|説明**recovery_health**、1 つの。<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**同期\_正常性**|**tinyint**|データベースの同期状態のロールアップを反映 (**synchronization_state**) すべての可用性データベースを参加させる (とも呼ばれます*レプリカ*) とレプリカ (可用性モード同期コミット モードまたは非同期コミット モード)。 ロールアップは、レプリカの正常では、少なくとも累積状態のデータベースが反映されます。 使用可能な値とその説明を次に示します。<br /><br /> 0:正常ではありません。   少なくとも 1 つの参加データベースが NOT SYNCHRONIZING 状態です。<br /><br /> 1:部分的に正常な状態にします。 一部のレプリカが目標の同期状態ではありません: 同期コミット レプリカは SYNCHRONIZED である必要があり、非同期コミット レプリカは SYNCHRONIZING である必要があります。<br /><br /> 2:正常な状態です。 すべてのレプリカが目標の同期状態です: 同期コミット レプリカは SYNCHRONIZED であり、非同期コミット レプリカは SYNCHRONIZING です。|  
|**synchronization_health_desc**|**nvarchar(60)**|説明**synchronization_health**、1 つの。<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|セカンダリ レプリカが現在あるかどうかは、プライマリ レプリカに接続されています。 使用可能な値は、その説明を以下に示します。<br /><br /> 0:[接続解除されました。] DISCONNECTED 状態の可用性レプリカの応答は、そのロールによって異なります。プライマリのレプリカでセカンダリ レプリカが切断された場合そのセカンダリ データベースが NOT SYNCHRONIZED とマークに再接続します。 セカンダリの待機、プライマリ レプリカで検出することが切断された場合と、セカンダリ レプリカでセカンダリ レプリカはプライマリ レプリカへの再接続しようとします。<br /><br /> 1:接続されています。<br /><br /> 各プライマリ レプリカでは、同じ可用性グループに含まれるすべてのセカンダリ レプリカの接続状態を追跡します。 セカンダリ レプリカでは、プライマリ レプリカの接続状態のみを追跡します。|  
|**connected_state_desc**|**nvarchar(60)**|説明**connection_state**、1 つの。<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|最後の接続エラーの番号。|  
|**last_connect_error_description**|**nvarchar(1024)**|テキスト、 **last_connect_error_number**メッセージ。|  
|**last_connect_error_timestamp**|**datetime**|示す日付と時刻のタイムスタンプ、 **last_connect_error_number**エラーが発生しました。|  
  
##  <a name="RolesAndOperationalStates"></a> ロールと操作状態  
 ロール、**ロール**、特定の可用性レプリカの状態と動作の状態を反映**operational_state**レプリカはすべてのクライアント要求を処理する準備ができているかどうかについて説明します、可用性レプリカのデータベースです。 各ロールの可能な操作の状態の概要を次に示します。解決する、プライマリおよびセカンダリ。  
  
 **解決するには。** 可用性レプリカが RESOLVING ロールの場合は、次の表に示すように運用状態には。  
  
|動作状態|説明|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|可用性グループに対するフェールオーバー コマンドを処理しています。|  
|OFFLINE|WSFC クラスターおよびローカル メタデータ内の可用性レプリカのすべての構成データが更新されたが、可用性グループには現在プライマリ レプリカがありません。|  
|FAILED|WSFC クラスターから情報を取得しようとして、読み取りエラーが発生しました。|  
|FAILED_NO_QUORUM|ローカルの WSFC ノードに、クォーラムがありません。 これは、推論された状態です。|  
  
 **プライマリ。** 可用性レプリカがプライマリ ロールを実行する場合、プライマリ レプリカでは現在です。 使用可能な操作状態は次の表に示すようにします。  
  
|動作状態|説明|  
|-----------------------|-----------------|  
|PENDING|これは一時的な状態ですが、ワーカーを使用して要求を処理できない場合、プライマリ レプリカがこの状態になることがあります。|  
|ONLINE|可用性グループ リソースがオンラインになっており、すべてのデータベース ワーカー スレッドが選択されました。|  
|FAILED|可用性レプリカは、WSFC クラスターに対して読み取りまたは書き込みを行うことができません。|  
  
 **セカンダリ:** 可用性レプリカがセカンダリ ロールを実行する場合、セカンダリ レプリカでは現在です。 可能な操作状態は、次の表に示すようにします。  
  
|動作状態|説明|  
|-----------------------|-----------------|  
|ONLINE|ローカル セカンダリ レプリカがプライマリ レプリカに接続されています。|  
|FAILED|ローカル セカンダリ レプリカが WSFC クラスターに対して読み取りまたは書き込みを行うことができません。|  
|NULL|プライマリ レプリカでは、行がセカンダリ レプリカに関係する場合に、この値が返されます。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
