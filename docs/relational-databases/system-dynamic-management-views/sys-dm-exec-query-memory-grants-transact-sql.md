---
title: sys.dm_exec_query_memory_grants (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5a833e5d1c3c67e61c4d81b4b575ab90b23f75fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097703"
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  要求したメモリ許可を待機しているし、メモリ許可が与えられているすべてのクエリに関する情報を返します。 メモリ許可を必要としないクエリは、このビューでは表示されません。 たとえば、並べ替えし、ハッシュ結合の操作なしのクエリ中に、クエリ実行メモリ許可がある、 **ORDER BY**句には、メモリ許可がありません。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開することを避けるため、接続されているテナントに属していないデータが含まれるすべての行はフィルターで除外します。さらに、列の値**scheduler_id**、 **wait_order**、 **pool_id**、 **group_id**フィルター処理され、列の値の設定NULL です。  
  
> [!NOTE]  
> これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_exec_query_memory_grants**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID (SPID) のこのクエリが実行されているセッションです。|  
|**request_id**|**int**|要求の ID。 セッションのコンテキスト内で一意です。|  
|**scheduler_id**|**int**|このクエリのスケジュールを設定しているスケジューラの ID。|  
|**dop**|**smallint**|このクエリの並列処理の次数。|  
|**request_time**|**datetime**|このクエリがメモリ許可を要求した日付と時刻。|  
|**grant_time**|**datetime**|日付と、このクエリのメモリが許可された時間。 メモリがまだ許可されていない場合は NULL です。|  
|**requested_memory_kb**|**bigint**|合計要求されたメモリ量 (キロバイト単位)。|  
|**granted_memory_kb**|**bigint**|実際には、キロバイト単位で許可されているメモリの総量。 メモリがまだ許可されていない場合、NULL を指定できます。 一般的な状況では、この値は同じ**requested_memory_kb**します。 インデックス作成では、最初に許可されたメモリ量を超えて、追加のオンデマンド メモリが許可される場合があります。|  
|**required_memory_kb**|**bigint**|最小メモリ (キロバイト単位)、このクエリを実行するために必要です。 **requested_memory_kb**は、この量よりも小さい場合。|  
|**used_memory_kb**|**bigint**|この時点で使用されている物理メモリ (KB 単位)。|  
|**max_used_memory_kb**|**bigint**|この時点までに使用された最大物理メモリ (KB 単位)。|  
|**query_cost**|**float**|推定クエリ コスト。|  
|**timeout_sec**|**int**|このクエリがメモリ許可要求をやめるまでのタイムアウト (秒単位)。|  
|**resource_semaphore_id**|**smallint**|このクエリが待機しているリソース セマフォの非一意の ID。<br /><br /> **注:** この ID は一意のバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]より前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]します。 この変更は、クエリの実行のトラブルシューティングに影響する可能性があります。 詳細については、このトピックの後半の「解説」セクションを参照してください。|  
|**queue_id**|**smallint**|このクエリがメモリ許可を待機している待機キューの ID。 メモリが既に与えられている場合は NULL です。|  
|**wait_order**|**int**|指定した待機クエリの順番**queue_id**します。 この値は、他のクエリ メモリ許可またはタイムアウトを取得する場合、特定のクエリを変更できます。メモリが既に与えられている場合は NULL です。|  
|**is_next_candidate**|**bit**|[次へ] のメモリ許可の候補。<br /><br /> 1 = はい<br /><br /> 0 = いいえ<br /><br /> NULL = メモリが既に与えられています。|  
|**wait_time_ms**|**bigint**|待機時間 (ミリ秒単位)。 メモリが既に与えられている場合は NULL です。|  
|**plan_handle**|**varbinary(64)**|このクエリ プランの識別子。 使用**sys.dm_exec_query_plan**を実際の XML プランを抽出します。|  
|**sql_handle**|**varbinary(64)**|このクエリの [!INCLUDE[tsql](../../includes/tsql-md.md)] テキストの識別子。 使用**sys.dm_exec_sql_text** 、実際に取得する[!INCLUDE[tsql](../../includes/tsql-md.md)]テキスト。|  
|**group_id**|**int**|このクエリが実行されているワークロード グループの ID。|  
|**pool_id**|**int**|このワークロード グループが属するリソース プールの ID。|  
|**is_small**|**tinyint**|1 に設定すると、この許可で小さなリソース セマフォが使用されます。 0 に設定すると、通常のセマフォが使用されることを示します。|  
|**ideal_memory_kb**|**bigint**|すべてのものを物理メモリに収まるようにメモリ許可のキロバイト (KB) 単位のサイズ。 これは、カーディナリティの推定に基づきます。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 上では、データベース内の `VIEW DATABASE STATE` アクセス許可が必要です。   
   
## <a name="remarks"></a>コメント  
 クエリ タイムアウトの一般的なデバッグ シナリオは、次のようになります可能性があります。  
  
-   全体的なシステム メモリを使用して状態を確認[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)、 [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)、およびさまざまなパフォーマンス カウンター。  
  
-   クエリ実行メモリ予約確認**sys.dm_os_memory_clerks**場所`type = 'MEMORYCLERK_SQLQERESERVATIONS'`します。  
  
-   確認を待機しているクエリ<sup>1</sup>を使用して許可**sys.dm_exec_query_memory_grants**します。  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup> このシナリオの場合、待機の種類は一般的に RESOURCE_SEMAPHORE になります。 詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。 
  
-   使用して、メモリ許可を使用したクエリのキャッシュを検索[sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)と[sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   使用してメモリを消費するクエリをさらに調べたり[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)します。  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   ランナウェイ クエリが疑いがある場合、確認のプラン表示から[sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)バッチからのテキストと[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)します。  
  
 含む動的管理ビューを使用するクエリ`ORDER BY`または集計がメモリ使用量が増えるし、問題のある問題をそれによって可能性があります。  
  
 リソース ガバナーの機能では、データベース管理者は、最大 64 個までのリソース プールでのサーバー リソースに分散できます。 以降で[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、各プールが小規模の独立したサーバー インスタンスのように動作し、2 つのセマフォを必要とします。 返される行の数**sys.dm_exec_query_resource_semaphores**できる最大 20 倍に返される行より[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]します。  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_exec_query_resource_semaphores &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
