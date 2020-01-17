---
title: dm_os_schedulers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_schedulers
- sys.dm_os_schedulers_TSQL
- sys.dm_os_schedulers
- dm_os_schedulers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_schedulers dynamic management view
ms.assetid: 3a09d81b-55d5-416f-9cda-1a3a5492abe0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e2597289894f3a037e9ad8ada499b5f2d259ff3f
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289393"
---
# <a name="sysdm_os_schedulers-transact-sql"></a>sys.dm_os_schedulers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスケジューラごとに 1 行のデータを返します。各スケジューラは個別のプロセッサにマップされています。 このビューは、スケジューラの状況の監視やランナウェイ タスクの特定に使用できます。 スケジューラの詳細については、「[スレッドおよびタスクアーキテクチャガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_schedulers**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|scheduler_address|**varbinary(8)**|スケジューラのメモリ アドレス。 NULL 値は許可されません。|  
|parent_node_id|**int**|スケジューラが属するノード (親ノード) の ID。 これは非均質メモリ アクセス (NUMA) ノードを表します。 NULL 値は許可されません。|  
|scheduler_id|**int**|スケジューラの ID。 定期的なクエリの実行に使用されるスケジューラにはすべて、1048576 未満の ID 番号が付いています。 Id が1048576以上のスケジューラは、専用管理者接続スケジューラなどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって内部的に使用されます。 NULL 値は許可されません。|  
|cpu_id|**smallint**|スケジューラに割り当てられた CPU ID。<br /><br /> NULL 値は許可されません。<br /><br /> **注:** 255 は、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]の場合とは関係がないことを示していません。 追加のアフィニティ情報については[、 &#40;&#41; 「sys. dm_os_threads transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md) 」を参照してください。|  
|ステータス|**nvarchar(60)**|スケジューラの状態。 次の値のいずれかです。<br /><br /> -非表示 (オンライン)<br />-非表示 (オフライン)<br />-オンラインで表示<br />-オフラインで表示<br />-オンラインで表示 (DAC)<br />-   HOT_ADDED<br /><br /> NULL 値は許可されません。<br /><br /> 非表示のスケジューラは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]内部の要求を処理するために使用されます。 VISIBLE スケジューラは、ユーザーの要求の処理に使用されます。<br /><br /> OFFLINE スケジューラは、関係マスクでオフラインになっているプロセッサにマップされます。そのため、要求の処理には使用されません。 ONLINE スケジューラは、関係マスクでオンラインになっているプロセッサにマップされ、スレッドの処理に使用されます。<br /><br /> DAC は、スケジューラが専用管理者接続で動作していることを示します。<br /><br /> HOT ADDED は、スケジューラがホット アド CPU イベントに応答して追加されたことを示します。|  
|is_online|**bit**|サーバーで使用可能なプロセッサの一部だけを使用するように構成されて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] いる場合、この構成では、一部のスケジューラが関係マスクに含まれていないプロセッサにマップされることを意味します。 これに該当する場合、この列には 0 が返されます。 この値は、スケジューラがクエリまたはバッチの処理に使用されていないことを意味します。<br /><br /> NULL 値は許可されません。|  
|is_idle|**bit**|1 = スケジューラはアイドル状態です。 現在実行中のワーカーはありません。 NULL 値は許可されません。|  
|preemptive_switches_count|**int**|スケジューラのワーカーがプリエンプティブ モードに切り替えられた回数。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部のコード (拡張ストアド プロシージャや分散クエリなど) を実行するには、スレッドを非プリエンプティブ スケジューラの制御外で実行する必要があります。 このとき、ワーカーはプリエンプティブ モードに切り替えられます。|  
|context_switches_count|**int**|スケジューラでコンテキストが切り替えられた回数。 NULL 値は許可されません。<br /><br /> 他のワーカーの実行を許可するには、現在実行しているワーカーでスケジューラの制御を解放するか、コンテキストを切り替える必要があります。<br /><br /> **注:** ワーカーがスケジューラを生成し、それ自体を実行可能キューに配置した後、他のワーカーを検索しない場合、ワーカーは自身を選択します。 この場合、context_switches_count は更新されませんが、yield_count は更新されます。|  
|idle_switches_count|**int**|スケジューラがアイドル中にイベントを待機した回数。 この列は context_switches_count と類似しています。 NULL 値は許可されません。|  
|current_tasks_count|**int**|このスケジューラに関連付けられている現在のタスクの数。 これには次のタスクが含まれます。<br /><br /> -ワーカーが実行するのを待機しているタスク。<br />-現在待機中または実行中のタスク (中断状態または実行可能状態)。<br /><br /> タスクが完了すると、このカウントは 1 減ります。 NULL 値は許可されません。|  
|runnable_tasks_count|**int**|実行可能キューにあるスケジュール待ちのワーカーで、タスクが割り当てられているワーカーの数。 NULL 値は許可されません。|  
|current_workers_count|**int**|このスケジューラに関連付けられているワーカーの数。 これにはタスクが割り当てられていないワーカーも含まれます。 NULL 値は許可されません。|  
|active_workers_count|**int**|アクティブなワーカーの数。 アクティブなワーカーがプリエンプティブになることはなく、必ずタスクが関連付けられています。また、実行中、実行可能、または中断状態のいずれかになっています。 NULL 値は許可されません。|  
|work_queue_count|**bigint**|保留キュー内のタスクの数。 保留キュー内のタスクは、ワーカーによる取得を待機しています。 NULL 値は許可されません。|  
|pending_disk_io_count|**int**|完了を待機している保留中の I/O の数。 各スケジューラには保留中の I/O の一覧が保持されており、コンテキストが切り替えられるたび、これらの I/O が完了したかどうかを確認するために、この一覧がチェックされます。 要求が挿入されると、カウントは 1 増えます。 要求が完了すると、カウントは 1 減ります。 この数は、I/O の状態を示すわけではありません。 NULL 値は許可されません。|  
|load_factor|**int**|スケジューラで認識されている負荷を示す内部値。 この値は、新しいタスクをこのスケジューラに指定するか、または他のスケジューラに指定するかを決定するために使用されます。 また、スケジューラの負荷が均等でないと思われる場合のデバッグに利用できます。 ルーティングはスケジューラの負荷に基づいて決定されます。 また [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ノードとスケジューラの占有率を使用して、リソースを取得するための最適な場所を決定します。 タスクがエンキューされると、占有率は増加します。 タスクが完了すると、占有率は減少します。 占有率を利用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OS で負荷を効率よく分散できます。 NULL 値は許可されません。|  
|yield_count|**int**|スケジューラの進行状況を示すために使用される内部値。 この値は、スケジューラ モニターで、このスケジューラのワーカーが予定どおりに他のワーカーに変更されるかどうかを確認するために使用されます。 ワーカーまたはタスクが新しいワーカーに移行するわけではありません。 NULL 値は許可されません。|  
|last_timer_activity|**bigint**|前回、スケジューラのタイマー キューがスケジューラにより確認された時間 (CPU ティック単位)。 NULL 値は許可されません。|  
|failed_to_create_worker|**bit**|スケジューラで新しいワーカーを作成できなかった場合は 1 になります。 これは通常、メモリ制約が原因で発生します。 NULL 値が許可されます。|  
|active_worker_address|**varbinary(8)**|現在アクティブなワーカーのメモリ アドレス。 NULL 値が許可されます。 詳細については、「 [sys &#40;. dm_os_workers transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)」を参照してください。|  
|memory_object_address|**varbinary(8)**|スケジューラのメモリ オブジェクトのメモリ アドレス。 NULL 値は許容されません。|  
|task_memory_object_address|**varbinary(8)**|タスクのメモリ オブジェクトのメモリ アドレス。 NULL 値は許可されません。 詳細については、「 [sys &#40;. dm_os_memory_objects transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)」を参照してください。|  
|quantum_length_us|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]SQLOS によって使用されるスケジューラ クォンタムを公開します。|  
| total_cpu_usage_ms |**bigint**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降 <br><br> 非プリエンプティブワーカーによって報告された、このスケジューラによって消費された合計 CPU。 NULL 値は許可されません。|
|total_cpu_idle_capped_ms|**bigint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] は、[サービスレベル目標](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu#service-level-objective)に基づく調整を示します。は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の非 Azure バージョンでは常に0になります。 NULL 値が許可されます。|
|total_scheduler_delay_ms|**bigint**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降 <br><br> 1つのワーカーが切り替えを行ってから、もう1つの切り替えが切り替わるまでの時間。 プリエンプティブなワーカーが次の非プリエンプティブワーカーのスケジュール設定を遅らせた場合、または他のプロセスからの OS スケジューリングスレッドによって発生する場合があります。 NULL 値は許可されません。|
|ideal_workers_limit|**int**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降 <br><br> スケジューラに最適なワーカーの数。 現在のワーカーが負荷分散されたタスクの負荷によって制限を超過した場合、アイドル状態になると、そのワーカーは切り捨てられます。 NULL 値は許可されません。|
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="examples"></a>使用例  
  
### <a name="a-monitoring-hidden-and-nonhidden-schedulers"></a>A. 非表示スケジューラと表示スケジューラを監視する  
 次のクエリでは、すべてのスケジューラにわたる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のワーカーとタスクの状態を出力します。 このクエリは、次の要件を満たすコンピューター システムで実行されました。  
  
-   2 つのプロセッサ (CPU)  
  
-   2 つの (NUMA) ノード  
  
-   1 つの NUMA ノードにつき 1 つの CPU  
  
-   関係マスクが `0x03` に設定されている  
  
```sql  
SELECT  
    scheduler_id,  
    cpu_id,  
    parent_node_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id cpu_id parent_node_id current_tasks_count  
------------ ------ -------------- -------------------  
0            1      0              9                    
257          255    0              1                    
1            0      1              10                   
258          255    1              1                    
255          255    32             2                    
  
runnable_tasks_count current_workers_count  
-------------------- ---------------------  
0                    11                     
0                    1                      
0                    18                     
0                    1                      
0                    3                      
  
active_workers_count work_queue_count  
-------------------- --------------------  
6                    0  
1                    0  
8                    0  
1                    0  
1                    0  
```  
  
 この出力では次のことがわかります。  
  
-   スケジューラは5つあります。 そのうちの 2 つの ID の値は 1048576 未満です。 ID > = 1048576 のスケジューラは非表示スケジューラと呼ばれます。 Scheduler `255` は、専用管理者接続 (DAC) を表します。 インスタンスごとに 1 つの DAC スケジューラが存在します。 メモリ負荷を調整するリソースモニターでは、scheduler `257` と scheduler `258`(NUMA ノードごとに1つ) が使用されます。  
  
-   出力では、23 のアクティブなタスクが示されています。 これらのタスクには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって開始されたリソース管理タスクに加えて、ユーザー要求が含まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] タスクの例としては、リソースモニター (NUMA ノードごとに1つ)、LAZY WRITER (NUMA ノードごとに1つ)、ロックモニター、チェックポイント、ログライターなどがあります。  
  
-   NUMA ノード `0` は CPU `1` にマップされており、NUMA ノード `1` は CPU `0` にマップされています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は通常、ノード0以外の NUMA ノードで開始されます。  
  
-   ここでは `runnable_tasks_count` に `0` が返されており、これはアクティブに実行中のタスクが存在しないことを意味します。 ただし、アクティブなセッションは存在する可能性があります。  
  
-   DAC を表す Scheduler `255` には `3` ワーカーが関連付けられています。 これらのワーカーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に割り当てられ、変更されることはありません。 これらのワーカーは DAC クエリの処理のみに使用されます。 このスケジューラ上の 2 つのタスクは、接続マネージャーとアイドル状態のワーカーを表します。  
  
-   `active_workers_count` は、タスクが関連付けられており、非プリエンプティブモードで実行されているすべてのワーカーを表します。 ネットワーク リスナーなどの一部のタスクは、プリエンプティブなスケジュール設定で実行されます。  
  
-   非表示スケジューラでは、通常のユーザー要求は処理されません。 ただし、DAC スケジューラは例外です。 この DAC スケジューラには、要求を処理するためのスレッドが 1 つあります。  
  
### <a name="b-monitoring-nonhidden-schedulers-in-a-busy-system"></a>b. 稼働率が高いシステムで表示スケジューラを監視する  
 次のクエリでは、負荷が高い表示スケジューラの状態を示します。このスケジューラでは、利用可能なワーカーの処理数を上回る要求が存在します。 この例では、256 のワーカーにタスクが割り当てられており、 一部のタスクはワーカーへの割り当てを待機中です。 実行可能なタスクの数が少ないということは、複数のタスクがリソースの待機中であることを意味します。  
  
> [!NOTE]  
>  sys.dm_os_workers でクエリを実行すると、ワーカーの状態を確認できます。 詳細については、「 [sys &#40;. dm_os_workers transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)」を参照してください。  
  
 クエリは次のようになります。  
  
```sql  
SELECT  
    scheduler_id,  
    cpu_id,  
    current_tasks_count,  
    runnable_tasks_count,  
    current_workers_count,  
    active_workers_count,  
    work_queue_count  
  FROM sys.dm_os_schedulers  
  WHERE scheduler_id < 255;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            144                 0                     
1            147                 1                     
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   125                  16  
128                   126                  19  
```  
  
 これに比較して次の結果では、実行可能なタスクが複数あり、ワーカーの取得を待機中のタスクがないことが示されています。 `work_queue_count` は両方のスケジューラで `0` になっています。  
  
```  
scheduler_id current_tasks_count runnable_tasks_count  
------------ ------------------- --------------------  
0            107                 98                    
1            110                 100                   
  
current_workers_count active_workers_count work_queue_count  
--------------------- -------------------- --------------------  
128                   104                  0  
128                   108                  0  
```  
  
## <a name="see-also"></a>参照  
 [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
