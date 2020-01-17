---
title: 自動シード処理を使用して、可用性グループを初期化する
description: 自動シード処理を使用して、手動でバックアップおよび復元を行うことなく、Always On 可用性グループ内のすべてのデータベースに対してセカンダリ レプリカを自動的に作成します。
ms.custom: seo-lt-2019
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 67c6a601-677a-402b-b3d1-8c65494e9e96
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 38bbab7ea9ae6aa7ddd70ede2161988c01431573
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254088"
---
# <a name="use-automatic-seeding-to-initialize-an-always-on-availability-group"></a>自動シード処理を使用して、Always On 可用性グループを初期化する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2016 には、可用性グループの自動シード処理が導入されています。 自動シード処理によって可用性グループを作成すると、グループの各データベースのセカンダリ レプリカが SQL Server で自動的に作成されます。 セカンダリ レプリカのバックアップと復元を手動で行う必要がありません。 自動シード処理を有効にするには、T-SQL を使用して可用性グループを作成するか、最新バージョンの SQL Server Management Studio を使用します。

背景情報については、「[セカンダリ レプリカの自動シード処理](automatic-seeding-secondary-replicas.md)」を参照してください。
 
## <a name="prerequisites"></a>前提条件

SQL Server 2016 の自動シード処理では、データとログ ファイルのパスが、可用性グループに参加しているすべての SQL Server インスタンスで同じである必要があります。 SQL Server 2017 では、異なるパスを使用できますが、すべてのレプリカを同じプラットフォーム (Windows または Linux など) でホストする場合、同じパスを使用することが推奨されます。 クロスプラットフォームの可用性グループのレプリカは、パスが異なります。 詳細については、「[ディスク レイアウト](automatic-seeding-secondary-replicas.md#disklayout)」を参照してください。

可用性グループのシード処理は、データベース ミラーリング エンドポイント経由で通信します。 各サーバー上のミラーリング エンドポイント ポートへの受信ファイアウォール規則を開きます。

可用性グループのデータベースは、完全復旧モデルにする必要があります。 データベースには、最新の完全バックアップとトランザクション ログのバックアップが必要です。 これらのバックアップ ファイルは、自動シード処理には使用されませんが、データベースを可用性グループに追加する前に必要になります。 
 
## <a name="create-availability-group-with-automatic-seeding"></a>自動シード処理によって可用性グループを作成する

自動シード処理によって可用性グループを作成するには、 `SEEDING_MODE=AUTOMATIC`を設定します。 

次の例では、2 つのノードがある Windows Server フェールオーバー クラスターに可用性グループを作成します。 スクリプトを実行する前に、環境に合わせて値を更新します。

1. エンドポイントを作成します。 各サーバーにエンドポイントが必要です。 次のスクリプトでは、リスナー用に TCP ポート 5022 を使用するエンドポイントを作成します。 環境に合わせて `<endpoint_name>` と `LISTENER_PORT` を設定し、両方のサーバーでスクリプトを実行します。

    ```sql
    CREATE ENDPOINT [<endpoint_name>] 
        STATE=STARTED
        AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
        FOR DATA_MIRRORING (
            ROLE = ALL, 
            AUTHENTICATION = WINDOWS NEGOTIATE, 
            ENCRYPTION = REQUIRED ALGORITHM AES
            )
    GO
    ```

1. 可用性グループを作成します。 次のスクリプトで可用性グループを作成します。 山かっこ `<>` 内のグループ名、サーバー名、およびドメイン名の値を更新し、SQL Server のプライマリ インスタンスで実行します。  

    ```sql
    CREATE AVAILABILITY GROUP [<availability_group_name>]
        FOR DATABASE db1
        REPLICA ON'<*primary_server*>'
        WITH (ENDPOINT_URL = N'TCP://<primary_server>.<fully_qualified_domain_name>:5022', 
            FAILOVER_MODE = AUTOMATIC, 
            AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
            BACKUP_PRIORITY = 50, 
            SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
            SEEDING_MODE = AUTOMATIC),
        N'<secondary_server>' WITH (ENDPOINT_URL = N'TCP://<secondary_server>.<fully_qualified_domain_name>:5022', 
            FAILOVER_MODE = AUTOMATIC, 
            AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
            BACKUP_PRIORITY = 50, 
            SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
            SEEDING_MODE = AUTOMATIC);
    GO
    ``` 

1. セカンダリ サーバー インスタンスを可用性グループに参加させ、可用性グループにデータベース作成アクセス許可を付与します。 次のスクリプトを更新し、山かっこ `<>` 内の値を環境に合わせて変更し、SQL Server のセカンダリ レプリカ インスタンスで実行します。 
 
    ```sql
    ALTER AVAILABILITY GROUP [<availability_group_name>] JOIN
    GO  
    ALTER AVAILABILITY GROUP [<availability_group_name>] GRANT CREATE ANY DATABASE
    GO
    ```

SQL Server はセカンダリ サーバー上にデータベースのレプリカを自動的に作成します。 データベースが大きい場合は、データベースの同期を完了するまで時間がかかることがあります。 自動シード処理の対象として構成されている可用性グループにデータベースがある場合は、 `sys.dm_hadr_automatic_seeding` システム ビューにクエリを実行してシード処理の進行状況を監視できます。 次のクエリは、自動シード処理の対象として構成されている可用性グループ内にあるデータベースごとに 1 つの行を返します。

```sql 
SELECT start_time,
    ag.name,
    db.database_name,
    current_state,
    performed_seeding,
    failure_state,
    failure_state_desc
FROM sys.dm_hadr_automatic_seeding autos 
    JOIN sys.availability_databases_cluster db 
        ON autos.ag_db_id = db.group_database_id
    JOIN sys.availability_groups ag 
        ON autos.ag_id = ag.group_id
```

## <a name="prevent-automatic-seeding-after-an-availability-group"></a>可用性グループの後の自動シード処理を防ぐ

一時的にプライマリ レプリカからセカンダリ レプリカにデータベースのシード処理が行われないようにするために、可用性グループのデータベース作成アクセス許可を拒否することができます。 可用性グループのレプリカ データベース作成権限を拒否するには、セカンダリ レプリカをホストしているインスタンスで次のクエリを実行します。

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    DENY CREATE ANY DATABASE
GO
```


## <a name="enable-automatic-seeding-on-an-existing-availability-group"></a>既存の可用性グループで自動シード処理を有効にする

既存のデータベースに対して自動シード処理を設定できます。 次のコマンドは、自動シード処理を使用するように可用性グループを変更します。 プライマリ レプリカで次のコマンドを実行します。

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<secondary_node>' 
    WITH (SEEDING_MODE = AUTOMATIC)
GO
```

上記のコマンドを実行すると、必要な場合にデータベースでシード処理が強制的に再開されます。 たとえば、セカンダリ レプリカでディスクの空き領域不足のためにシード処理が失敗した場合、空き領域を増やした後、`ALTER AVAILABILITY GROUP ... WITH (SEEDING_MODE=AUTOMATIC)` を実行してシード処理を再開します。

## <a name="stop-automatic-seeding"></a>自動シード処理を停止する

可用性グループの自動シード処理を停止するには、プライマリ レプリカで、次のスクリプトを実行します。

```sql
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<secondary_node>'   
    WITH (SEEDING_MODE = MANUAL)
GO
```

上記のスクリプトでは、現在シード処理中のレプリカがキャンセルされ、この可用性グループ内のレプリカが SQL Server によって自動的に初期化されることはありません。 既に初期化されているレプリカの同期は停止しません。 


## <a name="monitor-automatic-seeding-availability-group"></a>可用性グループの自動シード処理を監視する

### <a name="use-system-dynamic-management-views-to-monitor-seeding"></a>システム動的管理ビューを使用してシード処理を監視する

次のシステム ビューは、SQL Server の自動シード処理の状態を示します。

**sys.dm_hadr_automatic_seeding** 

プライマリ レプリカでクエリ `sys.dm_hadr_automatic_seeding` を実行して、自動シード処理プロセスの状態を確認します。 このビューは、シード処理プロセスごとに 1 つの行を返します。 次に例を示します。

```sql
SELECT start_time, 
    completion_time
    is_source,
    current_state,
    failure_state,
    failure_state_desc
FROM sys.dm_hadr_automatic_seeding
```
 
**sys.dm_hadr_physical_seeding_stats** 

プライマリ レプリカで、 `sys.dm_hadr_physical_seeding_stats` DMV のクエリを実行して、現在実行中の各シード処理プロセスの物理統計情報を表示します。 次のクエリは、シード処理が実行されているときの行数を返します。

```sql
SELECT * FROM sys.dm_hadr_physical_seeding_stats;
```

*total_disk_io_wait_time_ms* と *total_network_wait_time_ms* の 2 つの列は、自動シード処理プロセスにおけるパフォーマンスのボトルネックを特定するのに使用できます。 この 2 つの列は、*hadr_physical_seeding_progress* 拡張イベントにもあります。

**total_disk_io_wait_time_ms** は、ディスクで待機中にバックアップ/復元スレッドで費やされた時間を表します。 この値は、シード処理操作が開始されてからの累積です。 ディスクがバックアップ ストリームの読み取りまたは書き込みに対して準備ができていない場合、バックアップ/復元スレッドはスリープ状態に移行し、1 秒ごとにウェイク アップしてディスクの準備ができたかどうかをチェックします。
        
**total_network_wait_time_ms** は、プライマリ レプリカとセカンダリ レプリカで解釈のされ方が異なります。 プライマリ レプリカでは、このカウンターはネットワーク フローの制御時間を表します。 セカンダリ レプリカでは、これはメッセージがディスクに書き込めるようになるまで復元スレッドが待機する時間を表します。

### <a name="diagnose-database-initialization-using-automatic-seeding-in-the-error-log"></a>エラー ログ内の自動シード処理を使用してデータベースの初期化を診断する

自動シード処理の対象として構成されている可用性グループにデータベースを追加すると、SQL Server は可用性グループのエンドポイントを介して、VDI のバックアップを行います。 バックアップがいつ完了したか、およびセカンダリがいつ同期されたかについては、SQL Server エラー ログを確認してください。

### <a name="diagnose-database-level-health-with-extended-events"></a>拡張イベントを使用してデータベース レベルの正常性を診断する

自動シード処理には、初期化中の状態変更、エラー、およびパフォーマンス統計情報を追跡するための新しい拡張イベントが用意されています。 

たとえば、このスクリプトは、自動シード処理に関連したイベントをキャプチャする拡張イベント セッションを作成します。 

```sql
CREATE EVENT SESSION [AlwaysOn_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(
        SET filename=N'autoseed.xel',
            max_file_size=(5),
            max_rollover_files=(4)
        )
WITH (
    MAX_MEMORY=4096 KB,
    EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
    MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,
    MEMORY_PARTITION_MODE=NONE,
    TRACK_CAUSALITY=OFF,
    STARTUP_STATE=ON
    )
GO 

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO 
```


次の表に、自動シード処理に関連する拡張イベントを示します。 

| Name | [説明]|
|------------ |---------------| 
|hadr_db_manager_seeding_request_msg |  シード処理要求メッセージ。
|hadr_physical_seeding_backup_state_change |    物理シード処理のバックアップ側の状態変更。
|hadr_physical_seeding_restore_state_change |物理シード処理の復元側の状態変更。
|hadr_physical_seeding_forwarder_state_change | 物理シード処理のフォワーダー側の状態変更。
|hadr_physical_seeding_forwarder_target_state_change |  物理シード処理のフォワーダー ターゲット側の状態変更。
|hadr_physical_seeding_submit_callback  |物理シード処理のコールバック送信イベント。
|hadr_physical_seeding_failure  |物理シード処理のエラー イベント。
|hadr_physical_seeding_progress |   物理シード処理の進行状況イベント。
|hadr_physical_seeding_schedule_long_task_failure   |物理シード処理スケジュール長期タスク障害イベント。
|hadr_automatic_seeding_start   |自動シード処理操作が提出されるときに発生します。
|hadr_automatic_seeding_state_transition    |自動シード処理操作が状態を変更するときに発生します。
|hadr_automatic_seeding_success |自動シード処理操作が成功するときに発生します。
|hadr_automatic_seeding_failure |自動シード処理操作が失敗するときに発生します。
|hadr_automatic_seeding_timeout |自動シード処理操作がタイムアウトになるときに発生します。

### <a name="other-troubleshooting-considerations"></a>その他のトラブルシューティングに関する考慮事項

**自動シード処理時の監視**

`sys.dm_hadr_physical_seeding_stats` のクエリを実行して、現在実行中の自動シード処理プロセスを問い合わせます。 このビューは、データベースごとに 1 つの行を返します。 次に例を示します。

```sql
SELECT local_database_name, 
    role_desc, 
    internal_state_desc, 
    transfer_rate_bytes_per_second, 
    transferred_size_bytes, 
    database_size_bytes, 
    start_time_utc, 
    end_time_utc, estimate_time_complete_utc, 
    total_disk_io_wait_time_ms, 
    total_network_wait_time_ms, 
    is_compression_enabled 
FROM sys.dm_hadr_physical_seeding_stats
```

**自動シード処理の対象として構成されている可用性グループにデータベースが表示されない理由についてトラブルシューティングを行う**


自動シード処理が有効になっているデータベースが可用性グループの一部として表示されない場合、自動シード処理が失敗した可能性があります。 そのため、プライマリまたはセカンダリ レプリカで可用性グループにデータベースを追加できません。 プライマリ レプリカとセカンダリ レプリカの両方で `sys.dm_hadr_automatic_seeding` のクエリを実行します。 たとえば、自動シード処理のエラーの状態を確認するには、次のクエリを実行します。

```sql
SELECT start_time, 
    completion_time, 
    is_source, 
    current_state, 
    failure_state, 
    failure_state_desc, 
    error_code 
FROM sys.dm_hadr_automatic_seeding
```

## <a name="automatic-seeding-and-performance-considerations"></a>自動シード処理およびパフォーマンスに関する考慮事項

SQL Server が自動シード処理に使用するスレッドの数は固定されています。 プライマリ インスタンスでは、SQL Server は LUN ごとに 1 つのスレッドを使用して変更を読み取ります。 セカンダリ インスタンスでは、SQL Server は LUN ごとに 1 つのスレッドを使用してデータベースを初期化します。

プライマリ レプリカに対して自動シード処理時のデータ ストリームの圧縮を有効にするには、トレース フラグ 9567 を設定します。 これにより自動シード処理の転送時間が大幅に減少する一方、CPU 使用率が大きくなります。 詳細については、「 [Tune compression for availability group](../../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)」(可用性グループの圧縮を調整する) を参照してください。 


## <a name="when-not-to-use-automatic-seeding"></a>自動シード処理を使用すべきでない場合

セカンダリ レプリカを初期化するときに、自動シードが最適な処理ではない場合もあります。 自動シード処理時、SQL Server は初期化の前にネットワーク経由でバックアップを実行します。 データベースが大規模な場合やセカンダリ レプリカがリモートの場合は、この処理に時間がかかることがあります。 そのようなデータベースのトランザクション ログをバックアップ処理中に切り捨てることはできないため、ビジー状態のデータベースでは、長時間にわたる初期化プロセスによってトランザクション ログの容量が大幅に増加します。
自動シード処理によってデータベースを可用性グループに追加する前に、データベースのサイズ、負荷、およびレプリカ間のサイトの距離を評価してください。

## <a name="resources"></a>リソース

[CREATE AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)

[AlwaysOn 可用性グループのトラブルシューティングと監視のガイド](https://technet.microsoft.com/library/dn135328.aspx)

