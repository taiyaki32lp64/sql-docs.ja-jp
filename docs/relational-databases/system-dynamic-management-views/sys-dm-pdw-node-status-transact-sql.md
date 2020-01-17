---
title: sys.dm_pdw_node_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4cd8788d19b06329d0280efc43a13a9a218e056c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899367"
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  追加情報を保持 (経由で[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) のパフォーマンスとアプライアンスのすべてのノードの状態に関するします。 アプライアンス内のノードごとに 1 行が一覧表示します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ノードに関連付けられている一意の数値 id。<br /><br /> このビューのキー。|種類に関係なく、アプライアンスにわたって一意です。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar (255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|このノード上のメモリを割り当てられた合計数。||  
|available_memory|**bigint**|このノードで使用可能なメモリを合計します。||  
|process_cpu_usage|**bigint**|合計のプロセス CPU 使用率、タイマー刻みで。||  
|total_cpu_usage|**bigint**|合計 CPU 使用率、タイマー刻みで。||  
|thread_count|**bigint**|このノードで使用しているスレッドの合計数。||  
|handle_count|**bigint**|このノードで使用中のハンドルの合計数。||  
|total_elapsed_time|**bigint**|システムを起動または再起動後の経過時間の合計です。|システムを起動または再起動後の経過時間の合計です。 Total_elapsed_time では、整数値 (ミリ秒単位で 24.8 日) の最大値を超えるをオーバーフローしました期日の実体化エラーが発生します。<br /><br /> 最大値をミリ秒単位は 24.8 日に相当します。|  
|is_available|**bit**|このノードが使用できるかどうかを示すフラグします。||  
|sent_time|**datetime**|最後に、ネットワークのパッケージは、このノードに送信されました。||  
|received_time|**datetime**|最後に、ネットワークのパッケージは、このノードによって受信されました。||  
|error_id|**nvarchar(36)**|このノードで発生した最後のエラーの一意の識別子。||  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
