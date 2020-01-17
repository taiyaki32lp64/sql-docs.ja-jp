---
title: sys _resource_governor_external_resource_pools (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cf77a073a1432df839bfd13046c66018496e79f1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468520"
---
# <a name="sysdmresourcegovernorexternalresourcepools-transact-sql"></a>sys _resource_governor_external_resource_pools (Transact-sql)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

現在の外部リソースプールの状態、リソースプールの現在の構成、およびリソースプールの統計に関する情報を返します。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|名前の指定      |データの種類      |説明|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|リソースプールの ID。 NULL 値は許可されません。 |
| NAME|**sysname**|リソースプールの名前。 NULL 値は許可されません。 
| pool_version|**int**|内部バージョン番号。|
| max_cpu_percent|**int**|CPU の競合がある場合に、リソースプールのすべての要求で許容される最大平均 CPU 帯域幅の現在の構成。 NULL 値は許可されません。 |
| max_processes|**int**|同時外部プロセスの最大数。 既定値は 0 で、制限がないことを示します。 NULL 値は許可されません。|
| max_memory_percent|**int**|このリソースプール内の要求で使用できる合計サーバーメモリの割合の現在の構成。 NULL 値は許可されません。 |
| statistics_start_time|**datetime**|このプールの統計がリセットされた時刻。 NULL 値は許可されません。 
| peak_memory_kb|**bigint**|リソースプールに使用されるメモリの最大量 (kb 単位)。 NULL 値は許可されません。 |
| write_io_count|**int**|リソースガバナー統計がリセットされた後に発行された書き込み Io の合計。 NULL 値は許可されません。 |
| read_io_count|**int**|リソースガバナー統計がリセットされた後に発行された読み取り Io の合計。 NULL 値は許可されません。 |
| total_cpu_kernel_ms|**bigint**|リソースガバナー統計がリセットされてからの累積 CPU ユーザーカーネル時間 (ミリ秒単位)。 NULL 値は許可されません。 |
| total_cpu_user_ms|**bigint**|リソースガバナー統計がリセットされてからの累積 CPU ユーザー時間 (ミリ秒単位)。 NULL 値は許可されません。 |
| active_processes_count|**int**|要求の時点で実行されている外部プロセスの数。 NULL 値は許可されません。 |

 
## <a name="permissions"></a>アクセス許可

`VIEW SERVER STATE` 権限が必要です。

## <a name="see-also"></a>関連項目  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
