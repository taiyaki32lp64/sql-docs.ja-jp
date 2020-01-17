---
title: sys.dm_workload_management_workload_groups_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 6e77239d019cb51e66a34a3a5b909e01c28a7faa
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633436"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys.dm_workload_management_workload_groups_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

ワークロードグループの統計と、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]内のワークロードグループの有効な値を返します。  
  
|列名|[データ型]|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|ワークロード グループの一意の ID。||
|name|**sysname**|ワークロードグループの名前。||
|statistics_start_time|**datetime**|ワークロードグループの統計コレクションが開始された時刻。  この値は、ワークロードグループが作成されたとき、またはインスタンスが一時停止またはスケーリングされたときのいずれかになります。||
|total_request_count|**bigint**|ワークロードグループ内の完了した要求の累積数。||
|total_shared_resource_reqeusts|**bigint**|共有プールからリソースを使用したワークロードグループ内の完了した要求の累積数。||
|total_queued_request_count|**bigint**|Max_concurrency の制限に達した後にキューに登録された要求の累積数。||
|total_request_execution_timeouts|**bigint**|Query_execution_timeout_sec の設定に基づいて、完了前にタイムアウトしたワークロードグループ内の要求の累積数。||
|effective_min_percentage_resource|**tinyint**|有効な min_percentage_resource 設定では、サービスレベルとワークロードグループの設定を考慮することができます。 有効な min_percentage_resource は、より低いサービスレベルで調整できます。  たとえば、DW100c では、許可されている最小 min_percentage_resource は25% です。  値がサービスレベルで許可されていない場合、min_percentage_resource は0% に調整されます。  たとえば、DW6000c で10% に設定されている min_percentage_resource、DW100c にスケールダウンすると、effective_min_percentage_resource は0% になります。||
|effective_cap_percentage_resource|**tinyint**|ワークロードグループの有効な cap_percentage_resource。  Min_percentage_resource > 0 のワークロードグループが他にある場合、effective_cap_percentage_resource は比例して低くなります。||
|effective_request_min_resource_grant_percent|**decimal (5, 2)**|ワークロードグループの request_min_resource_grant_percent の有効なランタイム値。 サービスレベルと、ワークロードグループの構成方法を検討している有効な値。  サービスレベルによって min_percentage_resource が調整された場合は、それに応じて effective_request_min_resource_grant_percent が調整されます。||
|effective_request_max_resource_grant_percent|**decimal (5, 2)**|ワークロードグループの request_max_resource_grant_percent の有効なランタイム値は、すべてのワークロードグループの構成を検討しています。||
|||||

## <a name="see-also"></a>参照

 [SQL Data Warehouse および並列データウェアハウスの動的管理&#40;ビュー transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
