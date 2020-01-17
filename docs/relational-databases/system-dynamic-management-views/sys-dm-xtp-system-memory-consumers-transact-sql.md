---
title: sys.dm_xtp_system_memory_consumers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_system_memory_consumers
- sys.dm_xtp_system_memory_consumers_TSQL
- sys.dm_xtp_system_memory_consumers
- dm_xtp_system_memory_consumers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_system_memory_consumers dynamic management view
ms.assetid: 9eb0dd82-7920-42e0-9e50-7ce6e7ecee8b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 83e9368b562a7ac200171dc814830b21d677770a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090095"
---
# <a name="sysdmxtpsystemmemoryconsumers-transact-sql"></a>sys.dm_xtp_system_memory_consumers (TRANSACT-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  に関するシステム レベルのメモリ コンシューマーを報告[!INCLUDE[hek_2](../../includes/hek-2-md.md)]します。 これらのコンシューマーのメモリでは、既定のプール (割り当てがユーザー スレッドのコンテキストである場合) または内部プール (割り当てがシステムのスレッドのコンテキストである場合) になります。  
  
```  
-- system memory consumers @ instance  
select * from sys.dm_xtp_system_memory_consumers  
```  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|memory_consumer_id|**bigint**|メモリ コンシューマーの内部 ID。|  
|memory_consumer_type|**int**|次の値のいずれかのメモリ コンシューマーの種類を表す整数。<br /><br /> 0 - これは表示されません。 複数のコンシューマーのメモリ使用量を集計します。<br /><br /> 1-ルック アサイド:システムのルック アサイドのメモリ使用量を追跡します。<br /><br /> 2-VARHEAP:可変長ヒープのメモリ使用量を追跡します。<br /><br /> 4-IO ページ プール。IO 操作に使用されるシステム ページ プールのメモリ使用量を追跡します。|  
|memory_consumer_type_desc|**nvarchar(16)**|メモリ コンシューマーの種類の説明:<br /><br /> 0 - これは表示されません。<br /><br /> 1-ルック アサイド<br /><br /> 2-VARHEAP<br /><br /> 4-PGPOOL|  
|memory_consumer_desc|**nvarchar(64)**|メモリ コンシューマー インスタンスの説明。<br /><br /> VARHEAP: <br />システム ヒープ。 一般的な用途は。 現在、ガベージ コレクション作業項目の割り当てに使用されるだけです。<br />-または-<br />ルック アサイド ヒープ。 ルック アサイド リストに含まれる項目の数が事前に定義された上限 (通常は約 5,000 個の項目) に達した場合にルック アサイドで使用されます。<br /><br /> PGPOOL。IO システム プールは、3 つのサイズです。System 4 K ページ プール、System 64 K ページ プール、および System 256 K ページ プール。|  
|lookaside_id|**bigint**|スレッド ローカルなルック アサイド メモリ プロバイダーの ID。|  
|pagepool_id|**bigint**|スレッド ローカルなページ プール メモリ プロバイダーの ID。|  
|allocated_bytes|**bigint**|このコンシューマーのために予約されたバイト数。|  
|used_bytes|**bigint**|このコンシューマーによって使用されるバイト数。 varheap メモリ コンシューマーのみに適用されます。|  
|allocation_count|**int**|割り当ての数。|  
|partition_count|**int**|内部使用のみです。|  
|sizeclass_count|**int**|内部使用のみです。|  
|min_sizeclass|**int**|内部使用のみです。|  
|max_sizeclass|**int**|内部使用のみです。|  
|memory_consumer_address|**varbinary**|コンシューマーの内部アドレス。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="user-scenario"></a>ユーザー シナリオ  
  
```  
-- system memory consumers @ instance  
selectmemory_consumer_type_desc,   
allocated_bytes/1024 as allocated_bytes_kb,   
used_bytes/1024 as used_bytes_kb, allocation_count  
from sys.dm_xtp_system_memory_consumers  
```  
  
 出力はシステム レベルのすべてのメモリ コンシューマーを示します。 たとえば、トランザクション ルック アサイドのコンシューマーがあります。  
  
```  
memory_consumer_type_name           memory_consumer_desc                           allocated_bytes_kb   used_bytes_kb        allocation_count  
-------------------------------          ---------------------                          -------------------  --------------        ----------------  
VARHEAP                                  Lookaside heap                                 0                    0                    0  
VARHEAP                                  System heap                                    768                  0                    2  
LOOKASIDE                                GC transaction map entry                       64                   64                   910  
LOOKASIDE                                Redo transaction map entry                     128                  128                  1260  
LOOKASIDE                                Recovery table cache entry                     448                  448                  8192  
LOOKASIDE                                Transaction recent rows                        3264                 3264                 4444  
LOOKASIDE                                Range cursor                                   0                    0                    0  
LOOKASIDE                                Hash cursor                                    3200                 3200                 11070  
LOOKASIDE                                Transaction save-point set entry               0                    0                    0  
LOOKASIDE                                Transaction partially-inserted rows set        704                  704                  1287  
LOOKASIDE                                Transaction constraint set                     576                  576                  1940  
LOOKASIDE                                Transaction save-point set                     0                    0                    0  
LOOKASIDE                                Transaction write set                          704                  704                  672  
LOOKASIDE                                Transaction scan set                           320                  320                  156  
LOOKASIDE                                Transaction read set                           704                  704                  343  
LOOKASIDE                                Transaction                                    4288                 4288                 1459  
PGPOOL                                   System 256K page pool                          5120                 5120                 20  
PGPOOL                                   System 64K page pool                           0                    0                    0  
PGPOOL                                   System 4K page pool                            24                   24                   6  
```  
  
 システム アロケーターが使用するメモリの合計を表示するには、以下を実行します。  
  
```  
select sum(allocated_bytes)/(1024*1024) as total_allocated_MB, sum(used_bytes)/(1024*1024) as total_used_MB   
from sys.dm_xtp_system_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
2                    2  
```  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
