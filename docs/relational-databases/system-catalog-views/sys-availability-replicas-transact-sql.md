---
title: sys.availability_replicas (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_replicas_TSQL
- availability_replicas
- sys.availability_replicas
- sys.availability_replicas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_replicas catalog view
ms.assetid: 0a06e9b6-a1e4-4293-867b-5c3f5a8ff62c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6623d6b95dfe0ebd4e45b13d190d8176bcab1a3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942618"
---
# <a name="sysavailabilityreplicas-transact-sql"></a>sys.availability_replicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

WSFC フェールオーバー クラスター内の AlwaysOn 可用性グループに属している各可用性レプリカに対する行を返します。  
  
たとえばクラスターがダウンしたりクォーラムが失われたりしたために、ローカル サーバー インスタンスが WSFC フェールオーバー クラスターと通信できない場合は、ローカル可用性レプリカの行だけが返されます。 これらの行には、メタデータ内にローカルにキャッシュされているデータの列だけが含まれます。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|レプリカの一意の ID。|  
|**group_id**|**uniqueidentifier**|レプリカが属している可用性グループの一意の ID。|  
|**replica_metadata_id**|**int**|データベース エンジンの可用性レプリカのローカル メタデータ オブジェクトの ID。|  
|**replica_server_name**|**nvarchar (256)**|このレプリカをホストし、既定ではないインスタンスの場合はレプリカのインスタンス名もホストしている、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのサーバー名。|  
|**owner_sid**|**varbinary(85)**|このサーバー インスタンスに登録されている、この可用性レプリカの外部所有者のセキュリティ ID (SID)。<br /><br /> 非ローカル可用性レプリカの場合は NULL です。|  
|**endpoint_url**|**nvarchar(128)**|データ同期のためにプライマリとセカンダリのレプリカの間の接続で使用される、ユーザー指定のデータベース ミラーリング エンドポイントの文字列表現。 エンドポイント URL の構文の詳細については、「[可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)」を参照してください。<br /><br /> NULL = WSFC フェールオーバー クラスターと通信できません。<br /><br /> このエンドポイントを変更する、ENDPOINT_URL オプションを使用して、 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。|  
|**availability_mode**|**tinyint**|レプリカの可用性モード。次のいずれかです。<br /><br /> 0&#124;非同期コミットします。 プライマリ レプリカは、セカンダリがログをディスクに書き込むのを待機することなくトランザクションをコミットできます。<br /><br /> 1&#124;同期コミットします。 プライマリ レプリカは、セカンダリ レプリカがトランザクションをディスクに書き込むまで、特定のトランザクションのコミットを待機します。<br /><br />4&#124;構成のみです。 プライマリ レプリカは、同期的に、レプリカを可用性グループ構成メタデータを送信します。 ユーザー データは、レプリカに送信されません。 SQL Server 2017 CU1 以降を使用できます。<br /><br /> 詳細については、「[可用性モード &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。|  
|**availability_mode_desc**|**nvarchar(60)**|説明**可用性\_モード**、1 つの。<br /><br /> 非同期\_コミット<br /><br /> 同期\_コミット<br /><br /> 構成\_のみ<br /><br /> この可用性レプリカの可用性モードを変更するには、AVAILABILITY_MODE オプションを使用して[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。<br/><br>構成に、レプリカの可用性モードを変更することはできません\_のみです。 構成を変更することはできません\_セカンダリまたはプライマリ レプリカに専用のレプリカ。 |  
|**failover\_mode**|**tinyint**|[フェールオーバー モード](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)可用性レプリカのいずれかの。<br /><br /> 0&#124;自動フェールオーバー。 レプリカは、自動フェールオーバーの潜在的なターゲットです。  同期コミット可用性モードが設定されている場合にのみ、自動フェールオーバーがサポートされて (**可用性\_モード**= 1) 可用性レプリカが現在同期されています。<br /><br /> 1&#124;手動フェールオーバー。 手動フェールオーバーに設定するセカンダリ レプリカへのフェールオーバーは、データベース管理者が手動で開始する必要があります。 実行されるフェールオーバーの種類はかどうか、セカンダリ レプリカが同期されて、次のように異なります。<br /><br /> 可用性レプリカが同期していない場合、またはまだ同期を行っている場合は、強制フェールオーバーのみが可能です (データが失われる可能性があります)。<br /><br /> 同期コミット可用性モードが設定されている場合 (**可用性\_モード**= 1)、可用性レプリカが現在同期されて、手動フェールオーバー データの損失が発生する可能性がないとします。<br /><br /> 可用性レプリカのすべての可用性データベースのデータベースの同期のヘルスのロールアップを表示する、**同期\_ヘルス**と**同期\_正常性\_desc**の列、 [sys.dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)動的管理ビュー。 ロールアップでは、各可用性データベースの同期状態と、その可用性レプリカの可用性モードが考慮されます。<br /><br /> **注:** 特定の可用性データベースの同期状態を表示するには、クエリ、**同期\_状態**と**同期\_ヘルス**の列[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)動的管理ビュー。|  
|**failover\_mode\_desc**|**nvarchar(60)**|説明**フェールオーバー\_モード**、1 つの。<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> フェールオーバー モードを変更するには、フェールオーバーを使用\_モード オプションの[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。|  
|**session\_timeout**|**int**|タイムアウト時間 (秒単位)。 タイムアウト時間は、レプリカが別のレプリカからのメッセージの受信を待機する最大時間です。この時間を過ぎると、プライマリ レプリカとセカンダリ レプリカの間の接続は障害があるものと見なされます。 セッション タイムアウトは、セカンダリ レプリカがプライマリ レプリカに接続されているかどうかを検出します。<br /><br /> セカンダリ レプリカで障害が発生した接続を検出するには、プライマリ レプリカができないセカンダリ レプリカを考慮\_同期します。 プライマリ レプリカとの接続が確立されていないことを検出すると、セカンダリ レプリカは単に再接続を試みます。<br /><br /> **注:** セッション タイムアウトにより自動フェールオーバーが発生することはありません。<br /><br /> この値を変更するには、SESSION_TIMEOUT オプションを使用して[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。|  
|**プライマリ\_ロール\_許可\_接続**|**tinyint**|かどうか、可用性には、すべての接続や、1 つの読み取り/書き込み接続のみが使用できます。<br /><br /> 2 = すべて (既定)<br /><br /> 3 = 読み取り書き込み|  
|**プライマリ\_ロール\_許可\_接続\_desc**|**nvarchar(60)**|説明**プライマリ\_ロール\_許可\_接続**、1 つの。<br /><br /> ALL<br /><br /> 読み取る\_書き込み|  
|**セカンダリ\_ロール\_許可\_接続**|**tinyint**|セカンダリ ロールを実行している (つまりセカンダリ レプリカとして機能している) 可用性レプリカがクライアントからの接続を受け入れることができるかどうか。以下のいずれかです。<br /><br /> 0 = いいえ。 セカンダリ レプリカのデータベースに対する接続は許可されず、データベースに対して読み取りアクセスを実行できません。 これが既定の設定です。<br /><br /> 1 = 読み取り専用です。 セカンダリ レプリカのデータベースに対しては読み取り専用接続だけが許可されます。 レプリカ内のすべてのデータベースは読み取りアクセスで利用できます。<br /><br /> 2 = すべて。 読み取り専用アクセスに限り、セカンダリ レプリカのデータベースに対するすべての接続が許可されます。<br /><br /> 詳細については、「[アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|説明**secondary_role_allow_connections**、1 つの。<br /><br /> NO<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|レプリカが作成された日付。<br /><br /> NULL このサーバー インスタンスではなく、レプリカを = です。|  
|**modify_date**|**datetime**|レプリカが最後に変更された日付。<br /><br /> NULL このサーバー インスタンスではなく、レプリカを = です。|  
|**backup_priority**|**int**|同じ可用性グループ内の他のレプリカと比較して、このレプリカでバックアップを実行する優先順位を表す、ユーザー指定の値。 値は 0 ～ 100 の範囲の整数です。<br /><br /> 詳細については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。|  
|**read_only_routing_url**|**nvarchar (256)**|読み取り専用可用性レプリカの接続エンドポイント (URL) です。 詳細については、このトピックの後の「 [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)など) を含め、セカンダリ レプリカをホストするサーバー インスタンス上の読み書き可能なデータベースには書き込むことができます。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバー インスタンスに対する VIEW ANY DEFINITION 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
