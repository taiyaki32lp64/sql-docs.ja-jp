---
title: sys.dm_xtp_gc_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
ms.assetid: 8287d611-50e3-43e1-ba8d-3e3793d3ba0e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28d98f7f95d9e9c2af967976b875f61388342583
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090171"
---
# <a name="sysdmxtpgcstats-transact-sql"></a>sys.dm_xtp_gc_stats (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  現在の動作に関する情報 (全体的な統計情報) を提供します、[!INCLUDE[hek_2](../../includes/hek-2-md.md)]ガベージ コレクション プロセスです。  
  
 行は、ガベージ コレクションまたはアイドル状態のワーカーと呼ばれるメインのガベージ コレクション スレッドによって、通常のトランザクション処理の一部としてです。 ユーザー トランザクションがコミットされたときに、ガベージ コレクション キューから 1 つの作業項目をデキュー ([sys.dm_xtp_gc_queue_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md))。 ガベージ コレクションが可能であってもメイン ユーザー トランザクションでアクセスされなかった行のガベージ コレクションは、ダスティ コーナー スキャン (使用頻度が低いインデックスの領域のスキャン) の一環としてアイドル ワーカーによって実行されます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|rows_examined|**bigint**|サーバーが起動されたので、ガベージ コレクション サブシステムによって検査された行の数。|  
|rows_no_sweep_needed|**bigint**|ダスティ コーナー スキャンをせずに削除された行の数。|  
|rows_first_in_bucket|**bigint**|ガベージ コレクションによって検査された、ハッシュ バケットの最初の行であった行の数。|  
|rows_first_in_bucket_removed|**bigint**|ガベージ コレクションによって検査された行、ハッシュ バケットの最初の行が削除されている数。|  
|rows_marked_for_unlink|**bigint**|ガベージ コレクションによって検査された、ref_count が =0 のインデックスで既に unlinked としてマークされていた行の数。|  
|parallel_assist_count|**bigint**|ユーザー トランザクションで処理された行の数。|  
|idle_worker_count|**bigint**|アイドル ワーカーによって処理されたガベージ行の数。|  
|sweep_scans_started|**bigint**|ガベージ コレクション サブシステムによって実行されたダスティ コーナー スキャンの数。|  
|sweep_scans_retries|**bigint**|ガベージ コレクション サブシステムによって実行されたダスティ コーナー スキャンの数。|  
|sweep_rows_touched|**bigint**|ダスティ コーナー処理によって読み取られた行。|  
|sweep_rows_expiring|**bigint**|ダスティ コーナー処理によって読み取られた期限切れ間近の行。|  
|sweep_rows_expired|**bigint**|ダスティ コーナー処理によって読み取られた、期限切れの行。|  
|sweep_rows_expired_removed|**bigint**|ダスティ コーナー処理によって削除された行の有効期限が切れた。|  
  
## <a name="permissions"></a>アクセス許可  
 インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="usage-scenario"></a>使用シナリオ  
 サンプル出力を次に示します。  
  
```  
rows_examined        rows_no_sweep_needed rows_first_in_bucket rows_first_in_bucket_removed  
280085               209512               69905  
rows_first_in_bucket_removed rows_marked_for_unlink parallel_assist_count idle_worker_count  
69905                        0                      8953  
  
idle_worker_count    sweep_scans_started  sweep_scan_retries   sweep_rows_touched  
10306473             670                  0                    1343  
  
sweep_rows_expiring  sweep_rows_expired   sweep_rows_expired_removed  
               0                 673673  
```  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
