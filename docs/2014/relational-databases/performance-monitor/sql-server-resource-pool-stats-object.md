---
title: SQLServer:Resource Pool Stats オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fdf00d1291180197f66cd6cb23cf27f10659c68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183020"
---
# <a name="sql-server-resource-pool-stats-object"></a>SQLServer:Resource Pool Stats オブジェクト
  SQLServer:Resource Pool Stats オブジェクトには、リソース ガバナーのリソース プール統計に関する情報を報告するパフォーマンス カウンターが含まれています。  
  
 アクティブな各リソース プールでは、リソース ガバナー リソース プール名と同じインスタンス名を持つ SQLServer:Resource Pool Stats パフォーマンス オブジェクトのインスタンスが作成されます。 次の表では、このインスタンスでサポートされるカウンターについて説明します。  
  
|カウンター名|説明|  
|------------------|-----------------|  
|CPU usage %|このプールに属しているすべてのワークロード グループのすべての要求による CPU 帯域幅の使用率。 コンピューターを基準に測定され、システムのすべての CPU を基準に正規化されます。 この値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで使用できる CPU の量によって変化します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスに割り当てられた内容を基準にして正規化されるのではありません。|  
|CPU usage target %|リソース プールの構成設定とシステムの負荷に基づくリソース プールの CPU 使用率の目標値。|  
|CPU control effect %|リソース プールに対するリソース ガバナーの影響。 この値は、(CPU usage %) / (リソース ガバナーを除いた CPU usage %) で計算されます。|  
|Compile memory target (KB)|クエリ コンパイルの現在のメモリ ブローカー ターゲット (KB 単位)。|  
|Cache memory target (KB)|キャッシュの現在のメモリ ブローカー ターゲット (KB 単位)。|  
|Query exec memory target (KB)|クエリ実行メモリ許可の現在のメモリ ブローカー ターゲット (KB 単位)。 この情報は、 [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql)で取得することもできます。|  
|Memory grants/sec|1 秒間にこのリソース プールで発生しているメモリ許可の数。|  
|Active memory grants count|メモリ許可の現在の合計数。 この情報は、 [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql)で取得することもできます。|  
|Memory grant timeouts/sec|メモリ許可の 1 秒あたりのタイムアウト数。|  
|Active memory grant amount (KB)|許可されているメモリの現在の合計量 (KB 単位)。 この情報は、[sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql) で取得することもできます。|  
|Pending memory grant count|キューに保留されているメモリ許可の要求の数。 この情報は、 [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql)で取得することもできます。|  
|Max memory (KB)|リソース プール設定とサーバーの状態に基づいてリソース プールで利用できるメモリの最大量 (KB 単位)。|  
|Used memory (KB)|リソース プールに使用されているメモリ量 (KB 単位)。|  
|Target memory (KB)|リソース プール設定とサーバーの状態に基づいてリソース プールで取得しようとしている目標メモリ量 (KB 単位)。|  
|Disk Read IO/sec|最後の 1 秒間のディスクからの読み取り操作の数。|  
|Disk Read IO Throttled/sec|最後の 1 秒間に調整された読み取り操作の数。|  
|Disk Read Bytes/sec|最後の 1 秒間にディスクから読み取られたバイト数。|  
|Avg Disk Read IO (ms)|ディスクからの読み取り操作の平均時間 (秒単位)。|  
|Disk Write IO/sec|最後の 1 秒間のディスクへの書き込み操作の数。|  
|Disk Write IO Throttled/sec|最後の 1 秒間に調整された書き込み操作の数。|  
|Disk Write Bytes/sec|最後の 1 秒間にディスクに書き込まれたバイト数。|  
|Avg Disk Write IO (ms)|ディスクへの書き込み操作の平均時間 (秒単位)。|  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)   
 [SQLServer:Workload Group Stats オブジェクト](sql-server-workload-group-stats-object.md)   
 [リソース ガバナー](../resource-governor/resource-governor.md)  
  
  
