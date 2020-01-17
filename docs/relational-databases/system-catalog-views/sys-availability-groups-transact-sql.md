---
title: availability_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ca82c64d2d0269564567de175b9d6f778f76d4d7
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874261"
---
# <a name="sysavailability_groups-transact-sql"></a>availability_groups (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SQL Server のローカル インスタンスが可用性レプリカをホストしている各可用性グループの行を返します。 各行には、可用性グループ メタデータのキャッシュされたコピーが含まれます。  
   
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性グループの一意識別子 (GUID)。|  
|**name**|**sysname**|可用性グループの名前。 これはユーザー指定の名前であり、Windows Server フェールオーバー クラスター (WSFC) 内で一意であることが必要です。|  
|**resource_id**|**nvarchar(40)**|WSFC クラスター リソースのリソース ID。|  
|**resource_group_id**|**nvarchar(40)**|可用性グループの WSFC クラスター リソース グループのリソース グループ ID。|  
|**failure_condition_level**|**int**|自動フェールオーバーをトリガーする必要があるユーザー定義のエラー状態レベル。このレベルでは、このテーブルのすぐ下のテーブルに表示される整数値の1つです。<br /><br /> エラー状態レベルの範囲は 1 ～ 5 で、レベル 1 が最も制限が緩く、レベル 5 が最も制限の厳しい指定です。 任意の状態レベルは、それより制限が緩いすべてのレベルを含みます。 したがって、最も厳しい状態レベル 5 にはそれより制限が緩い状態レベル (1 から 4) が含まれ、レベル 4 にはレベル 1 から 3 が含まれます。以下同様です。<br /><br /> この値を変更するには、 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの FAILURE_CONDITION_LEVEL オプションを使用します。|  
|**health_check_timeout**|**int**|サーバーインスタンスが低速または応答していないと想定される前に、 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)システムストアドプロシージャがサーバーの正常性情報を返すまでの待機時間 (ミリ秒単位)。 既定値は 30000 ミリ秒 (30 秒) です。<br /><br /> この値を変更するには、 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの HEALTH_CHECK_TIMEOUT オプションを使用します。|  
|**automated_backup_preference**|**tinyint**|この可用性グループの可用性データベースでバックアップを実行するための推奨される場所です。 使用可能な値とその説明を次に示します。<br /><br /> <br /><br /> 0: プライマリ。 バックアップは常にプライマリレプリカで実行する必要があります。<br /><br /> 1: セカンダリのみ。 セカンダリレプリカでバックアップを実行することをお勧めします。<br /><br /> 2: セカンダリを優先します。 セカンダリレプリカでバックアップを実行することをお勧めしますが、バックアップ操作に使用できるセカンダリレプリカがない場合は、プライマリレプリカでバックアップを実行できます。 これは既定の動作です。<br /><br /> 3: 任意のレプリカ。 バックアップをプライマリレプリカとセカンダリレプリカのどちらで実行するかについては、優先順位はありません。<br /><br /> <br /><br /> 詳細については、「[アクティブなセカンダリ: セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|**Automated_backup_preference**の説明。次のいずれかになります。<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> NONE|  
|**version**|**smallint**|Windows フェールオーバークラスターに格納されている可用性グループのメタデータのバージョン。 このバージョン番号は、新しい機能が追加されたときにインクリメントされます。|  
|**basic_features**|**bit**|これが基本的な可用性グループかどうかを指定します。 詳細については、「[基本的な可用性グループ &#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)」を参照してください。|  
|**dtc_support**|**bit**|この可用性グループに対して DTC サポートが有効になっているかどうかを指定します。 **CREATE AVAILABILITY GROUP**の**DTC_SUPPORT**オプションは、この設定を制御します。|  
|**db_failover**|**bit**|可用性グループがデータベースの正常性状態のフェールオーバーをサポートするかどうかを指定します。 **CREATE AVAILABILITY GROUP**の**DB_FAILOVER**オプションは、この設定を制御します。|  
|**is_distributed**|**bit**|分散型可用性グループかどうかを指定します。 詳細については、「[Distributed Availability Groups &#40;Always On Availability Groups&#41; (分散型可用性グループ (Always On 可用性グループ))](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)」を参照してください。|  
  
## <a name="failure-condition-level--values"></a>エラー条件レベルの値  
 次の表では、 **failure_condition_level**列に対して考えられるエラー状態のレベルについて説明します。  
  
|ReplTest1|エラー条件|  
|-----------|-----------------------|  
|@shouldalert|次のいずれかが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> <br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスがダウンしています。<br /><br /> -サーバーインスタンスから ACK を受信しないため、WSFC フェールオーバークラスターに接続するための可用性グループのリースが期限切れになります。 詳細については、「 [動作方法: SQL Server Always On のリース タイムアウト](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)」を参照してください。|  
|2|次のいずれかが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> <br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがクラスターに接続していません。また、可用性グループのユーザー指定の**health_check_timeout**しきい値を超えています。<br /><br /> -可用性レプリカがエラー状態になっています。|  
|3|孤立したスピンロック、重大な書き込みアクセス違反、ダンプが多すぎるなどの重大な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> これが既定値です。|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部リソース プールに永続的なメモリ不足の状態があるなど [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。|  
|5|以下のような任意の修飾エラー状態に対して自動フェールオーバーを開始する必要があることを指定します。<br /><br /> <br /><br /> -SQL エンジンのワーカースレッドの枯渇。<br /><br /> -解決不可能なデッドロックの検出。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 サーバー インスタンスに対する VIEW ANY DEFINITION 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
