---
title: sys.dm_resource_governor_resource_pool_volumes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
ms.assetid: fa692e56-c561-4533-97c5-bc12c600553f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 801997509242bae7af2d2ae438dfdb952be9e1fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090811"
---
# <a name="sysdmresourcegovernorresourcepoolvolumes-transact-sql"></a>sys.dm_resource_governor_resource_pool_volumes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  現在のリソース プールのディスク ボリュームごとの IO の統計に関する情報を返します。 リソース プール レベルではこの情報は使用可能なも[sys.dm_resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)します。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|リソース プールの ID。 NULL 値は許可されません。|  
|volume_name|**sysname**|ディスク ボリュームの名前。 NULL 値は許可されません。|  
|read_io_queued_total|**int**|リソース ガバナーがリセットされた後、読み取り IOs エンキューを合計します。 NULL 値は許可されません。|  
|read_io_issued_total|**int**|読み取りリソース ガバナー統計がリセットされた後に発行される Io の合計。 NULL 値は許可されません。|  
|read_ios_completed_total|**int**|リソース ガバナー統計がリセットされた後に完了した読み取り IO の合計。 NULL 値は許可されません。|  
|read_ios_throttled_total|**int**|IOs のリソース ガバナー統計がリセットされた後に調整された読み取りの合計。 NULL 値は許可されません。|  
|read_bytes_total|**bigint**|リソース ガバナー統計がリセットされた後に読み取られたバイト数の合計。 NULL 値は許可されません。|  
|read_io_stall_total_ms|**bigint**|読み取り IO の到着から完了までのミリ秒単位で合計時間。 NULL 値は許可されません。|  
|確認するのに|**bigint**|読み取り IO の到着から発行までのミリ秒単位で合計時間。 これは、IO リソース管理によって遅延です。 NULL 値は許可されません。|  
|write_io_queued_total|**int**|リソース ガバナー統計がリセットされた後 IOs のエンキューされたを書き込みの合計。 NULL 値は許可されません。|  
|write_io_issued_total|**int**|リソース ガバナー統計がリセットされた後に発行される Io を書き込みの合計。 NULL 値は許可されません。|  
|write_io_completed_total|**int**|リソース ガバナー統計がリセットされた後に完了した書き込み IO の合計。 値が許容されません。|  
|write_io_throttled_total|**int**|IOs のリソース ガバナー統計がリセットされた後に調整された書き込みの合計。 値が許容されません。|  
|write_bytes_total|**bigint**|リソース ガバナー統計がリセットされた後に書き込まれたバイト数の合計。 NULL 値は許可されません。|  
|write_io_stall_total_ms|**bigint**|書き込み IO の発行から完了までのミリ秒単位の合計時間。 NULL 値は許可されません。|  
|write_io_stall_queued_ms|**bigint**|書き込み IO の到着から発行までの合計時間 (ミリ秒単位)。 これは、IO リソース管理によって遅延です。 NULL 値は許可されません。|  
|io_issue_violations_total|**int**|IO 発行違反の合計。 IO の割合を発行するときの回数が予約レートよりも低かった。 NULL 値は許可されません。|  
|io_issue_delay_total_ms|**bigint**|スケジュールされた問題と IO の実際の問題の間 (ミリ秒単位) の合計時間。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

