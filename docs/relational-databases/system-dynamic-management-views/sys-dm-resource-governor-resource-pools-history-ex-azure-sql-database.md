---
title: dm_resource_governor_resource_pools_history_ex (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: ae34c89fd570921bec26d8a11537c58b6bba2302
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247308"
---
# <a name="sysdm_resource_governor_resource_pools_history_ex-transact-sql"></a>dm_resource_governor_resource_pools_history_ex (Transact-sql)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Azure SQL Database のリソースプール統計の最後の32分 (合計 128) の20秒間隔でスナップショットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pool_id**|int|リソースプールの ID。 NULL 値は許可されません。
|**指定**|sysname|共有リソースの名前。 NULL 値は許可されません。|
|**snapshot_time**|datetime2|取得されたリソースプールの統計スナップショットの Datetime|
|**duration_ms**|int|現在のスナップショットと以前のスナップショットの間の期間|
|**statistics_start_time**|datetime2|このプールの統計がリセットされた時刻。 NULL 値は許可されません。|
|**active_session_count**|int|現在のスナップショット内のアクティブなセッションの合計数|
|**active_worker_count**|int|現在のスナップショット内の worker の合計数|
|**delta_cpu_usage_ms**|int|前回のスナップショットからの CPU 使用率 (ミリ秒)。 NULL 値は許可されません。|
|**delta_cpu_usage_preemptive_ms**|int|前回のスナップショット以降、SQL CPU RG によって制御されないプリエンプティブ win32 呼び出し|
|**used_data_space_kb**|bigint|ユーザープールに関連付けられているユーザーデータベースで使用されている領域の合計|
|**allocated_disk_space_kb**|bigint|ユーザープールに関連付けられている内のユーザーデータベースの合計データファイルサイズ|
|**target_memory_kb**|bigint|リソースプールが達成しようとしている目標メモリ量 (kb 単位)。 これは、現在の設定とサーバーの状態に基づいています。 NULL 値は許可されません。|
|**used_memory_kb**|bigint|リソースプールに使用されるメモリの量 (kb 単位)。 NULL 値は許可されません。|
|**cache_memory_kb**|bigint|現在の合計キャッシュ メモリ使用量 (KB 単位)。 NULL 値は許可されません。|
|**compile_memory_kb**|bigint|現在の合計メモリ流用量 (KB 単位)。 この量の大半はコンパイルと最適化に使用されますが、他のメモリ ユーザーに使用されている可能性もあります。 NULL 値は許可されません。|
|**active_memgrant_count**|bigint|メモリ許可の現在の数。 NULL 値は許可されません。|
|**active_memgrant_kb**|bigint|現在のメモリ許可の合計 (kb 単位)。 NULL 値は許可されません。|
|**used_memgrant_kb**|bigint|メモリ許可からの現在の (流用された) メモリの合計。 NULL 値は許可されません。|
|**delta_memgrant_timeout_count**|int|この期間のこのリソースプールにおけるメモリ許可のタイムアウトの数。 NULL 値は許可されません。|
|**delta_memgrant_waiter_count**|int|メモリ許可で現在保留中のクエリの数。 NULL 値は許可されません。|
|**delta_out_of_memory_count**|int|前回のスナップショット以降にプールで失敗したメモリ割り当ての数。 NULL 値は許可されません。|
|**delta_read_io_queued**|int|前回のスナップショット以降にエンキューされた読み取り Io の合計。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**delta_read_io_issued**|int|前回のスナップショット以降に発行された読み取り Io の合計。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**delta_read_io_completed**|int|前回のスナップショット以降に完了した読み取り Io の合計。 NULL 値は許可されません。|
|**delta_read_io_throttled**|int|スナップショット以降に調整された読み取り Io の合計。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**delta_read_bytes**|bigint|前回のスナップショット以降に読み取られたバイト数の合計です。 NULL 値は許可されません。|
|**delta_read_io_stall_ms**|int|前回のスナップショット以降の読み取り IO の到着から完了までの合計時間 (ミリ秒)。 NULL 値は許可されません。|
|**delta_read_io_stall_queued_ms**|int|読み取り IO の到着から最後のスナップショット以降の問題までの合計時間 (ミリ秒単位)。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。 0以外の delta_read_io_stall_queued_ms は、RG によって IO が影響を受けていることを意味します。|
|**delta_write_io_queued**|int|前回のスナップショット以降にエンキューされた書き込み Io の合計。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**delta_write_io_issued**|int|前回のスナップショット以降に発行された書き込み Io の合計。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**delta_write_io_completed**|int|前回のスナップショット以降に完了した書き込み Io の合計。 Null 値はありません|
|**delta_write_io_throttled**|int|前回のスナップショット以降に調整された書き込み Io の合計。 Null 値はありません|
|**delta_write_bytes**|bigint|前回のスナップショット以降に書き込まれたバイト数の合計です。 NULL 値は許可されません。|
|**delta_write_io_stall_ms**|int|前回のスナップショット以降の書き込み IO の到着から完了までの合計時間 (ミリ秒)。 NULL 値は許可されません。|
|**delta_write_io_stall_queued_ms**|int|書き込み IO の到着から最後のスナップショット以降の問題までの合計時間 (ミリ秒単位)。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**delta_io_issue_delay_ms**|int|スケジュールされた問題と最後のスナップショット以降の IO の実際の問題の間の合計時間 (ミリ秒単位)。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**max_iops_per_volume**|int|このプールのディスクボリューム設定ごとの1秒あたりの最大 IO 数 (IOPS)。 NULL 値が許可されます。 リソースプールに IO が適用されていない場合は Null です。|
|**max_memory_kb**|bigint|リソースプールが持つことができるメモリの最大量 (kb 単位)。 これは、現在の設定とサーバーの状態に基づいています。 NULL 値は許可されません。
|**max_log_rate_kb**|bigint|リソースプールレベルでの最大ログレート (1 秒あたりのキロバイト数)。|
|**max_data_space_kb**|bigint|このエラスティックプールのエラスティックプールの最大ストレージ制限の設定 (kb 単位)。|
|**max_session**|int|プールのセッション制限|
|**max_worker**|int|プールのワーカー制限|
|**min_cpu_percent**|int|CPU の競合がある場合に、リソースプール内のすべての要求に対して保証される平均 CPU 帯域幅の現在の構成。 NULL 値は許可されません。|
|**max_cpu_percent**|int|CPU の競合がある場合に、リソースプールのすべての要求で許容される最大平均 CPU 帯域幅の現在の構成。 NULL 値は許可されません。|
|**cap_cpu_percent**|int|リソースプール内のすべての要求が受信する CPU 帯域幅のハードキャップ。 CPU 帯域幅の最大レベルを指定されたレベルに制限します。 value の許容範囲は 1 ～ 100 です。 NULL 値は許可されません。|
|**min_vcores**|decimal (5, 2)|CPU の競合がある場合に、リソースプール内のすべての要求に対して保証される平均 CPU 帯域幅の現在の構成。  仮想コアの単位で|
|**max_vcores**|decimal (5, 2)|CPU の競合がある場合に、リソースプールのすべての要求で許容される最大平均 CPU 帯域幅の現在の構成。  仮想コアの単位|
|**cap_vcores**|decimal (5, 2)|リソースプール内のすべての要求が受信する CPU 帯域幅のハードキャップ。  仮想コアのユニット単位|
|**instance_cpu_count**|int|インスタンスに対して構成されている CPU の数|
|**instance_cpu_percent**|decimal (5, 2)|インスタンスに対して構成されている CPU の割合|
|**instance_vcores**|decimal (5, 2)|インスタンスに対して構成された仮想コアの数|
|**delta_log_bytes_used**|decimal (5, 2)|前回のスナップショット以降のプールレベルでのログ生成総数 (バイト単位)|
|**avg_login_rate_percent**|decimal (5, 2)|前回のスナップショット以降のログインの数 (ログインの制限と比較)|
|**delta_vcores_used**|decimal (5, 2)|前回のスナップショット以降の仮想コア数でのコンピューティング使用率。|
|**cap_vcores_used_percent**|decimal (5, 2)|プールの限度に対する割合で表した平均コンピューティング使用率。|
|**instance_vcores_used_percent**|decimal (5, 2)|SQL インスタンスの制限に対する割合での平均コンピューティング使用率。|
|**avg_data_io_percent**|decimal (5, 2)|プールの限度に対する割合で表した平均 I/O 使用率。|
|**avg_log_write_percent**|decimal (5, 2)|プールの限度に対する割合で表した平均書き込みリソース使用率。|
|**avg_storage_percent**|decimal (5, 2)|プールのストレージ限度に対する割合で表した平均ストレージ使用率。|
|**avg_allocated_storage_percent**|decimal (5, 2)|エラスティックプール内のすべてのデータベースによって割り当てられたデータ領域の割合。 これは、エラスティックプールのデータの最大サイズに割り当てられたデータ領域の比率です。 詳細については、「SQL DB でのファイル領域の管理」を参照してください。|
|**max_worker_percent**|decimal (5, 2)|プールの限度に対する割合で表した最大同時実行ワーカー (要求) 数。|
|**max_session_percent**|decimal (5, 2)|プールの限度に対する割合で表した最大同時実行セッション数。|
|||

## <a name="permissions"></a>アクセス許可

このビューには VIEW SERVER STATE 権限が必要です。

## <a name="remarks"></a>コメント

ユーザーは、この動的管理ビューにアクセスして、ユーザーワークロードプールと Azure SQL Database インスタンスのシステム内部プールについて、ほぼリアルタイムのリソース消費を監視できます。

> [!IMPORTANT]
> この DMV によって提示されるデータのほとんどは、内部使用を目的としており、変更される可能性があります。

## <a name="examples"></a>例

次の例では、ユーザープールごとに各スナップショットの最大ログレートデータと消費量を返します。  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

次の例では、論理マスターに接続しなくても、elastic_pool_resource_stats と同様の情報が返されます。

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>参照

- [翻訳ログレートガバナンス](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [エラスティックプールの DTU リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [エラスティックプールの仮想コアリソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
