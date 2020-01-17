---
title: SQL Server:Workload Group Stats オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 06651ffcfee30d538c8ede09914133a2ed818b3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151101"
---
# <a name="sql-server-workload-group-stats-object"></a>SQLServer:Workload Group Stats オブジェクト
  SQLServer:Workload Group Stats オブジェクトには、リソース ガバナーのワークロード グループ統計に関する情報を報告するパフォーマンス カウンターが含まれています。  
  
 アクティブな各ワークロード グループでは、リソース ガバナー ワークロード グループ名と同じインスタンス名を持つ SQLServer:Workload Group Stats パフォーマンス オブジェクトのインスタンスが作成されます。 次の表では、このインスタンスでサポートされるカウンターについて説明します。  
  
|カウンター名|説明|  
|------------------|-----------------|  
|Queued requests|現在キューに置かれている処理待ちの要求の数。 この数は、GROUP_MAX_REQUESTS の上限に達してからスロットルが行われると、0 以外の値になることがあります。|  
|Active requests|このワークロード グループの現在実行中の要求数。 グループ ID でフィルター選択した sys.dm_exec_requests の行数と同じ数になります。|  
|Requests completed/sec|このワークロード グループの完了した要求の数。 この数は累積数です。|  
|CPU usage %|このワークロード グループのすべての要求による CPU 帯域幅の使用率。コンピューターを基準に測定され、システムのすべての CPU を基準に正規化されます。 この値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで使用できる CPU の量によって変化します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスに割り当てられた内容を基準にして正規化されるのではありません。|  
|Max request CPU time (ms)|ワークロード グループの現在実行中の要求で使用される最大 CPU 時間 (ミリ秒単位)。|  
|Blocked requests|ワークロード グループのブロックされた要求の現在の数。 この数値を使用して負荷の特性を判別できます。|  
|Reduced memory grants/sec|最適な量に満たないメモリ許可を取得している 1 秒間のクエリ数。|  
|Max request memory grant (KB)|1 つのクエリに対するメモリ許可の最大値 (KB 単位)。|  
|Query optimizations/sec|1 秒間にこのワークロード グループで行われたクエリの最適化の数。 この数値を使用して負荷の特性を判別できます。|  
|Suboptimal plans/sec|1 秒間にこのワークロード グループで生成された最適ではないプランの数。|  
|Active parallel threads|並列スレッド使用の現在の数。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)   
 [SQLServer:Resource Pool Stats オブジェクト](sql-server-resource-pool-stats-object.md)   
 [リソース ガバナー](../resource-governor/resource-governor.md)  
  
  
