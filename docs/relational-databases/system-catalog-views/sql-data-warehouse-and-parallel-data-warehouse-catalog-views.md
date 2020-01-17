---
title: カタログ ビュー
titleSuffix: Azure SQL Data Warehouse and Parallel Data Warehouse
ms.date: 10/29/2019
ms.service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ef6f58e2-0162-4bb2-951a-a786da7453e4
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: b3d5780daea40f229ed7d4d86438be814dfe7d29
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844523"
---
# <a name="sql-data-warehouse-and-parallel-data-warehouse-catalog-views"></a>SQL Data Warehouse および並列データウェアハウスのカタログビュー

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 このトピックでは、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] カタログビューの一覧を示します。  
  
## <a name="includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd-catalog-views"></a>カタログビューの [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] と [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次のカタログビューは、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] と [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]の両方に適用されます。  
  
 [pdw_column_distribution_properties &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md)  
  
 [pdw_distributions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)  
  
 [pdw_index_mappings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
 [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
 [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
 [pdw_nodes_column_store_dictionaries &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
 [pdw_nodes_column_store_row_groups &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
 [pdw_nodes_column_store_segments &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)  
  
 [pdw_nodes_columns &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md)  
  
 [pdw_nodes_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md)  
  
 [pdw_nodes_partitions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md)  
  
 [pdw_nodes_pdw_physical_databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
 [pdw_nodes_tables &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md) 

 [sys.pdw_replicated_table_cache_state (Transact-SQL)](sys-pdw-replicated-table-cache-state-transact-sql.md) 
  
 [pdw_table_distribution_properties &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md)  
  
 [pdw_table_mappings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md) 

## <a name="includesssdwincludessssdw-mdmd-catalog-views"></a>カタログビューの [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]

 次のカタログビューは [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] にのみ適用されます。

 [pdw_materialized_view_column_distribution_properties &#40;transact-sql&#41; ](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest) (プレビュー)

 [pdw_materialized_view_distribution_properties &#40;transact-sql&#41; ](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest) (プレビュー)

 [pdw_materialized_view_mappings &#40;transact-sql&#41; ](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest) (プレビュー)

 [workload_management_workload_classifier_details &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)
  
 [workload_management_workload_classifiers &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
  
 [workload_management_workload_groups &#40;transact-sql&#41; ](/sql/relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql?view=azure-sqldw-latest) (プレビュー)


## <a name="includesspdwincludessspdw-mdmd-catalog-views"></a>カタログビューの [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

 次のカタログビューは [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] にのみ適用されます。

 [pdw_database_mappings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
 [pdw_diag_event_properties &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-event-properties-transact-sql.md)  
  
 [pdw_diag_events &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md)  
  
 [pdw_diag_sessions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md)  
  
 [pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)  
  
 [pdw_health_component_groups &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)  
  
 [pdw_health_component_properties &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)  
  
 [pdw_health_component_status_mappings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)  
  
 [pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)  
  
 [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
