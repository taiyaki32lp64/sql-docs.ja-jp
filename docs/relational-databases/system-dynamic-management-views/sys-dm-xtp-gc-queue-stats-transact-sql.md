---
title: sys.dm_xtp_gc_queue_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: addef774-318d-46a7-85df-f93168a800cb
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azuresqldb-mi-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: c56fe40ec6864ac48a991e155d06ce7c505ed593
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090197"
---
# <a name="sysdmxtpgcqueuestats-transact-sql"></a>sys.dm_xtp_gc_queue_stats (TRANSACT-SQL)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  各ガベージ コレクション ワーカー キューに関する情報をサーバー、およびそれぞれに関する各種統計を出力します。 論理 CPU ごとの 1 つのキューがあります。  
  
 メインのガベージ コレクション スレッド (アイドル状態のスレッド) は、すべてのトランザクションが、メインのガベージ コレクション スレッドの最後の呼び出し以降に完了の更新、削除、および挿入された行を追跡します。 ガベージ コレクション スレッドは、起動すると、最も古いアクティブなトランザクションのタイムスタンプが変化しているかどうかを判断します。 最も古いアクティブなトランザクションが変化した場合は、アイドル スレッドにより、書き込みセットが不要になったトランザクションの作業項目が (16 行ごとのチャンクで) エンキューされます。 たとえば、1,024 行を削除すると、64 のガベージ コレクション作業項目がエンキューされます (1 つの作業項目には削除された 16 行が含まれています)。  ユーザー トランザクションがコミットされた後は、スケジューラでエンキューされた項目をすべてを選択します。 スケジューラにエンキューされた項目がしない場合は、ユーザー トランザクションは、現在の NUMA ノード内の任意のキューを検索します。  
  
 sys.dm_xtp_gc_queue_stats を実行してエンキューされた作業が処理されているかどうかを確認することにより、削除された行についてガベージ コレクションでメモリが解放されるかどうかを確認できます。 Current_queue_depth のエントリが処理されていない場合、または current_queue_depth に新しい作業項目を追加しない場合は、これはガベージ コレクションがメモリを解放していないことを示します。 たとえば、実行時間の長いトランザクションがある場合は、ガベージ コレクションを実行できません。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  

|列名|型|説明|  
|-----------------|----------|-----------------|  
|queue_id|**int**|キューの一意の識別子。|  
|total_enqueues|**bigint**|ガベージ コレクションの合計数は、サーバーの起動後にこのキューに項目のエンキューを作業します。|  
|total_dequeues|**bigint**|サーバーが起動してからこのキューからデキューされたガベージ コレクションの作業項目の総数。|  
|current_queue_depth|**bigint**|ガベージ コレクションの作業項目がこのキューにある現在の数。 このアイテムは場合によっては 1 つ以上がガベージ コレクションの対象であることを示します。|  
|maximum_queue_depth|**bigint**|このキューに同時に存在した最大項目数。|  
|last_service_ticks|**bigint**|キューが最後に処理時に CPU のティックします。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW SERVER STATE 権限が必要です。  
  
## <a name="user-scenario"></a>ユーザー シナリオ  
 この出力は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が 4 コアで実行中か、または、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが 4 コアに関連付けられていることを示しています。  
  
 この出力は、処理する作業項目がキューにないことを示しています。 キュー 0 の場合、SQL の起動後、キューから削除された作業項目が合計 15625 で、キューの最大項目数は 215625 に設定されています。  
  
```  
queue_id total_enqueues total_dequeues current_queue_depth  maximum_queue_depth  last_service_ticks  
----------------------------------------------------------------------------------------------------  
0        15625                15625    0                    15625                1233573168347  
1        15625                15625    0                    15625                1234123295566  
2        15625                15625    0                    15625                1233569418146  
3        15625                15625    0                    15625                1233571605761  
```  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
