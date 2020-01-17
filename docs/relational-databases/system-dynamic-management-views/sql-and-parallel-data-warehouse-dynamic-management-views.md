---
title: SQL および Parallel Data Warehouse の動的管理ビュー
ms.custom: seo-dt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bbf63d4553630cce6d1d890f2d353442c14d6afd
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401623"
---
# <a name="sql-and-parallel-data-warehouse-dynamic-management-views"></a>SQL および Parallel Data Warehouse の動的管理ビュー
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

このトピックでは[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]および動的管理ビュー (dmv) の一覧を示します。  
  
 すべて[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]の[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]および dmv は、 **sys. dm_pdw**で始まります。  
  
## <a name="includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]および[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]動的管理ビュー  
 次の動的管理ビューは、と[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]の両方に適用されます。  
  
 [dm_pdw_dms_cores &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-cores-transact-sql.md)  
  
 [dm_pdw_dms_external_work &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)  
  
 [dm_pdw_dms_workers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)  
  
 [dm_pdw_errors &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)  
  
 [dm_pdw_exec_connections &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)  
  
 [dm_pdw_exec_requests &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
 [dm_pdw_exec_sessions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)  
  
 [dm_pdw_hadoop_operations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)  
  
 [dm_pdw_lock_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
 [dm_pdw_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)  
  
 [dm_pdw_nodes_database_encryption_keys &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
 [dm_pdw_os_threads &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)  
  
 [dm_pdw_request_steps &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)  
  
 [dm_pdw_resource_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
 [dm_pdw_sql_requests &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)  
  
 [dm_pdw_sys_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)  
  
 [dm_pdw_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
 [dm_pdw_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)

## <a name="includesssdwincludessssdw-mdmd-dynamic-management-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]動的管理ビュー 
 次の動的管理ビューはに[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]のみ適用されます。
 
[dm_pdw_nodes_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-plan-transact-sql.md)  

[dm_pdw_nodes_exec_query_profiles &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-profiles-transact-sql.md)  

[dm_pdw_nodes_exec_query_statistics_xml &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-statistics-xml-transact-sql.md)  

[dm_pdw_nodes_exec_sql-text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-sql-text-transact-sql.md)  

[dm_pdw_nodes_exec_text_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-text-query-plan-transact-sql.md)

 [dm_workload_management_workload_groups_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) (プレビュー)

## <a name="includesspdwincludessspdw-mdmd-dynamic-management-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]動的管理ビュー  
 次の動的管理ビューはに[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]のみ適用されます。  
  
 [dm_pdw_component_health_active_alerts &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)  
  
 [dm_pdw_component_health_alerts &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)  
  
 [dm_pdw_component_health_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)  
  
 [dm_pdw_diag_processing_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-diag-processing-stats-transact-sql.md)  
  
 [dm_pdw_network_credentials &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)  
  
 [dm_pdw_node_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-node-status-transact-sql.md)  
  
 [dm_pdw_os_event_logs &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)  
  
 [dm_pdw_os_performance_counters &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)  
  
 [dm_pdw_query_stats_xe &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-transact-sql.md)  
  
 [dm_pdw_query_stats_xe_file &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-file-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の動的管理ビューおよび関数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
