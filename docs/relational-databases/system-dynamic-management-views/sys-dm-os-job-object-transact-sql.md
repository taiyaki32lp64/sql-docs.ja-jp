---
title: sys.dm_os_job_object (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 43063bb56607d1b5a21ae04b40ee4c7a17825521
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900135"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

ジョブのオブジェクト レベルで特定リソース消費量の統計と同様に、SQL Server プロセスを管理するジョブ オブジェクトの構成を記述する 1 つの行を返します。 SQL Server はジョブ オブジェクトで実行されていない場合は、空のセットを返します。 

ジョブ オブジェクトは、オペレーティング システム レベルでの CPU、メモリ、および IO リソース ガバナンスを実装する Windows コンストラクトです。 ジョブ オブジェクトの詳細については、次を参照してください。[ジョブ オブジェクト](/windows/desktop/ProcThread/job-objects)します。 
  
|[列]|データ型|説明|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|SQL Server スレッドは、各スケジュールの間隔中に使用できるプロセッサ サイクルの部分を指定します。 値は 10000 サイクルのスケジュール間隔内で利用可能なサイクルの割合として報告されます。 たとえば、スレッドが CPU コアを使用できる値 100 には、完全な容量が。|
|cpu_affinity_mask|**bigint**|論理プロセッサを記述するビット マスク、SQL Server プロセスは、プロセッサ グループ内で使用できます。 たとえば、cpu_affinity_mask 255 (1111 バイナリ) という最初の 8 つの論理プロセッサを使用することができます。|
|cpu_affinity_group|**int**|SQL Server で使用されるプロセッサ グループの数。|
|memory_limit_mb|**bigint**|最大 (mb) を SQL Server を含む、ジョブ オブジェクトのすべてのプロセスは累積的に使用できる、コミットされたメモリ量。| 
|process_memory_limit_mb |**bigint**|SQL Server など、ジョブ オブジェクトの 1 つのプロセスを mb 単位でのコミットされたメモリの最大量を使用できます。|
|workingset_limit_mb |**bigint**|最大 (mb)、SQL Server のワーキング セットが使用できるメモリ量。|
|non_sos_mem_gap_mb|**bigint**|MB 単位でのメモリの量は、スレッド スタック、Dll、およびその他の非 SOS のメモリ割り当ての確保。 SOS ターゲット メモリの違いは、`process_memory_limit_mb`と`non_sos_mem_gap_mb`します。| 
|low_mem_signal_threshold_mb|**bigint**|メモリしきい値 (MB 単位)。 ジョブ オブジェクトの使用可能なメモリの量がこのしきい値を下回ると、SQL Server プロセスにメモリ不足通知信号が送信されます。 |
|total_user_time|**bigint**|ジョブ オブジェクトが作成されたため、ジョブ オブジェクト内のスレッドがユーザー モードで費やさが 100 ns 刻みの合計数。 |
|total_kernel_time |**bigint**|ジョブ オブジェクトが作成されたため、ジョブ オブジェクト内のスレッドがカーネル モードで費やさが 100 ns 刻みの合計数。 |
|write_operation_count |**bigint**|合計数は、ジョブ オブジェクトが作成された後に、SQL Server によって発行されたローカル ディスク上の IO 操作を記述します。 |
|read_operation_count |**bigint**|ジョブ オブジェクトが作成された後に、SQL Server によって発行されたローカル ディスク上の読み取りの IO 操作の合計数。 |
|peak_process_memory_used_mb|**bigint**|ピーク (mb)、SQL Server など、ジョブ オブジェクトの 1 つのプロセスのメモリ量は、ジョブ オブジェクトが作成されたために使用されます。| 
|peak_job_memory_used_mb|**bigint**|ピーク時のジョブ オブジェクトのすべてのプロセスは、ジョブ オブジェクトから累積的使用いたを mb 単位でのメモリ量が作成されました。|
  
## <a name="permissions"></a>アクセス許可  
SQL Database マネージ インスタンスが必要です。`VIEW SERVER STATE`権限。 SQL Database では、データベースにおける `VIEW DATABASE STATE` アクセス許可が必要です。  
 
## <a name="see-also"></a>参照  

マネージ インスタンスについては、次を参照してください。 [SQL Database マネージ インスタンス](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)します。
  
