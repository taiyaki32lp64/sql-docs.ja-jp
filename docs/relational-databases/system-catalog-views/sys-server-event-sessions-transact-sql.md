---
title: server_event_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_sessions
- server_event_sessions_TSQL
- sys.server_event_sessions_TSQL
- sys.server_event_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_sessions catalog view
- xe
ms.assetid: 796f3093-6a3e-4d67-8da6-b9810ae9ef5b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 142e4bfd81a60ec6f80294bce16bfb7a59d3211a
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313711"
---
# <a name="sysserver_event_sessions-transact-sql"></a>server_event_sessions (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に存在するすべてのイベント セッションの定義を一覧表示します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|イベント セッションの一意な ID。 NULL 値は許可されません。|  
|name|**sysname**|イベントセッションを識別するためのユーザー定義の名前。 名前は一意です。 NULL 値は許可されません。|  
|event_retention_mode|**nchar(1)**|イベントの損失を処理する方法を決定します。 既定値は S です。NULL 値は許可されません。 次のいずれかを指定します。<br /><br /> S. Event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS にマップされる<br /><br /> M. Event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS にマップされる<br /><br /> N. Event_retention_mode_desc = NO_EVENT_LOSS にマップされる|  
|event_retention_mode_desc|**sysname**|イベントの損失を処理する方法について説明します。 既定値は ALLOW_SINGLE_EVENT_LOSS です。 NULL 値は許可されません。 次のいずれかを指定します。<br /><br /> ALLOW_SINGLE_EVENT_LOSS。 イベントはセッションから失われることがあります。 1つのイベントは、すべてのイベントバッファーがいっぱいになったときにのみ削除されます。 イベント バッファーがいっぱいのときに単独のイベントを削除することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス特性が許容可能な状態になり、処理後のイベント ストリームでの損失を最小限に抑えることができます。<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS。 セッションから完全なイベントバッファーが失われる可能性があります。 失われるイベントの数は、セッションに割り当てられているメモリサイズ、メモリのパーティション分割、およびバッファー内のイベントのサイズによって異なります。 このオプションを使用すると、イベント バッファーがすぐにいっぱいになるときにサーバーのパフォーマンスに与える影響を最小限に抑えることができます。 ただし、多数のイベントがセッションから失われる可能性があります。<br /><br /> NO_EVENT_LOSS。 イベントの削除は許可されません。 このオプションにより、発生したすべてのイベントが保持されます。 このオプションを使用すると、イベントを発生させるすべてのタスクが、イベントバッファー内の領域が使用可能になるまで待機します。 これにより、イベントセッションがアクティブな間、パフォーマンスが低下する可能性があります。|  
|max_dispatch_latency|**int**|イベントをセッション ターゲットに渡す前にメモリにバッファリングする時間 (ミリ秒単位)。 有効な値は 0 ~ 2147483648、および0です。 値0は、ディスパッチ待機時間が無制限であることを示します。 NULL 値が許可されます。|  
|max_memory|**int**|イベントのバッファリングのためにセッションに割り当てられたメモリの量。 既定値は 4 MB です。 NULL 値が許可されます。|  
|max_event_size|**int**|イベント セッション バッファーに収まらないイベント用に確保するメモリの量。 計算されたバッファー サイズを max_event_size が超える場合、サイズが max_event_size のバッファーが追加で 2 つイベント セッションに割り当てられます。 NULL 値が許可されます。|  
|memory_partition_mode|**nchar(1)**|イベントバッファーが作成されるメモリ内の場所。 既定のパーティション モードは G です。NULL 値は許可されません。 memory_partition_mode は次のいずれかです。<br /><br /> G : NONE<br /><br /> C-PER_CPU<br /><br /> N-PER_NODE|  
|memory_partition_mode_desc|**sysname**|既定値は NONE です。 NULL 値は許可されません。 次のいずれかを指定します。<br /><br /> NONE。 1 つのバッファー セットが SQL Server インスタンス内で作成されます。<br /><br /> PER_CPU。 CPU ごとにバッファーのセットが作成されます。<br /><br /> PER_NODE。 NUMA (non-uniform memory access) ノードごとに、一連のバッファーが作成されます。|  
|track_causality|**bit**|因果関係の追跡を有効または無効にします。 1 (ON) に設定すると、追跡が有効になり、異なるサーバー接続上の関連イベントを関連付けることができます。 既定の設定は 0 (オフ) です。 NULL 値は許可されません。|  
|startup_state|**bit**|値は、サーバーの起動時にセッションを自動的に開始するかどうかを決定します。 既定値は 0 です。 NULL 値は許可されません。 次のいずれか:<br /><br /> 0 (オフ)。 サーバーの起動時にセッションは開始されません。<br /><br /> 1 (ON)。 サーバーの起動時にイベント セッションが開始されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Extended Events Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
