---
title: システム ビュー
description: 分析プラットフォームシステム (APS) SQL Server 並列データウェアハウス (PDW) のシステムビュー。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a7e6a0bda01de76787033607fbf35a0ca123ef95
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399805"
---
# <a name="system-views-for-analytics-platform-system-parallel-data-warehouse"></a>Analytics Platform System Parallel Data Warehouse のシステムビュー
分析プラットフォームシステム (APS) SQL Server 並列データウェアハウス (PDW) のシステムビュー。

## <a name="parallel-data-warehouse-catalog-views"></a>並列データウェアハウスのカタログビュー
* [pdw_column_distribution_properties](https://msdn.microsoft.com/library/mt204022.aspx)
* [pdw_database_mappings](https://msdn.microsoft.com/library/mt203891.aspx)
* [pdw_distributions](https://msdn.microsoft.com/library/mt203892.aspx)
* [pdw_index_mappings](https://msdn.microsoft.com/library/mt203912.aspx)
* [pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)
* [pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)
* [pdw_nodes_column_store_dictionaries](https://msdn.microsoft.com/library/mt203902.aspx)
* [pdw_nodes_column_store_row_groups](https://msdn.microsoft.com/library/mt203880.aspx)
* [pdw_nodes_column_store_segments](https://msdn.microsoft.com/library/mt203916.aspx)
* [pdw_nodes_columns](https://msdn.microsoft.com/library/mt203881.aspx)
* [pdw_nodes_indexes](https://msdn.microsoft.com/library/mt203885.aspx)
* [pdw_nodes_partitions](https://msdn.microsoft.com/library/mt203908.aspx)
* [pdw_nodes_pdw_physical_databases](https://msdn.microsoft.com/library/mt203897.aspx)
* [pdw_nodes_tables](https://msdn.microsoft.com/library/mt203886.aspx)
* [pdw_table_distribution_properties](https://msdn.microsoft.com/library/mt203896.aspx)
* [pdw_table_mappings](https://msdn.microsoft.com/library/mt203876.aspx)

## <a name="parallel-data-warehouse-dynamic-management-views-dmvs"></a>並列データウェアハウスの動的管理ビュー (Dmv)
* [sys.dm_pdw_dms_cores](https://msdn.microsoft.com/library/mt203911.aspx)
* [dm_pdw_dms_external_work](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)
* [dm_pdw_dms_workers](https://msdn.microsoft.com/library/mt203878.aspx)
* [dm_pdw_errors](https://msdn.microsoft.com/library/mt203904.aspx)
* [dm_pdw_exec_connections](https://msdn.microsoft.com/library/mt203882.aspx)
* [dm_pdw_exec_requests](https://msdn.microsoft.com/library/mt203887.aspx)
* [sys.dm_pdw_exec_sessions](https://msdn.microsoft.com/library/mt203883.aspx)
* [dm_pdw_hadoop_operations](../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)
* [dm_pdw_lock_waits](https://msdn.microsoft.com/library/mt203901.aspx)
* [dm_pdw_nodes](https://msdn.microsoft.com/library/mt203907.aspx)
* [dm_pdw_nodes_database_encryption_keys](https://msdn.microsoft.com/library/mt203922.aspx)
* [dm_pdw_os_threads](https://msdn.microsoft.com/library/mt203917.aspx)
* [dm_pdw_request_steps](https://msdn.microsoft.com/library/mt203913.aspx)
* [dm_pdw_resource_waits](https://msdn.microsoft.com/library/mt203906.aspx)
* [dm_pdw_sql_requests](https://msdn.microsoft.com/library/mt203889.aspx)
* [dm_pdw_sys_info](https://msdn.microsoft.com/library/mt203900.aspx)
* [dm_pdw_wait_stats](https://msdn.microsoft.com/library/mt203909.aspx)
* [dm_pdw_waits](https://msdn.microsoft.com/library/mt203909.aspx)

## <a name="sql-server-dmvs-applicable-to-parallel-data-warehouse"></a>並列データウェアハウスに適用可能な SQL Server Dmv
次の Dmv は並列データウェアハウスに適用できますが、 **master**データベースに接続することによって実行する必要があります。

* [database_service_objectives](../relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database.md)
* [dm_operation_status](../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)
* [fn_helpcollations ()](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)

## <a name="sql-server-catalog-views"></a>SQL Server カタログ ビュー
* [all_columns](https://msdn.microsoft.com/library/ms177522.aspx)
* [all_objects](https://msdn.microsoft.com/library/ms178618.aspx)
* [all_parameters](https://msdn.microsoft.com/library/ms190340.aspx)
* [all_sql_modules](https://msdn.microsoft.com/library/ms184389.aspx)
* [all_views](https://msdn.microsoft.com/library/ms189510.aspx)
* [sys. アセンブリ](https://msdn.microsoft.com/library/ms189790.aspx)
* [assembly_modules](https://msdn.microsoft.com/library/ms180052.aspx)
* [assembly_types](https://msdn.microsoft.com/library/ms178020.aspx)
* [sys. 証明書](https://msdn.microsoft.com/library/ms189774.aspx)
* [check_constraints](https://msdn.microsoft.com/library/ms187388.aspx)
* [sys.columns](https://msdn.microsoft.com/library/ms176106.aspx)
* [computed_columns](https://msdn.microsoft.com/library/ms188744.aspx)
* [sys. 資格情報](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)
* [data_spaces](https://msdn.microsoft.com/library/ms190289.aspx)
* [database_credentials](../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md)
* [database_files](https://msdn.microsoft.com/library/ms174397.aspx)
* [database_permissions](https://msdn.microsoft.com/library/ms188367.aspx)
* [database_principals](https://msdn.microsoft.com/library/ms187328.aspx)
* [database_role_members](https://msdn.microsoft.com/library/ms189780.aspx)
* [システムデータベース](https://msdn.microsoft.com/library/ms178534.aspx)
* [default_constraints](https://msdn.microsoft.com/library/ms173758.aspx)
* [external_data_sources](https://msdn.microsoft.com/library/dn935019.aspx)
* [external_file_formats](https://msdn.microsoft.com/library/dn935025.aspx)
* [external_tables](https://msdn.microsoft.com/library/dn935029.aspx)
* [sys. ファイルグループ](https://msdn.microsoft.com/library/ms187782.aspx)
* [foreign_key_columns](https://msdn.microsoft.com/library/ms186306.aspx)
* [foreign_keys](https://msdn.microsoft.com/library/ms189807.aspx)
* [identity_columns](https://msdn.microsoft.com/library/ms187334.aspx)
* [index_columns](https://msdn.microsoft.com/library/ms175105.aspx)
* [システムインデックス](https://msdn.microsoft.com/library/ms173760.aspx)
* [key_constraints](https://msdn.microsoft.com/library/ms174321.aspx)
* [numbered_procedures](https://msdn.microsoft.com/library/ms179865.aspx)
* [sys.objects](https://msdn.microsoft.com/library/ms190324.aspx)
* [sys. パラメーター](https://msdn.microsoft.com/library/ms176074.aspx)
* [partition_functions](https://msdn.microsoft.com/library/ms187381.aspx)
* [partition_parameters](https://msdn.microsoft.com/library/ms175054.aspx)
* [partition_range_values](https://msdn.microsoft.com/library/ms187780.aspx)
* [partition_schemes](https://msdn.microsoft.com/library/ms189752.aspx)
* [sys. パーティション](https://msdn.microsoft.com/library/ms175012.aspx)
* [sys. プロシージャ](https://msdn.microsoft.com/library/ms188737.aspx)
* [sys.schemas](https://msdn.microsoft.com/library/ms176011.aspx)
* [securable_classes](https://msdn.microsoft.com/library/ms408301.aspx)
* [sql_expression_dependencies](https://msdn.microsoft.com/library/bb677315.aspx)
* [sql_modules](https://msdn.microsoft.com/library/ms175081.aspx)
* [sys.stats](https://msdn.microsoft.com/library/ms177623.aspx)
* [sys.stats_columns](https://msdn.microsoft.com/library/ms187340.aspx)
* [symmetric_keys](../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)
* [sys](../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)
* [syscharsets](../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)
* [syscolumns](../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md)
* [sysdatabases](../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)
* [sys.syslanguages](../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)
* [sys. sysobjects](../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)
* [sys 参照](../relational-databases/system-compatibility-views/sys-sysreferences-transact-sql.md)
* [system_columns](https://msdn.microsoft.com/library/ms178596.aspx)
* [system_objects](https://msdn.microsoft.com/library/ms173551.aspx)
* [system_parameters](../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)
* [system_sql_modules](https://msdn.microsoft.com/library/ms188034.aspx)
* [system_views](https://msdn.microsoft.com/library/ms187764.aspx)
* [systypes](../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)
* [sys. sysusers](../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)
* [sys.tables](https://msdn.microsoft.com/library/ms187406.aspx)
* [sys 型](https://msdn.microsoft.com/library/ms188021.aspx)
* [システムビュー](https://msdn.microsoft.com/library/ms190334.aspx)

## <a name="sql-server-dmvs-available-in-parallel-data-warehouse"></a>並列データウェアハウスで使用できる Dmv の SQL Server
並列データウェアハウスは、SQL Server の動的管理ビュー (Dmv) の多くを公開します。 これらのビューは、並列データウェアハウスでクエリを実行すると、ディストリビューションで実行されている SQL Server データベースの状態を報告します。

これらの DMV には、pdw_node_id と呼ばれる特定の列があります。 これは、コンピューティングノードの識別子です。 

> [!NOTE]
> これらのビューを使用するには、次の表に示すように、名前に ' pdw_nodes_ ' を挿入します。
> 
> 

| Parallel Data Warehouse の DMV 名 | SQL Server T-sql トピックへのリンク |
|:--- |:--- |
| sys.dm_pdw_nodes_db_file_space_usage |[dm_db_file_space_usage](https://msdn.microsoft.com/library/ms174412.aspx) |
| sys.dm_pdw_nodes_db_index_usage_stats |[dm_db_index_usage_stats](https://msdn.microsoft.com/library/ms188755.aspx) |
| sys.dm_pdw_nodes_db_partition_stats |[dm_db_partition_stats](https://msdn.microsoft.com/library/ms187737.aspx) |
| sys.dm_pdw_nodes_db_session_space_usage |[dm_db_session_space_usage](https://msdn.microsoft.com/library/ms187938.aspx) |
| sys.dm_pdw_nodes_db_task_space_usage |[dm_db_task_space_usage](https://msdn.microsoft.com/library/ms190288.aspx) |
| sys.dm_pdw_nodes_exec_background_job_queue |[dm_exec_background_job_queue](https://msdn.microsoft.com/library/ms173512.aspx) |
| sys.dm_pdw_nodes_exec_background_job_queue_stats |[dm_exec_background_job_queue_stats](https://msdn.microsoft.com/library/ms176059.aspx) |
| sys.dm_pdw_nodes_exec_cached_plans |[dm_exec_cached_plans](https://msdn.microsoft.com/library/ms187404.aspx) |
| sys.dm_pdw_nodes_exec_connections |[dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) |
| sys.dm_pdw_nodes_exec_procedure_stats |[dm_exec_procedure_stats](https://msdn.microsoft.com/library/cc280701.aspx) |
| sys.dm_pdw_nodes_exec_query_memory_grants |[dm_exec_query_memory_grants](https://msdn.microsoft.com/library/ms365393.aspx) |
| sys.dm_pdw_nodes_exec_query_optimizer_info |[dm_exec_query_optimizer_info](https://msdn.microsoft.com/library/ms175002.aspx) |
| sys.dm_pdw_nodes_exec_query_resource_semaphores |[dm_exec_query_resource_semaphores](https://msdn.microsoft.com/library/ms366321.aspx) |
| sys.dm_pdw_nodes_exec_query_stats |[dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) |
| sys.dm_pdw_nodes_exec_requests |[dm_exec_requests](https://msdn.microsoft.com/library/ms177648.aspx) |
| sys.dm_pdw_nodes_exec_sessions |[dm_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) |
| sys.dm_pdw_nodes_io_pending_io_requests |[dm_io_pending_io_requests](https://msdn.microsoft.com/library/ms188762.aspx) |
| sys.dm_pdw_nodes_os_buffer_descriptors |[dm_os_buffer_descriptors](https://msdn.microsoft.com/library/ms173442.aspx) |
| sys.dm_pdw_nodes_os_child_instances |[dm_os_child_instances](https://msdn.microsoft.com/library/ms165698.aspx) |
| sys.dm_pdw_nodes_os_cluster_nodes |[dm_os_cluster_nodes](https://msdn.microsoft.com/library/ms187341.aspx) |
| sys.dm_pdw_nodes_os_dispatcher_pools |[dm_os_dispatcher_pools](https://msdn.microsoft.com/library/bb630336.aspx) |
| sys.dm_pdw_nodes_os_dispatchers |Transact-SQL のドキュメントはありません。 |
| sys.dm_pdw_nodes_os_hosts |[dm_os_hosts](https://msdn.microsoft.com/library/ms187800.aspx) |
| sys.dm_pdw_nodes_os_latch_stats |[dm_os_latch_stats](https://msdn.microsoft.com/library/ms175066.aspx) |
| sys.dm_pdw_nodes_os_memory_brokers |[dm_os_memory_brokers](https://msdn.microsoft.com/library/bb522548.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_clock_hands |[dm_os_memory_cache_clock_hands](https://msdn.microsoft.com/library/ms173786.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_counters |[dm_os_memory_cache_counters](https://msdn.microsoft.com/library/ms188760.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_entries |[dm_os_memory_cache_entries](https://msdn.microsoft.com/library/ms189488.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_hash_tables |[dm_os_memory_cache_hash_tables](https://msdn.microsoft.com/library/ms182388.aspx) |
| sys.dm_pdw_nodes_os_memory_clerks |[dm_os_memory_clerks](https://msdn.microsoft.com/library/ms175019.aspx) |
| sys.dm_pdw_nodes_os_memory_node_access_stats |Transact-SQL のドキュメントはありません。 |
| sys.dm_pdw_nodes_os_memory_nodes |[dm_os_memory_nodes](https://msdn.microsoft.com/library/bb510622.aspx) |
| sys.dm_pdw_nodes_os_memory_objects |[dm_os_memory_objects](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) |
| sys.dm_pdw_nodes_os_memory_pools |[dm_os_memory_pools](https://msdn.microsoft.com/library/ms175022.aspx) |
| sys.dm_pdw_nodes_os_nodes |[dm_os_nodes](https://msdn.microsoft.com/library/bb510628.aspx) |
| sys.dm_pdw_nodes_os_performance_counters |[dm_os_performance_counters](https://msdn.microsoft.com/library/ms187743.aspx) |
| sys.dm_pdw_nodes_os_process_memory |[dm_os_process_memory](https://msdn.microsoft.com/library/bb510747.aspx) |
| sys.dm_pdw_nodes_os_schedulers |[dm_os_schedulers](https://msdn.microsoft.com/library/ms177526.aspx) |
| sys.dm_pdw_nodes_os_spinlock_stats |Transact-SQL のドキュメントはありません。 |
| sys.dm_pdw_nodes_os_sys_info |[dm_os_sys_info](https://msdn.microsoft.com/library/ms175048.aspx) |
| sys.dm_pdw_nodes_os_sys_memory |[dm_os_memory_nodes](https://msdn.microsoft.com/library/bb510622.aspx) |
| sys.dm_pdw_nodes_os_tasks |[dm_os_tasks](https://msdn.microsoft.com/library/ms174963.aspx) |
| sys.dm_pdw_nodes_os_threads |[dm_os_threads](https://msdn.microsoft.com/library/ms187818.aspx) |
| sys.dm_pdw_nodes_os_virtual_address_dump |[dm_os_virtual_address_dump](../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md) |
| sys.dm_pdw_nodes_os_wait_stats |[dm_os_wait_stats](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) |
| sys.dm_pdw_nodes_os_waiting_tasks |[dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md) |
| sys.dm_pdw_nodes_os_workers |[dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md) |
| sys.dm_pdw_nodes_resource_governor_resource_pools |[dm_resource_governor_resource_pools](https://msdn.microsoft.com/library/bb934023.aspx) |
| sys.dm_pdw_nodes_resource_governor_workload_groups |[dm_resource_governor_workload_groups](https://msdn.microsoft.com/library/bb934197.aspx) |
| sys.dm_pdw_nodes_tran_active_snapshot_database_transactions |[dm_tran_active_snapshot_database_transactions](https://msdn.microsoft.com/library/ms180023.aspx) |
| sys.dm_pdw_nodes_tran_active_transactions |[dm_tran_active_transactions](https://msdn.microsoft.com/library/ms174302.aspx) |
| sys.dm_pdw_nodes_tran_commit_table |[dm_tran_commit_table](../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md) |
| sys.dm_pdw_nodes_tran_current_snapshot |[dm_tran_current_snapshot](https://msdn.microsoft.com/library/ms184390.aspx) |
| sys.dm_pdw_nodes_tran_current_transaction |[dm_tran_current_transaction](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md) |
| sys.dm_pdw_nodes_tran_database_transactions |[dm_tran_database_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) |
| sys.dm_pdw_nodes_tran_locks |[dm_tran_locks](https://msdn.microsoft.com/library/ms190345.aspx) |
| sys.dm_pdw_nodes_tran_session_transactions |[dm_tran_session_transactions](https://msdn.microsoft.com/library/ms188739.aspx) |
| sys.dm_pdw_nodes_tran_top_version_generators |[dm_tran_top_version_generators](https://msdn.microsoft.com/library/ms188778.aspx) |

## <a name="sql-server-2016-polybase-dmvs-available-in-parallel-data-warehouse"></a>並列データウェアハウスで使用可能な SQL Server 2016 PolyBase Dmv
* [dm_exec_compute_node_errors](https://msdn.microsoft.com/library/mt146380.aspx)
* [dm_exec_compute_node_status](https://msdn.microsoft.com/library/mt146382.aspx)
* [dm_exec_compute_nodes](../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)
* [dm_exec_distributed_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)
* [dm_exec_distributed_requests](https://msdn.microsoft.com/library/mt146385.aspx)
* [dm_exec_distributed_sql_requests](https://msdn.microsoft.com/library/mt146390.aspx)
* [dm_exec_dms_services](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)
* [dm_exec_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)
* [dm_exec_external_operations](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)
* [dm_exec_external_work](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)

## <a name="sql-server-information_schema-views"></a>SQL Server INFORMATION_SCHEMA ビュー
* [CHECK_CONSTRAINTS](../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)
* [欄](../relational-databases/system-information-schema-views/columns-transact-sql.md)
* [パラメータ](../relational-databases/system-information-schema-views/parameters-transact-sql.md)
* [ルーチン](../relational-databases/system-information-schema-views/routines-transact-sql.md)
* [スキーマ](../relational-databases/system-information-schema-views/schemata-transact-sql.md)
* [テーブル](../relational-databases/system-information-schema-views/tables-transact-sql.md)
* [VIEW_COLUMN_USAGE](../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)
* [VIEW_TABLE_USAGE](../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)
* [表示モード](../relational-databases/system-information-schema-views/views-transact-sql.md)

## <a name="next-steps"></a>次の手順
詳細については、「 [t-sql 言語要素](tsql-language-elements.md)」および「 [t-sql ステートメント](tsql-statements.md)」を参照してください。

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse reference overview]: sql-data-warehouse-overview-reference.md

<!--MSDN references-->


<!--Other Web references-->
