---
title: availability_groups_cluster (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9ca998a0b65fff44e71549d1dae879d73288dfb
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874271"
---
# <a name="sysavailability_groups_cluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Windows Server フェールオーバー クラスタリング (WSFC) の各 AlwaysOn 可用性グループに対する行を返します。 各行には、WSFC クラスターからの可用性グループ メタデータが含まれます。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性グループの一意識別子 (GUID)。|  
|**name**|**sysname**|可用性グループの名前。 これはユーザー指定の名前であり、Windows Server フェールオーバー クラスター (WSFC) 内で一意であることが必要です。|  
|**resource_id**|**nvarchar(40)**|WSFC クラスター リソースのリソース ID。|  
|**resource_group_id**|**nvarchar(40)**|可用性グループの WSFC クラスター リソース グループのリソース グループ ID。|  
|**failure_condition_level**|**int**|自動フェールオーバーをトリガーする必要があるユーザー定義のエラー状態レベル。次のいずれかの整数値を指定できます。<br /><br /> 1: 次のいずれかが発生した場合に、自動フェールオーバーを開始する必要があることを指定します。 <br />-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスがダウンしています。<br />-サーバーインスタンスから ACK を受信しないため、WSFC フェールオーバークラスターに接続するための可用性グループのリースが期限切れになります。 詳細については、「 [動作方法: SQL Server Always On のリース タイムアウト](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)」を参照してください。<br /><br /> 2: 次のいずれかが発生した場合に、自動フェールオーバーを開始する必要があることを指定します。  <br />-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがクラスターに接続していません。また、可用性グループのユーザー指定の**health_check_timeout**しきい値を超えています。 <br />-可用性レプリカがエラー状態になっています。 <br />3: 孤立したスピンロック、深刻な書き込みアクセス違反、ダンプが多すぎるなど、重大な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。 これが既定値です。 <br />4: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部リソースプールに永続的なメモリ不足の状態があるなど、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に、自動フェールオーバーを開始する必要があることを指定します。<br />5: 次のように、すべての修飾されたエラー条件で自動フェールオーバーを開始する必要があることを指定します。<br />-SQL エンジンのワーカースレッドの枯渇。 <br />-解決不可能なデッドロックの検出。<br /><br /> エラー状態レベルの範囲は 1 ～ 5 で、レベル 1 が最も制限が緩く、レベル 5 が最も制限の厳しい指定です。 任意の状態レベルは、それより制限が緩いすべてのレベルを含みます。 したがって、最も厳しい状態レベル 5 にはそれより制限が緩い状態レベル (1 から 4) が含まれ、レベル 4 にはレベル 1 から 3 が含まれます。以下同様です。<br /><br /> この値を変更するには、 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの FAILURE_CONDITION_LEVEL オプションを使用します。|  
|**health_check_timeout**|**int**|サーバーインスタンスが低速または応答していないと想定される前に、 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)システムストアドプロシージャがサーバーの正常性情報を返すまでの待機時間 (ミリ秒単位)。 既定値は 30000 ミリ秒 (30 秒) です。<br /><br /> この値を変更するには、 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの HEALTH_CHECK_TIMEOUT オプションを使用します。|  
|**automated_backup_preference**|**tinyint**|この可用性グループの可用性データベースでバックアップを実行するための推奨される場所です。 次の値のいずれかになります。<br /><br /> 0: プライマリ。 バックアップは常にプライマリレプリカで実行する必要があります。<br />1: セカンダリのみ。 セカンダリレプリカでバックアップを実行することをお勧めします。<br />2: セカンダリを優先します。 セカンダリレプリカでバックアップを実行することをお勧めしますが、バックアップ操作に使用できるセカンダリレプリカがない場合は、プライマリレプリカでバックアップを実行できます。 これは既定の動作です。<br />3: 任意のレプリカ。 バックアップをプライマリレプリカとセカンダリレプリカのどちらで実行するかについては、優先順位はありません。<br /><br /> 詳細については、「[アクティブなセカンダリ: セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|**Automated_backup_preference**の説明。次のいずれかになります。<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> NONE|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 サーバー インスタンスに対する VIEW ANY DEFINITION 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
