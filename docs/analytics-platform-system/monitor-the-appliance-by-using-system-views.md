---
title: システムビューで監視する
description: この記事では、Analytics Platform system appliance の監視に使用できるシステムビューの一覧を示します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1979d5e698747e6104f7e743108cc1553de702e5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400954"
---
# <a name="monitor-the-appliance-with-system-views---analytics-platform-system"></a>システムビューを使用したアプライアンスの監視-Analytics Platform System
この記事では、SQL Server PDW の監視に使用できるシステムビューの一覧を示します。  
  
## <a name="to-monitor-the-appliance-by-using-system-views"></a>システムビューを使用してアプライアンスを監視するには  
SQL Server PDW には、アプライアンスの正常性、状態、およびパフォーマンスに関する詳細情報を取得するための包括的なシステムビューが含まれています。 次の表に、各監視機能に使用できるシステムビューへのリンクを示します。  
  
![PDW システム ビューの警告](./media/monitor-the-appliance-by-using-system-views/PDW_system_views_alerts.png "PDW_system_views_alerts")  
  
|||  
|-|-|  
|**情報の種類**|**関連するシステムビュー**|  
|アプライアンスの全体的な状態|[dm_pdw_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)|  
|アラート|[sys.pdw_health_alerts](../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)<br /><br />[sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)|  
|アプライアンスコンポーネントとその状態|[sys.pdw_health_component_groups](../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)<br /><br />[sys.pdw_health_components](../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)<br /><br />[sys.pdw_health_component_properties](../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)<br /><br />[sys.pdw_health_component_status_mappings](../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)<br /><br />[dm_pdw_nodes](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)|  
|要求の監視 (クエリ、読み込み、バックアップ、復元など)|[sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)<br /><br />[dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)<br /><br />[dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)<br /><br />[dm_pdw_sql_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)<br /><br />[dm_pdw_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)<br /><br />[dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)<br /><br />[dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)<br /><br />[pdw_distributions](../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)|  
|読み込み、バックアップ、復元の追加情報を監視します。|[pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)<br /><br />[pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)<br /><br />[sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)|  
|OS レベルのログとパフォーマンス情報|[sys.dm_pdw_os_performance_counters](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)<br /><br />[sys.dm_pdw_os_event_logs](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)<br /><br />[dm_pdw_os_threads](../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)|  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[アプライアンス監視 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
