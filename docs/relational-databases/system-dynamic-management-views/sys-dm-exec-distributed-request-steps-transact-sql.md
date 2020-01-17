---
title: sys.dm_exec_distributed_request_steps (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5c40ce6d1c7b7ef85f24fc8032559e000d89be1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097823"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  指定の PolyBase 要求またはクエリを作成するすべてのステップに関する情報を保持します。 これには、クエリのステップごとに 1 行が一覧表示します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id と step_index は、このビューのキーを構成します。 要求に関連付けられている一意の数値 id です。|内の ID を参照してください。 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)します。|  
|step_index|**int**|この手順の要求を構成する手順のシーケンス内の位置。|ステップを含む要求に対して (n 1) に 0 を返します。|  
|operation_type|**nvarchar(128)**|この手順で表される操作の種類。|'MoveOperation'、'OnOperation'、'RandomIDOperation'、'RemoteOperation'、'ReturnOperation'、'ShuffleMoveOperation'、'TempTablePropertiesOperation'、'DropDiagnosticsNotifyOperation'、'HadoopShuffleOperation'、'HadoopBroadCastOperation'' HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|手順を実行しています。|' AllComputeNodes '、' AllDistributions'、'ComputeNode'、'Distribution'、'AllNodes'、'SubsetNodes'、'SubsetDistributions'、' 指定されていない '。|  
|location_type|**nvarchar(32)**|手順を実行しています。|'Compute'、'ヘッド' または 'DMS' です。 すべてのデータ移動の手順では、'DMS' を表示します。|  
|status|**nvarchar(32)**|この手順の状態|'保留中'、'Running'、'完了'、'失敗'、'UndoFailed'、'PendingCancel'、' キャンセル '、'を元に戻す'、'中止'|  
|error_id|**nvarchar(36)**|この手順では、存在する場合に関連するエラーの一意の id|Id を参照してください。 [sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)、エラーが発生しなかった場合は NULL です。|  
|start_time|**datetime**|ステップの実行開始時刻|小さいまたは現在の時刻と等しい、大きいか等しい end_compile_time が、この手順が属している、クエリのです。|  
|end_time|**datetime**|このステップ実行を完了したが取り消された場合、または失敗したの時間です。|小さいまたは現在の時刻に等しいと大きいか等しい start_time、手順については、現在実行中に NULL に設定するか、キューに格納します。|  
|total_elapsed_time|**int**|クエリ ステップが実行されて、ミリ秒単位で時間の合計|0 ～ start_time と end_time の間の違いです。 手順についてはキューに置かれた 0 を返します。|  
|row_count|**bigint**|変更されたか、この要求によって返される行の合計数|変更またはデータ、それ以外の場合の影響を受ける行の数を返すしていないするステップの 0 を返します。 DMS の手順に達すると-1 に設定します。|  
|command|nvarchar (4000)|このステップのコマンドの完全なテキストを保持します。|ステップの任意の有効な要求文字列。 4,000 文字より長い場合に切り捨てられます。|  
  
## <a name="see-also"></a>関連項目  
 [PolyBase 動的管理ビューでのトラブルシューティング](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
