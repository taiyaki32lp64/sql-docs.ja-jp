---
title: _resource_governor_workload_groups_history_ex (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
ms.openlocfilehash: 5fea5badf14ce9863f07dff189f1665788ec5fb6
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873774"
---
# <a name="sysdm_resource_governor_workload_groups_history_ex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Azure SQL Database のリソースプール統計の最後の32分 (合計 128) の20秒間隔でスナップショットを返します。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pool_id**| int |リソースプールの ID。 NULL 値は許可されません。|
|**group_id**| int |ワークロードグループの ID。 NULL 値は許可されません。|
|**name**| nvarchar (256) |ワークロード グループの名前。 NULL 値は許可されません。|
|**snapshot_time**| DATETIME |取得したリソースグループの統計スナップショットの Datetime。|
|**duration_ms**| int |現在のスナップショットから以前のスナップショットまでの期間。|
|**active_worker_count**| int |現在のスナップショット内の worker の合計数。|
|**active_request_count**| int |現在の要求数。 NULL 値は許可されません。|
|**active_session_count**| int |現在のスナップショット内のアクティブなセッションの合計数。|
|**total_request_count**| BIGINT |ワークロードグループ内の完了した要求の累積数。 NULL 値は許可されません。|
|**delta_request_count**| int |前回のスナップショット以降のワークロードグループ内の完了した要求の数。 NULL 値は許可されません。|
|**total_cpu_usage_ms**| BIGINT |このワークロードグループによる累積 CPU 使用率 (ミリ秒単位)。 NULL 値は許可されません。|
|**delta_cpu_usage_ms**| int |前回のスナップショットからの CPU 使用率 (ミリ秒)。 NULL 値は許可されません。|
|**delta_cpu_usage_preemptive_ms**| int |前回のスナップショット以降、プリエンプティブ win32 呼び出しは SQL CPU RG によって制御されません。|
|**delta_reads_reduced_memgrant_count**| int |最後のスナップショット以降のクエリサイズの上限に達したメモリ許可の数。 NULL 値は許可されません。|
|**reads_throttled**| int |スロットルされた読み取りの合計数。|
|**delta_reads_queued**| int |前回のスナップショット以降にエンキューされた読み取り Io の合計。 NULL 値が許可されます。 リソースグループに IO が適用されていない場合は Null です。|
|**delta_reads_issued**| int |前回のスナップショット以降に発行された読み取り Io の合計。 NULL 値が許可されます。 リソースグループに IO が適用されていない場合は Null です。|
|**delta_reads_completed**| int |前回のスナップショット以降に完了した読み取り Io の合計。 NULL 値は許可されません。|
|**delta_read_bytes**| BIGINT |前回のスナップショット以降に読み取られたバイト数の合計です。 NULL 値は許可されません。|
|**delta_read_stall_ms**| int |前回のスナップショット以降の読み取り IO の到着から完了までの合計時間 (ミリ秒)。 NULL 値は許可されません。|
|**delta_read_stall_queued_ms**| int |読み取り IO の到着から最後のスナップショット以降の問題までの合計時間 (ミリ秒単位)。 NULL 値が許可されます。 リソースグループに IO が適用されていない場合は Null です。 0以外の delta_read_stall_queued_ms は、RG によって IO が影響を受けていることを意味します。|
|**delta_writes_queued**| int |前回のスナップショット以降にエンキューされた書き込み Io の合計。 NULL 値が許可されます。 リソースグループに IO が適用されていない場合は Null です。|
|**delta_writes_issued**| int |前回のスナップショット以降に発行された書き込み Io の合計。 NULL 値が許可されます。 リソースグループに IO が適用されていない場合は Null です。|
|**delta_writes_completed**| int |前回のスナップショット以降に完了した書き込み Io の合計。 NULL 値は許可されません。|
|**delta_writes_bytes**| BIGINT |前回のスナップショット以降に書き込まれたバイト数の合計です。 NULL 値は許可されません。|
|**delta_write_stall_ms**| int |前回のスナップショット以降の書き込み IO の到着から完了までの合計時間 (ミリ秒)。 NULL 値は許可されません。|
|**delta_background_writes**| int |前回のスナップショット以降にバックグラウンドタスクによって実行された書き込みの合計数。|
|**delta_background_write_bytes**| BIGINT |前回のスナップショット以降にバックグラウンドタスクで実行された書き込みサイズの合計 (バイト単位)。|
|**delta_log_bytes_used**| BIGINT |最後のスナップショット以降に使用されたログ (バイト単位)。|
|**delta_log_temp_db_bytes_used**| BIGINT |最後のスナップショットから使用された Tempdb ログ (バイト単位)。|
|**delta_query_optimizations**| BIGINT |前回のスナップショット以降にこのワークロードグループで行われたクエリの最適化の数。 NULL 値は許可されません。|
|**delta_suboptimal_plan_generations**| BIGINT |前回のスナップショット以降のメモリ不足が原因で、このワークロードグループで発生した最適ではないプランの生成の数。 NULL 値は許可されません。
|**max_memory_grant_kb**| BIGINT |グループの最大メモリ許可 (KB 単位)。|
|**max_request_cpu_msec**| BIGINT |1つの要求に対する最大 CPU 使用率 (ミリ秒単位)。 NULL 値は許可されません。|
|**max_concurrent_request**| int |同時要求の最大数の現在の設定です。 NULL 値は許可されません。|
|**max_io**| int |グループの最大 IO 制限。|
|**max_global_io**| int |単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。
|**max_queued_io**| int |単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。|
|**max_log_rate_kb**| BIGINT |リソースグループレベルでの最大ログレート (1 秒あたりのキロバイト数)。|
|**max_session**| int |グループのセッション制限。|
|**max_worker**| int |グループの Worker 制限。|
|||

## <a name="permissions"></a>アクセス許可

このビューには VIEW SERVER STATE 権限が必要です。

## <a name="remarks"></a>コメント

ユーザーは、この動的管理ビューにアクセスして、ユーザーワークロードプールと Azure SQL Database インスタンスのシステム内部プールについて、ほぼリアルタイムのリソース消費を監視できます。

> [!IMPORTANT]
> この DMV によって提示されるデータのほとんどは、内部使用を目的としており、変更される可能性があります。

## <a name="examples"></a>使用例

次の例では、ユーザープールによって各スナップショットの最大ログレートデータと消費量を返します。

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>関連項目

- [翻訳ログレートガバナンス](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [エラスティックプールの DTU リソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [エラスティックプールの仮想コアリソースの制限](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
