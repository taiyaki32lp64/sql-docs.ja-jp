---
title: sys.dm_xe_sessions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_sessions_TSQL
- dm_xe_sessions
- sys.dm_xe_sessions_TSQL
- sys.dm_xe_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_sessions dynamic management view
- extended events [SQL Server], views
ms.assetid: defd6efb-9507-4247-a91f-dc6ff5841e17
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9b42a6808d9cab6a3431a68bff9e29e83354a2af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090219"
---
# <a name="sysdmxesessions-transact-sql"></a>sys.dm_xe_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アクティブな拡張イベント セッションに関する情報を返します。 このセッションは、イベント、アクション、およびターゲットのコレクションです。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|address|**varbinary(8)**|セッションのメモリ アドレス。 アドレスは、ローカル システム全体で一意です。 NULL 値は許可されません。|  
|NAME|**nvarchar (256)**|セッションの名前。 名前は、ローカル システム全体で一意です。 NULL 値は許可されません。|  
|pending_buffers|**int**|いっぱいになって処理が保留されているバッファーの数。 NULL 値は許可されません。|  
|total_regular_buffers|**int**|セッションに関連付けられている標準バッファーの総数。 NULL 値は許可されません。<br /><br /> 注:ほとんどの場合は標準バッファーが使用されます。 標準バッファーには、多数のイベントを保持できるだけの十分なサイズがあります。 通常は、各セッションに 3 つ以上のバッファーがあります。 標準バッファーの数は、MEMORY_PARTITION_MODE オプションによって設定されるメモリのパーティション分割に基づいて、サーバーで自動的に決定されます。 標準バッファーのサイズは、MAX_MEMORY オプションの値 (既定では 4 MB) をバッファーの数で割った値になります。 MEMORY_PARTITION_MODE オプションと MAX_MEMORY オプションの詳細については、次を参照してください。 [CREATE EVENT SESSION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)します。|  
|regular_buffer_size|**bigint**|標準バッファーのサイズ (バイト単位)。 NULL 値は許可されません。|  
|total_large_buffers|**int**|ラージ バッファーの総数。 NULL 値は許可されません。<br /><br /> 注:ラージ バッファーは、イベントが標準バッファーより大きい場合に使用されます。 この目的のために明示的に確保されています。 ラージ バッファーは、イベント セッションが開始されるときに割り当てられ、サイズは MAX_EVENT_SIZE オプションによって決まります。 MAX_EVENT_SIZE オプションの詳細については、次を参照してください。 [CREATE EVENT SESSION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)します。|  
|large_buffer_size|**bigint**|ラージ バッファーのサイズ (バイト単位)。 NULL 値は許可されません。|  
|total_buffer_size|**bigint**|セッションのイベントを格納するためのメモリ バッファーの合計サイズ (バイト単位)。 NULL 値は許可されません。|  
|buffer_policy_flags|**int**|すべてのバッファーがいっぱいになっているときに新しいイベントが発生した場合のセッション イベント バッファーの動作を示すビットマップ。 NULL 値は許可されません。|  
|buffer_policy_desc|**nvarchar (256)**|すべてのバッファーがいっぱいになっているときに新しいイベントが発生した場合のセッション イベント バッファーの動作を示す説明。  NULL 値は許可されません。 buffer_policy_desc は、次のいずれかを指定できます。<br /><br /> Drop event<br /><br /> Do not drop events<br /><br /> Drop full buffer<br /><br /> Allocate new buffer|  
|flags|**int**|セッションに設定されているフラグを示すビットマップ。 NULL 値は許可されません。|  
|flag_desc|**nvarchar (256)**|セッションに設定されているフラグの説明。  NULL 値は許可されません。 flag_desc は、次の任意の組み合わせを指定できます。<br /><br /> Flush buffers on close<br /><br /> Dedicated dispatcher<br /><br /> Allow recursive events|  
|dropped_event_count|**int**|バッファーがいっぱいのときに削除されたイベントの数。 この値は**0**バッファー ポリシーが Drop full buffer"または"Do not drop events"のかどうか。 NULL 値は許可されません。|  
|dropped_buffer_count|**int**|バッファーがいっぱいのときに削除されたバッファーの数。 この値は**0**かどうか、バッファーのポリシーは、Drop event"または"Do not drop events"に設定されます。 NULL 値は許可されません。|  
|blocked_event_fire_time|**int**|バッファーがいっぱいのときにイベントの発生がブロックされていた時間。 この値は**0**バッファー ポリシーが [Drop full buffer] または [Drop event] のかどうか。 NULL 値は許可されません。|  
|create_time|**datetime**|セッションが作成された時刻。 NULL 値は許可されません。|  
|largest_event_dropped_size|**int**|セッション バッファーに収まらなかった最大のイベントのサイズ。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

