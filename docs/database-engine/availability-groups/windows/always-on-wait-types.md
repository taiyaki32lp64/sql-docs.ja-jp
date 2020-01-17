---
title: 可用性グループに関連付けられている待機を識別する
description: Transact-SQL (T-SQL) と拡張イベントを使用し、Always On 可用性グループに関連付けられている待機を識別する
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
author: rothja
ms.author: jroth
ms.openlocfilehash: a62145645a965d46c8da076eca14cd8a3dd85857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934968"
---
# <a name="identify-waits-associated-with-availability-groups"></a>可用性グループに関連付けられている待機を識別する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 可用性グループの遅延のトラブルシューティングを行うときには、動的管理ビュー(DMV) [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) で可用性グループ固有の待機の種類を使用して、累積の統計を監視できるまで待ちます。  
  
 待機の統計の使用に関する概要については、「[SQL Server 2005 Waits and Queues](https://technet.microsoft.com/library/cc966413.aspx)」(SQL Server 2005 の待機とキュー) を参照してください。 このドキュメントは、SQL Server 2005 を対象として記述されましたが、その情報は、それ以降の SQL Server バージョンに適用できます。  
  
## <a name="query-for-availability-groups-wait-types"></a>可用性グループの待機の種類のクエリ  
 次の T-SQL クエリを使用して、可用性グループの待機の種類のすべての待機統計を取得します。  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 拡張イベントをキャプチャして待機の統計を監視するには、次の T-SQL コマンドを使用します。  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 待機の種類のキー値のマッピングを表示するには、次のクエリを実行します。  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>次の手順  
 [待機の種類](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
  
